# Skills por Perfil de UsuÃ¡rio

> Guia curado de skills OpenClaw organizadas por perfil. Copie o comando de instalaÃ§Ã£o e vÃ¡.

---

## âš ï¸ Avisos Importantes

### SeguranÃ§a Primeiro
**Sempre revise o cÃ³digo antes de instalar uma skill!** Skills tÃªm acesso ao seu workspace, credenciais e podem executar comandos. Instale apenas de fontes confiÃ¡veis (ClawHub verificado, repositÃ³rios oficiais).

```bash
# Antes de instalar, inspecione o cÃ³digo:
git clone <repo> /tmp/skill-review
cat /tmp/skill-review/SKILL.md
```

### Evite RedundÃ¢ncias
- **remind-me â‰ˆ cron nativo** â€” OpenClaw jÃ¡ tem cron integrado. SÃ³ instale remind-me se precisar de features extras (recorrÃªncia complexa, snooze)
- **mÃºltiplos skills de clima** â€” escolha um (weather built-in Ã© suficiente)
- **creators duplicados** â€” um gerador de imagens basta (openai-image-gen built-in ou stable-diffusion)

### Creators SÃ£o Skills, NÃ£o Agentes
âŒ **Errado:** 8 agentes especializados (ImageAgent, VideoAgent, WriterAgent...)  
âœ… **Certo:** 1 agente principal + 8 skills (image-gen, video-edit, grammar-check...)

**Por quÃª?** Um agente com contexto unificado e vÃ¡rias ferramentas > mÃºltiplos agentes desconexos. Agents devem ter *propÃ³sitos*, nÃ£o *funÃ§Ãµes*.

---

## Skills Essenciais (Todos os Perfis)

Independente do seu trabalho, estas sÃ£o fundamentais:

### 1. **github** (built-in)
- **O que faz:** Cria issues, PRs, busca cÃ³digo, gerencia repos
- **Por que Ã© essencial:** Seu workspace estÃ¡ no Git. Este Ã© o controle de versÃ£o do seu agente.
- **InstalaÃ§Ã£o:** `openclaw skill enable github`

### 2. **1password** (built-in)
- **O que faz:** LÃª/cria/atualiza credenciais no 1Password via CLI
- **Por que Ã© essencial:** Nunca hardcode credenciais. Seu agente precisa gerenciar segredos com seguranÃ§a.
- **InstalaÃ§Ã£o:** `openclaw skill enable 1password` (requer 1Password CLI configurado)

### 3. **weather** (built-in)
- **O que faz:** Consulta previsÃ£o do tempo via wttr.in
- **Por que Ã© essencial:** Contexto fÃ­sico importa. "Devo sair agora?" "Vai chover na reuniÃ£o externa?"
- **InstalaÃ§Ã£o:** `openclaw skill enable weather`

### 4. **healthcheck** (built-in)
- **O que faz:** Monitora serviÃ§os HTTP/HTTPS, notifica quando caem
- **Por que Ã© essencial:** Proatividade. Saiba se seu site/API caiu antes dos clientes reclamarem.
- **InstalaÃ§Ã£o:** `openclaw skill enable healthcheck`

---

## ðŸ‘” Empreendedor / Founder

Foco em operaÃ§Ãµes, mÃ©tricas, relatÃ³rios, tomada de decisÃ£o.

### 1. **gog (Google Workspace)** (built-in)
- **O que faz:** Acessa Gmail, Calendar, Drive, Sheets, Docs
- **Por que Ã© Ãºtil:** Centraliza comunicaÃ§Ã£o e dados. Leia emails, crie eventos, gere relatÃ³rios direto de Sheets.
- **InstalaÃ§Ã£o:** `openclaw skill enable gog` (requer credenciais OAuth)

### 2. **stripe-api** (clawhub.com/stripe)
- **O que faz:** Consulta receita, clientes, assinaturas, faturas no Stripe
- **Por que Ã© Ãºtil:** MÃ©tricas de receita em tempo real. "Quanto faturei hoje?" "Quantas assinaturas novas?"
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/stripe`

### 3. **analytics-reports** (clawhub.com/analytics)
- **O que faz:** Puxa dados do Google Analytics e gera relatÃ³rios
- **Por que Ã© Ãºtil:** TrÃ¡fego, conversÃ£o, funil â€” tudo acessÃ­vel via chat.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/analytics`

### 4. **postgres-query** (clawhub.com/postgres)
- **O que faz:** Executa queries SQL no seu banco de produÃ§Ã£o (read-only recomendado)
- **Por que Ã© Ãºtil:** "Quantos usuÃ¡rios ativos?" "Qual feature mais usada?" Respostas instantÃ¢neas.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/postgres`

### 5. **notion-db** (clawhub.com/notion)
- **O que faz:** LÃª/cria/atualiza databases no Notion
- **Por que Ã© Ãºtil:** Se vocÃª gerencia projetos/CRM no Notion, o agente acessa e atualiza tudo.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/notion`

