# PRD: Debug na VPS com Claude Code

> Roteiro para gravaÃ§Ã£o da Aula Extra B
> PÃºblico: leigo total â€” pode nunca ter acessado um servidor antes

---

## Objetivo da Aula

Ensinar como acessar a VPS e usar o Claude Code (CLI do OpenClaw) direto no terminal pra:
1. **Debugar problemas** quando o agente travar ou dar erro
2. **Arrumar pastas e arquivos** do workspace
3. **Usar `openclaw doctor`** pra diagnÃ³stico automÃ¡tico
4. **Usar `openclaw doctor fix`** pra correÃ§Ã£o automÃ¡tica

**Premissa:** O aluno pode nÃ£o saber usar terminal. Vai aprender fazendo.

---

## Tempo estimado: 18-22 minutos

---

## Estrutura da Aula

### Bloco 1: Por que aprender a debugar? (2 min)

**O que mostrar:**
- Agente travou e nÃ£o responde? Ã‰ normal â€” vocÃª vai saber resolver.
- Erro estranho apareceu? VocÃª vai saber onde procurar.
- Autonomia: nÃ£o depender de suporte pra problema simples.

**Frase-chave:**
> "VocÃª nÃ£o precisa ser tÃ©cnico. Mas precisa saber abrir o capÃ´ do carro quando a luz vermelha acende."

**CenÃ¡rios reais que o aluno vai enfrentar:**
- Agente parou de responder no Telegram
- Erro "token limit exceeded"
- **Agente ficou MUITO lento (respostas demoram 30s+)**
- Workspace bagunÃ§ado (arquivos demais)
- Gateway nÃ£o inicia depois de um restart
- Cron nÃ£o roda no horÃ¡rio

---

### Bloco 2: Como acessar a VPS (4 min)

**OpÃ§Ã£o 1: Terminal local (Mac/Linux/Windows Terminal)**

1. **Pegar o IP e senha da VPS** (no painel da Hostinger)

2. **Conectar via SSH:**
   ```bash
   ssh root@SEU_IP_AQUI
   ```
   Digite a senha quando pedir.

3. **VocÃª estÃ¡ dentro!** O prompt muda:
   ```
   root@vps-12345:~#
   ```

**OpÃ§Ã£o 2: Terminal do painel da Hostinger (mais fÃ¡cil pra iniciante)**

1. Ir em hPanel â†’ VPS â†’ clicar no botÃ£o "Terminal" (topo direito)
2. Terminal abre no navegador â€” sem configurar nada
3. JÃ¡ estÃ¡ conectado como root

**Mostrar os dois jeitos e deixar o aluno escolher.**

---

### Bloco 3: Comandos bÃ¡sicos de sobrevivÃªncia (3 min)

**Antes de debugar, ensinar o mÃ­nimo:**

1. **Ver onde vocÃª estÃ¡:**
   ```bash
   pwd
   ```
   Mostra o caminho atual (tipo `/root`)

2. **Listar arquivos:**
   ```bash
   ls -la
   ```
   Mostra tudo, incluindo pastas ocultas (comeÃ§am com `.`)

3. **Ir pro workspace do agente:**
   ```bash
   cd ~/.openclaw/workspace-NOME-DO-SEU-AGENTE
   ```
   Exemplo:
   ```bash
   cd ~/.openclaw/workspace-meu-agente
   ```

4. **Ver conteÃºdo de um arquivo:**
   ```bash
   cat AGENTS.md
   ```
   Ou pra arquivos grandes:
   ```bash
   less AGENTS.md
   ```
   (aperta `q` pra sair)

5. **Ver logs do gateway em tempo real:**
   ```bash
   openclaw gateway logs --follow
   ```
   (aperta Ctrl+C pra sair)

**Explicar o conceito de "caminho":**
> "Pensa no servidor como uma Ã¡rvore de pastas. VocÃª comeÃ§a na raiz (`/`) e vai descendo. `~` Ã© atalho pra pasta do usuÃ¡rio atual (`/root`)."

---

### Bloco 4: Usar Claude Code no terminal (5 min)

**O que Ã© o Claude Code:**
> "Ã‰ o Claude rodando DENTRO do terminal da VPS. VocÃª pergunta, ele responde e pode executar comandos pra vocÃª."

**Como invocar:**
```bash
claude
```

Abre uma sessÃ£o interativa. Agora vocÃª pode conversar:

**Exemplo 1 â€” Diagnosticar problema:**
```
VocÃª: Meu agente parou de responder no Telegram. O que pode ser?

Claude: Vou checar. Primeiro, status do gateway...
[executa: openclaw gateway status]

Claude: Gateway estÃ¡ parado. Vou ver os Ãºltimos logs...
[executa: openclaw gateway logs --tail 50]

Claude: Erro de token limit. O problema Ã© excesso de contexto.
Quer que eu limpe os logs antigos e reinicie?
```

