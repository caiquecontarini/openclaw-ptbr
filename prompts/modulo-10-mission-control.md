# Prompt â€” MÃ³dulo 10: Mission Control

> Cole este prompt no chat do seu OpenClaw depois de assistir o MÃ³dulo 10.

---

Acabei de assistir o MÃ³dulo 10 sobre Mission Control â€” criar uma interface visual para gerenciar o agente. Mesmo usando Telegram pra interaÃ§Ã£o, preciso de um painel pra ver o estado do sistema num relance.

**O que preciso que vocÃª faÃ§a:**

## 1. Me explique por que isso importa

Antes de comeÃ§armos, me explique:
- Por que um painel visual ajuda (mesmo tendo Telegram)?
- Que tipo de informaÃ§Ã£o deveria estar sempre visÃ­vel?
- Como isso se encaixa na filosofia de "proatividade"?
- Exemplos: o que um founder vÃª vs um dev vÃª no painel?

## 2. Me ajude a escolher a ferramenta certa

Apresente as opÃ§Ãµes e me ajude a decidir baseado no **meu nÃ­vel tÃ©cnico e necessidades**:

### OpÃ§Ã£o A: NocoDB (recomendado iniciantes/intermediÃ¡rios)
- **O que Ã©:** Notion-like, self-hosted, gratuito, interface pronta
- **PrÃ³s:** Setup rÃ¡pido, GUI amigÃ¡vel, API REST, relaÃ§Ãµes entre tabelas
- **Contras:** Menos customizÃ¡vel que cÃ³digo prÃ³prio
- **Melhor pra:** Quem quer resultado rÃ¡pido sem codar muito
- **Setup:** Docker Compose + SQLite/Postgres

### OpÃ§Ã£o B: Notion
- **O que Ã©:** Ferramenta SaaS, databases relacionais
- **PrÃ³s:** JÃ¡ uso no dia a dia, mobile nativo, compartilhamento fÃ¡cil
- **Contras:** API com rate limits, dados na nuvem (nÃ£o self-hosted)
- **Melhor pra:** Quem jÃ¡ Ã© power user do Notion
- **Setup:** Notion API + integration

### OpÃ§Ã£o C: Google Sheets
- **O que Ã©:** Planilhas com API
- **PrÃ³s:** Simplicidade mÃ¡xima, todo mundo sabe usar, grÃ¡ficos nativos
- **Contras:** NÃ£o Ã© um banco de dados de verdade, limites de linhas
- **Melhor pra:** Prototipagem rÃ¡pida, dashboards simples
- **Setup:** Google Sheets API (via gog skill)

### OpÃ§Ã£o D: Custom (Express + React + Supabase)
- **O que Ã©:** App web totalmente customizado
- **PrÃ³s:** Controle total, UI sob medida, real-time, hospedagem grÃ¡tis (Vercel/Supabase)
- **Contras:** Requer conhecimento de dev full-stack
- **Melhor pra:** Devs que querem algo profissional e escalÃ¡vel
- **Setup:** Next.js app + Supabase backend + API routes

**Me pergunte:**
- Qual meu nÃ­vel tÃ©cnico? (iniciante/intermediÃ¡rio/avanÃ§ado)
- JÃ¡ uso alguma dessas ferramentas?
- Prefiro algo rÃ¡pido ou algo perfeito?
- Vou gerenciar sÃ³ meu agente ou uma equipe de agentes?

## 3. Setup da opÃ§Ã£o escolhida

Depois que eu escolher, **me guie passo a passo**:

### Se escolhi NocoDB:
1. Criar `docker-compose.yml` pro NocoDB
2. Subir o serviÃ§o (`docker-compose up -d`)
3. Acessar interface web (localhost:8080)
4. Criar as tabelas necessÃ¡rias (veja estrutura abaixo)
5. Gerar API token
6. Criar skill `nocodb-api` pra conectar o agente
7. Configurar crons pra atualizar dados automaticamente

