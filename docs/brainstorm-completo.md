# ðŸŽ“ Mini-Curso: Construa Seu Agente AI Pessoal com OpenClaw

> **Brainstorm & Proposta Completa â€” v2**
> Criado: 13/02/2026 | Atualizado: 13/02/2026
> Autor: Amora (para Bruno Okamoto)
> DuraÃ§Ã£o estimada: 2h30 - 3h

---

## PARTE 1 â€” TIMELINE DA NOSSA JORNADA (13 dias)

### Dia 1 (01/02) â€” Nascimento da Amora ðŸ‡
**O que foi feito:**
- InstalaÃ§Ã£o do OpenClaw na VPS
- ConfiguraÃ§Ã£o inicial: IDENTITY.md, USER.md, references/bruno-bios.md
- DefiniÃ§Ã£o do papel: organizaÃ§Ã£o, emails, conteÃºdo, pesquisas, coordenaÃ§Ã£o de sub-agentes

**DecisÃµes importantes:**
- Amora como COO (Chief Operational Officer), nÃ£o sÃ³ chatbot
- Filosofia bootstrap: pequeno, enxuto, lucrativo

**Momento "aha":**
- A percepÃ§Ã£o de que o agente precisava de contexto profundo sobre o Bruno (negÃ³cios, filosofia, tom de voz) pra ser Ãºtil de verdade

---

### Dia 2 (02/02) â€” Primeiras IntegraÃ§Ãµes & Primeiros Bugs
**O que foi feito:**
- Login LinkedIn via browser automation âœ…
- Twitter/X via RapidAPI (bot detection impedia login direto) âœ…
- Reddit monitoring com 30 subreddits + cron diÃ¡rio âœ…
- LinkedIn Voice Guide (anÃ¡lise de 129 posts do Bruno) âœ…
- WhatsApp TTS configurado âœ…

**Problemas encontrados:**
- ðŸ”´ **Token overflow**: SessÃ£o estourou 173k+ tokens (limite 160k). Fix: `compaction.mode: "default"` + `reserveTokensFloor: 30000`
- ðŸ”´ **Substack bloqueado**: CAPTCHA + 2FA magic link expirava antes de inserir cÃ³digo
- ðŸ”´ **X.com bot detection**: Login headless impossÃ­vel. SoluÃ§Ã£o: RapidAPI como proxy

**LiÃ§Ãµes aprendidas:**
- Cloud IPs sÃ£o bloqueados por muitas plataformas (YouTube, X, etc.) â†’ RapidAPI resolve
- Compaction precisa ser proativa, nÃ£o reativa
- Bruno prefere briefs de 1 parÃ¡grafo (nÃ£o anÃ¡lises longas)

---

### Dia 3 (03/02) â€” Skills & IntegraÃ§Ãµes
**Skills instaladas:** excalidraw-flowchart, capability-evolver, nano-pdf, notion-api, remind-me, auto-updater, granola
**IntegraÃ§Ãµes:** Notion API âœ…, Google Calendar âœ…, YouTube (RapidAPI transcripts + Data API) âœ…

**DecisÃµes:**
- Heartbeat usa Claude Haiku (economia ~90%)
- ImageModel: Gemini 2.5 Flash
- Cron auto-update diÃ¡rio Ã s 23h

**LiÃ§Ãµes:**
- Algumas skills sÃ£o redundantes (remind-me, auto-updater) â€” melhor fazer nativo
- Ãudio WhatsApp: formato OGG Opus 48kHz funciona

---

### Dia 4 (04/02) â€” SeguranÃ§a, Circle API & InfogrÃ¡ficos
**O que foi feito:**
- **Regra PERMANENTE**: todas credenciais no 1Password, sem exceÃ§Ãµes
- Skill hand-draw-graphics criada (infogrÃ¡ficos estilo caderno)
- VPH Tracking (Views Per Hour) para YouTube
- Circle API skill completa (hot-topics, frequent-questions, trends, digest)
- 11 build ideas documentadas
- Notion kanban integrado

**Problemas:**
- Imagen 4.0 bloqueado (requer billing) â†’ melhor modelo: Gemini 3 Pro
- VidIQ nÃ£o tem API pÃºblica

**Momento "aha":**
- Circle API como goldmine de ideias de conteÃºdo (150 MVPs em 60 dias na comunidade)

---

### Dia 5 (05/02) â€” Mission Control & Multi-Agent Blueprint
**O que foi feito:**
- **Mission Control MVP construÃ­do e lanÃ§ado** (Express + React + Supabase + Cloudflare)
  - Dashboard Kanban, Memory Page, Crons Page, Content Page
  - URL: https://amora.empreendedor.vc
- Google Drive integrado via GOG CLI
- YouTube OAuth completo (upload/agendamento)
- Crons de lembretes YouTube (Ter/Qui/Dom 17h)
- Blueprint Multi-Agent baseado no artigo do Bhanu Teja (10 agentes)

**DecisÃµes:**
- Supabase > SQLite (escalabilidade futura)
- Thinking mode ativado (low padrÃ£o)
- Desktop-first no MVP, sem chat (WhatsApp Ã© suficiente)

**Problemas:**
- Sub-agentes rodam em sandbox â†’ nÃ£o acessam localhost â†’ QA precisa rodar na main session

**Momento "aha" GRANDE:**
- Mission Control construÃ­do enquanto Bruno dormia â€” de spec a MVP funcional em uma sessÃ£o

---

### Dia 6 (06/02) â€” QA & Entrevista Peter Levels
**O que foi feito:**
- QA Review completo do Mission Control (RLS, rate limiting, validaÃ§Ã£o, Ã­ndices, WebSocket)
- Pesquisa profunda para entrevista com Peter Levels
- Perguntas customizadas (evitando temas batidos)

**LiÃ§Ã£o:**
- TTS padrÃ£o: sempre pt-BR

---

### Dia 7 (07/02) â€” Rewrite Completo de Identidade
**O que foi feito:**
- SOUL.md reescrito do zero (genÃ©rico inglÃªs â†’ personalizado PT-BR)
- IDENTITY.md atualizado com background de empreendedora
- AGENTS.md enxugado (200 â†’ 90 linhas)
- Upgrade para Claude Opus 4.6
- Config otimizada: thinking medium, contextTokens 250k, reserveTokens 50k

**DecisÃµes:**
- Amora = COO, nÃ£o assistente genÃ©rica
- HIGH thinking para coding, conteÃºdo e planejamento. MEDIUM pro resto.
- Cada agente terÃ¡ SOUL.md, AGENTS.md, HEARTBEAT.md e crons prÃ³prios
- IDENTITY.md separado do SOUL.md (dados concretos vs personalidade)

