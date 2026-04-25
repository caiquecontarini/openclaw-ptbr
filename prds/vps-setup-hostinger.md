# PRD: Setup VPS na Hostinger (Bare Metal, sem Docker)

> Guia step-by-step para o MÃ³dulo 1 do curso.
> Bruno segue este roteiro na gravaÃ§Ã£o.
> **Atualizado para OpenClaw v2026.4.9** (ChatGPT OAuth como padrÃ£o)

---

## PrÃ©-requisitos

- Conta na Hostinger (https://www.hostinger.com)
- Conta no ChatGPT (https://chat.openai.com) â€” Plus (R$99/mÃªs) ou Pro. O login OAuth nÃ£o precisa de API key.
- Telegram instalado no celular

## Tempo estimado: 15-20 minutos

---

## Passo 1: Criar a VPS na Hostinger (3 min)

1. Acesse https://www.hostinger.com/vps-hosting
2. Escolha o plano KVM 2 (melhor custo-benefÃ­cio):
   - 2 vCPUs, 4GB RAM, 80GB SSD â€” ~R$50-70/mÃªs com cupom BRUNOOKAMOTO (10% off)
3. **IMPORTANTE:** NÃƒO use o template Docker/One-Click do OpenClaw
4. Selecione **Ubuntu 24.04** como sistema operacional
5. Gere uma **SSH key** (mais seguro que senha root):
   ```bash
   ssh-keygen -t ed25519 -C "seu-email@exemplo.com"
   cat ~/.ssh/id_ed25519.pub
   ```
   Cole a chave pÃºblica no painel Hostinger. Se preferir senha: defina uma root forte.
6. Anote o IP da VPS

> **Por que nÃ£o o One-Click Docker?**
> O Docker isola o agente num container â€” instalar skills, integraÃ§Ãµes e ferramentas extras fica muito mais complicado. Pra quem nÃ£o Ã© tÃ©cnico, Ã© uma barreira desnecessÃ¡ria. Instalando direto, tudo funciona como esperado.

---

## Passo 2: Conectar na VPS via SSH (2 min)

### No Mac/Linux:
```bash
ssh root@SEU_IP_DA_VPS
```
(digita a senha quando pedir)

### No Windows:
- Use o PuTTY ou o Windows Terminal
- Host: SEU_IP_DA_VPS
- User: root

### Primeira vez? A Hostinger tem terminal no painel:
- hPanel â†’ VPS â†’ Terminal (botÃ£o no topo)
- Funciona direto no navegador, sem instalar nada

> ðŸ’¡ **Dica pro curso:** Mostrar as duas opÃ§Ãµes (terminal local + terminal do painel) pra atender quem nÃ£o sabe usar SSH.

---

## Passo 3: Instalar o OpenClaw (3 min)

```bash
# Instalar OpenClaw (1 comando)
curl -fsSL https://openclaw.ai/install.sh | bash
```

Isso instala o Node.js (se necessÃ¡rio) e o OpenClaw.

Depois, rodar o wizard de configuraÃ§Ã£o:

```bash
openclaw onboard --install-daemon
```

O wizard vai perguntar:

1. **Gateway mode:** â†’ Escolher `Local`
2. **AI Provider:** â†’ Escolher `OpenAI`
3. **Login OAuth:** â†’ O wizard abre o fluxo OAuth do ChatGPT. Login com conta Plus/Pro. **NÃ£o precisa de API key.**
4. **Model:** â†’ `GPT-5.4` (recomendado) ou `GPT-4o` (mais econÃ´mico)
5. **Instalar como serviÃ§o?** â†’ Sim (roda 24/7 automaticamente)

> ðŸ’¡ **Dica pro curso:** Mostrar o fluxo OAuth â€” 1 clique no navegador, muito mais simples que API key. Explicar que a assinatura ChatGPT existente Ã© suficiente.

---

## âš ï¸ Passo 3.5: Configurar Perfil de Ferramentas (NOVO â€” v2026.3.2)

> ðŸ”´ **CRÃTICO:** Este passo Ã© OBRIGATÃ“RIO a partir da versÃ£o 2026.3.2. Sem ele, seu agente vai responder mensagens mas nÃ£o vai conseguir fazer NADA Ãºtil.

A partir da versÃ£o **2026.3.2**, o OpenClaw vem com `tools.profile = messaging` por padrÃ£o. Isso significa que o agente sÃ³ pode responder mensagens, mas **NÃƒO pode** executar comandos, ler arquivos, usar ferramentas ou fazer qualquer coisa alÃ©m de conversar.

Para ter um agente verdadeiramente funcional, vocÃª PRECISA mudar para o perfil `full`:

```bash
openclaw config set tools.profile full
```

Em seguida, valide que tudo estÃ¡ correto com o novo comando de validaÃ§Ã£o:

```bash
openclaw config validate
```

A saÃ­da deve mostrar algo como:

```
âœ… tools.profile: full
âœ… gateway.mode: local
âœ… ai.provider: openai
âœ… Configuration valid â€” 0 warnings
```

> ðŸ’¡ **Por que esse default mudou?** A comunidade de seguranÃ§a identificou que muitas instalaÃ§Ãµes expostas na internet davam acesso completo de ferramentas a qualquer pessoa que encontrasse o bot. O novo default `messaging` Ã© mais seguro para quem nÃ£o sabe o que estÃ¡ fazendo. Mas **para o curso**, queremos `full` â€” daÃ­ este passo.

> ðŸ“º **Dica pro curso:** Mostrar o "antes e depois" â€” enviar uma mensagem pro bot sem configurar (`tools.profile = messaging`) e ver ele respondendo mas sem conseguir executar comandos. Depois configurar e mostrar a diferenÃ§a. Muito didÃ¡tico!

---

## âš ï¸ Passo 3.6: Configurar Timezone (NOVO â€” v2026.3.13)

> ðŸ• **IMPORTANTE para quem vai usar crons:** Sem este passo, todos os seus crons vÃ£o disparar no horÃ¡rio UTC â€” 3 horas adiantados em relaÃ§Ã£o ao Brasil. Um cron configurado "todo dia Ã s 9h" vai disparar Ã s 12h.

```bash
sudo systemctl edit openclaw
```

No editor que abrir, adicione dentro de `[Service]`:

```
[Service]
Environment="OPENCLAW_TZ=America/Sao_Paulo"
```

Salve e aplique:

```bash
sudo systemctl daemon-reload
sudo systemctl restart openclaw
```

Verifique que o gateway reiniciou corretamente:

```bash
openclaw gateway status
```

> ðŸ“º **Dica pro curso:** Demonstrar o efeito ao vivo â€” criar um cron de teste, mostrar ele disparando no horÃ¡rio errado (UTC), depois configurar OPENCLAW_TZ e mostrar o horÃ¡rio correto. Momento muito didÃ¡tico.

---

## Passo 4: Verificar se estÃ¡ rodando (30 seg)

```bash
openclaw gateway status
```

Deve mostrar: `running` âœ…

Se quiser ver o painel web:
```bash
openclaw dashboard
```
Acesse: `http://SEU_IP:18789`

> ðŸ“¡ **Novo na v2026.3.2:** O Telegram streaming agora Ã© ativado por padrÃ£o. Quando seu agente estiver "pensando", vocÃª vai ver o indicador "digitando..." no Telegram em tempo real. Isso Ã© normal e esperado â€” o agente estÃ¡ processando sua mensagem ao vivo!

---

## Passo 5: Criar o Bot no Telegram (3 min)

1. Abra o Telegram no celular
2. Busque por `@BotFather`
3. Envie `/newbot`
4. Escolha um nome (ex: "Meu Agente AI")
5. Escolha um username (deve terminar em "bot", ex: "meuagenteai_bot")
6. **Copie o token** que o BotFather der

---

## Passo 6: Conectar Telegram ao OpenClaw (2 min)

De volta no terminal da VPS:

```bash
openclaw provider add telegram
```

Quando pedir, cole o token do bot.

Depois, abra o chat com seu bot no Telegram e envie `/start`.

---

## Passo 7: SeguranÃ§a IMEDIATA (2 min)

**ANTES de fazer qualquer outra coisa**, blindar o acesso:

```bash
# Ver a config atual
cat ~/.openclaw/openclaw.json
```

Garantir que `dmPolicy` estÃ¡ como `allowlist` e que SÃ“ o seu Telegram ID estÃ¡ autorizado.

Para descobrir seu Telegram ID:
- Envie qualquer mensagem pro bot
- Cheque os logs: `openclaw gateway logs`
- O ID aparece nas mensagens recebidas

> ðŸ”´ **ALERTA no curso:** Se dmPolicy estiver "open", QUALQUER PESSOA que encontrar seu bot pode comandar seu agente. Isso Ã© um risco de seguranÃ§a gravÃ­ssimo. Mostrar isso no vÃ­deo com Ãªnfase.

---

## Passo 8: Primeiro teste (1 min)

Envie uma mensagem pro bot no Telegram:

> "Oi! Me diz quem vocÃª Ã© e o que pode fazer."

Se o agente responder â†’ **SETUP COMPLETO!** ðŸŽ‰

> ðŸ“± **Novo na v2026.3.2:** VocÃª vai ver "digitando..." aparecer no Telegram enquanto o agente processa. Isso Ã© o streaming ativo â€” Ã© normal e significa que o agente estÃ¡ funcionando!

---

## Checkpoint do MÃ³dulo 1

- [ ] VPS rodando na Hostinger (Ubuntu 24.04)
- [ ] OpenClaw instalado (bare metal, nÃ£o Docker)
- [ ] Gateway rodando como serviÃ§o (24/7)
- [ ] **`tools.profile = full` configurado** â† NOVO (v2026.3.2)
- [ ] `openclaw config validate` sem erros â† NOVO (v2026.3.2)
- [ ] **`OPENCLAW_TZ=America/Sao_Paulo` configurado** â† NOVO (v2026.3.13)
- [ ] Bot do Telegram criado e conectado
- [ ] dmPolicy = allowlist (seguranÃ§a bÃ¡sica)
- [ ] Primeiro "oi" respondido âœ…

---

## Troubleshooting Comum

### "Command not found: openclaw"
```bash
# Recarregar o PATH
source ~/.bashrc
# Ou reinstalar
curl -fsSL https://openclaw.ai/install.sh | bash
```

### "Falha na autenticaÃ§Ã£o OAuth"
- Verificar se a conta ChatGPT tem assinatura Plus/Pro ativa
- Tentar login manual em https://chat.openai.com
- Se ok: openclaw auth login --provider openai
- Copiar a key novamente (sem espaÃ§os extras)

### "Bot nÃ£o responde no Telegram"
```bash
# Ver logs
openclaw gateway logs
# Verificar status
openclaw gateway status
```

### "Agente responde mas nÃ£o consegue executar comandos" (NOVO â€” v2026.3.2)
```bash
# Sintoma: bot responde "nÃ£o consigo fazer isso" para qualquer tarefa
# Causa: tools.profile ainda estÃ¡ como 'messaging'
openclaw config set tools.profile full
openclaw gateway restart
```

### "Gateway nÃ£o inicia"
```bash
# Checar porta
ss -tlnp | grep 18789
# Reiniciar
openclaw gateway restart
```

---

## Quanto custa?

| Item | Custo mensal |
|------|-------------|
| VPS Hostinger (KVM 2) | ~$10-15/mÃªs (cupom BRUNOOKAMOTO 10% off) |
| ChatGPT API fallback (opcional) | ~$5-15/mÃªs |
| OpenRouter multi-LLM (opcional) | ~$5-15/mÃªs |
| Telegram | GrÃ¡tis |
| **Total (ChatGPT OAuth)** | **~$99/mÃªs (sÃ³ assinatura)** |
| **Total (ChatGPT API key)** | **~$15-30/mÃªs** |
| **Total (OpenRouter â€” opÃ§Ã£o econÃ´mica)** | **~$10-25/mÃªs** | â€” opÃ§Ã£o econÃ´mica)** | **~$10-25/mÃªs** |

> ðŸ’¡ **Dica pro curso:** "Se vocÃª jÃ¡ tem ChatGPT Plus, o custo marginal Ã© zero â€” o OpenClaw usa sua conta existente."

> ðŸ’° **OpenRouter como alternativa:** Se quiser usar mÃºltiplos modelos (GPT-4o, Gemini Flash, Claude, etc.), a OpenRouter Ã© ~$5-15/mÃªs. Ver aula extra de OpenRouter.

---

*Este Ã© o mÃ³dulo mais tÃ©cnico. Depois daqui, Ã© sÃ³ configurar o agente â€” e isso Ã© a parte divertida.* ðŸ‡


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
