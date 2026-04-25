# ðŸŽ“ Estrutura Final do Curso

**"Construa Seu AI COO: De Zero a Agente Pessoal com OpenClaw"**

> 11 mÃ³dulos, ~3h30 de conteÃºdo. Do zero ao agente em produÃ§Ã£o.
> Cada mÃ³dulo entrega: ðŸŽ¥ VÃ­deo + ðŸ“„ PDF + ðŸ’¬ Prompt pro agente

---

## MÃ³dulo 0 â€” Abertura & Contexto (10 min)
**Formato:** Slides + talking head

**ConteÃºdo:**
- Por que agentes AI pessoais sÃ£o o "next big thing"
- A analogia do Matrix (Trinity + skills = superpoderes)
- Demo rÃ¡pido da Amora no Telegram (1 min, comandos reais)
- Mapa do curso: o que vamos construir juntos
- Apresentar o Kit: "Cada mÃ³dulo vem com arquivos prontos pra jogar no seu agente"

**Kit do mÃ³dulo:** Nenhum (sÃ³ slides)

---

## MÃ³dulo 1 â€” Setup: Do Zero ao Primeiro "Oi" (25 min)
**Formato:** Live coding (tela + face cam)

**ConteÃºdo:**
1. O que Ã© o OpenClaw e como funciona (arquitetura: gateway + agente + canal)
2. Criando a VPS na Hostinger (plano KVM 1, Ubuntu 24.04)
   - Docker vs Bare Metal â€” por que bare metal Ã© melhor pra quem nÃ£o Ã© dev
3. Conectar via SSH (terminal local + painel Hostinger)
4. Instalar OpenClaw:
   ```bash
   curl -fsSL https://openclaw.ai/install.sh | bash
   openclaw onboard --install-daemon
   ```
5. Wizard de configuraÃ§Ã£o (provider, model, serviÃ§o)
6. Criar bot no Telegram (BotFather â†’ /newbot â†’ token)
7. Conectar Telegram + primeiro "Oi" ðŸŽ‰

**Quanto custa:**
| Item | Custo/mÃªs |
|------|-----------|
| VPS Hostinger (KVM 1) | ~$5-10 |
| API Anthropic (uso moderado) | ~$10-30 |
| Telegram | GrÃ¡tis |
| **Total** | **~$15-40** |

**Checkpoint:** Agente respondendo no Telegram âœ…

**Kit:**
- `prds/vps-setup-hostinger.md`
- `configs/modelo-config.md`
- `prompts/modulo-01-setup.md`

---

## MÃ³dulo 2 â€” SeguranÃ§a: Blindando Seu Agente (15 min)
**Formato:** Live coding

**ConteÃºdo:**
1. Por que agora? Mostrar log real: 1.015+ tentativas de brute force em 24h
2. Telegram Allowlist (dmPolicy) â€” de "open" pra "allowlist" com seu ID
3. Firewall UFW:
   ```bash
   sudo ufw default deny incoming
   sudo ufw allow ssh
   sudo ufw --force enable
   ```
4. Fail2ban (proteÃ§Ã£o SSH): 5 tentativas â†’ ban 1h
5. Credenciais seguras: 1Password CLI ou variÃ¡veis de ambiente (NUNCA hardcodar)
6. Portas de aplicaÃ§Ã£o: 127.0.0.1 (nÃ£o 0.0.0.0) + Cloudflare Tunnel

**Checkpoint:** Servidor blindado âœ…

**Kit:**
- `prds/security-hardening.md`
- `prompts/modulo-02-seguranca.md`

---

## MÃ³dulo 3 â€” Identidade: Dando Personalidade ao Agente (25 min)
**Formato:** Demo + slides

**ConteÃºdo:**
1. SOUL.md: a alma do agente
   - Mostrar diff: genÃ©rico vs personalizado da Amora
   - Anti-patterns concretos: exemplos âŒ/âœ…
   - "Never dos" explÃ­citos
   - Inspirational anchors (fale como X, nunca como Y)
2. USER.md: quem Ã© vocÃª?
   - Contexto profundo > superficial
   - Tom de voz por plataforma
   - Dica: importar CLAUDE.md se jÃ¡ usa Claude Code
3. IDENTITY.md: dados concretos vs personalidade
   - Nome, email prÃ³prio, cofre de senhas prÃ³prio
   - "Trate como uma pessoa, nÃ£o como um robÃ´"
4. AGENTS.md: regras operacionais
   - O que pode fazer sozinho vs perguntar
5. Escolhendo modelo: Opus vs Sonnet vs Haiku
   - Economia real: Haiku pra heartbeats (90% economia)
6. Thinking mode: quando ligar o turbo e quanto custa