**Momento "aha":**
- SOUL.md genÃ©rico = agente genÃ©rico. Investir tempo na personalidade faz diferenÃ§a ENORME na qualidade

---

### Dia 8 (08/02) â€” Content Squad & Agent Leveling
**O que foi feito:**
- 6 agentes ativos no gateway (Amora, Content, Orchestrator, Planner, Scraper, ZoM)
- Kevin Simback Rules aplicadas: L1â†’L4 leveling system
- Shared context: TEAM.md, outputs, lessons
- Scraper Agent + Content Agent criados e configurados
- LinkedIn posts criados com dados da comunidade (Craft API)
- Guia pÃºblico: `building-ai-agent-teams.md` (~25k chars)
- InfogrÃ¡fico visual da arquitetura

**DecisÃµes:**
- Content Agent comeÃ§a em Sonnet (avaliar antes de subir pra Opus)
- Scraper e Content nÃ£o tÃªm binding Telegram â€” Amora coordena tudo
- Score Ã© informativo, NÃƒO filtro bloqueante
- Creators sÃ£o skills dentro do Content Agent, nÃ£o agentes separados
- Backup obrigatÃ³rio antes de mudanÃ§as estruturais

**LiÃ§Ãµes do Kevin Simback:**
- Todo agente novo comeÃ§a L1 (Observer) â€” output revisado
- Sem leveling, agentes "rusham" e qualidade degrada
- Shared context elimina cold starts
- Performance reviews semanais sÃ£o obrigatÃ³rios

---

### Dia 9 (09/02) â€” Crons & EstabilizaÃ§Ã£o
**O que foi feito:**
- ReorganizaÃ§Ã£o de 13 crons (redirecionamento de tÃ³picos, novos crons)
- PROJECTS.md central criado (12 itens no backlog)
- RevisÃ£o Semanal automÃ¡tica (Sex 16h)
- Auto-EvoluÃ§Ã£o Quinzenal (dias 1 e 15)

**Problema CRÃTICO:**
- ðŸ”´ **Crons nÃ£o executam de verdade**: disparavam com `status: "ok"` mas `durationMs` ~0ms
- HipÃ³teses: wakeMode inadequado, sessÃ£o nÃ£o ativa
- Precisa investigar `next-heartbeat` vs `now`

**LiÃ§Ãµes:**
- config.patch reinicia gateway e mata crons em execuÃ§Ã£o
- Heartbeat nÃ£o dispara durante conversa ativa
- NÃ£o propor infra antes de ter o problema

---

### Dia 10 (10/02) â€” Roadmap & AnÃ¡lise Crisp
**O que foi feito:**
- Roadmap 2026 criado (5 fases, 18+ semanas)
- 6 ideias priorizadas (Content Waterfall P0)
- AnÃ¡lise completa do Crisp: 187 conversas, 95% WhatsApp, vibe coding dominante
- Circle API dados cruzados
- Post LinkedIn "Matrix/Skills" (co-criado com Bruno, alta qualidade)
- SessÃ£o sobre Claude Code vs OpenClaw (clarificaÃ§Ã£o para Bruno)

**Insight de conteÃºdo do Crisp:**
- Vibe coding DOMINA (172 menÃ§Ãµes em 187 conversas)
- Pessoas travam na "Ãºltima milha" (deploy, config, go-live)
- Demanda por "do zero ao deploy" completo

**Momento "aha":**
- Crisp como goldmine de ideias: as perguntas dos clientes revelam exatamente o que o pÃºblico quer aprender

---

### Dia 11 (11/02) â€” IntegraÃ§Ãµes & MÃ©tricas
**O que foi feito:**
- ChartMogul integrado (MRR Jan: R$7,367, -8.5%)
- Crisp API integraÃ§Ã£o completa + cron mensal
- InÃ­cio exploraÃ§Ã£o Notion API
- Social Media metrics: LinkedIn, Instagram (RapidAPI), YouTube, X/Twitter
- Security hardening: dmPolicy allowlist, UFW ativo
- Skills removidas (granola, openai-image-gen, video-frames)

**LiÃ§Ãµes:**
- Instagram: texto longo > reels (21x mais ER!)
- Crisp Ã© canal de vendas, nÃ£o suporte
- Notion API requer paginaÃ§Ã£o

---

### Dia 12 (12/02) â€” Immune System & Feedback Loops
**O que foi feito:**
- AnÃ¡lise do artigo Eric Siu "30 OpenClaw Jobs A Day" â†’ implementaÃ§Ãµes
- Watchdog de Crons com auto-retry 3x
- Sonnet/Opus Split (economia ~90% em crons simples)
- Feedback Loops universal (4 domÃ­nios: content, tasks, recommendations, digest)
- Fix definitivo de crons: `sessionTarget: isolated` + `agentTurn` + `announce`
- Security: fail2ban, localhost binding, rotaÃ§Ã£o trimestral de chaves
- LiÃ§Ãµes categorizadas com expiraÃ§Ã£o (estratÃ©gicas permanentes, tÃ¡ticas 30 dias)

**Frase-chave do Eric Siu:**
> "Agents are 30% of the work. The other 70% is the immune system."

**Conceitos aprendidos:**
- Ralph Loop (Geoffrey Huntley) vs Feedback Loop â€” complementares
- Capability Evolver: NÃƒO rodar automaticamente (sub-agents com autonomia total = risco)

---

### Dia 13 (13/02) â€” ConsolidaÃ§Ã£o & Mission Control v2
**O que foi feito:**
- Todos os projetos sobrepostos consolidados em Mission Control v2
- 6 mÃ³dulos, ~18 semanas
- Prioridade: MÃ³dulo 1 â€” Content HQ (4h/dia â†’ 1h15/dia)
- Projetos absorvidos: Content Waterfall, Social Metrics, ChartMogul, Multi-Agent specs, Agent Leveling, Price Monitor
- QA automatizado do MC (sub-agent encontrou 5 bugs: 2 crÃ­ticos, 3 mÃ©dios)
- IntegraÃ§Ã£o Notion + Granola + Amie como hub de tasks
- Crons consolidados: todos em Sonnet (economia)

---

## RESUMO QUANTITATIVO (13 dias)

| MÃ©trica | Valor |
|---------|-------|
| IntegraÃ§Ãµes ativas | 15+ (1Password, YouTube, LinkedIn, X, Reddit, Circle, Crisp, ChartMogul, Google Drive, Calendar, Notion, Craft, Telegram, WhatsApp, Tella) |
| Skills instaladas | 19 (apÃ³s cleanup) |
| Agentes ativos | 6 (Amora, Content, Orchestrator, Planner, Scraper, ZoM) |
| Crons configurados | 17+ |
| Projetos concluÃ­dos | Mission Control v1, Agent Leveling, Content Squad spec |
| Bugs crÃ­ticos resolvidos | Token overflow, crons nÃ£o executando, security hardening |
| Arquivos de memÃ³ria | 40+ (daily notes, topic files, knowledge base) |
| Posts LinkedIn co-criados | 3+ |
| DecisÃµes documentadas | 20+ |
| LiÃ§Ãµes extraÃ­das | 35+ |

