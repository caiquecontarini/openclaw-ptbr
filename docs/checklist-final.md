# Checklist Final â€” ValidaÃ§Ã£o Completa do Curso

> MÃ³dulo 11: Wrap-up  
> Use este checklist para confirmar que tudo foi configurado corretamente.

---

## ðŸŽ¯ Como Usar Este Checklist

1. VÃ¡ mÃ³dulo por mÃ³dulo, verificando cada item
2. Marque `[x]` conforme confirmar que funciona
3. Se algo falhar, volte ao mÃ³dulo correspondente e corrija
4. **NÃ£o pule itens!** Cada um valida algo crÃ­tico
5. Ao final, vocÃª terÃ¡ um agente OpenClaw de produÃ§Ã£o, 100% funcional

---

## âœ… MÃ³dulo 1: Setup & Infraestrutura

**Objetivo:** Gateway rodando, Telegram conectado, VPS seguro.

- [ ] `openclaw gateway status` retorna "running"
- [ ] Gateway estÃ¡ acessÃ­vel via URL pÃºblica (se configurado)
- [ ] Telegram bot responde no chat 1:1
- [ ] VPS tem IP fixo e estÃ¡ acessÃ­vel via SSH
- [ ] Node.js versÃ£o â‰¥ 18 instalado (`node --version`)
- [ ] Git configurado (`git config user.name` e `user.email`)
- [ ] Workspace em `/root/.openclaw/workspace-<nome>` existe
- [ ] `.env` existe e contÃ©m `TELEGRAM_TOKEN`

**Teste rÃ¡pido:**
```bash
curl -I http://localhost:3339/health  # deve retornar 200 OK
```

---

## ðŸ”’ MÃ³dulo 2: SeguranÃ§a

**Objetivo:** Servidor hardened, credenciais seguras, allowlist ativo.

- [ ] UFW instalado e ativo (`ufw status`)
- [ ] Apenas portas necessÃ¡rias abertas (22, 80, 443, 3339 se gateway pÃºblico)
- [ ] Fail2ban instalado e rodando (`systemctl status fail2ban`)
- [ ] `dmPolicy: "allowlist"` configurado no `config.yaml`
- [ ] `.env` contÃ©m credenciais (nÃ£o hardcodadas no cÃ³digo)
- [ ] `.env` estÃ¡ no `.gitignore`
- [ ] Root login via SSH desabilitado (ou usa chave SSH)
- [ ] Backups automÃ¡ticos configurados (cron ou script)

**Teste rÃ¡pido:**
```bash
cat ~/.openclaw/agents/<agente>/config.yaml | grep dmPolicy  # deve ser "allowlist"
grep ".env" .gitignore  # deve existir
```

---

## ðŸ§¬ MÃ³dulo 3: Identidade

**Objetivo:** Agente tem personalidade, conhece vocÃª, tem nome prÃ³prio.

- [ ] `SOUL.md` existe e tem â‰¥100 linhas
- [ ] `SOUL.md` contÃ©m personalidade forte (nÃ£o genÃ©rico)
- [ ] `SOUL.md` tem anti-patterns com exemplos âŒ/âœ…
- [ ] `USER.md` existe e tem â‰¥200 linhas (idealmente 400+)
- [ ] `USER.md` contÃ©m rotina, estilo de comunicaÃ§Ã£o, negÃ³cios
- [ ] `USER.md` define horÃ¡rios de "nÃ£o perturbe"
- [ ] `AGENTS.md` configurado com regras operacionais
- [ ] `IDENTITY.md` existe (nome, emoji, email prÃ³prio)
- [ ] `BOOT.md` existe com checklist de startup

**Teste rÃ¡pido:**
Pergunte ao agente: "Quem Ã© vocÃª?" e "Quem sou eu?" â€” as respostas devem ser detalhadas e personalizadas.

---

## ðŸ§  MÃ³dulo 4: MemÃ³ria

**Objetivo:** MemÃ³ria persistente, daily notes, compactaÃ§Ã£o automÃ¡tica.