**Insight do Dia 7:** Amora reescreveu o prÃ³prio SOUL.md â€” a diferenÃ§a foi absurda.

**ExercÃ­cio:** Aluno pega templates, preenche os [campos], joga no agente.

**Checkpoint:** Agente com personalidade e contexto âœ…

**Kit:**
- `templates/SOUL-template.md`
- `templates/USER-template.md`
- `templates/AGENTS-template.md`
- `templates/IDENTITY-template.md`
- `prompts/modulo-03-identidade.md`
- `prompts/onboarding.md`
- `prompts/interview-your-agent.md`

---

## MÃ³dulo 4 â€” MemÃ³ria: O Segredo que NinguÃ©m Ensina (25 min) â­
**Formato:** Demo + diagramas

**ConteÃºdo:**
1. O problema: agentes esquecem tudo a cada sessÃ£o (Alzheimer reset)
2. Arquitetura de memÃ³ria em camadas:
   - SessÃ£o â†’ Nota diÃ¡ria â†’ Topic files â†’ MEMORY.md (Ã­ndice)
3. Topic files especializados:
   - `decisions.md` â€” permanentes
   - `lessons.md` â€” categorizadas (estratÃ©gicas permanentes, tÃ¡ticas 30 dias)
   - `projects.md` â€” estado atual
   - `people.md` â€” contatos, equipe
   - `pending.md` â€” aguardando input
4. Regra INVIOLÃVEL: extrair liÃ§Ãµes/decisÃµes ANTES de cada compactaÃ§Ã£o
   - "Se nÃ£o extrair antes de compactar, perde 80% do valor"
5. CompactaÃ§Ã£o: tokens de contexto, reserva, evitar overflow
   - Caso real: token overflow de 173k+ no Dia 2
6. ConsolidaÃ§Ã£o periÃ³dica (a cada 15 dias)
7. Feedback Loops: approve/reject â†’ evoluÃ§Ã£o do agente
   - 4 domÃ­nios: content, tasks, recommendations, digest
   - Agente consulta ANTES de sugerir â†’ evita repetir erros

**Demo ao vivo:** Mostrar como a Amora lembra de uma decisÃ£o do Dia 4 no Dia 13.

**Este Ã© o mÃ³dulo diferenciador.** NinguÃ©m cobre memÃ³ria estruturada + feedback loops.

**Checkpoint:** Sistema de memÃ³ria configurado âœ…

**Kit:**
- `prds/memory-architecture.md`
- `templates/MEMORY-template.md`
- `templates/HEARTBEAT-template.md`
- `templates/memory/` (5 arquivos)
- `prompts/modulo-04-memoria.md`

---

## MÃ³dulo 5 â€” IntegraÃ§Ãµes & Crons: Conectando ao Mundo Real (25 min)
**Formato:** Live coding + demo

**ConteÃºdo:**
1. 1Password: seguranÃ§a de credenciais (NUNCA hardcodar)
   - Cuidado: systemd override sobrescreve .env â€” atualizar AMBOS
2. Google Calendar & Drive via GOG CLI
3. YouTube: Data API + OAuth
4. RapidAPI como proxy universal:
   - Cloud IPs bloqueados por YouTube, X, Instagram â†’ RapidAPI resolve
   - APIs: Instagram Statistics, X/Twitter API45, YouTube Transcripts
5. Telegram como hub operacional:
   - TÃ³picos = war room organizado
   - Por que nÃ£o WhatsApp (sessÃ£o Ãºnica vs mÃºltiplas)
6. Crons â€” automatizar tarefas recorrentes:
   - **O bug que TODO MUNDO vai encontrar:**
     - systemEvent + main = dispara mas NÃƒO executa (durationMs ~0ms)
     - **SoluÃ§Ã£o:** `sessionTarget: isolated` + `agentTurn` + `announce`
   - ColisÃ£o de horÃ¡rios â†’ espaÃ§ar 15-30min
   - config.patch reinicia gateway e mata crons â†’ fazer em horÃ¡rios sem crons
   - Lembretes: systemEvent NÃƒO notifica â†’ usar agentTurn + message send

**Checkpoint:** Pelo menos 1 integraÃ§Ã£o + 1 cron funcionando âœ…

**Kit:**
- `prds/integrations-setup.md`
- `configs/cron-examples.md`
- `prompts/modulo-05-integracoes.md`

---

## MÃ³dulo 6 â€” Skills: Superpoderes InstantÃ¢neos (15 min)
**Formato:** Demo

**ConteÃºdo:**
1. O que sÃ£o skills e como instalar (ClawHub + GitHub)
2. Skills essenciais por perfil:
   - Empreendedor: nano-pdf, excalidraw, perplexity
   - Creator: hand-draw-graphics, video-frames, openai-image-gen
   - Dev: github, coding-agent, tmux
