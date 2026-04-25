# PRD: Multi-Agent OS v2.0 â€” Arquitetura AvanÃ§ada

> âš ï¸ **Nota (19/02/2026):** Este PRD descreve a v2 como foi projetada. A estrutura `shared/` real foi reorganizada na Shared Memory v2 (ver `shared/projects/PRD-SHARED-V2.md`). Paths como `shared/context/`, `shared/governance/`, `shared/costs/`, `shared/audit/`, `shared/lessons/` e `TOOLS-SHARED.md` foram consolidados em `shared/tools/`, `shared/assets/`, `shared/projects/`, `shared/decisions.md` e `shared/lessons.md`.

> Para quando seu agente Ãºnico virou gargalo. Jogue no agente principal.

## 1. Contexto: Por Que Evoluir?

### Problemas do modelo v1 (1 agente hub + workers)

| Problema | Sintoma |
|----------|---------|
| **Gargalo central** | Agente principal coordena E executa â€” fica lento |
| **Context rot** | Threads longas = respostas piores (degradaÃ§Ã£o antes do limite) |
| **Zero governance** | Sem tracking de custo, sem audit, sem digest |
| **Sem especializaÃ§Ã£o** | Um agente tentando ser bom em tudo = medÃ­ocre em tudo |
| **Escala quebrada** | Adicionar mais workers nÃ£o resolve se o hub Ã© o bottleneck |

### A soluÃ§Ã£o: Hierarquia com Bosses

Em vez de 1 agente fazendo tudo, vocÃª cria uma **organizaÃ§Ã£o**:

```
VocÃª (CEO)
    â†“
Agente Principal (Chief of Staff) â€” coordena, nÃ£o executa
    â†“
Bosses (por domÃ­nio) â€” gerenciam seus workers
    â†“
Workers (especializados) â€” executam tarefas
```

---

## 2. Arquitetura v2

### Hierarquia

```
VocÃª (CEO)
    â†“ fala com
Agente Principal (Chief of Staff, L4)
    â€” NÃ£o executa tasks
    â€” Coordena bosses
    â€” Governance + daily digest
    â€” Traduz suas prioridades
    â†“
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  Boss A      â”‚  Boss B      â”‚  Boss C      â”‚
â”‚  (domÃ­nio 1) â”‚  (domÃ­nio 2) â”‚  (domÃ­nio 3) â”‚
â”‚  Sonnet, L2  â”‚  Sonnet, L2  â”‚  Sonnet, L2  â”‚
â”‚  Topic prÃ³prioâ”‚  Topic prÃ³prioâ”‚  Topic prÃ³prioâ”‚
â””â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”˜
       â†“              â†“              â†“
    Workers         Workers        Workers
    (L1, Haiku/    (L1, Haiku/    (L1, Haiku/
     Sonnet)        Sonnet)        Sonnet)
```

### O que muda do v1 para v2

| Aspecto | v1 | v2 |
|---------|----|----|
| **Papel do agente principal** | COO â€” faz tudo | CoS â€” coordena, nÃ£o executa |
| **DelegaÃ§Ã£o** | Hub â†’ Workers direto | CoS â†’ Bosses â†’ Workers |
| **Governance** | Nenhuma | Dia 1: cost tracking, audit, digest |
| **ComunicaÃ§Ã£o** | Tudo passa pelo hub | VocÃª fala direto com bosses via topics |
| **Escala** | Limitada (hub = gargalo) | Cada boss Ã© autÃ´nomo no seu domÃ­nio |
| **Custo** | Descontrolado | Kill switch + tracking por agente |

---

## 3. Definindo Seus Bosses

### Como decidir quais bosses criar

Responda: **"Quais sÃ£o os 3-5 grandes domÃ­nios do meu trabalho?"**

**Exemplos por perfil:**

| Perfil | Boss A | Boss B | Boss C | Boss D |
|--------|--------|--------|--------|--------|
| **SaaS Founder** | ConteÃºdo | Produto/Ops | Dev | Analytics |
| **Freelancer** | Projetos | ProspecÃ§Ã£o | Admin/Financeiro | â€” |
| **Creator** | ConteÃºdo | Comunidade | MonetizaÃ§Ã£o | Analytics |
| **Startup** | Growth | Engineering | Customer Success | Data |
| **AgÃªncia** | Clientes | ProduÃ§Ã£o | Comercial | Ops |

### Regras para criar bosses

1. **MÃ¡ximo 5 bosses** para comeÃ§ar (complexidade cresce exponencialmente)
2. **Cada boss = 1 domÃ­nio claro** â€” se vocÃª nÃ£o consegue descrever em 1 frase, Ã© grande demais
3. **Boss â‰  Worker** â€” boss COORDENA workers, nÃ£o executa tudo sozinho
4. **Comece com 2-3** â€” adicione conforme necessidade real, nÃ£o especulativa

