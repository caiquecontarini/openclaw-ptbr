# ðŸ“‹ PRD MASTER â€” RegravaÃ§Ã£o & AtualizaÃ§Ã£o do Curso OpenClaw
> VersÃ£o: 1.0 Â· Data: 06/03/2026 Â· Autor: Amora (curso-openclaw)
> Status: **AGUARDANDO APROVAÃ‡ÃƒO DO BRUNO**

---

## 1. CONTEXTO E OBJETIVO

O curso OpenClaw foi estruturado em **12 mÃ³dulos (M0-M11)** + **5 aulas extras (A-E)** + **6 aulas de troubleshooting (N1-N6)** entre 15/02 e 06/03/2026.

Desde a gravaÃ§Ã£o das primeiras aulas, o OpenClaw lanÃ§ou **3 releases significativas** (2026.2.12, 2026.2.21, 2026.3.2) com **breaking changes crÃ­ticos** que invalidam partes do conteÃºdo existente.

AlÃ©m disso, foram coletadas **~2000 mensagens dos grupos** de alunos (24/02 a 06/03), gerando um ranking das **Top 10 dÃºvidas** que precisam ser endereÃ§adas nas aulas.

**Objetivo:** Produzir um plano completo de regravaÃ§Ã£o, atualizaÃ§Ã£o e criaÃ§Ã£o de novas aulas, garantindo que o curso reflita a versÃ£o 2026.3.2+ e cubra as dores reais dos alunos.

---

## 2. INVENTÃRIO COMPLETO DE AULAS

### 2.1 MÃ³dulos Principais (12)
| # | MÃ³dulo | DuraÃ§Ã£o | Status Material | Status GravaÃ§Ã£o |
|---|--------|---------|-----------------|-----------------|
| M0 | Abertura | 10min | âœ… PRD pronto | â“ Verificar |
| M1 | Setup (VPS + InstalaÃ§Ã£o) | 25min | âœ… PRD pronto | âœ… **GRAVADA** (Aula 1 â€” 04/03) |
| M2 | SeguranÃ§a | 15min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M3 | Identidade | 25min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M4 | MemÃ³ria | 25min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M5 | IntegraÃ§Ãµes | 25min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M6 | Skills | 15min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M7 | Proatividade | 15min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M8 | Multi-Agentes | 20min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M9 | Immune System | 20min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M10 | Mission Control | 10min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |
| M11 | Wrap-up | 10min | âœ… PRD pronto | âŒ NÃƒO GRAVADA |

### 2.2 Aulas Gravadas (04/03/2026)
| # | Tema Real Gravado | Corresponde a | Precisa Regravar? |
|---|-------------------|---------------|-------------------|
| Aula 1 | Como instalar pela VPS e remover o Docker | M1 Setup | âš ï¸ **SIM** â€” falta `tools.profile full` |
| Aula 2 | Como usar assinatura ChatGPT no OpenClaw | N-1 OAuth | âœ… ATUALIZADO â€” ChatGPT OAuth como padrÃ£o |
| Aula 3 | Como configurar agentes pra executar tarefas | N-3 Config Set | âœ… OK (cobre o `config set`) |
| Aula 4 | O que acontece quando agente para de responder | N-4/N-5 Debug | âš ï¸ **PARCIAL** â€” faltam cenÃ¡rios |

### 2.3 Aulas Extras (Material pronto, nÃ£o gravadas)
| # | Tema | Material | Status GravaÃ§Ã£o |
|---|------|----------|-----------------|
| Extra A | IntegraÃ§Ã£o de Ferramentas | âœ… PRD + Prompt + HTML + PDF | âŒ NÃƒO GRAVADA |
| Extra B | Debug na VPS com Claude Code | âœ… PRD + Prompt + HTML + PDF | âŒ NÃƒO GRAVADA |
| Extra C | TÃ³picos no Telegram | âœ… PRD + Prompt + HTML + PDF | âŒ NÃƒO GRAVADA |
| Extra D | AutomaÃ§Ãµes Evolutivas | âœ… PRD + Prompt + HTML + PDF | âŒ NÃƒO GRAVADA |
| Extra E | Contexto & MemÃ³ria | âœ… PRD + Prompt + HTML + PDF | âŒ NÃƒO GRAVADA |