### 6. **slack-admin** (clawhub.com/slack)
- **O que faz:** Envia mensagens, lÃª canais, cria threads no Slack
- **Por que Ã© Ãºtil:** Delegue notificaÃ§Ãµes ao time, resuma conversas importantes.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/slack`

### 7. **financial-dashboard** (clawhub.com/finance)
- **O que faz:** Conecta mÃºltiplas APIs financeiras (Stripe, QuickBooks, PagSeguro) e gera dashboards
- **Por que Ã© Ãºtil:** VisÃ£o unificada de receita, despesas, fluxo de caixa.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/finance`

---

## ðŸŽ¨ Criador de ConteÃºdo

Foco em produÃ§Ã£o de conteÃºdo, redes sociais, design, ediÃ§Ã£o.

### 1. **openai-image-gen** (built-in)
- **O que faz:** Gera imagens com DALL-E
- **Por que Ã© Ãºtil:** Thumbnails, ilustraÃ§Ãµes, assets visuais sob demanda.
- **InstalaÃ§Ã£o:** `openclaw skill enable openai-image-gen`

### 2. **openai-whisper-api** (built-in)
- **O que faz:** Transcreve Ã¡udio para texto (podcasts, entrevistas, vÃ­deos)
- **Por que Ã© Ãºtil:** TranscriÃ§Ãµes automÃ¡ticas para legendas, blog posts, show notes.
- **InstalaÃ§Ã£o:** `openclaw skill enable openai-whisper-api`

### 3. **video-frames** (built-in)
- **O que faz:** Extrai frames de vÃ­deos para anÃ¡lise
- **Por que Ã© Ãºtil:** Escolha o melhor frame para thumbnail, analise composiÃ§Ã£o.
- **InstalaÃ§Ã£o:** `openclaw skill enable video-frames`

### 4. **ffmpeg-edit** (clawhub.com/ffmpeg)
- **O que faz:** Corta, concatena, converte vÃ­deos via ffmpeg
- **Por que Ã© Ãºtil:** EdiÃ§Ãµes rÃ¡pidas sem abrir Premiere. "Corta os primeiros 10s e exporta em 720p."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/ffmpeg`

### 5. **youtube-metadata** (clawhub.com/youtube)
- **O que faz:** Faz upload, atualiza tÃ­tulo/descriÃ§Ã£o/tags de vÃ­deos no YouTube
- **Por que Ã© Ãºtil:** Automatize publicaÃ§Ã£o. "Faz upload desse vÃ­deo com essa thumbnail e essa descriÃ§Ã£o."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/youtube`

### 6. **twitter-scheduler** (clawhub.com/twitter)
- **O que faz:** Agenda tweets, threads, analisa engajamento
- **Por que Ã© Ãºtil:** Crie threads inteiras em uma conversa, o agente agenda e publica.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/twitter`

### 7. **canva-api** (clawhub.com/canva)
- **O que faz:** Cria designs via Canva API (posts, stories, banners)
- **Por que Ã© Ãºtil:** GeraÃ§Ã£o de assets visuais em escala. "Cria 5 variaÃ§Ãµes desse post."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/canva`

### 8. **subtitle-sync** (clawhub.com/subtitles)
- **O que faz:** Gera e sincroniza legendas SRT/VTT
- **Por que Ã© Ãºtil:** Acessibilidade automÃ¡tica. TranscriÃ§Ã£o â†’ legendas sincronizadas.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/subtitles`

---

## ðŸ’» Desenvolvedor

Foco em coding, CI/CD, debugging, deploy, monitoramento.

### 1. **github** (built-in)
- **O que faz:** Cria issues, PRs, busca cÃ³digo, gerencia repos
- **Por que Ã© Ãºtil:** "Abre uma issue pra esse bug." "Lista PRs pendentes de review."
- **InstalaÃ§Ã£o:** `openclaw skill enable github`

### 2. **tmux** (built-in)
- **O que faz:** Gerencia sessÃµes tmux (cria, lista, mata, envia comandos)
- **Por que Ã© Ãºtil:** Rode servidores/builds em background, monitore processos.
- **InstalaÃ§Ã£o:** `openclaw skill enable tmux`

### 3. **docker-compose** (clawhub.com/docker)
- **O que faz:** Sobe/desce containers, lÃª logs, reinicia serviÃ§os
- **Por que Ã© Ãºtil:** "Reinicia o container do Redis." "Logs do backend nos Ãºltimos 5min."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/docker`

### 4. **postgres-query** (clawhub.com/postgres)
- **O que faz:** Executa queries SQL no banco de dev/staging
- **Por que Ã© Ãºtil:** Debugging rÃ¡pido. "Mostra o Ãºltimo pedido do usuÃ¡rio X."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/postgres`

### 5. **sentry-alerts** (clawhub.com/sentry)
- **O que faz:** Consulta erros no Sentry, cria issues no GitHub automaticamente
- **Por que Ã© Ãºtil:** Proatividade. Erros crÃ­ticos viram issues sem intervenÃ§Ã£o manual.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/sentry`