---

## 4. Workers: Watcher vs Maker

Nem todo worker precisa ficar "ligado". Dois tipos:

### Watcher (Fica de plantÃ£o)
- Tem heartbeat ativo (30-60 min)
- Reage a eventos sem o boss pedir
- Custo: ~$1-2/mÃªs cada
- **Exemplo:** Monitor de comunidade, scraper de dados, coletor de mÃ©tricas

```markdown
# HEARTBEAT.md (Watcher)
1. Ler WORKING.md â€” tem task? Sim â†’ executar. NÃ£o â†’ HEARTBEAT_OK
2. Checar [fonte de dados] por novidades
3. Se encontrou algo relevante â†’ registrar em shared/outputs/
```

### Maker (SÃ³ existe quando tem trabalho)
- Sem heartbeat â€” boss usa `sessions_spawn` quando precisa
- Custo quando idle: **$0**
- **Exemplo:** Writer, editor, dev, analista de dados

```
Boss recebe pedido â†’ spawna Maker com briefing â†’ Maker entrega â†’ Boss revisa
```

### Regra de decisÃ£o

> "Esse worker precisa reagir a algo sem que o boss peÃ§a?"
> â†’ **Sim** = Watcher | **NÃ£o** = Maker

---

## 5. Governance (DESDE O DIA 1)

> A governance nÃ£o Ã© "depois que tiver funcionando". Ã‰ a **fundaÃ§Ã£o**.
> Sem ela, o sistema cresce sem visibilidade e o custo explode.

### 5.1 Cost Tracking

```
shared/costs/
â”œâ”€â”€ YYYY-MM-DD.csv       â† log diÃ¡rio (agent_id, model, tokens_in, tokens_out, cost_usd)
â””â”€â”€ monthly-summary.md   â† consolidado mensal
```

### 5.2 Audit Log

```
shared/audit/
â””â”€â”€ YYYY-MM-DD.jsonl     â† {timestamp, agent, api, endpoint, operation: read|write}
```

### 5.3 Daily Digest (cron automÃ¡tico)

O CoS envia todo dia de manhÃ£:

```
ðŸ‡ Daily Digest â€” DD/MM/YYYY

âœ… Ontem: [X tasks por boss]
âš ï¸ Bloqueios: [lista]
ðŸ’° Custo: $X.XX dia | $X.XX mÃªs
ðŸ”” Alertas: [anomalias]

Boss A: [1 linha status]
Boss B: [1 linha status]
Boss C: [1 linha status]
```

### 5.4 Kill Switch

| Threshold | AÃ§Ã£o |
|-----------|------|
| 2x custo esperado | âš ï¸ Alerta no Telegram |
| 3x custo esperado | ðŸš¨ Avisa vocÃª e PERGUNTA antes de pausar |

**NUNCA auto-kill** â€” sempre pedir confirmaÃ§Ã£o humana.

### 5.5 Escalation Rules

| SituaÃ§Ã£o | Quem decide |
|----------|-------------|
| Task dentro do domÃ­nio do boss | Boss decide sozinho |
| Envolve dinheiro real (pagamentos, refunds) | **Sempre pede aprovaÃ§Ã£o** |
| Cross-boss (precisa de outro domÃ­nio) | CoS coordena |
| Urgente fora do horÃ¡rio | Notifica vocÃª |
| Erro/rollback necessÃ¡rio | Boss registra + avisa CoS |

---

## 6. Estrutura Compartilhada

```
shared/
â”œâ”€â”€ TEAM.md                     â† Registry: quem faz o quÃª, nÃ­vel, status
â”œâ”€â”€ context/
â”‚   â”œâ”€â”€ USER.md                 â† Canonical â€” todos herdam daqui
â”‚   â”œâ”€â”€ TOOLS-SHARED.md         â† IntegraÃ§Ãµes compartilhadas
â”‚   â””â”€â”€ business-context.md     â† Contexto do negÃ³cio
â”œâ”€â”€ governance/
â”‚   â”œâ”€â”€ DAILY-DIGEST-TEMPLATE.md
â”‚   â”œâ”€â”€ CROSS-BOSS-PROTOCOL.md
â”‚   â”œâ”€â”€ QUALITY-GATES.md
â”‚   â”œâ”€â”€ ESCALATION-RULES.md
â”‚   â””â”€â”€ APPROVAL-LOG.md
â”œâ”€â”€ costs/
â”‚   â””â”€â”€ YYYY-MM-DD.csv
â”œâ”€â”€ audit/
â”‚   â””â”€â”€ YYYY-MM-DD.jsonl
â”œâ”€â”€ templates/
â”‚   â”œâ”€â”€ BOSS-WORKSPACE/         â† Template para novo boss (8 arquivos)
â”‚   â””â”€â”€ WORKER-WORKSPACE/       â† Template mÃ­nimo para worker
â”œâ”€â”€ outputs/                    â† Entregas dos agentes
â””â”€â”€ lessons/                    â† LiÃ§Ãµes cross-agent
```