3. Criando sua primeira skill customizada
4. SeguranÃ§a de skills:
   - ReferÃªncia: estudo sobre vulnerabilidades em skills de terceiros
   - Sempre revisar antes de instalar
5. Skills redundantes: remind-me â‰ˆ cron nativo â†’ auditar
6. Creators como skills, nÃ£o agentes:
   - 1 agente com 8 skills > 8 agentes especializados

**Analogia Matrix:** "Tank, I need a pilot program"

**Checkpoint:** 2-3 skills instaladas e testadas âœ…

**Kit:**
- `skills/skills-by-profile.md`
- `prompts/modulo-06-skills.md`

---

## MÃ³dulo 7 â€” Proatividade: Heartbeats & AutomaÃ§Ãµes (15 min)
**Formato:** Demo + slides

**ConteÃºdo:**
1. Heartbeats: o que sÃ£o e como configurar
   - HEARTBEAT.md: checklist periÃ³dico (emails, calendÃ¡rio, projetos)
   - Modelo econÃ´mico: Haiku pra heartbeats (~$0.005 vs ~$0.10 em Opus)
2. O que checar automaticamente:
   - Emails urgentes
   - Eventos nas prÃ³ximas 24-48h
   - Projetos parados hÃ¡ >5 dias
   - MÃ©tricas de negÃ³cio
3. Quando falar vs ficar quieto:
   - HorÃ¡rio silencioso (23h-8h)
   - Nada novo = HEARTBEAT_OK
4. Trabalho proativo sem pedir:
   - Organizar memÃ³ria
   - Git status de projetos
   - Atualizar documentaÃ§Ã£o
5. Exemplos reais da Amora:
   - Daily briefing de redes sociais
   - Alertas de agenda
   - RevisÃ£o semanal de projetos

**Checkpoint:** Heartbeat configurado + 2 automaÃ§Ãµes ativas âœ…

**Kit:**
- `templates/HEARTBEAT-template.md`
- `prompts/proactive-mandate.md`

---

## MÃ³dulo 8 â€” Multi-Agentes: De Solo a Time (20 min)
**Formato:** Slides + demo

**ConteÃºdo:**
1. Quando um agente nÃ£o Ã© suficiente (e quando Ã‰ â€” menos Ã© mais)
2. Arquitetura: single gateway + agents.list
3. Leveling System (Kevin Simback): L1â†’L4
   - L1 Observer â†’ L2 Contributor â†’ L3 Operator â†’ L4 Trusted
   - PromoÃ§Ã£o via performance review semanal
   - Caso real: Content Agent caiu de L3 â†’ L2 quando comeÃ§ou a "rushar"
4. Criando agentes com o Orchestrator:
   - Agente que cria agentes (SOUL, AGENTS, USER, memÃ³ria)
5. Shared Context:
   - TEAM.md â†’ registry (quem faz o quÃª)
   - shared/outputs/ â†’ resultados compartilhados
   - shared/lessons/ â†’ aprendizados do time
6. CoordenaÃ§Ã£o: hub model > mesh model
   - Agente principal curadoria > todos leem tudo
   - Agentes sem binding Telegram â€” comunicam via principal
7. Economia real:
   - Sonnet pra execuÃ§Ã£o/crons, Opus pra interaÃ§Ã£o/anÃ¡lise
   - "Agentes que nÃ£o precisam de Opus nÃ£o devem usar Opus"
8. Sub-agents e delegaÃ§Ã£o:
   - sessions_spawn para tasks paralelas
   - Retry + aviso ao usuÃ¡rio (NUNCA limbo silencioso)

**Checkpoint:** 1-2 agentes extras configurados com leveling âœ…

**Kit:**
- `prds/multi-agent-setup.md`
- `prompts/modulo-07-multiagentes.md`

---

## MÃ³dulo 9 â€” O Sistema ImunolÃ³gico: Manter Tudo Funcionando (20 min) â­
**Formato:** Slides + demo

**ConteÃºdo:**
1. "Agents are 30% of the work. The other 70% is the immune system." â€” Eric Siu
2. Watchdog com auto-retry (3x antes de alertar):
   - Monitora crons, detecta falhas, retry automÃ¡tico
3. Feedback Loops universais:
   - Ciclo: Feedback (JSON) â†’ Lessons (curado) â†’ Decisions (permanente)
4. Security hardening avanÃ§ado:
   - Audit de seguranÃ§a semanal (cron)
   - `openclaw security-audit` + `openclaw doctor fix`
   - RotaÃ§Ã£o trimestral de credenciais
5. Monitoramento de custos:
   - Sonnet/Opus/Haiku split
   - Breakdown real: quanto custa rodar 17 crons/dia + interaÃ§Ã£o