- [ ] Pasta `memory/` existe no workspace
- [ ] `memory/YYYY-MM-DD.md` sendo criado automaticamente todo dia
- [ ] `MEMORY.md` existe e contÃ©m insights curados (nÃ£o raw logs)
- [ ] `memory/decisions.md` ou similar existe (opcional mas recomendado)
- [ ] CompactaÃ§Ã£o configurada (cron semanal ou mensal)
- [ ] Agente extrai liÃ§Ãµes ANTES de compactar (nÃ£o perde contexto)
- [ ] Workflow de compactaÃ§Ã£o documentado em `AGENTS.md`

**Teste rÃ¡pido:**
```bash
ls -la memory/  # deve ter arquivo da data de hoje
wc -l MEMORY.md  # deve ter pelo menos 50 linhas se jÃ¡ usou por alguns dias
```

---

## ðŸ”Œ MÃ³dulo 5: IntegraÃ§Ãµes

**Objetivo:** Pelo menos 1 integraÃ§Ã£o externa funcionando + 1 cron isolado.

- [ ] Pelo menos 1 integraÃ§Ã£o configurada (Gmail, Calendar, GitHub, etc.)
- [ ] Credenciais da integraÃ§Ã£o no `.env` ou 1Password
- [ ] Testei a integraÃ§Ã£o manualmente (ex: "liste meus emails")
- [ ] Pelo menos 1 cron job configurado
- [ ] Cron usa `sessionMode: "isolated"` + `notifyMode: "agentTurn"`
- [ ] **Nunca** `systemEvent` + `main` (isso quebra contexto)
- [ ] Cron rodou pelo menos 1x e funcionou (confira logs)
- [ ] NotificaÃ§Ãµes do cron chegam no canal correto

**Teste rÃ¡pido:**
```bash
openclaw cron list  # deve listar pelo menos 1 cron
openclaw cron logs <id>  # deve mostrar execuÃ§Ãµes recentes
```

---

## ðŸ› ï¸ MÃ³dulo 6: Skills

**Objetivo:** 2-3 skills instaladas e funcionando.

- [ ] Pelo menos 2 skills instaladas (`openclaw skill list`)
- [ ] Skills foram **revisadas** antes de instalar (seguranÃ§a)
- [ ] Skills testadas manualmente e funcionam
- [ ] ConfiguraÃ§Ãµes de skills documentadas em `TOOLS.md`
- [ ] NÃ£o tenho skills redundantes (ex: 3 geradores de imagem)
- [ ] Entendo quando usar skill vs quando criar cron vs quando pedir ao main agent

**Teste rÃ¡pido:**
```bash
openclaw skill list --enabled  # deve listar as skills ativas
```
PeÃ§a ao agente para usar uma skill e confirme que funciona.

---

## ðŸ’“ MÃ³dulo 7: Proatividade

**Objetivo:** Heartbeats configurados, agente checa coisas periodicamente.

- [ ] `HEARTBEAT.md` existe e contÃ©m checklist curto
- [ ] Heartbeat configurado no `config.yaml` (interval ~30min)
- [ ] Heartbeat usa modelo barato (Haiku ou Sonnet, nÃ£o Opus)
- [ ] `heartbeat-state.json` existe em `memory/` (tracking de checks)
- [ ] Agente checa email/calendar/notificaÃ§Ãµes algumas vezes ao dia
- [ ] Agente sabe quando ficar quieto (HEARTBEAT_OK) vs quando avisar
- [ ] NÃ£o perturba de madrugada (23:00-08:00) a menos que urgente

**Teste rÃ¡pido:**
Aguarde um heartbeat (ou force um manualmente) e veja se o agente faz alguma aÃ§Ã£o proativa ou retorna `HEARTBEAT_OK`.

---

## ðŸ¤ MÃ³dulo 8: Multi-Agentes (Opcional)

**Objetivo:** Time de agentes configurado, com leveling e hierarquia.

Se vocÃª configurou multi-agentes:

- [ ] `TEAM.md` existe com descriÃ§Ã£o da equipe
- [ ] Cada agente tem seu prÃ³prio `SOUL.md`
- [ ] Sistema de nÃ­veis (L1-L5) documentado
- [ ] Agentes novos comeÃ§am em L1 (Observer)
- [ ] PromoÃ§Ãµes baseadas em performance (nÃ£o automÃ¡ticas)
- [ ] Main agent sabe quando delegar vs fazer sozinho
- [ ] Subagents nÃ£o tentam ser o main agent