### TEAM.md (Fonte de Verdade)

```markdown
# ðŸ¢ Team Registry

| Agente | Papel | NÃ­vel | Modelo | Tipo | Status |
|--------|-------|-------|--------|------|--------|
| [nome] | CoS / Hub | L4 | Sonnet | Principal | Ativo |
| [boss-a] | Boss [domÃ­nio] | L2 | Sonnet | Boss | Ativo |
| [boss-b] | Boss [domÃ­nio] | L2 | Sonnet | Boss | Ativo |
| [worker-1] | [funÃ§Ã£o] | L1 | Haiku | Watcher | Ativo |
| [worker-2] | [funÃ§Ã£o] | L1 | Sonnet | Maker | Idle |
```

---

## 7. ComunicaÃ§Ã£o

### VocÃª â†’ Bosses (Acesso Direto)

Cada boss tem topic prÃ³prio no Telegram. VocÃª fala **direto** com qualquer boss:
- Topic do Boss A â†’ Boss A responde
- Topic do Boss B â†’ Boss B responde

O CoS **nÃ£o intercepta** mensagens dos topics dos bosses.

### Boss â†’ Boss (Cross-Domain)

Quando um boss precisa de outro:
1. Cria card/registro com @[outro-boss]
2. Reporta no daily digest
3. CoS coordena na prÃ³xima janela
4. Se urgente â†’ boss menciona CoS diretamente

### Boss â†’ Workers

- **Watcher:** Boss atualiza `WORKING.md` do worker â†’ worker pega no prÃ³ximo heartbeat
- **Maker:** Boss usa `sessions_spawn` com briefing completo

---

## 8. Economia de Modelos

| Tier | Modelo sugerido | Custo/mÃªs estimado |
|------|----------------|-------------------|
| CoS (1x) | Sonnet | ~$30-50 |
| Bosses (3-5x) | Sonnet, heartbeat ativo | ~$5-8 cada |
| Watchers (3-5x) | Haiku, heartbeat 30-60min | ~$1-2 cada |
| Makers (5-10x) | Sonnet/Haiku, sob demanda | ~$0 quando idle |
| **Total estimado (3 bosses)** | | **~$60-80/mÃªs** |
| **Total estimado (5 bosses)** | | **~$80-120/mÃªs** |

### Regras de economia
- Worker que nÃ£o precisa de Sonnet â†’ **Haiku** (90% mais barato)
- Heartbeat de worker â†’ **Haiku** (mesmo que o worker use Sonnet pra tasks)
- CoS NÃƒO precisa de Opus â€” Sonnet coordena bem
- Maker idle = **$0** â€” nÃ£o existe custo se nÃ£o Ã© spawnado

---

## 9. Leveling System

| NÃ­vel | Nome | Autonomia | Review |
|-------|------|-----------|--------|
| L1 | Observer | Zero â€” output sempre revisado | Cada entrega |
| L2 | Contributor | Baixa â€” executa dentro de guidelines | Semanal |
| L3 | Operator | MÃ©dia â€” autonomia com guardrails | Semanal |
| L4 | Trusted | Alta â€” quase total | Quinzenal |

**Regras:**
- Todo agente novo comeÃ§a **L1**
- PromoÃ§Ã£o via performance review semanal
- Rebaixamento Ã© possÃ­vel (se qualidade cair)
- **NUNCA** rushar um agente pra L3+ sem histÃ³rico

### Performance Review (semanal, automÃ¡tica)

CoS roda review todo domingo com critÃ©rios:
1. **Responsividade** â€” respondeu dentro do SLA?
2. **Qualidade** â€” outputs precisaram de correÃ§Ã£o?
3. **Custo** â€” dentro do budget?
4. **Autonomia** â€” tomou boas decisÃµes sozinho?

---

## 10. MigraÃ§Ã£o: v1 â†’ v2 (Passo a Passo)

### Etapa 0: Backup (1 hora)
- [ ] Backup completo do workspace atual
- [ ] Verificar que backup Ã© restaurÃ¡vel
- [ ] Documentar estado atual (quais agentes, quais crons)

### Etapa 1: Foundation (1 dia)
- [ ] Promover agente principal: COO â†’ Chief of Staff
- [ ] Atualizar SOUL.md com novo papel
- [ ] Criar `shared/` com toda a estrutura
- [ ] Criar templates de Boss e Worker
- [ ] Ativar governance: daily digest + kill switch