---

## PARTE 2 â€” PESQUISA DE MERCADO

### O que existe hoje (Fev/2026)

#### ðŸŽ¥ YouTube â€” ConteÃºdo sobre OpenClaw/AI Agents

**Alex Finn** (top creator, Vibe Coding Academy)
- "ClawdBot is the most powerful AI tool I've ever used" â€” 427K views
- "Open Claw: App Store Moment for AI Agents" â€” entrevista com Cailyn (OpenClaw team)
- "AI Co-Pilot for Your Life with Claude Code" â€” 25 min tutorial (slash commands, sub-agents)
- Foco: vibe coding, automaÃ§Ã£o de conteÃºdo, "AI employee 24/7"
- **Gap**: setup raso, nÃ£o entra em gestÃ£o de multi-agentes, feedback loops, ou memÃ³ria estruturada

**Matthew Berman**
- "I Played with Clawdbot all Weekend" â€” review
- "Openclaw is NUTS" â€” overview
- "OpenClaw Use Cases that are actually helpful" â€” use cases prÃ¡ticos
- 6 agentes rodando, NocoDB task board
- **Gap**: nÃ£o mostra gestÃ£o de longo prazo, evoluÃ§Ã£o do agente, "immune system"

**freeCodeCamp**
- "OpenClaw Full Tutorial for Beginners" â€” tutorial completo
- **Gap**: tÃ©cnico demais, sem perspectiva de negÃ³cios

**Outros:**
- Artigos DEV Community, Medium, blogs SEO genÃ©ricos sobre "como instalar OpenClaw"
- Bhanu Teja (@pbteja1998): thread viral sobre 10 agentes (3.7M views, 8.1K bookmarks)
- Kevin Simback: guide sobre agent team management e leveling
- Eric Siu: "30 OpenClaw Jobs A Day" (49K views, 1.3K bookmarks)

#### ðŸ“š Cursos Estruturados (Udemy, Coursera, etc.)

| Curso | Plataforma | Foco | PreÃ§o |
|-------|-----------|------|-------|
| 2026 Bootcamp: Build Professional AI Agents | Udemy | LangChain, memory, to-do assistant | ~$40 |
| AI Agents For All! No-Code | Udemy | Langflow, no-code | ~$30 |
| AI Agent Developer | Coursera | Custom GPTs, multi-industry | Subscription |
| 5-Day AI Agents Intensive | Kaggle/Google | Fundamentals | Free |

#### ðŸ“° Guias Escritos

- **Reddit r/ThinkingDeeplyAI**: "The Ultimate Guide to OpenClaw" â€” post viral e bem completo cobrindo setup, use cases e riscos de seguranÃ§a
- **DEV Community**: "Unleashing OpenClaw: The Ultimate Guide for Developers in 2026"
- **o-mega.ai**: "OpenClaw: Ultimate Guide to AI Agent Workforce 2026"

#### ðŸ”‘ Gaps que NINGUÃ‰M cobre (oportunidade do Bruno)

1. **ExperiÃªncia REAL de 13 dias rodando em produÃ§Ã£o** â€” nÃ£o Ã© "fiz um setup bonito num vÃ­deo de 20 min"
2. **Perspectiva de empreendedor/fundador** â€” nÃ£o de dev/engenheiro de AI
3. **GestÃ£o de longo prazo** â€” memÃ³ria, feedback loops, evoluÃ§Ã£o, manutenÃ§Ã£o
4. **Multi-agentes na prÃ¡tica** â€” leveling, coordenaÃ§Ã£o, shared context
5. **"Immune System"** â€” watchdogs, auto-retry, Sonnet/Opus split, security hardening
6. **IntegraÃ§Ã£o com stack real de negÃ³cios** â€” 1Password, ChartMogul, Crisp, YouTube OAuth, Google Drive, etc.
7. **Crons que FUNCIONAM** â€” debugging real (crons disparando mas nÃ£o executando)
8. **Content em portuguÃªs** â€” zero cursos em PT-BR sobre OpenClaw
9. **Custo real e economia** â€” Haiku para heartbeats, Sonnet para execuÃ§Ã£o, Opus para anÃ¡lise
10. **Tom de voz e identidade do agente** â€” SOUL.md, voice guides, nÃ£o um chatbot genÃ©rico
11. **Feedback Loops com approve/reject** â€” ninguÃ©m ensina a fazer o agente aprender com suas decisÃµes
12. **SeguranÃ§a real** â€” fail2ban, allowlist, UFW, rotaÃ§Ã£o de credenciais (o Reddit Guide menciona riscos mas ninguÃ©m mostra a soluÃ§Ã£o)
13. **Sub-agents e delegaÃ§Ã£o** â€” spawnar tasks paralelas, coordenar output, lidar com falhas

---

## PARTE 3 â€” PROPOSTA DE CURSO (v2 â€” com liÃ§Ãµes aplicadas)

### TÃ­tulo
**"Construa Seu AI COO: De Zero a Agente Pessoal em 2 Horas com OpenClaw"**

SubtÃ­tulo: *Como eu construÃ­ uma assistente AI que substituiu 3-4 pessoas em 13 dias â€” e como vocÃª pode fazer o mesmo.*

### PÃºblico-Alvo
- Empreendedores e founders (especialmente solo)
- Criadores de conteÃºdo
- Profissionais que querem produtividade 10x
- Comunidade Micro-SaaS do Bruno
- **NÃƒO** Ã© para devs que querem aprender LangChain â€” Ã© para quem quer USAR

### O que torna este curso ÃšNICO

1. **ExperiÃªncia real, nÃ£o teoria** â€” Bruno mostra a Amora funcionando em produÃ§Ã£o, com bugs reais e como resolveu
2. **Perspectiva de CEO/founder** â€” nenhum outro curso ensina a configurar um agente do ponto de vista de quem dirige negÃ³cios
3. **13 dias documentados** â€” timeline real com problemas, decisÃµes e breakthroughs
4. **Multi-agentes** â€” nÃ£o sÃ³ "um chatbot" mas um time de 6 agentes coordenados
5. **Immune System** â€” ninguÃ©m ensina feedback loops, watchdogs, auto-retry
6. **Em portuguÃªs** â€” primeiro mini-curso em PT-BR sobre OpenClaw
7. **Stack real** â€” 1Password, YouTube, LinkedIn, Telegram, ChartMogul, nÃ£o toy examples
8. **Framework de evoluÃ§Ã£o** â€” o agente melhora sozinho ao longo do tempo