**Exemplo 2 â€” Arrumar workspace:**
```
VocÃª: Meu workspace tÃ¡ cheio de arquivos de teste. Como limpo?

Claude: Vou listar o que tem aqui...
[executa: ls -lah]

Claude: Tem vÃ¡rios .txt e .json de teste. Posso mover pra uma pasta
/archive. Confirma?

VocÃª: Confirma.

Claude: [cria pasta, move arquivos, mostra resultado]
Pronto. Workspace limpo.
```

**Exemplo 3 â€” Ver uso de disco:**
```
VocÃª: Quanto espaÃ§o tenho na VPS?

Claude: [executa: df -h]
VocÃª tem 50GB total, 12GB usados, 38GB livres.
```

**Sair do Claude Code:**
- Digite `exit` ou aperta Ctrl+D

---

### Bloco 5: openclaw doctor â€” DiagnÃ³stico automÃ¡tico (3 min)

**O que faz:**
Roda uma bateria de checks e mostra o que tÃ¡ errado.

**Executar:**
```bash
openclaw doctor
```

**O que ele verifica:**
- âœ… Gateway rodando?
- âœ… Node.js na versÃ£o certa?
- âœ… Disco tem espaÃ§o?
- âœ… MemÃ³ria RAM disponÃ­vel?
- âœ… Config vÃ¡lida? (`openclaw.json`)
- âœ… Provider API key funciona?
- âœ… Canais conectados? (Telegram, etc.)
- âš ï¸ Logs muito grandes?
- âš ï¸ Workspaces com arquivos demais?

**SaÃ­da exemplo:**
```
âœ… Gateway: running
âœ… Node.js: v22.22.0
âœ… Disk: 38GB free (76%)
âœ… Memory: 2.1GB free (52%)
âœ… Config: valid
âœ… Provider: OpenAI API OK
âœ… Telegram: connected
âš ï¸ Logs: 450MB (considere limpar)
âš ï¸ Workspace "amora-cos": 2.3GB (revisar arquivos grandes)
```

**Explicar cada linha:**
> "Verde = tudo certo. Amarelo = atenÃ§Ã£o, pode virar problema. Vermelho = precisa corrigir agora."

---

### Bloco 6: openclaw doctor fix â€” CorreÃ§Ã£o automÃ¡tica (2 min)

**O que faz:**
Tenta corrigir problemas comuns automaticamente.

**Executar:**
```bash
openclaw doctor fix
```

**O que ele pode consertar sozinho:**
- Reiniciar gateway travado
- Limpar logs antigos (mantÃ©m Ãºltimos 7 dias)
- Corrigir permissÃµes de arquivos
- Recriar pastas ausentes
- Atualizar dependÃªncias quebradas

**O que ele NÃƒO faz (precisa de confirmaÃ§Ã£o):**
- Deletar arquivos do workspace
- Alterar config crÃ­tica
- Fazer upgrade de versÃ£o major

**Fluxo:**
```bash
openclaw doctor fix
```

SaÃ­da:
```
ðŸ” Scanning for issues...
âš ï¸ Found 3 fixable issues:

1. Gateway not responding â†’ restart
2. Logs > 500MB â†’ rotate
3. /tmp full â†’ cleanup

Apply fixes? [y/N]
```

Digitar `y` e Enter.

```
âœ… Gateway restarted
âœ… Logs rotated (freed 380MB)
âœ… /tmp cleaned (freed 1.2GB)

All checks passed. System healthy.
```

---

### Bloco 7: CenÃ¡rios reais + soluÃ§Ãµes (5 min)

**Mostrar 4 problemas comuns e como resolver:**

#### CenÃ¡rio 1: "Agente nÃ£o responde no Telegram"

**Passo a passo:**
1. SSH na VPS
2. `openclaw gateway status` â†’ se "stopped", rodar `openclaw gateway start`
3. Se continua parado, ver logs: `openclaw gateway logs --tail 50`
4. Se erro de API key, reconfigurar: `openclaw provider update openai`
5. Se erro de token, rodar `openclaw doctor fix`

#### CenÃ¡rio 2: "Erro de contexto muito grande"

**Sintoma:** Mensagem de erro "context window exceeded"

**SoluÃ§Ã£o:**
1. SSH na VPS
2. Ir pro workspace: `cd ~/.openclaw/workspace-SEU-AGENTE`
3. Abrir Claude Code: `claude`
4. Perguntar: "Meu contexto tÃ¡ muito grande. Pode compactar memory/YYYY-MM-DD.md antigos?"
5. Claude vai mover pra arquivo compactado e limpar

#### CenÃ¡rio 3: "Agente ficou MUITO lento (respostas demoram 30s+)"