### Etapa 2: Primeiro Boss (2-3 dias)
- [ ] Criar workspace do Boss A (usar template)
- [ ] Configurar binding Telegram (topic prÃ³prio)
- [ ] Adicionar ao agents.list
- [ ] Criar 1-2 workers iniciais
- [ ] Testar spawn chain: CoS â†’ Boss â†’ Worker
- [ ] Validar que funciona antes de avanÃ§ar

### Etapa 3: Segundo Boss (2-3 dias)
- [ ] Repetir processo do Boss A
- [ ] Testar comunicaÃ§Ã£o cross-boss
- [ ] Validar daily digest com 2 bosses

### Etapa 4: Demais Bosses (1 dia cada)
- [ ] Seguir o mesmo padrÃ£o
- [ ] MÃ¡ximo 1 boss novo por dia
- [ ] Sempre testar antes de avanÃ§ar

### Etapa 5: Hardening (ongoing)
- [ ] Context sync automÃ¡tico (cron semanal)
- [ ] Memory lifecycle (cleanup de notas velhas)
- [ ] Performance reviews semanais
- [ ] Ajustar workers conforme uso real

---

## 11. RestauraÃ§Ã£o de EmergÃªncia

Se algo der errado durante a migraÃ§Ã£o:

```bash
openclaw gateway stop
cp -r ~/.openclaw/workspace ~/.openclaw/workspace-failed-v2/
cd ~/.openclaw
tar -xzf workspace-pre-v2-backup.tar.gz
openclaw gateway start
```

**Regra:** SEMPRE backup antes de cada etapa. Paranoia Ã© feature, nÃ£o bug.

---

## 12. Resultado Esperado

Ao final da implementaÃ§Ã£o v2, vocÃª terÃ¡:

- âœ… CoS coordenando (nÃ£o executando)
- âœ… 3-5 Bosses autÃ´nomos por domÃ­nio
- âœ… Workers especializados (Watchers + Makers)
- âœ… Governance completa desde o Dia 1
- âœ… Cost tracking com kill switch
- âœ… Daily digest automÃ¡tico
- âœ… Performance reviews semanais
- âœ… Acesso direto a qualquer boss via topic
- âœ… Custo controlado (~$60-120/mÃªs)

---

*"Agents are 30% of the work. The other 70% is the immune system + governance."*

## 13. ACP bind â€” Agentes Isolados em Topics (v2026.4+)

O ACP bind permite criar agentes **isolados** em topics Telegram especÃ­ficos, cada um com seu prÃ³prio contexto e memÃ³ria â€” sem interferir no CoS (Chief of Staff) principal.

**Como usar:**
```
/acp spawn codex --bind here
```

Isso cria um agente isolado no topic onde o comando foi executado.

**Arquitetura com ACP bind:**
```
VocÃª (CEO)
    â†“
CoS (Chief of Staff, topic principal)
    â†“ coordena via sessions_spawn
Bosses (topics prÃ³prios)
    â†“
Workers (spawnados sob demanda)

+ ACP bind agents (isolados por topic)
  â†’ Cada ACP bind agent = seu prÃ³prio contexto/memÃ³ria
  â†’ NÃ£o compartilha com CoS nem com outros ACP bind agents
```

**Quando usar ACP bind vs Boss:**

| CritÃ©rio | Boss (sessions_spawn) | ACP bind
|----------|----------------------|----------|
| Compartilha memÃ³ria com CoS | âœ… Sim | âŒ NÃ£o
| Contexto isolado | âŒ NÃ£o | âœ… Sim
| Melhor para | DomÃ­nios conectados ao negÃ³cio | experiments, Ã¡reas muito distintas |
| Custo | Tokens do CoS | Tokens independentes |

## 14. ACPX Runtime e Embed (v2026.4+)

O ACPX Ã© o modelo de runtime que permite a agentes operarem de forma **embedded** (embutida) â€” rodando como processos leves dentro do gateway, sem overhead de LLM externo para tarefas simples de coordenaÃ§Ã£o.

**BenefÃ­cios:**
- Tasks de coordenaÃ§Ã£o nÃ£o precisam de LLM externo
- ReduÃ§Ã£o de latÃªncia e custo
- Agentes podem reagir a eventos sem round-trip de API

> âš ï¸ **Nota:** ACPX runtime Ã© um conceito avanÃ§ado. A configuraÃ§Ã£o padrÃ£o com `sessions_spawn` + `sessions_yield` Ã© suficiente para a maioria dos casos. Explore ACPX quando a orquestraÃ§Ã£o de mÃºltiplos agentes comeÃ§ar a custar caro ou ficar lenta.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
