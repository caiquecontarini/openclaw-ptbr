# PRD: Sistema ImunolÃ³gico

> "Agents are 30% of the work. The other 70% is the immune system." â€” Eric Siu
> Jogue no agente: "Implementa este sistema imunolÃ³gico"

## Contexto

Agentes quebram silenciosamente. Crons falham sem avisar. Sub-agents travam no limbo. Sem monitoramento, vocÃª descobre problemas dias depois.

## 1. Watchdog de Crons

Criar um cron que monitora os outros crons:

**LÃ³gica:**
1. Listar todos os crons ativos
2. Checar Ãºltimo run de cada um
3. Se algum falhou â†’ retry automÃ¡tico (atÃ© 3x)
4. Se falhou 3x â†’ alertar o usuÃ¡rio no Telegram

**ConfiguraÃ§Ã£o:**
```json
{
  "name": "Watchdog - Monitor de Crons",
  "schedule": { "kind": "cron", "expr": "0 8 * * *", "tz": "America/Sao_Paulo" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Checar saÃºde de todos os crons. Listar os que falharam nas Ãºltimas 24h. Fazer retry dos que falharam. Se algum falhar 3x, alertar no Telegram."
  },
  "delivery": { "mode": "announce" }
}
```

## 2. Feedback Loops

Sistema de aprendizado contÃ­nuo: o agente aprende com suas decisÃµes (approve/reject).

### Setup

Criar `memory/feedback/` com arquivos JSON por domÃ­nio:

- `content.json` â€” feedback sobre conteÃºdo, drafts, sugestÃµes
- `tasks.json` â€” feedback sobre entregas de tasks
- `recommendations.json` â€” feedback sobre sugestÃµes de tools/processos

### Formato

```json
{
  "entries": [
    {
      "date": "2026-02-13",
      "context": "Sugeri thread sobre X para LinkedIn",
      "decision": "approve",
      "reason": "Tom certeiro, dados especÃ­ficos",
      "tags": ["linkedin", "thread", "tom"]
    }
  ]
}
```

### Regras
- Max 30 entradas por arquivo (FIFO â€” remove as mais antigas)
- Agente DEVE consultar feedback antes de sugerir â†’ evita repetir erros
- Consolidar padrÃµes em `lessons/` mensalmente
- Ciclo: Feedback (granular, JSON) â†’ Lessons (curado, prose) â†’ Decisions (permanente)

## 3. Monitoramento de Custos

### Split de modelos
| Uso | Modelo | Custo relativo |
|-----|--------|---------------|
| InteraÃ§Ã£o direta | Opus | $$$ |
| Crons e automaÃ§Ã£o | Sonnet | $ |
| Heartbeats | Haiku | Â¢ |

### Regra
- TODOS os crons devem rodar em Sonnet (nunca Opus)
- Heartbeats em Haiku
- SÃ³ a interaÃ§Ã£o direta usa Opus

## 4. Sub-agents: sessions_yield (v2026.3.13+) â€” Nunca "Fire and Forget"

A partir da v2026.3.13, o tool `sessions_yield` permite encerrar o turno do agente principal imediatamente apÃ³s spawnar um sub-agent, sem ficar "preso" esperando. Isso reduz tokens e melhora a coordenaÃ§Ã£o.

**Fluxo com sessions_yield:**
```
1. Agent spawna sub-agent com sessions_spawn
2. Agent chama sessions_yield â†’ turno encerra limpo
3. Sub-agent termina â†’ prÃ³ximo turno comeÃ§a com o resultado
```

**Regras de follow-up (sempre.apply):**
1. **Ao spawnar:** informar o que o sub-agent vai fazer
2. **sessions_yield:** chamar apÃ³s spawnar para encerrar turno limpo
3. **Follow-up:** checar status em 15-30 min
4. **Sucesso:** resumir resultado em linguagem humana
5. **Falha:** retry imediato â†’ se falhar 2x â†’ avisar o usuÃ¡rio
6. **Nunca** deixar cair no limbo silencioso

## 5. Backup antes de mudanÃ§as

Antes de criar agentes, modificar config, ou reorganizar workspace:

```bash
mkdir -p backups/$(date +%Y-%m-%d)
cp /root/.openclaw/openclaw.json backups/$(date +%Y-%m-%d)/
```

## 6. Auditoria de Secrets

