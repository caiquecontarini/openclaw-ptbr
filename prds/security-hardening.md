# PRD: Security Hardening do OpenClaw

> Jogue este arquivo no chat do seu agente e diga: "Executa este PRD de seguranÃ§a"
> Ele vai blindar seu servidor seguindo cada passo.
> **Atualizado para OpenClaw v2026.3.13**

---

## âš ï¸ Por Que Isso Ã‰ Urgente

Em fevereiro de 2026, uma vulnerabilidade crÃ­tica (**CVE com CVSS 8.8**) foi descoberta em instÃ¢ncias OpenClaw expostas na internet. Mais de **30.000 instÃ¢ncias** foram identificadas como vulnerÃ¡veis antes do patch da versÃ£o 2026.2.12. Servidores sem proteÃ§Ã£o bÃ¡sica foram comprometidos â€” dados exfiltrados, API keys roubadas, agentes usados para spam.

AlÃ©m disso: servidores OpenClaw expostos na internet recebem 1.000+ tentativas de brute force por dia. Sem proteÃ§Ã£o, qualquer pessoa pode acessar seu agente e seus dados.

Este guia te protege contra todos os vetores de ataque conhecidos.

## Contexto da v2026.3.2+

**WebSocket agora Ã© loopback-only por padrÃ£o.** O painel web do OpenClaw (`http://IP:18789`) sÃ³ aceita conexÃµes de `127.0.0.1` â€” ou seja, sÃ³ de dentro do prÃ³prio servidor. Para acessar remotamente, vocÃª precisa do Cloudflare Tunnel (coberto abaixo).

### Novidades de seguranÃ§a na v2026.3.13

A versÃ£o 2026.3.13 trouxe um pacote expressivo de correÃ§Ãµes de seguranÃ§a:

- **Device pairing single-use:** CÃ³digos de setup agora sÃ£o de uso Ãºnico â€” nÃ£o podem ser reaproveitados para ganhar acesso. Cada `openclaw qr` ou `/pair` gera um cÃ³digo que expira no primeiro scan (ou em poucos minutos sem uso). Se tentar usar o mesmo QR duas vezes â†’ erro "cÃ³digo expirado". Gere um novo para cada pareamento. âš ï¸ Nunca compartilhe QR por screenshot â€” quem escanear primeiro ganha acesso.
- **Exec approvals hardened:** VÃ¡rias formas de contornar a anÃ¡lise de comandos foram corrigidas (Unicode zero-width, backslash-newline, pnpm wrappers, Perl/Ruby -r/-I flags)
- **WebSocket preauth:** Janela de handshake nÃ£o-autenticado reduzida; frames oversized rejeitados antes do parsing
- **Proxy attachments:** Limite de 5MB restaurado para arquivos persistidos pelo browser proxy
- **GIT_EXEC_PATH blocked:** VariÃ¡vel de ambiente herdada nÃ£o pode mais redirecionar Git helpers
- **Webhook secrets:** Feishu, LINE e Zalo com validaÃ§Ã£o de assinatura mais rigorosa

> âœ… NÃ£o hÃ¡ aÃ§Ãµes especÃ­ficas necessÃ¡rias para o aluno alÃ©m de manter o OpenClaw atualizado. As correÃ§Ãµes sÃ£o automÃ¡ticas apÃ³s o `npm update -g openclaw`.

---

## Tarefas (executar na ordem)

### 1. Telegram Allowlist (CRÃTICO â€” fazer PRIMEIRO)

> ðŸ”´ **Ordem importa:** Configure o dmPolicy ANTES de qualquer outra coisa. O UFW e outras proteÃ§Ãµes vÃªm depois.

Verificar se o OpenClaw estÃ¡ configurado com `dmPolicy: "allowlist"` e que APENAS os IDs autorizados estÃ£o na lista.

```bash
# Verificar config atual
cat /root/.openclaw/openclaw.json | grep -A5 dmPolicy
```

Se estiver "open", mudar IMEDIATAMENTE para "allowlist" com os IDs corretos.

> **Por que primeiro?** O UFW protege a porta do servidor, mas o Telegram Ã© uma conexÃ£o de SAÃDA â€” nÃ£o tem porta pra bloquear. Se o dmPolicy estiver "open", qualquer pessoa que descobrir o username do seu bot consegue commandar seu agente, mesmo com UFW ativo. SÃ£o duas camadas diferentes de proteÃ§Ã£o.

### 2. Firewall (UFW)

```bash
# Instalar e configurar
sudo apt install -y ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw --force enable
sudo ufw status
```

### 3. Fail2ban (proteÃ§Ã£o SSH)

```bash
# Instalar
sudo apt install -y fail2ban

# Configurar
sudo cat > /etc/fail2ban/jail.local << 'EOF'
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
bantime = 3600
findtime = 600
EOF

# Ativar
sudo systemctl enable fail2ban
sudo systemctl restart fail2ban

# Verificar
sudo fail2ban-client status sshd
```

### 4. Cloudflare Tunnel (acesso remoto seguro)

> ðŸ”’ **Novo na v2026.3.2:** O WebSocket do painel OpenClaw agora sÃ³ aceita conexÃµes de `127.0.0.1` (loopback). Para acessar o painel remotamente (Mission Control, dashboards), vocÃª **precisa** do Cloudflare Tunnel. NÃ£o tem atalho.

Usar Cloudflare Tunnel pra expor serviÃ§os web (Mission Control, dashboards) sem abrir portas:

```bash
# Instalar cloudflared
curl -L https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb -o cloudflared.deb
sudo dpkg -i cloudflared.deb

# Autenticar
cloudflared tunnel login

# Criar tunnel
cloudflared tunnel create meu-tunnel

# Configurar (exemplo pra app na porta 18789 â€” painel OpenClaw)
cat > ~/.cloudflared/config.yml << 'EOF'
tunnel: meu-tunnel
credentials-file: /root/.cloudflared/<TUNNEL_ID>.json

ingress:
  - hostname: painel.meudominio.com
    service: http://127.0.0.1:18789
  - service: http_status:404
EOF

# Rodar como serviÃ§o
cloudflared service install
systemctl enable cloudflared
systemctl start cloudflared
```

**Por que:**
- Zero portas expostas na internet â€” tunnel faz conexÃ£o de SAÃDA
- Servidor fica "invisÃ­vel" (sem IP pÃºblico exposto)
- SSL/TLS automÃ¡tico pelo Cloudflare
- ProteÃ§Ã£o DDoS gratuita inclusa
- NUNCA usar `0.0.0.0` â€” sempre `127.0.0.1` + tunnel

### 5. Portas de aplicaÃ§Ã£o

Se tiver aplicaÃ§Ãµes web rodando (Mission Control, dashboards, etc.):
- Mudar binding de `0.0.0.0` para `127.0.0.1`
- Usar Cloudflare Tunnel (acima) para acesso externo
- NUNCA expor portas direto na internet

### 6. SSH Hardening

```bash
# Verificar se root login com senha estÃ¡ ativo
grep "PermitRootLogin" /etc/ssh/sshd_config
```

Ideal: `PermitRootLogin prohibit-password` (sÃ³ SSH key, sem senha)

### 7. Credenciais: Auditar com `openclaw secrets`

**O problema:** A CVE de 2026.2.12 explorou justamente API keys hardcodadas em arquivos de configuraÃ§Ã£o. Se alguÃ©m acessa seu servidor, pega TODAS as suas chaves de uma vez.

**A partir da v2026.3.2**, o OpenClaw tem o comando `openclaw secrets` para gerenciar credenciais de forma segura. **Use esse comando em vez de editar .env manualmente.**

**Passo 1 â€” Auditar (descobrir se tem chaves expostas):**

```bash
# Ver tudo que estÃ¡ exposto nos seus arquivos
openclaw secrets audit
```

Este comando escaneia todos os arquivos do workspace e configuraÃ§Ã£o, procurando padrÃµes de API keys hardcodadas. Se encontrar algo, vai listar com o caminho e linha exata.

**Passo 2 â€” Migrar pro sistema seguro:**

```bash
# Migrar automaticamente para o gerenciador de secrets seguro
openclaw secrets apply
```

Este comando move as credenciais encontradas para o cofre seguro do OpenClaw, onde ficam criptografadas. Os arquivos originais tÃªm as chaves removidas automaticamente.

**Passo 3 â€” Verificar que tudo foi migrado:**

```bash
# Rodar audit de novo â€” deve retornar limpo
openclaw secrets audit
# Output esperado: "âœ… No exposed credentials found"
```

> â„¹ï¸ **Compatibilidade retroativa:** Se vocÃª jÃ¡ tem um `.env` manual com chaves, o `openclaw secrets apply` lÃª de lÃ¡ tambÃ©m e migra pro sistema seguro. ApÃ³s migraÃ§Ã£o, o `.env` manual pode ser removido.

**RotaÃ§Ã£o trimestral:** A cada 3 meses, gerar novas chaves nos painÃ©is (OpenAI, OpenRouter, Telegram). O `openclaw secrets` faz a atualizaÃ§Ã£o:

```bash
openclaw secrets set ANTHROPIC_API_KEY=sk-ant-nova-chave-aqui
```

### 8. Sync systemd + secrets (armadilha comum!)

Quando trocar qualquer credencial, o systemd precisa saber:

```bash
# 1. Atualizar o secret
openclaw secrets set NOME_DA_CHAVE=novo-valor

# 2. Atualizar o override do systemd se tiver variÃ¡vel hard-coded lÃ¡
sudo systemctl edit openclaw

# 3. Recarregar e reiniciar
sudo systemctl daemon-reload
sudo systemctl restart openclaw
```

**Por que:** O systemd override tem prioridade sobre o sistema de secrets. Se trocar sÃ³ o secret e o override tiver o valor antigo, vai continuar usando o antigo. Muita gente perde horas debugando isso.

---

## Checklist Final

- [ ] **dmPolicy = allowlist** (PRIMEIRO â€” antes do UFW)
- [ ] UFW ativo
- [ ] Fail2ban ativo
- [ ] Cloudflare Tunnel configurado (painel loopback-only na v2026.3.2)
- [ ] Portas em 127.0.0.1 (nÃ£o 0.0.0.0)
- [ ] SSH hardened (key-only)
- [ ] `openclaw secrets audit` â€” zero resultados
- [ ] `openclaw secrets apply` â€” credenciais migradas pro cofre seguro
- [ ] RotaÃ§Ã£o trimestral agendada
- [ ] systemd + secrets sincronizados

## Resultado Esperado

Servidor blindado contra os ataques mais comuns, incluindo o vetor da CVE 2026.2.12. **9 camadas de proteÃ§Ã£o** ativas. Reportar status de cada item.

## Manter Atualizado

Execute periodicamente para garantir que estÃ¡ na versÃ£o mais recente (com todos os patches de seguranÃ§a):

```bash
npm update -g openclaw
openclaw gateway restart
openclaw gateway status
```

> âœ… A versÃ£o 2026.3.13 Ã© o pacote de seguranÃ§a mais robusto atÃ© hoje â€” inclui correÃ§Ãµes em exec approvals, device pairing, WebSocket e webhooks.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