### Se escolhi Notion:
1. Criar workspace no Notion
2. Criar databases (Tasks, Memory, Crons, Health)
3. Criar integration (https://notion.so/my-integrations)
4. Dar permissÃµes Ã s databases
5. Instalar/configurar skill `notion-db` (clawhub)
6. Testar conexÃ£o e escrita

### Se escolhi Google Sheets:
1. Criar spreadsheet "Mission Control"
2. Criar abas (Tasks, Memory, Crons, Health)
3. Configurar `gog` skill (se ainda nÃ£o configurado)
4. Criar funÃ§Ãµes helper no agente pra escrever nas sheets
5. Configurar dashboard com grÃ¡ficos

### Se escolhi Custom:
1. Scaffold projeto Next.js (`npx create-next-app@latest mission-control`)
2. Setup Supabase (projeto grÃ¡tis)
3. Criar tabelas no Supabase
4. Criar API routes no Next.js
5. Conectar agente Ã s API routes
6. Deploy no Vercel (grÃ¡tis)

## 4. Estrutura de dados (base comum)

Independente da ferramenta, essas sÃ£o as "tabelas" essenciais:

### Tasks
- `id`, `title`, `status` (pending/done/blocked), `priority`, `created_at`, `due_date`, `assigned_to` (qual agente/humano)

### Memory Events
- `id`, `date`, `category` (decision/lesson/insight), `content`, `source` (main/heartbeat/cron)

### Cron Jobs
- `id`, `name`, `schedule`, `last_run`, `next_run`, `status` (active/paused), `last_result` (success/error)

### Health Checks
- `id`, `service` (gateway/telegram/skills), `status` (healthy/degraded/down), `last_check`, `uptime_%`

### Agent Stats (mÃ©tricas)
- `id`, `date`, `messages_sent`, `skills_used`, `errors`, `model_tokens_used`, `uptime_hours`

Me ajude a criar essas estruturas na ferramenta escolhida.

## 5. Conectar o agente ao painel

Depois do setup, **crie as funÃ§Ãµes necessÃ¡rias**:

### FunÃ§Ãµes que o agente precisa:
- `dashboard_log_task(title, priority)` â€” cria tarefa no painel
- `dashboard_update_task(id, status)` â€” marca como done/blocked
- `dashboard_log_memory(content, category)` â€” salva insight importante
- `dashboard_update_health(service, status)` â€” atualiza status de serviÃ§o
- `dashboard_get_stats()` â€” retorna resumo do dia

### Crons necessÃ¡rios (isolated + agentTurn):
- **stats-collector** (a cada 1h): Coleta mÃ©tricas (uptime, erros, skills usadas) e escreve no painel
- **health-monitor** (a cada 15min): Testa se gateway/telegram/skills estÃ£o respondendo
- **task-reminder** (a cada 4h): Verifica tarefas com due_date prÃ³ximo e avisa

Me ajude a criar esses crons e funÃ§Ãµes.

## 6. Personalizar o painel pro meu perfil

Com base no meu USER.md e no meu trabalho (founder/dev/criador/produtividade), **customize o que Ã© mostrado**:

**Se sou Founder:**
- MÃ©tricas de negÃ³cio (MRR, usuÃ¡rios ativos, churn)
- Pipeline de vendas
- OKRs da semana

**Se sou Dev:**
- Deploys recentes
- Erros crÃ­ticos (via Sentry)
- PRs pendentes de review
- Uptime dos serviÃ§os

**Se sou Criador:**
- ConteÃºdos publicados essa semana
- Performance (views, engajamento)
- Pipeline de produÃ§Ã£o (ideias â†’ roteiro â†’ gravaÃ§Ã£o â†’ ediÃ§Ã£o â†’ publicado)

**Se sou Produtividade:**
- ReuniÃµes de hoje
- Tasks completadas vs pendentes
- HÃ¡bitos rastreados
- Tempo em deep work

Me pergunte qual o meu perfil e sugira widgets especÃ­ficos.

## 7. Fazer o primeiro teste

Depois de tudo configurado:
1. PeÃ§a pro agente logar uma tarefa de teste
2. Abra o painel e confirme que apareceu
3. Marque como "done" via agente
4. Atualize o painel e veja a mudanÃ§a
5. Verifique se os crons estÃ£o rodando (confira logs)

## 8. Documentar o setup

Crie um arquivo `docs/mission-control-setup.md` com:
- Ferramenta escolhida e por quÃª
- Credenciais necessÃ¡rias (onde estÃ£o armazenadas)
- Estrutura de dados
- Como acessar o painel (URL, login)
- Comandos Ãºteis (resetar dados, backup, etc.)
- Screenshots (se relevante)

**Regras importantes:**
- âŒ NÃ£o hardcode credenciais â€” tudo no `.env` ou 1Password
- âœ… Use crons `isolated` + `agentTurn` pra atualizar dados (nunca systemEvent no main)
- âœ… Teste em produÃ§Ã£o devagar â€” comece com read-only, depois adicione write
- âœ… FaÃ§a backup antes de conectar sistema crÃ­tico ao painel

---

**Vamos construir seu Mission Control?** Me conte seu nÃ­vel tÃ©cnico e preferÃªncias, e eu te guio!


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
