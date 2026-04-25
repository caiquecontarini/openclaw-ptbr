# ConfiguraÃ§Ãµes Recomendadas do OpenClaw

> ReferÃªncia para configurar seu openclaw.json

## Modelo por Uso

| Uso | Modelo Recomendado | Por quÃª |
|-----|-------------------|---------|
| InteraÃ§Ã£o direta | Claude Opus | Melhor raciocÃ­nio, mais criativo |
| Crons / automaÃ§Ã£o | Claude Sonnet | 90% mais barato, suficiente pra tasks |
| Heartbeats | Claude Haiku | MÃ­nimo custo, sÃ³ checa e reporta |
| Imagens | Gemini Flash | Bom e barato |
| AnÃ¡lise avanÃ§ada / multimodal | Gemini 2.5 Pro | Contexto enorme (1M tokens), multimodal nativo |
| Alternativa Google | Gemini 3.1 Pro (`google/gemini-3.1-pro-preview`) | Reasoning avanÃ§ado, boa opÃ§Ã£o de fallback |
| Volume alto / custo mÃ­nimo | MiniMax (`minimax/minimax-01`) | Contexto de 1M tokens a custo extremamente baixo |

### IDs dos Modelos (para openclaw.json)

```json
"anthropic/claude-opus-4-5"       // Claude Opus â€” interaÃ§Ã£o principal
"anthropic/claude-sonnet-4-5"     // Claude Sonnet â€” crons e automaÃ§Ã£o
"anthropic/claude-haiku-4-5"      // Claude Haiku â€” heartbeats
"google/gemini-2.5-pro-preview"   // Gemini 2.5 Pro â€” anÃ¡lise avanÃ§ada
"google/gemini-3.1-pro-preview"   // Gemini 3.1 Pro â€” reasoning / fallback
"google/gemini-flash-2.0"         // Gemini Flash â€” imagens e volume
"minimax/minimax-01"              // MiniMax â€” custo mÃ­nimo, contexto longo
```

## Config de Compaction (IMPORTANTE)

Se nÃ£o configurar, sua sessÃ£o vai estourar tokens e o agente trava.

```json
{
  "compaction": {
    "mode": "default"
  },
  "contextTokens": 160000,
  "reserveTokensFloor": 30000
}
```

## Thinking Mode

| NÃ­vel | Quando usar | Custo |
|-------|------------|-------|
| off | Tasks simples, respostas rÃ¡pidas | $ |
| low | Dia a dia, maioria das interaÃ§Ãµes | $$ |
| medium | AnÃ¡lise, planejamento, conteÃºdo | $$$ |
| high | Coding, problemas complexos, estratÃ©gia | $$$$ |

## Crons: Regra de Ouro

**SEMPRE:**
```json
{
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Sua tarefa aqui"
  },
  "delivery": { "mode": "announce" }
}
```

**NUNCA** usar `sessionTarget: "main"` + `payload.kind: "systemEvent"` â€” dispara mas nÃ£o executa.

## Dicas de Economia

1. Heartbeats com Haiku: ~$0.005 cada (vs ~$0.10 com Opus)
2. Crons com Sonnet: economia de ~90% vs Opus
3. EspaÃ§ar crons: nÃ£o colocar mÃºltiplos no mesmo minuto (rate limit)
4. config.patch reinicia gateway â€” fazer em horÃ¡rios sem crons


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