---

### ESTRUTURA DO CURSO (v3 â€” reordenada + kit por mÃ³dulo)

> **Nova ordem:** Setup â†’ SeguranÃ§a â†’ Personalidade â†’ MemÃ³ria â†’ IntegraÃ§Ãµes â†’ Skills â†’ Multi-agentes â†’ Immune System â†’ Mission Control
> **Cada mÃ³dulo entrega:** ðŸ“¹ VÃ­deo + ðŸ“¦ Kit (PRDs, templates, prompts, skills)

---

#### MÃ³dulo 0 â€” Abertura & Contexto (10 min)
**Formato:** Slides + talking head

- Por que agentes AI pessoais sÃ£o o "next big thing"
- A analogia do Matrix (Trinity + skills = superpoderes)
- O que a Amora faz hoje: demo rÃ¡pido (1 min, Telegram, mostrando comandos reais)
- Mapa do curso: o que vamos construir juntos
- **Apresentar o Kit:** "Cada mÃ³dulo vem com arquivos prontos pra copiar â€” Ã© sÃ³ jogar no seu agente"

ðŸ“¦ **Kit:** Nenhum (sÃ³ slides)

---

#### MÃ³dulo 1 â€” Setup: Do Zero ao Primeiro "Oi" (25 min)
**Formato:** Live coding (tela + face cam)

**TÃ³picos:**
1. O que Ã© o OpenClaw e como funciona (arquitetura: gateway + agente + canal)
2. **Criando a VPS na Hostinger** (plano KVM 1, Ubuntu 24.04)
   - **Docker vs Bare Metal:** "A Hostinger tem One-Click Docker, mas vamos instalar direto porque Ã© mais flexÃ­vel â€” skills, integraÃ§Ãµes e tudo que vamos fazer depois funciona melhor assim"
   - Docker = isolamento que atrapalha (skills nÃ£o instalam fÃ¡cil, sub-agents limitados, debug difÃ­cil)
   - Bare Metal = tudo funciona como esperado, acesso direto
3. **Conectar via SSH** (mostrar terminal local + terminal do painel Hostinger)
4. **Instalar OpenClaw:**
   ```bash
   curl -fsSL https://openclaw.ai/install.sh | bash
   openclaw onboard --install-daemon
   ```
5. **Wizard de configuraÃ§Ã£o:**
   - Gateway mode: Local
   - Provider: Anthropic (mostrar onde pegar API key em console.anthropic.com)
   - Model: Claude Sonnet (bom e barato pra comeÃ§ar)
   - Instalar como serviÃ§o: Sim (roda 24/7)
6. **Criar bot no Telegram** (BotFather â†’ /newbot â†’ copiar token)
7. **Conectar Telegram:**
   ```bash
   openclaw provider add telegram
   ```
8. **Primeiro teste:** Mandar "Oi" no Telegram â†’ agente responde ðŸŽ‰

**ðŸ†• Checkpoint prÃ¡tico:** Aluno tem agente respondendo no Telegram âœ…

**Quanto custa rodar:**
| Item | Custo/mÃªs |
|------|-----------|
| VPS Hostinger (KVM 1) | ~$5-10 |
| API Anthropic (uso moderado) | ~$10-30 |
| Telegram | GrÃ¡tis |
| **Total** | **~$15-40** |

> "Menos que um almoÃ§o por semana pra ter um assistente AI 24/7"

ðŸ“¦ **Kit do mÃ³dulo:**
- `prds/vps-setup-hostinger.md` â€” step-by-step completo
- `configs/modelo-config.md` â€” configuraÃ§Ãµes recomendadas

---

#### MÃ³dulo 2 â€” SeguranÃ§a: Blindando Seu Agente (15 min)
**Formato:** Live coding

> âš¡ SeguranÃ§a ANTES de tudo. Servidores expostos recebem 1.000+ ataques/dia.

**TÃ³picos:**
1. **Por que agora?** Mostrar log real: 1.015 tentativas de brute force em 24h
2. **Telegram Allowlist (CRÃTICO):**
   - dmPolicy "open" = qualquer pessoa comanda seu agente
   - Mudar pra "allowlist" com seu Telegram ID
   - Mostrar como descobrir o ID
3. **Firewall (UFW):**
   ```bash
   sudo apt install -y ufw
   sudo ufw default deny incoming
   sudo ufw allow ssh
   sudo ufw --force enable
   ```
4. **Fail2ban (proteÃ§Ã£o SSH):**
   ```bash
   sudo apt install -y fail2ban
   ```
   - Configurar: 5 tentativas â†’ ban 1h
5. **Credenciais seguras:**
   - NUNCA hardcodar API keys
   - 1Password CLI ou variÃ¡veis de ambiente
6. **Portas de aplicaÃ§Ã£o:**
   - Se tiver web apps: 127.0.0.1 (nÃ£o 0.0.0.0)
   - Cloudflare Tunnel pra acesso remoto

**Checkpoint:** Servidor blindado âœ…

ðŸ“¦ **Kit do mÃ³dulo:**
- `prds/security-hardening.md` â€” PRD copy-paste (joga no agente, ele blinda sozinho)

---

#### MÃ³dulo 3 â€” Personalidade e Contexto (25 min)
**Formato:** Demo + slides

**TÃ³picos:**
1. **SOUL.md: a alma do agente** â€” mostrar diff genÃ©rico vs personalizado da Amora
   - Anti-patterns concretos: exemplos âŒ/âœ… dentro do SOUL.md
   - "Never dos" explÃ­citos: coisas que o agente NUNCA deve fazer
   - Inspirational anchors: dar ao agente referÃªncias de tom ("fale como X, nunca como Y")
2. **USER.md: quem Ã© vocÃª?** â€” contexto que faz o agente Ãºtil
   - Contexto profundo > superficial: negÃ³cios, filosofia, horÃ¡rios, estilo de comunicaÃ§Ã£o
   - Tom de voz por plataforma (se cria conteÃºdo)
3. **IDENTITY.md: dados concretos vs personalidade** â€” separar "quem sou" de "como ajo"
4. **AGENTS.md: regras operacionais** â€” o que pode, o que nÃ£o pode, como operar
5. **Choosing your model:** Opus vs Sonnet vs Haiku (e quando usar cada um)
   - Economia real: Haiku para heartbeats (90% economia), Sonnet para crons, Opus para interaÃ§Ã£o
6. **Thinking mode:** quando ligar o turbo e quanto custa

**ExercÃ­cio prÃ¡tico:** Aluno pega os templates, preenche os [campos] e joga no agente

