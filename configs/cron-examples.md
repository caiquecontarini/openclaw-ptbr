# Exemplos de Crons Ãšteis

> Copie e adapte. Todos usam isolated + agentTurn (a forma que funciona).

## ðŸ“… Check de Agenda (diÃ¡rio, 8h)

```json
{
  "name": "Check Agenda",
  "schedule": { "kind": "cron", "expr": "0 8 * * *", "tz": "America/Sao_Paulo" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Checar agenda do Google Calendar para hoje e amanhÃ£. Se tiver compromissos, avisar no Telegram com horÃ¡rios e contexto.",
    "model": "anthropic/claude-sonnet-4-5"
  },
  "delivery": { "mode": "announce" }
}
```

## ðŸ” Watchdog de Crons (diÃ¡rio, 8h30)

```json
{
  "name": "Watchdog - Monitor de Crons",
  "schedule": { "kind": "cron", "expr": "30 8 * * *", "tz": "America/Sao_Paulo" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Listar todos os crons. Checar Ãºltimo run de cada um. Se algum falhou nas Ãºltimas 24h, tentar re-executar. Se falhar de novo, alertar no Telegram.",
    "model": "anthropic/claude-sonnet-4-5"
  },
  "delivery": { "mode": "announce" }
}
```

## ðŸ“Š RevisÃ£o Semanal (sexta, 16h)

```json
{
  "name": "RevisÃ£o Semanal",
  "schedule": { "kind": "cron", "expr": "0 16 * * 5", "tz": "America/Sao_Paulo" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Fazer revisÃ£o semanal: 1) Ler notas diÃ¡rias da semana 2) Consolidar em topic files 3) Atualizar MEMORY.md 4) Listar pendÃªncias 5) Reportar resumo no Telegram.",
    "model": "anthropic/claude-sonnet-4-5"
  },
  "delivery": { "mode": "announce" }
}
```

## â° Lembrete One-shot (exemplo)

```json
{
  "name": "Lembrete: ReuniÃ£o com Fulano",
  "schedule": { "kind": "at", "at": "2026-02-15T09:00:00-03:00" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Lembrete: ReuniÃ£o com Fulano em 30 minutos. Enviar mensagem no Telegram.",
    "model": "anthropic/claude-sonnet-4-5"
  },
  "delivery": { "mode": "announce" }
}
```

## ðŸ”´ Dicas Importantes

1. **Sempre** usar `model: "anthropic/claude-sonnet-4-5"` (nome completo, nÃ£o alias)
2. **EspaÃ§ar** crons por 15-30 min (evita rate limit)
3. **Nunca** usar `sessionTarget: "main"` com `systemEvent` (nÃ£o funciona direito)
4. **Teste** com `cron run <id>` antes de confiar que vai funcionar


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