6. Backup antes de mudanÃ§as estruturais:
   - Config + ROLLBACK.md com instruÃ§Ãµes
7. Sub-agents com autonomia = risco:
   - Capability Evolver: NÃƒO rodar automaticamente
   - Sempre revisar output antes de aprovar
8. Ralph Loop vs Feedback Loop:
   - Ralph (coding loop) vs Feedback (aprendizado entre sessÃµes)

**Este mÃ³dulo separa "tÃ´ brincando" de "tÃ´ em produÃ§Ã£o".**

**Checkpoint:** Watchdog + feedback loops + audit configurados âœ…

**Kit:**
- `prds/immune-system.md`
- `prompts/modulo-08-immune-system.md`

---

## MÃ³dulo 10 â€” Mission Control: Seu Painel Operacional (10 min)
**Formato:** Demo

**ConteÃºdo:**
1. Por que uma UI visual ajuda (mesmo tendo Telegram)
2. Overview do Mission Control da Amora:
   - Kanban de tarefas
   - Memory Page
   - Crons Page
   - Content HQ (229 packs, 773 peÃ§as)
3. Como construir o seu:
   - Stack: Express + React + Supabase + Cloudflare Tunnel
   - QA automatizado: sub-agent rodou 23 endpoints, encontrou 5 bugs em 7min
4. Alternativas mais simples:
   - NocoDB (self-hosted, grÃ¡tis)
   - Notion (integra com skill)
   - Google Sheets (simples e funcional)

**Checkpoint:** Pelo menos uma alternativa visual configurada âœ…

**Kit:**
- `reports/report-templates.md`

---

## MÃ³dulo 11 â€” Wrap-up & PrÃ³ximos Passos (10 min)
**Formato:** Talking head + slides

**ConteÃºdo:**
1. Recap: o que construÃ­mos juntos (checklist visual)
2. Os erros que eu cometi (consolidaÃ§Ã£o real):
   - Token overflow no Dia 2
   - Crons que nÃ£o executavam por 3 dias
   - Sub-agent que travou no limbo
   - Security "open" nos primeiros dias
3. Quanto custa rodar um agente AI? (breakdown REAL)
   - API costs com split Sonnet/Opus/Haiku
   - VPS + ferramentas + APIs externas
4. 10 regras inviolÃ¡veis (consolidaÃ§Ã£o)
5. Comunidade: Discord OpenClaw, ClawHub, awesome-skills
6. O futuro: agent-to-agent, MCP, Claude Code integration
7. CTA: Comunidade + prÃ³ximos conteÃºdos

**Kit:**
- Checklist final de validaÃ§Ã£o
- Links de recursos
- `docs/custos.md` (breakdown detalhado)

---

## Resumo por MÃ³dulo

| # | MÃ³dulo | Tempo | Formato | Kit |
|---|--------|-------|---------|-----|
| 0 | Abertura & Contexto | 10 min | Slides + face | â€” |
| 1 | Setup: Do Zero ao "Oi" | 25 min | Live coding | PRD + config + prompt |
| 2 | SeguranÃ§a | 15 min | Live coding | PRD + prompt |
| 3 | Identidade & Personalidade | 25 min | Demo + slides | 4 templates + 3 prompts |
| 4 | MemÃ³ria â­ | 25 min | Demo + diagramas | PRD + templates + prompt |
| 5 | IntegraÃ§Ãµes & Crons | 25 min | Live coding | PRD + config + prompt |
| 6 | Skills | 15 min | Demo | Curadoria + prompt |
| 7 | Proatividade | 15 min | Demo + slides | Template + prompt |
| 8 | Multi-Agentes | 20 min | Slides + demo | PRD + prompt |
| 9 | Immune System â­ | 20 min | Slides + demo | PRD + prompt |
| 10 | Mission Control | 10 min | Demo | Templates |
| 11 | Wrap-up | 10 min | Talking head | Checklist + custos |
| **Total** | | **~3h35** | | **~50 arquivos** |

---

## ReferÃªncias

- **Kevin Simback:** Agent team management, leveling L1-L4
- **Bhanu Teja (@pbteja1998):** Blueprint de 10 agentes (3.7M views)
- **Eric Siu:** "30 OpenClaw Jobs A Day" â€” immune system
- **Geoffrey Huntley:** Ralph Loop
- **Lenny's Newsletter:** Context engineering
- **Reddit Ultimate Guide:** r/ThinkingDeeplyAI
- **Alex Finn / Vibe Coding Academy:** Use cases, proactive mandate
- **Simon Willison:** Security research â€” 900+ servidores expostos

---

*Estrutura final v1 â€” 16/02/2026*
*Curado pelo agente curso-openclaw ðŸ‡*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