**Insight do Dia 7:**
- Mostrar como a Amora reescreveu o prÃ³prio SOUL.md do zero â€” a diferenÃ§a foi absurda
- "SOUL.md nÃ£o pode ser rushado" â€” Kevin Simback

ðŸ“¦ **Kit do mÃ³dulo:**
- `templates/SOUL-template.md` â€” com [PREENCHA AQUI] nos campos
- `templates/USER-template.md`
- `templates/AGENTS-template.md`
- `templates/IDENTITY-template.md`
- `prompts/onboarding.md` â€” primeira conversa com o agente configurado
- `prompts/proactive-mandate.md` â€” ativa modo proativo
- `prompts/interview-your-agent.md` â€” descobre capacidades ocultas

---

#### MÃ³dulo 3 â€” MemÃ³ria: O Segredo que NinguÃ©m Ensina (25 min)
**Formato:** Demo + diagramas

**TÃ³picos:**
1. O problema: agentes esquecem tudo a cada sessÃ£o
2. Arquitetura de memÃ³ria da Amora: daily notes â†’ topic files â†’ MEMORY.md (Ã­ndice)
3. **ðŸ†• Topic files especializados:**
   - `decisions.md` â€” decisÃµes permanentes (nunca perder)
   - `lessons.md` â†’ `lessons/` categorizadas (integrations, crons, content, infra)
   - `projects.md` â€” estado atual de todos os projetos
   - `people.md` â€” contatos, equipe, parceiros
   - `pending.md` â€” aguardando input do usuÃ¡rio
4. **ðŸ†• RetenÃ§Ã£o inteligente de liÃ§Ãµes:**
   - ðŸ”’ EstratÃ©gicas = permanentes (padrÃµes, filosofia)
   - â³ TÃ¡ticas = expiram em 30 dias (bugs, workarounds)
   - RevisÃ£o mensal: deletar tÃ¡ticas vencidas
5. Auto-compaction: como configurar pra nÃ£o estourar tokens
   - ðŸ†• **Token overflow Ã© real:** mostramos estourar 173k+ tokens no Dia 2
6. **ðŸ†• ExtraÃ§Ã£o obrigatÃ³ria na compactaÃ§Ã£o:**
   - REGRA: Antes de CADA compactaÃ§Ã£o, extrair liÃ§Ãµes â†’ lessons, decisÃµes â†’ decisions, etc.
   - "Se nÃ£o extrair antes de compactar, perde 80% do valor"
7. **ðŸ†• Feedback Loops: approve/reject â†’ evoluÃ§Ã£o do agente**
   - 4 domÃ­nios: content, tasks, recommendations, digest
   - JSON com {date, context, decision, reason, tags}
   - Agente consulta ANTES de sugerir â†’ evita repetir erros
   - Max 30 entradas/arquivo (FIFO) â†’ consolidar em lessons mensalmente

**ðŸ†• Demo ao vivo:**
- Mostrar como a Amora lembra de uma decisÃ£o do Dia 4 no Dia 13
- "Bruno prefere briefs de 1 parÃ¡grafo" â†’ decisÃ£o anotada â†’ respeitada automaticamente
- Feedback loop: "Rejeitei este formato de post â†’ agente nÃ£o sugere mais"

**Este Ã© o mÃ³dulo diferenciador.** Nenhum outro curso cobre memÃ³ria estruturada + feedback loops.

ðŸ“¦ **Kit do mÃ³dulo:**
- `templates/MEMORY-template.md`
- `templates/HEARTBEAT-template.md`
- `templates/memory/` (decisions, lessons, projects, people, pending)
- `prds/memory-architecture.md` â€” PRD copy-paste

---

#### MÃ³dulo 5 â€” IntegraÃ§Ãµes: Conectando ao Mundo Real (25 min)
**Formato:** Live coding + demo