### 2.4 Aulas Troubleshooting (Material pronto, parcialmente gravadas)
| # | Tema | Material | Status |
|---|------|----------|--------|
| N-1 | OAuth & ConfiguraÃ§Ã£o de API | âœ… PRD + HTML + PDF | âš ï¸ GRAVADA (Aula 2) â€” precisa update |
| N-2 | Bot sem Shell (Sandboxing) | âœ… PRD + HTML + PDF | âŒ NÃƒO GRAVADA |
| N-3 | Config Set (tools.profile) | âœ… PRD + HTML + PDF | âœ… GRAVADA (Aula 3) |
| N-4 | LentidÃ£o no Telegram | âœ… PRD + HTML + PDF | âš ï¸ PARCIAL (Aula 4) |
| N-5 | Debug Runbook | âœ… PRD + HTML + PDF | âš ï¸ PARCIAL (Aula 4) |
| N-6 | VPS vs Mac Mini | âœ… PRD + HTML + PDF | âŒ NÃƒO GRAVADA |

---

## 3. TOP 10 DÃšVIDAS DOS ALUNOS (24/02 a 06/03/2026)

> Fonte: ~2000 mensagens dos grupos "Tira DÃºvidas OpenClaw" + "OpenClaw Geral 1"

| # | DÃºvida | Freq. | Aula que Cobre | Status |
|---|--------|-------|----------------|--------|
| 1 | ðŸ”‘ **OAuth/Token ChatGPT â€” "NÃ£o consigo autenticar"** | ~20x | N-1 (OAuth) | âœ… Atualizado â€” ChatGPT OAuth como caminho padrÃ£o |
| 2 | ðŸ’¥ **Contexto estourando â€” "Agente promete e some"** | ~15x | Extra E (Contexto) | âœ… Coberto no material |
| 3 | ðŸ’° **Assinatura vs API â€” "Quanto vou gastar?"** | ~15x | âŒ NOVA AULA NECESSÃRIA | ðŸ†• Criar aula de Custos |
| 4 | ðŸ“¹ **"Onde estÃ£o as aulas?" â€” Onboarding confuso** | ~12x | NÃ£o Ã© aula â€” Ã© UX da plataforma | ðŸ“‹ Fix operacional |
| 5 | ðŸ“± **Telegram: bot nÃ£o responde no grupo** | ~12x | N-2 (Bot sem Shell) + Extra C (TÃ³picos) | âš ï¸ Precisa seÃ§Ã£o especÃ­fica |
| 6 | ðŸ—ï¸ **Sub-agentes vs SessÃµes â€” "Quando usar?"** | ~10x | M8 (Multi-Agentes) | âœ… Coberto no material |
| 7 | ðŸ–¥ï¸ **VPS vs Local â€” "Precisa de VPS?"** | ~10x | N-6 (VPS vs Mac Mini) | âœ… Coberto no material |
| 8 | âš™ï¸ **Modelo por tarefa â€” "Qual modelo usar?"** | ~10x | âŒ NOVA SEÃ‡ÃƒO NECESSÃRIA | ðŸ†• Adicionar em M1 ou nova aula |
| 9 | ðŸ“± **IntegraÃ§Ã£o Google (Drive/Gmail/Calendar)** | ~10x | Extra A (IntegraÃ§Ãµes) + M5 | âš ï¸ Precisa atualizar com gog |
| 10 | ðŸ”§ **"Meu agente nÃ£o executa nada"** (tools.profile) | ~8x | N-3 (Config Set) | âœ… **COBERTO â€” Aula 3 gravada** |

### 3.1 Novas Aulas/SeÃ§Ãµes Derivadas das DÃºvidas