### 6. **cloudflare-dns** (clawhub.com/cloudflare)
- **O que faz:** Gerencia DNS, cache, firewall rules na Cloudflare
- **Por que Ã© Ãºtil:** "Adiciona um registro A pra staging." "Limpa o cache."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/cloudflare`

### 7. **aws-cli-wrapper** (clawhub.com/aws)
- **O que faz:** Executa comandos AWS (EC2, S3, Lambda, RDS)
- **Por que Ã© Ãºtil:** "Lista instÃ¢ncias ativas." "Faz deploy da Lambda." Infraestrutura via chat.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/aws`

### 8. **code-review-ai** (clawhub.com/code-review)
- **O que faz:** Analisa PRs, sugere melhorias, detecta bugs
- **Por que Ã© Ãºtil:** Review automÃ¡tico antes de pedir ao time. Feedback instantÃ¢neo.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/code-review`

---

## ðŸ“… Produtividade Pessoal

Foco em calendÃ¡rio, notas, tarefas, automaÃ§Ã£o de rotina.

### 1. **gog (Google Workspace)** (built-in)
- **O que faz:** Acessa Gmail, Calendar, Drive, Docs
- **Por que Ã© Ãºtil:** "Qual minha prÃ³xima reuniÃ£o?" "Cria um doc com minhas notas de hoje."
- **InstalaÃ§Ã£o:** `openclaw skill enable gog`

### 2. **todoist-sync** (clawhub.com/todoist)
- **O que faz:** LÃª/cria/completa tarefas no Todoist
- **Por que Ã© Ãºtil:** Gerenciamento de tarefas via chat. "Adiciona 'comprar cafÃ©' pra amanhÃ£."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/todoist`

### 3. **notion-db** (clawhub.com/notion)
- **O que faz:** LÃª/cria/atualiza databases no Notion
- **Por que Ã© Ãºtil:** Se vocÃª usa Notion como segundo cÃ©rebro, o agente acessa tudo.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/notion`

### 4. **obsidian-vault** (clawhub.com/obsidian)
- **O que faz:** LÃª/cria/busca notas no Obsidian (vault local)
- **Por que Ã© Ãºtil:** PKM integrado. "Busca minhas notas sobre X." "Cria uma nota com esse conteÃºdo."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/obsidian`

### 5. **calendar-assistant** (clawhub.com/calendar)
- **O que faz:** Agenda reuniÃµes, detecta conflitos, sugere horÃ¡rios
- **Por que Ã© Ãºtil:** "Agenda 30min com JoÃ£o na prÃ³xima semana, de manhÃ£."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/calendar`

### 6. **email-summarizer** (clawhub.com/email-summary)
- **O que faz:** Resume inbox nÃ£o lida, destaca urgÃªncias
- **Por que Ã© Ãºtil:** "Resume meus emails de hoje." Zero-inbox assistido.
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/email-summary`

### 7. **habit-tracker** (clawhub.com/habits)
- **O que faz:** Rastreia hÃ¡bitos diÃ¡rios, envia lembretes
- **Por que Ã© Ãºtil:** "JÃ¡ bebi 2L de Ã¡gua hoje?" "Lembra de meditar Ã s 19h."
- **InstalaÃ§Ã£o:** `openclaw skill install clawhub/habits`

---

## ðŸ” Como Descobrir Mais Skills

- **ClawHub oficial:** https://clawhub.com
- **GitHub topic:** procure por `openclaw-skill` no GitHub
- **Comunidade Discord:** pergunte no #skills o que as pessoas usam
- **Crie a sua:** se nÃ£o existe, Ã© uma oportunidade! Skills sÃ£o sÃ³ bash + SKILL.md

---

## ðŸ“ Anatomia de uma Skill

Uma skill OpenClaw Ã© simplesmente:

```
skill-name/
â”œâ”€â”€ SKILL.md          # DocumentaÃ§Ã£o + declaraÃ§Ã£o de tools
â”œâ”€â”€ tool-one.sh       # Script executÃ¡vel
â””â”€â”€ tool-two.sh       # Outro script
```

O agente lÃª `SKILL.md`, descobre as tools disponÃ­veis, e executa os scripts quando necessÃ¡rio.

**Dica:** Comece simples. Uma skill de 50 linhas que resolve SEU problema > uma skill de 500 linhas genÃ©rica.

---

## âœ… Checklist de InstalaÃ§Ã£o

Antes de instalar uma skill:

- [ ] Li o `SKILL.md` e entendo o que ela faz
- [ ] Revisei os scripts bash (procuro por `rm -rf`, `curl` suspeito, `eval`)
- [ ] Verifiquei que nÃ£o duplica funcionalidade que jÃ¡ tenho
- [ ] Sei quais credenciais/APIs ela precisa
- [ ] Testei em ambiente isolado primeiro (se crÃ­tico)

Depois de instalar:

- [ ] Configurei credenciais no `.env` ou 1Password
- [ ] Testei cada tool manualmente
- [ ] Documentei uso especÃ­fico no meu `TOOLS.md`
- [ ] Atualizei `AGENTS.md` se a skill requer regras especiais

---

**Lembre-se:** Skills amplificam o agente. Mas um agente sem identidade forte (SOUL.md, USER.md) continua genÃ©rico, independente de quantas skills instalar. Invista tempo em quem o agente Ã‰ antes de multiplicar o que ele FAZ.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