### openclaw secrets audit (v2026.3.2+)

A versÃ£o 3.2 traz um comando dedicado para auditar secrets expostos:

```bash
# Auditar todos os arquivos do workspace por secrets vazados
openclaw secrets audit

# Auditar diretÃ³rio especÃ­fico
openclaw secrets audit --path /root/.openclaw/workspace-meu-agente

# SaÃ­da com relatÃ³rio detalhado
openclaw secrets audit --report
```

O comando detecta:
- API keys hardcodadas em arquivos `.json`, `.md`, `.env`
- Tokens no histÃ³rico de git
- Credenciais em SOUL.md, AGENTS.md ou TOOLS.md
- Patterns conhecidos (OpenAI, Stripe, Telegram, AWS, etc.)

> âš ï¸ Execute `openclaw secrets audit` antes de compartilhar qualquer arquivo do workspace ou fazer backup em cloud.

### Plugin SDK â€” Novo Path (v2026.3.22+)

A partir da v2026.3.22, o Plugin SDK mudou de path:

```bash
# ANTES (v3.21 e anterior):
@anthropic-ai/extension-api

# AGORA (v3.22+):
@openclaws/extension-api
```

Se vocÃª usa plugins no workspace, atualize o import nos arquivos do plugin.

### openclaw doctor â€” Melhorado na 3.2

O comando `openclaw doctor` foi expandido na 3.2 e agora verifica:

```bash
openclaw doctor
```

Checks adicionados na 3.2:
- âœ… `tools.profile` compatibility (detecta profile incompatÃ­vel com tarefas)
- âœ… ACP dispatch status
- âœ… Secrets audit rÃ¡pido (arquivos mais crÃ­ticos)
- âœ… VersÃ£o do Node.js e dependÃªncias
- âœ… Conectividade com canais configurados (Telegram, WhatsApp, Slack)
- âœ… Crons com configuraÃ§Ã£o invÃ¡lida (`systemEvent` + `main` = problema)

> ðŸ’¡ Dica: rode `openclaw doctor` apÃ³s qualquer atualizaÃ§Ã£o de versÃ£o ou quando algo estiver "estranho". Ã‰ o ponto de partida do diagnÃ³stico.

## 7. Exec Approvals â€” Nunca Desabilite

O OpenClaw pode executar comandos no seu servidor. O sistema de approvals Ã© a sua Ãºltima linha de defesa: quando o agente quer executar algo fora do padrÃ£o, ele pausa e pede sua confirmaÃ§Ã£o antes de prosseguir.

**Por que isso existe:** Em marÃ§o/2026, 7 formas de burlar esse sistema foram encontradas e corrigidas â€” atacantes tentavam esconder comandos perigosos usando caracteres invisÃ­veis Unicode, quebras de linha com backslash, e wrappers de ferramentas comuns (pnpm, npm, Perl). O sistema existe exatamente para bloquear isso.

**Verificar configuraÃ§Ã£o:**
```bash
openclaw config get exec.approvals
# Deve retornar: ask
```

**Nunca use `allow`** (executa tudo sem confirmaÃ§Ã£o). Mantenha sempre `ask`.

> ðŸ“º **Dica pro curso:** Mostrar ao vivo o sistema pausando e pedindo aprovaÃ§Ã£o. O aluno tende a achar que Ã© burocracia â€” mostrar o contexto de seguranÃ§a muda a percepÃ§Ã£o.

## Checklist

- [ ] Watchdog de crons ativo
- [ ] Feedback loops configurados (pelo menos 1 domÃ­nio)
- [ ] Split de modelos aplicado
- [ ] Regra de sub-agents documentada no AGENTS.md
- [ ] Backup automÃ¡tico antes de mudanÃ§as
- [ ] `openclaw secrets audit` executado â€” zero leaks confirmados
- [ ] `openclaw doctor` rodado e sem erros crÃ­ticos
- [ ] `exec.approvals = ask` (nunca `allow`!) â† v2026.3.13
- [ ] ACP bind configurado (se usar topic separado para agente secundÃ¡rio) â† v2026.4
- [ ] Plugin SDK path atualizado (`@openclaws/extension-api`) â† v2026.3.22

## Resultado Esperado

Sistema resiliente que se auto-monitora, aprende com decisÃµes e nÃ£o deixa nada cair no limbo.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