| DÃºvida | AÃ§Ã£o | Prioridade |
|--------|------|-----------|
| **Custos & Modelos** (#3 + #8) | Criar aula nova: "Quanto custa e qual modelo usar" | ðŸ”´ ALTA |
| **Onboarding** (#4) | NÃ£o Ã© aula â€” Ã© link direto na landing page + mensagem de boas-vindas | ðŸŸ¡ OPERACIONAL |
| **Telegram grupo** (#5) | Expandir N-2 com seÃ§Ã£o "Bot nÃ£o responde no grupo" (BotFather privacy) | ðŸ”´ ALTA |
| **Google Integration** (#9) | Atualizar Extra A com passo a passo gog CLI | ðŸŸ¡ MÃ‰DIA |

---

## 4. ANÃLISE DE MUDANÃ‡AS â€” OpenClaw Fev/Mar 2026

### 4.1 Releases Analisadas
- **2026.2.12** (12/02)
- **2026.2.21** (21/02) â€” Gemini 3.1, Streaming Telegram, Discord Voice, Apple Watch
- **2026.3.2** (03/03) â€” **BREAKING CHANGES CRÃTICOS**

### 4.2 MudanÃ§as que Afetam o Curso

| MudanÃ§a | Release | Impacto | Aulas Afetadas |
|---------|---------|---------|----------------|
| ðŸš¨ **`tools.profile` default = messaging** | 3.2 | **CRÃTICO** â€” novas instalaÃ§Ãµes nÃ£o executam nada | M1, N-2, N-3 |
| ðŸ”‘ **`openclaw secrets` (64 targets)** | 3.2 | **ALTO** â€” substitui gestÃ£o manual de .env | M2, M9 |
| âœ… **`openclaw config validate`** | 3.2 | **MÃ‰DIO** â€” novo comando Ãºtil pra ensinar | M1, M3 |
| ðŸ“º **Telegram streaming = partial (default)** | 3.2 | **MÃ‰DIO** â€” alunos veem "digitando" ao vivo | M1 (mencionar) |
| ðŸ”’ **WebSocket loopback-only** | 3.2 | **MÃ‰DIO** â€” painel remoto sem tunnel quebra | M2, Extra B |
| ðŸ”’ **CVE CVSS 8.8 â€” 30k instÃ¢ncias expostas** | 2.12 | **ALTO** â€” gateway em 0.0.0.0 sem firewall | M2 (motivaÃ§Ã£o) |
| ðŸ“„ **PDF tool nativo** | 3.2 | **BAIXO** â€” feature nova, nÃ£o quebra nada | M5 (mencionar) |
| ðŸ§  **Ollama embeddings pra memÃ³ria** | 3.2 | **BAIXO** â€” alternativa local | M4 (mencionar) |
| ðŸ¤– **ACP dispatch enabled por default** | 3.2 | **BAIXO** â€” sub-agents routing | M8 (mencionar) |
| ðŸ“± **Gemini 3.1 support** | 2.21 | **BAIXO** â€” mais opÃ§Ã£o de modelo | M1 (tabela de modelos) |
| âŒš **Apple Watch companion** | 2.21 | **INFO** â€” feature nova | M10 (mencionar) |
| ðŸŽ™ï¸ **Audio echo transcript** | 3.2 | **INFO** â€” nova config | Extra C (mencionar) |

### 4.3 Impacto por Aula â€” O Que Mudou

| Aula | Status Atual | O que precisa mudar |
|------|-------------|---------------------|
| **M1 Setup** | âš ï¸ REGRAVAR | + `openclaw config set tools.profile full` (OBRIGATÃ“RIO) Â· + `config validate` Â· + mencionar streaming visual Â· + tabela de modelos atualizada (Gemini 3.1) |
| **M2 SeguranÃ§a** | âš ï¸ REGRAVAR | + `openclaw secrets audit/apply` substitui .env manual Â· + CVE 30k instÃ¢ncias como motivaÃ§Ã£o Â· + WebSocket loopback Â· + ordem correta: dmPolicy ANTES do UFW |
| **M3 Identidade** | âœ… MANTER | + Apenas adicionar `config validate` como dica |
| **M4 MemÃ³ria** | âœ… MANTER | + Mencionar Ollama embeddings como opÃ§Ã£o local |
| **M5 IntegraÃ§Ãµes** | âš ï¸ ATUALIZAR | + PDF tool nativo Â· + gog CLI passo a passo |
| **M6 Skills** | âœ… MANTER | Sem mudanÃ§as relevantes |
| **M7 Proatividade** | âœ… MANTER | Sem mudanÃ§as relevantes |
| **M8 Multi-Agentes** | âš ï¸ ATUALIZAR | + ACP dispatch default Â· + sessions_spawn attachments |
| **M9 Immune System** | âš ï¸ ATUALIZAR | + `openclaw secrets audit` no checklist Â· + `openclaw doctor` melhorado |
| **M10 Mission Control** | âœ… MANTER | + Mencionar Apple Watch |
| **M11 Wrap-up** | âœ… MANTER | Sem mudanÃ§as |
| **N-1 OAuth** | âš ï¸ ATUALIZAR | + ChatGPT OAuth como caminho padrÃ£o Â· OpenAI API Key como fallback |
| **N-2 Bot sem Shell** | âš ï¸ ATUALIZAR | + `tools.profile full` como causa #1 Â· + BotFather privacy mode |
| **N-3 Config Set** | âœ… MANTER | âœ… JÃ¡ cobre o necessÃ¡rio |
| **N-4 LentidÃ£o** | âœ… MANTER | Sem mudanÃ§as |
| **N-5 Debug Runbook** | âœ… MANTER | Sem mudanÃ§as |
| **N-6 VPS vs Mac Mini** | âœ… MANTER | Sem mudanÃ§as |
| **Extra A IntegraÃ§Ãµes** | âš ï¸ ATUALIZAR | + gog CLI Â· + PDF tool nativo |
| **Extra B Debug VPS** | âœ… MANTER | Sem mudanÃ§as |
| **Extra C TÃ³picos** | âœ… MANTER | + Mencionar audio echo transcript |
| **Extra D AutomaÃ§Ãµes** | âœ… MANTER | Sem mudanÃ§as |
| **Extra E Contexto** | âœ… MANTER | Sem mudanÃ§as |

---

## 5. DECISÃƒO DE REGRAVAÃ‡ÃƒO

### ðŸ”´ REGRAVAR (conteÃºdo desatualizado ou incompleto)
| Aula | Motivo | Prioridade |
|------|--------|-----------|
| **M1 Setup** (Aula 1) | Falta `tools.profile full` â€” alunos travam | ðŸ”´ P0 |
| **M2 SeguranÃ§a** | `openclaw secrets` muda todo o fluxo + CVE | ðŸ”´ P0 |
| **N-1 OAuth** (Aula 2) | Fluxo ChatGPT OAuth pronto | ðŸ”´ P1 |

### ðŸŸ¡ ATUALIZAR MATERIAL (regravaÃ§Ã£o opcional, mas docs precisam update)
| Aula | O que mudar no material | Regravar? |
|------|------------------------|-----------|
| **M5 IntegraÃ§Ãµes** | PDF tool + gog CLI | Opcional |
| **M8 Multi-Agentes** | ACP dispatch + attachments | Opcional |
| **M9 Immune System** | `openclaw secrets audit` | Opcional |
| **N-2 Bot sem Shell** | tools.profile + BotFather | Recomendado |
| **Extra A IntegraÃ§Ãµes** | gog CLI | Opcional |

### âœ… MANTER (sem mudanÃ§as necessÃ¡rias)
M0, M3, M4, M6, M7, M10, M11, N-3, N-4, N-5, N-6, Extra B, Extra C, Extra D, Extra E

### ðŸ†• CRIAR NOVA AULA
| Aula | Tema | Justificativa | Prioridade |
|------|------|--------------|-----------|
| **N-7** | **Custos & Modelos â€” "Quanto vou gastar?"** | Top 3 dÃºvida dos alunos (~15x). Tabela clara: Assinatura vs API, custo por modelo, recomendaÃ§Ã£o por uso, config de modelos baratos pra heartbeat/crons | ðŸ”´ P1 |
| **N-8** | **Telegram: Bot nÃ£o responde no grupo** | Top 5 dÃºvida (~12x). BotFather privacy, allowlist, dmPolicy vs groupPolicy, diagnÃ³stico passo a passo | ðŸ”´ P1 |

---

## 6. PLANO DE EXECUÃ‡ÃƒO â€” TASKS

### FASE 1: Atualizar Material Existente (Amora faz)
> â±ï¸ Estimativa: 2-3 horas

| Task | DescriÃ§Ã£o | Depende de | Output |
|------|-----------|-----------|--------|
| T1.1 | Atualizar PRD M1 Setup com `tools.profile full` + `config validate` + streaming | â€” | PRD atualizado |
| T1.2 | Atualizar PRD M2 SeguranÃ§a com `openclaw secrets` + CVE + WebSocket | â€” | PRD atualizado |
| T1.3 | Atualizar PRD N-1 OAuth com fluxo ChatGPT OAuth | â€” | PRD atualizado |
| T1.4 | Atualizar PRD N-2 com tools.profile como causa #1 + BotFather privacy | â€” | PRD atualizado |
| T1.5 | Criar PRD N-7 (Custos & Modelos) do zero | â€” | PRD novo |
| T1.6 | Criar PRD N-8 (Telegram Bot em Grupo) do zero | â€” | PRD novo |
| T1.7 | Atualizar PRDs M5, M8, M9, Extra A com mudanÃ§as menores | â€” | PRDs atualizados |

### FASE 2: AprovaÃ§Ã£o do Bruno
> â±ï¸ Estimativa: 30 min de revisÃ£o

| Task | DescriÃ§Ã£o | Depende de |
|------|-----------|-----------|
| T2.1 | Bruno revisa lista de mudanÃ§as (seÃ§Ã£o 4.3 acima) | T1.* |
| T2.2 | Bruno aprova/rejeita cada item | T2.1 |
| T2.3 | Bruno decide ordem de gravaÃ§Ã£o | T2.2 |

### FASE 3: Gerar Deliverables (Amora faz)
> â±ï¸ Estimativa: 3-4 horas

| Task | DescriÃ§Ã£o | Depende de | Output |
|------|-----------|-----------|--------|
| T3.1 | Gerar HTML atualizado de cada aula modificada | T2.2 | HTMLs |
| T3.2 | Gerar PDF de cada aula modificada | T3.1 | PDFs |
| T3.3 | Gerar/atualizar Prompts do aluno de cada aula modificada | T3.1 | Prompts .md |
| T3.4 | Gerar documento HTML+PDF consolidado (v2) com todas as aulas | T3.2 | curso-openclaw-completo-v2.html/pdf |
| T3.5 | Atualizar Base de Conhecimento no Notion com novos Q&A | T3.1 | Notion atualizado |

### FASE 4: GravaÃ§Ã£o (Bruno faz)
> â±ï¸ Estimativa: depende do Bruno

| Task | O que gravar | PRD de referÃªncia | Prioridade |
|------|-------------|-------------------|-----------|
| T4.1 | **M1 Setup** (regravar) â€” incluir `tools.profile full` | PRD M1 atualizado | ðŸ”´ P0 |
| T4.2 | **M2 SeguranÃ§a** (gravar do zero) â€” `openclaw secrets` + CVE | PRD M2 atualizado | ðŸ”´ P0 |
| T4.3 | **N-1 OAuth** (regravar) â€” novo fluxo pÃ³s-bloqueio | PRD N-1 atualizado | ðŸ”´ P1 |
| T4.4 | **N-7 Custos & Modelos** (nova) â€” tabela de custos, config modelos | PRD N-7 novo | ðŸ”´ P1 |
| T4.5 | **N-8 Telegram Bot em Grupo** (nova) â€” BotFather + allowlist | PRD N-8 novo | ðŸ”´ P1 |
| T4.6 | **N-2 Bot sem Shell** (gravar) â€” tools.profile + diagnÃ³stico | PRD N-2 atualizado | ðŸŸ¡ P2 |
| T4.7 | **M3-M11 restantes** (gravar do zero) | PRDs existentes | ðŸŸ¡ P2 |
| T4.8 | **Extras A-E** (gravar) | PRDs existentes | ðŸŸ¢ P3 |

### FASE 5: PÃ³s-ProduÃ§Ã£o
| Task | DescriÃ§Ã£o | Depende de |
|------|-----------|-----------|
| T5.1 | Upload dos vÃ­deos na plataforma | T4.* |
| T5.2 | Vincular material (PDF/HTML/Prompt) a cada vÃ­deo | T5.1 |
| T5.3 | Criar mensagem de boas-vindas com link direto pros vÃ­deos | T5.1 |
| T5.4 | Atualizar landing page / Google Drive | T5.1 |

---

## 7. RESUMO EXECUTIVO

| MÃ©trica | Valor |
|---------|-------|
| **Total de aulas no curso** | 23 (12 mÃ³dulos + 5 extras + 6 troubleshooting) |
| **Aulas jÃ¡ gravadas** | 4 (Aulas 1-4 de 04/03) |
| **Aulas que precisam REGRAVAR** | 2 (M1 Setup, N-1 OAuth) |
| **Aulas que precisam GRAVAR do zero** | 19 |
| **Novas aulas a CRIAR** | 2 (N-7 Custos, N-8 Telegram Grupo) |
| **Total final** | **25 aulas** |
| **Material que precisa ATUALIZAR** | 7 PRDs + HTMLs + PDFs |
| **Material OK (sem mudanÃ§a)** | 16 aulas |
| **Top dÃºvidas cobertas pelo curso** | 9/10 (apÃ³s criar N-7 e N-8) |
| **DÃºvida #4 (onboarding)** | Fix operacional, nÃ£o aula |

---

## 8. PRÃ“XIMO PASSO IMEDIATO

**Bruno precisa:**
1. âœ… ou âŒ em cada item da seÃ§Ã£o 4.3 (O que mudou por aula)
2. Confirmar criaÃ§Ã£o das 2 novas aulas (N-7 e N-8)
3. Definir ordem de gravaÃ§Ã£o

**Assim que aprovar, eu:**
1. Atualizo todos os PRDs (Fase 1)
2. Gero HTML + PDF + Prompt de cada um (Fase 3)
3. Entrego pacote completo pronto pra gravar

---

## 9. ITENS FALTANTES IDENTIFICADOS NO DOUBLE CHECK

### 9.1 Material Existente NÃ£o Mencionado no PRD Original

| Item | Status | AÃ§Ã£o |
|------|--------|------|
| **MÃ³dulo BÃ´nus: Multi-Agent v2** | âœ… PRD + Prompt + HTML prontos (`prds/multi-agent-v2.md`, `prompts/modulo-bonus-multi-agent-v2.md`, `pdfs/modulo-bonus-multi-agent-v2.html`) | Faltava no inventÃ¡rio â€” adicionar como **BÃ´nus 1** |
| **Ebook 20 Use Cases** | âœ… v7 pronta (`pdfs/ebook-20-use-cases-v7.html/pdf`) | Material de apoio â€” nÃ£o Ã© aula, Ã© bÃ´nus de marketing/vendas |
| **PDFs por mÃ³dulo (M0-M11)** | âœ… Todos gerados (`pdfs/modulo-00-abertura.pdf` atÃ© `modulo-11-wrapup.pdf`) | Prontos â€” verificar se precisam update com mudanÃ§as da 3.2 |
| **Templates (6 arquivos)** | âœ… SOUL, USER, AGENTS, IDENTITY, MEMORY, HEARTBEAT templates | Material de apoio dos mÃ³dulos M3-M7 |
| **Use Cases (6 categorias)** | âœ… business, community, content, productivity, research, support | Material de apoio â€” complementa ebook |
| **Configs de exemplo** | âœ… `configs/cron-examples.md` + `configs/modelo-config.md` | Material de apoio dos mÃ³dulos M5 e M1 |
| **10 Regras InviolÃ¡veis** | âœ… `docs/10-regras-inviolaveis.md` | Material de apoio do M11 (Wrap-up) â€” **verificar se regra #2 precisa update** (agora Ã© `openclaw secrets`, nÃ£o `.env`) |
| **Troubleshooting doc** | âœ… `docs/troubleshooting.md` (35+ problemas) | Material de apoio â€” **verificar se precisa update** |
| **Custos doc** | âœ… `docs/custos.md` | Material de apoio do M11 â€” **verificar se valores ainda batem** |
| **Guia Setup AutomÃ¡tico** | âœ… `docs/guia-setup-automatico.md` | Speed run alternativo â€” **verificar se precisa `tools.profile`** |
| **Guia SobrevivÃªncia** | âœ… `docs/guia-sobrevivencia-openclaw.html/pdf` | Novo â€” verificar conteÃºdo |
| **Pauta YouTube (podcast Rony)** | âœ… Pauta completa gerada (23/02) | NÃ£o Ã© aula do curso â€” Ã© conteÃºdo de marketing |
| **N-3 Config Set** | âš ï¸ **NÃƒO TEM PRD PRÃ“PRIO** â€” sÃ³ existe em `memory/2026-03-04-config-set.md` | Criar PRD dedicado se for virar aula separada, ou manter como parte da Aula 3 jÃ¡ gravada |
| **Base de Conhecimento Notion** | âœ… 14 seÃ§Ãµes publicadas | **Precisa atualizar** com mudanÃ§as da 3.2 |

### 9.2 Gaps Identificados

| Gap | Impacto | AÃ§Ã£o Recomendada |
|-----|---------|-----------------|
| **N-3 nÃ£o tem PRD formal** | Baixo (Aula 3 jÃ¡ gravada e funciona) | Documentar o fluxo `config set` no PRD do M1 atualizado |
| **PDFs dos mÃ³dulos M0-M11 podem estar desatualizados** | MÃ©dio (alunos podem baixar PDF com info velha) | Regenerar apÃ³s atualizar PRDs na Fase 1 |
| **10 Regras InviolÃ¡veis â€” regra #2 desatualizada** | MÃ©dio (menciona .env, agora Ã© `openclaw secrets`) | Atualizar doc na Fase 1 |
| **`docs/custos.md` pode ter valores desatualizados** | MÃ©dio (preÃ§os de modelos mudam) | Verificar e atualizar com preÃ§os atuais |
| **`docs/guia-setup-automatico.md` falta `tools.profile full`** | Alto (aluno segue o speed run e trava) | Atualizar na Fase 1 |
| **`configs/modelo-config.md` pode faltar Gemini 3.1 e MiniMax** | Baixo | Atualizar com modelos novos |
| **Base Notion desatualizada com mudanÃ§as 3.2** | Alto (alunos consultam e recebem info velha) | Adicionar task T1.8 na Fase 1 |
| **Falta aula sobre WhatsApp** | MÃ©dio (dÃºvida #5 inclui WhatsApp) | Considerar seÃ§Ã£o em N-8 ou aula separada |

### 9.3 Tasks Adicionais (complementam a Fase 1)

| Task | DescriÃ§Ã£o | Prioridade |
|------|-----------|-----------|
| T1.8 | Atualizar Base de Conhecimento Notion (14 seÃ§Ãµes) com mudanÃ§as 3.2 | ðŸ”´ ALTA |
| T1.9 | Atualizar `docs/10-regras-inviolaveis.md` (regra #2: .env â†’ openclaw secrets) | ðŸŸ¡ MÃ‰DIA |
| T1.10 | Atualizar `docs/guia-setup-automatico.md` com `tools.profile full` | ðŸ”´ ALTA |
| T1.11 | Verificar e atualizar `docs/custos.md` com preÃ§os atuais | ðŸŸ¡ MÃ‰DIA |
| T1.12 | Atualizar `configs/modelo-config.md` com Gemini 3.1 + MiniMax | ðŸŸ¢ BAIXA |
| T1.13 | Regenerar PDFs M0-M11 apÃ³s updates dos PRDs | ðŸŸ¡ MÃ‰DIA (Fase 3) |
| T1.14 | Adicionar MÃ³dulo BÃ´nus (Multi-Agent v2) ao inventÃ¡rio oficial | ðŸŸ¢ BAIXA |
| T1.15 | Atualizar `docs/troubleshooting.md` com problemas novos da 3.2 | ðŸŸ¡ MÃ‰DIA |

### 9.4 Contagem Atualizada

| MÃ©trica | Antes | Depois do Double Check |
|---------|-------|----------------------|
| Total de aulas | 25 | **26** (+1 BÃ´nus Multi-Agent v2) |
| Docs de apoio a atualizar | 0 | **6** (10 regras, custos, guia setup, modelo config, troubleshooting, Base Notion) |
| Tasks Fase 1 | 7 | **15** (+8 tasks de atualizaÃ§Ã£o de material de apoio) |
| Material de marketing/bÃ´nus | nÃ£o listado | Ebook 20 Use Cases + Pauta YouTube |

---

## 10. RESUMO EXECUTIVO FINAL (PÃ“S DOUBLE CHECK)

**Tudo que precisa acontecer, em ordem:**

### ðŸ”´ URGENTE (antes de gravar qualquer coisa)
1. Atualizar `guia-setup-automatico.md` com `tools.profile full`
2. Atualizar Base Notion com mudanÃ§as 3.2
3. Atualizar PRDs M1 + M2 + N-1 + N-2

### ðŸŸ¡ IMPORTANTE (antes de publicar material)
4. Criar PRDs N-7 (Custos) + N-8 (Telegram Grupo)
5. Atualizar 10 Regras InviolÃ¡veis
6. Atualizar custos.md + troubleshooting.md
7. Regenerar todos PDFs

### ðŸŸ¢ NICE TO HAVE
8. Adicionar MÃ³dulo BÃ´nus ao inventÃ¡rio
9. Atualizar modelo-config.md
10. Verificar ebook use cases

---

*PRD gerado por Amora Â· curso-openclaw Â· 06/03/2026*
*Double check realizado: +8 tasks, +1 aula, +6 docs de apoio identificados*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