**Sintoma:** Agente demora pra responder, Ã s vezes timeout

**Causas comuns:**

1. **Contexto de sessÃ£o passou de 100k tokens**
   - UsuÃ¡rio nunca deu `/new` ou `/compact`
   - SessÃ£o acumula meses de histÃ³rico
   
   **SoluÃ§Ã£o:**
   ```bash
   # Ver tamanho das sessÃµes
   cd ~/.openclaw
   du -sh sessions/*.json | sort -h | tail -10
   ```
   Se tiver session.json com mais de 5MB:
   - Pedir pro usuÃ¡rio rodar `/compact` ou `/new`
   - Ou mover pra backup: `mv sessions/SESSAO.json sessions/backup/`

2. **session.json corrompido ou gigante**
   - Arquivo pode chegar a 50MB+ se nunca compactou
   
   **SoluÃ§Ã£o:**
   ```bash
   # Ver o maior session.json
   ls -lh ~/.openclaw/sessions/ | sort -k5 -h | tail -5
   ```
   Se achar arquivo > 10MB, pode arquivar:
   ```bash
   mkdir -p ~/.openclaw/sessions/backup
   mv ~/.openclaw/sessions/ARQUIVO-GIGANTE.json ~/.openclaw/sessions/backup/
   ```

3. **Muitos agentes rodando em paralelo**
   - Cada agente consome memÃ³ria e CPU
   - VPS pequena nÃ£o aguenta 5+ agentes simultÃ¢neos
   
   **SoluÃ§Ã£o:**
   ```bash
   # Ver quantos processos do OpenClaw estÃ£o rodando
   ps aux | grep openclaw | wc -l
   ```
   Se tiver mais de 3-4 em VPS pequena (4GB RAM), considerar:
   - Parar agentes nÃ£o-usados
   - Upgrade de VPS
   - Usar `sessionTarget: isolated` com `cleanup: delete` nos crons

**Explicar no vÃ­deo:**
> "O contexto Ã© como a memÃ³ria de curto prazo do agente. Se vocÃª nunca limpar, Ã© como tentar lembrar de TUDO que aconteceu nos Ãºltimos 6 meses â€” o cÃ©rebro trava. Use `/compact` toda semana ou `/new` quando precisar recomeÃ§ar."

#### CenÃ¡rio 4: "VPS sem espaÃ§o"

**Sintoma:** "No space left on device"

**SoluÃ§Ã£o:**
1. Rodar `openclaw doctor` â†’ vai mostrar o problema
2. Rodar `openclaw doctor fix` â†’ limpa logs e /tmp
3. Se continua cheio, usar Claude Code:
   ```
   VocÃª: Preciso liberar espaÃ§o. O que tÃ¡ ocupando mais?
   Claude: [executa: du -sh ~/.openclaw/* | sort -h]
   Mostra os workspaces maiores...
   ```
4. Decidir o que arquivar ou deletar

---

## Checkpoint da Aula

Ao final, o aluno deve saber:
- [ ] Como conectar na VPS via SSH (terminal local ou painel Hostinger)
- [ ] Comandos bÃ¡sicos de navegaÃ§Ã£o (pwd, ls, cd, cat)
- [ ] Como invocar Claude Code no terminal (`claude`)
- [ ] Como usar `openclaw doctor` pra diagnÃ³stico
- [ ] Como usar `openclaw doctor fix` pra correÃ§Ã£o automÃ¡tica
- [ ] Resolver 4 problemas comuns sozinho (nÃ£o responde, contexto, lentidÃ£o, sem espaÃ§o)

---

## Alertas de SeguranÃ§a

ðŸ”´ **NUNCA** deletar arquivos sem saber o que sÃ£o
ðŸ”´ **SEMPRE** fazer backup antes de mudanÃ§as grandes
ðŸ”´ **CUIDADO** com `rm -rf` â€” pode apagar tudo

**Regra de ouro:**
> "Se nÃ£o sabe o que o comando faz, pergunte pro Claude Code antes de rodar."

---

## Prompt que vai no PDF

Vai estar no arquivo `prompts/modulo-extra-b-debug.md`.

---

## Troubleshooting Comum

### "Permission denied" ao tentar algo
Provavelmente precisa de `sudo`. Mas como root, nÃ£o deveria acontecer.

### "Command not found: claude"
```bash
# Reinstalar OpenClaw CLI
npm install -g @anthropic-ai/claude-code
```

### "SSH connection refused"
- Verificar se o IP tÃ¡ certo
- Verificar se a VPS tÃ¡ ligada (painel Hostinger)
- Verificar se a porta 22 tÃ¡ aberta (firewall)

---

*Esta aula dÃ¡ autonomia. Antes dela, o aluno depende de suporte. Depois, resolve 80% dos problemas sozinho.*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