**Teste rÃ¡pido:**
PeÃ§a ao main agent para spawnar um subagent e execute uma tarefa delegada. Confirme que o subagent reporta de volta ao main.

---

## ðŸ›¡ï¸ MÃ³dulo 9: Sistema ImunolÃ³gico

**Objetivo:** Watchdog, feedback loops, model split, backups automÃ¡ticos.

- [ ] Watchdog configurado (detecta agente travado/loop infinito)
- [ ] Retry policy: 2x retry â†’ avisar humano (nunca limbo silencioso)
- [ ] Model split: Sonnet pra crons, Opus pra interaÃ§Ã£o, Haiku pra heartbeats
- [ ] Feedback loops: agente aprende com erros e atualiza docs
- [ ] Backup automÃ¡tico antes de mudanÃ§as estruturais
- [ ] Logs de erro monitorados (manualmente ou via cron)
- [ ] Rollback plan documentado (se algo der errado)

**Teste rÃ¡pido:**
Simule um erro (ex: cron que falha) e confirme que:
1. Retry acontece
2. VocÃª Ã© notificado apÃ³s 2 falhas
3. Erro Ã© logado em `memory/`

---

## ðŸ“Š MÃ³dulo 10: Mission Control (Opcional)

**Objetivo:** Painel visual para ver estado do sistema.

Se vocÃª configurou Mission Control:

- [ ] Ferramenta escolhida (NocoDB/Notion/Sheets/Custom) rodando
- [ ] Tabelas criadas (Tasks, Memory, Crons, Health)
- [ ] Agente consegue escrever no painel
- [ ] Crons atualizam painel automaticamente
- [ ] Dashboard acessÃ­vel via browser
- [ ] Credenciais no `.env` (nÃ£o hardcodadas)
- [ ] Setup documentado em `docs/mission-control-setup.md`

**Teste rÃ¡pido:**
PeÃ§a ao agente para logar uma tarefa no painel. Abra o painel e confirme que apareceu.

---

## ðŸŽ“ ValidaÃ§Ã£o Final

**Meta-checklist â€” confirme que vocÃª domina:**

- [ ] Sei reiniciar o gateway (`openclaw gateway restart`)
- [ ] Sei onde ficam os logs (`~/.openclaw/logs/`)
- [ ] Sei criar um cron isolado com agentTurn
- [ ] Sei quando usar Sonnet vs Opus vs Haiku
- [ ] Sei fazer backup manual do workspace
- [ ] Sei revisar cÃ³digo de uma skill antes de instalar
- [ ] Sei editar `config.yaml` sem quebrar o agente
- [ ] Sei usar `.env` pra credenciais
- [ ] Sei quando o agente deve me perguntar vs fazer sozinho
- [ ] Li as 10 Regras InviolÃ¡veis e entendo por quÃª cada uma importa

---

## ðŸš€ PrÃ³ximos Passos

Se marcou tudo acima, **parabÃ©ns!** VocÃª tem um agente OpenClaw de produÃ§Ã£o rodando.

**Agora:**
1. **Use por 7 dias** â€” deixe ele trabalhar, veja o que funciona e o que nÃ£o funciona
2. **Itere** â€” ajuste SOUL.md, HEARTBEAT.md, crons baseado no uso real
3. **Expanda** â€” adicione mais skills, integraÃ§Ãµes, automaÃ§Ãµes conforme surgir necessidade
4. **Documente** â€” seu `AGENTS.md` e `TOOLS.md` devem crescer com o tempo
5. **Compartilhe** â€” ensine alguÃ©m, contribua na comunidade, crie skills

**Lembre-se das 10 Regras InviolÃ¡veis** (veja `docs/10-regras-inviolaveis.md`).

---

## ðŸ“ Log de ValidaÃ§Ã£o

Registre quando completou este checklist:

```
Data: _______________
Itens completos: ___ / 70+
Tempo desde inÃ­cio do curso: ___ dias
PrÃ³xima revisÃ£o: _______________ (recomendado: 30 dias)
```

---

**VocÃª nÃ£o completou um curso. VocÃª construiu um sistema.** ðŸŽ‰


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
