# Prompt â€” Aula Extra B: Debug na VPS com Claude Code

> Cole este prompt no chat do seu agente **dentro da VPS** (via `claude` no terminal) depois de assistir a Aula Extra B.

---

Acabei de assistir a aula sobre debug na VPS. Agora quero que vocÃª me ajude a garantir que meu ambiente estÃ¡ saudÃ¡vel e me ensine a resolver problemas quando aparecerem.

**O que preciso fazer:**

## 1. Health Check completo

Rode um diagnÃ³stico completo do sistema:
1. Status do gateway (`openclaw gateway status`)
2. EspaÃ§o em disco disponÃ­vel
3. Uso de memÃ³ria RAM
4. Tamanho dos logs
5. Tamanho do meu workspace
6. ConexÃµes ativas (Telegram, etc.)
7. Ãšltima vez que o gateway reiniciou

Me mostre tudo de forma clara e me diga:
- âœ… O que tÃ¡ OK
- âš ï¸ O que precisa de atenÃ§Ã£o
- ðŸ”´ O que precisa ser corrigido agora

## 2. Limpar o que for necessÃ¡rio

Se tiver algo pra limpar (logs velhos, arquivos temporÃ¡rios, workspace bagunÃ§ado):
1. Me mostre O QUE vai ser limpo e QUANTO espaÃ§o vai liberar
2. Me peÃ§a confirmaÃ§Ã£o
3. FaÃ§a a limpeza
4. Me mostre o antes/depois

**Regras de limpeza:**
- âŒ NUNCA deletar arquivos do workspace sem minha aprovaÃ§Ã£o explÃ­cita
- âœ… Pode comprimir/arquivar `memory/YYYY-MM-DD.md` com mais de 30 dias
- âœ… Pode limpar logs com mais de 7 dias
- âœ… Pode limpar `/tmp`

## 3. Revisar meu workspace

VÃ¡ pro meu workspace principal e me diga:
- Quantos arquivos tenho?
- Qual o tamanho total?
- Tem arquivos grandes ou duplicados?
- Tem arquivos de teste esquecidos?
- A estrutura tÃ¡ organizada?

Se encontrar algo estranho, me sugira o que fazer.

## 4. Ensinar comandos Ãºteis

Me ensine 5 comandos que vou usar sempre:
1. Ver logs do gateway em tempo real
2. Reiniciar o gateway
3. Ver espaÃ§o em disco
4. Ver processos rodando
5. Ir pro meu workspace rapidamente

Pra cada um, me explique:
- O que o comando faz
- Quando usar
- Como interpretar a saÃ­da

## 5. Simular 3 problemas comuns

Me explique o que fazer em cada cenÃ¡rio:

**CenÃ¡rio A:** Agente parou de responder no Telegram
- Passo 1: ...
- Passo 2: ...
- Como saber se resolveu: ...

**CenÃ¡rio B:** Erro "context window exceeded"
- O que significa: ...
- Como resolver: ...
- Como prevenir: ...

**CenÃ¡rio C:** VPS ficou sem espaÃ§o
- Como identificar: ...
- O que limpar primeiro: ...
- Como evitar no futuro: ...

## 6. Configurar alertas preventivos (se possÃ­vel)

Me ajude a configurar um sistema que me avise ANTES dos problemas:
- Se disco passar de 80% cheio
- Se logs passarem de 1GB
- Se gateway cair
- Se contexto de sessÃ£o passar de 80% do limite

Se nÃ£o rolar via OpenClaw nativo, me sugira alternativas (cron job, script simples).

---

**Ao final, me dÃª um resumo tipo:**

```
âœ… Sistema saudÃ¡vel
ðŸ“Š Disco: XX% usado (XGB livres)
ðŸ’¾ MemÃ³ria: XX% usada
ðŸ“ Logs: XMB (Ãºltimos 7 dias)
ðŸ“ Workspace: XMB
ðŸ”— Telegram: conectado
â±ï¸ Uptime: X dias

PrÃ³xima manutenÃ§Ã£o recomendada: [data]
```

Vamos comeÃ§ar pelo health check. Me mostre tudo.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
