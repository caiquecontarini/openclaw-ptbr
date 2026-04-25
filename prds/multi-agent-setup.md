# PRD: Setup Multi-Agentes

> âš ï¸ **Nota (19/02/2026):** Refs a `shared/TEAM.md` refletem a v2 original. Na estrutura real, equipe estÃ¡ em `shared/people.md` e agentes nos workspace files.

> Para quando um agente nÃ£o Ã© suficiente. Jogue no agente principal.

## Contexto

Quando as responsabilidades crescem, um Ãºnico agente fica sobrecarregado. A soluÃ§Ã£o: mÃºltiplos agentes especializados, coordenados por um principal (hub).

## Arquitetura

```
Gateway (1 servidor)
â”œâ”€â”€ Agente Principal (Opus) â† hub, coordena tudo
â”œâ”€â”€ Agente de ConteÃºdo (Sonnet) â† produÃ§Ã£o, drafts
â”œâ”€â”€ Agente Scraper (Sonnet) â† coleta de dados
â””â”€â”€ [Outros conforme necessidade]
```

## Leveling System (Kevin Simback)

Todo agente novo comeÃ§a em L1 e sobe conforme ganha confianÃ§a:

| NÃ­vel | Nome | Autonomia | RevisÃ£o |
|-------|------|-----------|---------|
| L1 | Observer | Zero â€” output sempre revisado | Cada entrega |
| L2 | Contributor | Baixa â€” pode sugerir, nÃ£o executar | Semanal |
| L3 | Operator | MÃ©dia â€” executa dentro de guidelines | Semanal |
| L4 | Trusted | Alta â€” autonomia quase total | Quinzenal |

**Regras:**
- PromoÃ§Ã£o via performance review semanal
- Rebaixamento Ã© possÃ­vel (se qualidade cair)
- NUNCA "rushar" um agente pra L3+ sem histÃ³rico

## Shared Context

Criar pasta `shared/` acessÃ­vel por todos os agentes:

```
shared/
â”œâ”€â”€ TEAM.md          â† Registry: quem faz o quÃª, nÃ­vel, status
â”œâ”€â”€ outputs/         â† Resultados compartilhados
â””â”€â”€ lessons/         â† Aprendizados do time
```

**TEAM.md exemplo:**
```markdown
| Agente | Papel | NÃ­vel | Modelo | Status |
|--------|-------|-------|--------|--------|
| Amora | COO / Hub | L4 | Opus | Ativo |
| Content | ProduÃ§Ã£o | L1 | Sonnet | Ativo |
| Scraper | Coleta | L1 | Sonnet | Ativo |
```

## Economia

- **Agente principal:** Opus (interaÃ§Ã£o, decisÃµes)
- **Agentes de execuÃ§Ã£o:** Sonnet (crons, tarefas rotineiras)
- **Heartbeats:** Haiku (economia ~90%)
- Regra: agente que nÃ£o precisa de Opus NÃƒO deve usar Opus

## CoordenaÃ§Ã£o

- Agente principal Ã© o HUB â€” usuÃ¡rio fala sÃ³ com ele
- Agentes secundÃ¡rios nÃ£o tÃªm binding Telegram
- Hub model > Mesh model (aprendizado cruzado entre domÃ­nios distintos nÃ£o funciona)
- Sub-agents (sessions_spawn) para tasks paralelas
- **ApÃ³s spawnar sub-agents: use `sessions_yield`** para encerrar o turno limpo e receber os resultados na prÃ³xima mensagem (v2026.3.12+)

## Novidades 3.13

### sessions_yield â€” Novo Tool de OrquestraÃ§Ã£o

A versÃ£o 2026.3.13 adicionou o tool `sessions_yield`, que permite ao agente principal **encerrar o turno atual imediatamente** apÃ³s spawnar sub-agentes, recebendo os resultados como prÃ³xima mensagem.

```json
// Fluxo antes (3.12 e anterior):
// 1. Agent spawna sub-agent
// 2. Agent continua "rodando" (esperando, processando)
// 3. Sub-agent termina e anuncia

// Fluxo com sessions_yield (3.13+):
// 1. Agent spawna sub-agent
// 2. Agent chama sessions_yield â†’ turno encerra
// 3. Sub-agent termina â†’ prÃ³ximo turno comeÃ§a com resultado
```

**Por que importa:** O orquestrador agora pode encerrar a sessÃ£o limpa, sem ficar "preso" enquanto sub-agents trabalham. Reduz consumo de tokens e melhora a coordenaÃ§Ã£o.

**Exemplo prÃ¡tico:**
```
ApÃ³s spawnar 3 sub-agents para tarefas paralelas, o hub chama
sessions_yield para sair do turno. Os resultados chegam como
a prÃ³xima mensagem â€” tudo organizado.
```

> âœ… **NÃ£o requer config extra.** O tool `sessions_yield` jÃ¡ estÃ¡ disponÃ­vel apÃ³s atualizar para v2026.3.13.

## Novidades 3.2

### ACP Dispatch â€” Enabled by Default
A partir da versÃ£o 3.2, o ACP (Agent Communication Protocol) dispatch estÃ¡ **habilitado por padrÃ£o**. NÃ£o Ã© mais necessÃ¡rio habilitar manualmente no config.

```json
// ANTES (3.1 e anterior):
{
  "acp": {
    "dispatch": true
  }
}

// AGORA (3.2+): nÃ£o precisa mais desta config
// ACP dispatch jÃ¡ estÃ¡ ativo automaticamente
```

> âœ… Se vocÃª tem essa config antiga, pode remover â€” nÃ£o causa problema, mas Ã© redundante.

### sessions_spawn com Attachments
`sessions_spawn` agora suporta envio de **attachments** (arquivos, imagens, buffers) diretamente ao spawnar um sub-agente:

```json
{
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Analise este relatÃ³rio e me dÃª um resumo executivo.",
    "attachments": [
      {
        "type": "file",
        "path": "/workspace/relatorio-mensal.pdf"
      }
    ]
  }
}
```

Casos de uso: passar PDFs pra anÃ¡lise, imagens pra processamento, arquivos de dados pra transformaÃ§Ã£o â€” tudo numa Ãºnica chamada sem etapas extras.

## ACP bind (v2026.4+)

O ACP bind permite vincular um agente secundÃ¡rio a um topic Telegram especÃ­fico, criando um "agente escravo" que sÃ³ responde naquele topic â€” isolado do agente principal.

**Como usar:**
```
/acp spawn codex --bind here
```

Isso spawna um agente Codex isolado no topic atual do Telegram, sem interferir no agente principal.

**Casos de uso:**
- Criar um agente de conteÃºdo isolado num topic prÃ³prio
- experiments em topics separados sempoluir o contexto do agente principal
- Ter mÃºltiplos agentes "slave" em topics diferentes, cada um com seu prÃ³prio contexto

> âš ï¸ O ACP bind cria um agente **isolado** â€” ele nÃ£o compartilha memÃ³ria nem contexto com o hub. Use quando precisa de isolamento real de contexto.

## Tarefas

1. Definir quais agentes vocÃª precisa (max 2-3 pra comeÃ§ar)
2. Criar config de cada agente com SOUL.md prÃ³prio
3. Configurar shared/TEAM.md
4. Definir modelos (GPT-4o para coordenaÃ§Ã£o, GPT-4o-mini para tarefas)
5. Fazer primeiro test drive com task simples
6. Review apÃ³s 1 semana â†’ decidir promoÃ§Ã£o

## Resultado Esperado

Time de 2-3 agentes coordenados, cada um com papel claro e nÃ­vel definido.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