**TÃ³picos:**
1. **1Password:** seguranÃ§a de credenciais (regra #1 â€” NUNCA hardcodar)
   - ðŸ†• **Cuidado:** systemd override sobrescreve .env â€” atualizar AMBOS
2. **Google Calendar & Drive** via GOG CLI
3. **YouTube:** Data API + OAuth (listar vÃ­deos, analytics)
4. **ðŸ†• RapidAPI como proxy universal:**
   - Cloud IPs bloqueados por YouTube, X, Instagram â†’ RapidAPI resolve TUDO
   - APIs especÃ­ficas: Instagram Statistics, X/Twitter API45, YouTube Transcripts
   - Free tiers generosos
5. **ðŸ†• Telegram como hub operacional:**
   - TÃ³picos no grupo = war room organizado (conteÃºdo, mÃ©tricas, operacional, projetos)
   - dmPolicy allowlist = seguranÃ§a
   - Bot com inline buttons para interaÃ§Ãµes rÃ¡pidas
6. **Crons: automatizar tarefas recorrentes**
   - ðŸ†• **O bug que TODO MUNDO vai encontrar:**
     - systemEvent + main = cron dispara mas NÃƒO executa (durationMs ~0ms)
     - ðŸ†• **SoluÃ§Ã£o definitiva:** `sessionTarget: isolated` + `agentTurn` + `announce`
     - Esse fix sozinho vale o curso inteiro
   - ðŸ†• **ColisÃ£o de horÃ¡rio:** mÃºltiplos crons no mesmo minuto = rate limit â†’ espaÃ§ar 15-30min
   - ðŸ†• **config.patch reinicia gateway** e mata crons em execuÃ§Ã£o â†’ fazer em horÃ¡rios sem crons
   - ðŸ†• **Lembretes:** systemEvent NÃƒO notifica no Telegram â†’ usar agentTurn + message send

**Checkpoint prÃ¡tico:** Aluno tem pelo menos 1 integraÃ§Ã£o + 1 cron funcionando âœ…

**LiÃ§Ãµes da trincheira:**
- yt-dlp nÃ£o funciona de cloud â†’ Tella.tv ou API alternativa
- Brave Search API instÃ¡vel â†’ ter fallback
- Notion API requer paginaÃ§Ã£o

ðŸ“¦ **Kit do mÃ³dulo:**
- `prds/integrations-setup.md` â€” PRD com integraÃ§Ãµes por nÃ­vel
- `configs/cron-examples.md` â€” 4 crons prontos (agenda, watchdog, revisÃ£o, lembrete)

---

#### MÃ³dulo 6 â€” Skills: Superpoderes InstantÃ¢neos (15 min)
**Formato:** Demo

**TÃ³picos:**
1. O que sÃ£o skills e como instalar (ClawHub)
2. Skills essenciais: excalidraw, nano-pdf, hand-draw-graphics
3. Criando sua primeira skill customizada
4. ðŸ†• **Skills da comunidade: cuidado!**
   - ReferÃªncia: Cisco study â€” % significativa de skills com vulnerabilidades
   - Sempre revisar antes de instalar
   - Skills redundantes existem (remind-me â‰ˆ cron nativo) â†’ auditar
5. ðŸ†• **Creators como skills, nÃ£o agentes:**
   - LinkedIn Creator, Newsletter Creator, etc. = prompts/skills DENTRO de um agente
   - 1 agente com 8 skills > 8 agentes especializados (menos custo, menos coordenaÃ§Ã£o)

**Analogia Matrix:**
- "Tank, I need a pilot program" â€” post viral do Bruno no LinkedIn

ðŸ“¦ **Kit do mÃ³dulo:**
- `skills/skills-by-profile.md` â€” curadoria por perfil (empreendedor, creator, dev, ops)

---

#### MÃ³dulo 7 â€” Multi-Agentes: De Solo a Time (20 min)
**Formato:** Slides + demo

**TÃ³picos:**
1. Quando um agente nÃ£o Ã© suficiente
2. Arquitetura: single gateway + agents.list
3. **Leveling System (Kevin Simback): L1â†’L4**
   - L1 Observer â†’ L2 Contributor â†’ L3 Operator â†’ L4 Trusted
   - ðŸ†• **PromoÃ§Ã£o via performance review semanal** â€” rebaixamento Ã© possÃ­vel
   - ðŸ†• **Caso real:** Content Agent do Kevin caiu de L3 â†’ L2 quando comeÃ§ou a "rushar"
4. Squad da Amora: 6 agentes, cada um com papel definido
5. **ðŸ†• Shared Context:**
   - `shared/TEAM.md` â†’ registry de todos os agentes (quem faz o quÃª)
   - `shared/outputs/` â†’ resultados compartilhados
   - `shared/lessons/` â†’ aprendizados do time
   - "Last updated by" header â€” saber quem tocou no arquivo
   - ðŸ†• Shared context elimina cold starts â†’ agente novo jÃ¡ sabe quem sÃ£o os outros
6. CoordenaÃ§Ã£o: Amora como hub, agentes nos bastidores
   - ðŸ†• **Hub model > Mesh model:** aprendizado cruzado entre domÃ­nios distintos nÃ£o faz sentido
   - ðŸ†• Agentes de conteÃºdo sem binding Telegram â€” Bruno fala sÃ³ com a Amora
7. **ðŸ†• Economia real:**
   - Sonnet para execuÃ§Ã£o/crons, Opus para interaÃ§Ã£o/anÃ¡lise
   - Todos os 17 crons em Sonnet = economia massiva
   - ðŸ†• **Agentes que nÃ£o precisam de Opus nÃ£o devem usar Opus**

**Sub-agents e delegaÃ§Ã£o:**
- sessions_spawn para tasks paralelas (3 sub-agents rodando ao mesmo tempo)
- Tratamento de falhas: retry + avisa o usuÃ¡rio (NUNCA deixar cair no limbo silencioso)
- Sub-agent travou? â†’ retry imediato â†’ se falhar 2x â†’ avisar

ðŸ“¦ **Kit do mÃ³dulo:**
- `prds/multi-agent-setup.md` â€” PRD completo com leveling + shared context

---

#### MÃ³dulo 8 â€” O Sistema ImunolÃ³gico: Manter Tudo Funcionando (20 min)
**Formato:** Slides + demo

**TÃ³picos:**
1. **"Agents are 30% of the work. The other 70% is the immune system."** â€” Eric Siu
2. **ðŸ†• Watchdog com auto-retry (3x antes de alertar)**
   - Monitora crons, detecta falhas, retry automÃ¡tico
   - Se falhar 3x â†’ alerta humano
3. **Feedback Loops universais (recap do MÃ³dulo 3 aplicado)**
   - Ciclo: Feedback (granular, JSON) â†’ Lessons (curado, prose) â†’ Decisions (permanente)
4. **ðŸ†• Security hardening REAL (nÃ£o sÃ³ teoria):**
   - fail2ban: 1.015+ tentativas de brute force/24h â†’ ban automÃ¡tico
   - UFW firewall ativo
   - Telegram allowlist (dmPolicy)
   - SSH hardening (ideal: key-only, sem password)
   - Portas de aplicaÃ§Ã£o: 0.0.0.0 â†’ 127.0.0.1 (sÃ³ Cloudflare Tunnel acessa)
   - ðŸ†• **RotaÃ§Ã£o trimestral de credenciais** â€” schedule no calendÃ¡rio
5. **ðŸ†• Monitoramento de custos real:**
   - Sonnet/Opus split (crons: Sonnet, interaÃ§Ã£o: Opus)
   - Heartbeat com Haiku (~$0.005/heartbeat vs ~$0.10/heartbeat em Opus)
   - Breakdown: quanto custa rodar 17 crons/dia + interaÃ§Ã£o diÃ¡ria
6. **ðŸ†• Backup antes de mudanÃ§as estruturais:**
   - Salvar config + ROLLBACK.md com instruÃ§Ãµes
   - Especialmente antes de: criar agentes, modificar gateway config, reorganizar workspace
7. **ðŸ†• Sub-agents com autonomia = risco:**
   - Capability Evolver: NÃƒO rodar automaticamente
   - Qualquer sub-agent com "fire and forget" pode causar danos
   - Sempre revisar output antes de aprovar

**ðŸ†• Ralph Loop vs Feedback Loop:**
- Ralph Loop (Geoffrey Huntley): loop de execuÃ§Ã£o de cÃ³digo (agente roda atÃ© completar)
- Feedback Loop: aprendizado entre sessÃµes via approve/reject
- SÃ£o complementares: Ralph pra coding, Feedback pra decisÃµes

**Este mÃ³dulo Ã© o que separa "tÃ´ brincando" de "tÃ´ em produÃ§Ã£o".**

ðŸ“¦ **Kit do mÃ³dulo:**
- `prds/immune-system.md` â€” PRD completo (watchdog, feedback loops, custos, backups)

---

#### MÃ³dulo 9 â€” Mission Control: Seu Painel Operacional (10 min)
**Formato:** Demo

**TÃ³picos:**
1. Por que uma UI visual ajuda (mesmo tendo Telegram)
2. Overview do Mission Control da Amora (Kanban, Memory, Crons, Content HQ)
   - ðŸ†• **Content HQ:** 229 packs, 773 peÃ§as, filtros por plataforma, approve/reject
   - ðŸ†• **File Manager** com seguranÃ§a (path traversal bloqueado)
3. Como construir o seu (Express + React + Supabase + Cloudflare Tunnel)
4. Alternativas mais simples: NocoDB, Notion, Google Sheets
5. **QA automatizado:** sub-agent rodou 23 endpoints, encontrou 5 bugs em 7 minutos

ðŸ“¦ **Kit do mÃ³dulo:**
- `reports/report-templates.md` â€” guidelines de design + estrutura de reports

---

#### MÃ³dulo 10 â€” Wrap-up & PrÃ³ximos Passos (10 min)
**Formato:** Talking head + slides

**TÃ³picos:**
1. Recap: o que construÃ­mos juntos
2. **ðŸ†• Os erros que eu cometi (consolidaÃ§Ã£o real):**
   - Token overflow no Dia 2 (nÃ£o configurar compaction)
   - Crons que nÃ£o executavam por 3 dias (systemEvent vs agentTurn)
   - Sub-agent que travou e ninguÃ©m avisou (limbo silencioso)
   - Security "open" nos primeiros dias (qualquer um podia comandar)
   - Propor infra antes de ter o problema (premature optimization)
3. **ðŸ†• Quanto custa rodar um agente AI? (breakdown REAL)**
   - API costs: ~$X/dia com split Sonnet/Opus/Haiku
   - VPS: $5-10/mÃªs
   - RapidAPI: free tiers generosos
   - Total estimado: $XX/mÃªs para operaÃ§Ã£o completa
4. Comunidade: onde buscar ajuda, awesome-skills, ClawHub
5. O futuro: agent-to-agent, MCP, Claude Code integration
6. CTA: Comunidade Micro-SaaS + imersÃ£o

---

### TIMELINE POR MÃ“DULO

| MÃ³dulo | Tempo | Formato | Kit entregue |
|--------|-------|---------|-------------|
| 0 - Abertura | 10 min | Slides + talking head | â€” |
| 1 - Setup VPS | 25 min | Live coding | PRD setup + configs |
| 2 - SeguranÃ§a | 15 min | Live coding | PRD security |
| 3 - Personalidade | 25 min | Demo + slides | 4 templates + 3 prompts |
| 4 - MemÃ³ria | 25 min | Demo + diagramas | MEMORY + memory/ + PRD |
| 5 - IntegraÃ§Ãµes | 25 min | Live coding | PRD integraÃ§Ãµes + crons |
| 6 - Skills | 15 min | Demo | Curadoria por perfil |
| 7 - Multi-agentes | 20 min | Slides + demo | PRD multi-agent |
| 8 - Immune System | 20 min | Slides + demo | PRD immune system |
| 9 - Mission Control | 10 min | Demo | Templates de reports |
| 10 - Wrap-up | 10 min | Talking head | Kit completo (zip) |
| **TOTAL** | **~3h20** | | **24+ arquivos** |

---

### ðŸ†• LIÃ‡Ã•ES APLICADAS AO CURSO (v2)

Estas sÃ£o liÃ§Ãµes que vivemos nos 13 dias e que se transformaram em conteÃºdo ensinÃ¡vel:

#### LiÃ§Ãµes de Infraestrutura
| LiÃ§Ã£o | MÃ³dulo | O que ensinar |
|-------|--------|---------------|
| Token overflow real (173k+ tokens) | M3 | Configurar compaction + reserveTokens ANTES de precisar |
| systemd override sobrescreve .env | M4 | Atualizar AMBOS ao trocar credenciais |
| Brave Search intermitente | M4 | Ter fallback para web_fetch |
| Sub-agents podem retornar histÃ³rico vazio | M6 | Ter fallback manual |
| trash-cli nÃ£o vem instalado | M1 | `apt install trash-cli` no setup |

#### LiÃ§Ãµes de Crons
| LiÃ§Ã£o | MÃ³dulo | O que ensinar |
|-------|--------|---------------|
| Crons systemEvent nÃ£o executam | M4 | Usar isolated + agentTurn (SEMPRE) |
| systemEvent nÃ£o notifica | M4 | Usar agentTurn + message send pra lembretes |
| config.patch mata crons | M4 | Planejar patches em horÃ¡rios sem crons |
| ColisÃ£o de horÃ¡rios = rate limit | M4 | EspaÃ§ar 15-30 min |
| Crons sem agentId falham | M6 | Sempre criar pela main session |

#### LiÃ§Ãµes de ConteÃºdo & IntegraÃ§Ã£o
| LiÃ§Ã£o | MÃ³dulo | O que ensinar |
|-------|--------|---------------|
| Cloud IPs bloqueados | M4 | RapidAPI como proxy universal |
| yt-dlp nÃ£o funciona | M4 | Tella.tv ou Whisper como alternativa |
| Instagram texto > reels | M4 | Dados reais que surpreendem |
| Crisp = canal de vendas | M4 | Usar pra insights de conteÃºdo |
| Notion API requer paginaÃ§Ã£o | M4 | Sempre paginar |

#### LiÃ§Ãµes de Agentes & GestÃ£o
| LiÃ§Ã£o | MÃ³dulo | O que ensinar |
|-------|--------|---------------|
| SOUL.md genÃ©rico = agente genÃ©rico | M2 | Investir tempo em personalidade |
| Todo agente comeÃ§a L1 | M6 | Sem confianÃ§a = sem autonomia |
| Shared context elimina cold starts | M6 | TEAM.md + outputs compartilhados |
| Creators sÃ£o skills, nÃ£o agentes | M5/M6 | 1 agente com N skills > N agentes |
| Hub > Mesh para aprendizado | M6 | Amora curadoria > todos leem tudo |

#### LiÃ§Ãµes de SeguranÃ§a
| LiÃ§Ã£o | MÃ³dulo | O que ensinar |
|-------|--------|---------------|
| dmPolicy open = risco crÃ­tico | M1/M7 | Allowlist desde o Dia 1 |
| 1.015+ brute force tentativas/dia | M7 | fail2ban OBRIGATÃ“RIO |
| 0.0.0.0 â†’ 127.0.0.1 + Cloudflare | M7 | Nunca expor portas direto |
| Credenciais no 1Password | M4/M7 | NUNCA hardcodar |
| Sub-agent com autonomia = risco | M7 | Sempre revisar output |

---

### SUGESTÃ•ES DE FORMATO

#### OpÃ§Ã£o A: YouTube (Gratuito) â€” MÃ¡ximo Alcance
- 1 vÃ­deo longo (~3h) dividido em capÃ­tulos
- Ou sÃ©rie de 9 episÃ³dios â†’ playlist
- **PrÃ³s:** Alcance massivo, SEO, primeiro em PT-BR
- **Contras:** NÃ£o monetiza diretamente

#### OpÃ§Ã£o B: Mini-curso na Comunidade (Pago) â€” MonetizaÃ§Ã£o
- Acesso exclusivo para membros Micro-SaaS PRO
- Live sessions com Q&A
- **PrÃ³s:** Valor agregado Ã  comunidade, monetizaÃ§Ã£o indireta
- **Contras:** Alcance limitado

#### OpÃ§Ã£o C: HÃ­brido (RECOMENDADO) â­
- **YouTube:** MÃ³dulos 0-2 gratuitos (atrair audiÃªncia â€” ~60 min)
  - "Como eu construÃ­ uma assistente AI que substituiu 3-4 pessoas"
  - Setup + personalidade = valor imediato, mas quer mais
- **Pago (Comunidade/curso):** MÃ³dulos 3-9 (memÃ³ria, integraÃ§Ãµes, multi-agents, immune system)
  - O conteÃºdo avanÃ§ado que ninguÃ©m mais tem
- **PrÃ³s:** Funil natural, conteÃºdo premium diferenciado
- **Contras:** Mais trabalho de produÃ§Ã£o

#### OpÃ§Ã£o D: Workshop Live + GravaÃ§Ã£o
- 1 sessÃ£o live (Zoom/YouTube Live) de 3h com screen share
- Participantes constroem junto em tempo real
- GravaÃ§Ã£o vira o produto
- **PrÃ³s:** InteraÃ§Ã£o, Q&A, urgÃªncia
- **Contras:** Uma chance de acertar

---

### SUGESTÃ•ES DE PRODUÃ‡ÃƒO

1. **Gravar na Tella.tv** â†’ transcriÃ§Ã£o automÃ¡tica â†’ waterfall de conteÃºdo
2. **Tela dividida:** terminal + Telegram + face cam
3. **Diagramas:** Excalidraw (jÃ¡ temos skill) para arquitetura
4. **InfogrÃ¡ficos:** Hand-draw-graphics para resumos visuais
5. **Antes/depois:** Mostrar o dia 1 vs dia 13 (o que mudou)
6. **Bugs ao vivo:** NÃƒO esconder os erros â€” mostrar e resolver = autenticidade

---

### MATERIAL COMPLEMENTAR

1. **Checklist de setup** (PDF/Notion) â€” passo-a-passo reproduzÃ­vel
2. **Templates:** SOUL.md, USER.md, AGENTS.md, MEMORY.md modelo
3. **Lista de integraÃ§Ãµes** com links e instruÃ§Ãµes
4. **Awesome skills list** curada para empreendedores
5. **Planilha de custos** (quanto cada modelo custa por mÃªs)
6. **Repo GitHub** com configs de exemplo (sem credenciais, claro)
7. **ðŸ†• Tabela de liÃ§Ãµes aprendidas** (as 35+ liÃ§Ãµes categorizadas)
8. **ðŸ†• Template de feedback loop** (JSONs prontos para usar)
9. **ðŸ†• Checklist de seguranÃ§a** (fail2ban, UFW, allowlist, SSH, rotaÃ§Ã£o de keys)

---

### TÃTULOS ALTERNATIVOS PARA TESTAR

1. "Construa Seu AI COO: De Zero a Agente Pessoal em 2 Horas"
2. "Como Criei Uma Assistente AI Que Substituiu 3-4 Pessoas (E VocÃª Pode TambÃ©m)"
3. "OpenClaw na PrÃ¡tica: 13 Dias Construindo um Agente AI de Verdade"
4. "De Chatbot a COO: O Guia Definitivo do Agente AI Pessoal"
5. "Seu Primeiro Agente AI: Setup Completo com OpenClaw (Sem Saber Programar)"

---

### DIFERENCIAIS vs CONCORRÃŠNCIA (Resumo Atualizado)

| Aspecto | Outros cursos/guias | Nosso curso |
|---------|---------------------|-------------|
| Perspectiva | Dev/engenheiro | CEO/founder |
| ExperiÃªncia | "Acabei de instalar" | 13 dias em produÃ§Ã£o |
| MemÃ³ria | NÃ£o cobrem | MÃ³dulo inteiro + feedback loops |
| Multi-agentes | Superficial | Leveling system + shared context |
| Bugs reais | Escondidos | Mostrados e resolvidos ao vivo |
| Immune system | NÃ£o existe | MÃ³dulo dedicado (watchdog, retry, security) |
| Idioma | EN | PT-BR (primeiro!) |
| IntegraÃ§Ãµes | Toy examples | Stack real de negÃ³cios (15+ APIs) |
| Custo | NÃ£o discutem | Breakdown real com split Sonnet/Opus/Haiku |
| Framework evoluÃ§Ã£o | NÃ£o existe | Feedback loops + liÃ§Ãµes categorizadas |
| SeguranÃ§a | "Cuidado com isso" | SoluÃ§Ã£o completa (fail2ban, UFW, allowlist, rotaÃ§Ã£o) |
| Sub-agents | NÃ£o cobrem | DelegaÃ§Ã£o paralela + tratamento de falhas |
| Crons | Setup bÃ¡sico | Debug real + fix definitivo (isolated) |

---

### IDEIAS DE CONTEÃšDO DERIVADO (Content Waterfall)

Do mini-curso, podemos extrair:
1. **5-7 posts LinkedIn** (um por mÃ³dulo, insights isolados)
2. **3-5 Reels/Shorts** (bugs ao vivo, analogia Matrix, demo Telegram)
3. **1 Thread X** ("13 dias construindo um AI COO â€” thread completa")
4. **1 Newsletter** (behind the scenes, o que deu errado)
5. **InfogrÃ¡fico** (arquitetura da Amora, hand-drawn style)
6. **Podcast/Ãudio** (transcriÃ§Ã£o Tella â†’ ediÃ§Ã£o)

---

### ðŸ†• REFERÃŠNCIAS USADAS

- **Kevin Simback:** "My Complete Guide to Managing OpenClaw Agent Teams" â€” leveling L1-L4, shared context, performance reviews
- **Bhanu Teja** (@pbteja1998): Blueprint de 10 agentes â€” heartbeat staggered, Mission Control como hub
- **Eric Siu:** "I Run 30 OpenClaw Jobs A Day" â€” immune system, 70% Ã© manutenÃ§Ã£o
- **Geoffrey Huntley:** Ralph Loop â€” coding agent loop infinito
- **Lenny's Newsletter:** Context engineering â€” progressive disclosure, context rot
- **Reddit Ultimate Guide:** r/ThinkingDeeplyAI â€” setup completo + riscos de seguranÃ§a (https://www.reddit.com/r/ThinkingDeeplyAI/comments/1qsoq4h/)
- **Alex Finn / Vibe Coding Academy:** Use cases, proactive mandate
- **Simon Willison:** Security research â€” 900+ servidores expostos

---

*Arquivo criado em 13/02/2026, atualizado 13/02/2026 (v2) por Amora ðŸ‡*
*Base para brainstorm com Bruno â€” prÃ³ximo passo: revisar, priorizar, decidir formato e data de gravaÃ§Ã£o.*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
