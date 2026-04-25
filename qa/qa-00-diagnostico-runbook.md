# ðŸš¨ Runbook de DiagnÃ³stico â€” "Meu bot nÃ£o estÃ¡ funcionando"

> Use este guia ANTES de qualquer outra coisa. Resolve 90% dos problemas.
> Sem terminal. SÃ³ prompts.

---

## Passo 1 â€” Meu bot estÃ¡ respondendo?

**Se SIM:** VÃ¡ para o Passo 2.

**Se NÃƒO:**
- Espere 2 minutos e tente de novo (pode ser instabilidade temporÃ¡ria)
- Tente enviar uma mensagem simples: `oi`
- Se ainda nÃ£o responder: acesse o painel Mission Control ou reinicie o gateway pelo link que vocÃª configurou no setup

---

## Passo 2 â€” PeÃ§a um diagnÃ³stico ao bot

Cole esse prompt:

```
Faz um diagnÃ³stico rÃ¡pido pra mim agora:
1. O gateway estÃ¡ funcionando? (/status)
2. Tem algum erro recente nos logs?
3. O modelo de IA estÃ¡ respondendo?
4. Alguma automaÃ§Ã£o ou cron com problema?
Me diz o que encontrar em linguagem simples.
```

---

## Passo 3 â€” Identifique o sintoma e vÃ¡ para o Q&A certo

| O que estÃ¡ acontecendo | Arquivo de ajuda |
|---|---|
| Bot nÃ£o responde / lento / respostas pioraram | â†’ qa-03-contexto-memoria.md |
| Erro 401, token invÃ¡lido, problema de API key | â†’ qa-01-auth-modelo.md |
| Qualquer pessoa usa meu bot / bot nÃ£o responde no grupo | â†’ qa-02-telegram.md |
| "Port in use", "command not found", nÃ£o conecta | â†’ qa-04-infra-basica.md |
| DÃºvida sobre modelos / custo / Claude bloqueado | â†’ qa-06-llms-comparativo.md |
| DÃºvida sobre como o sistema funciona | â†’ qa-05-arquitetura.md |

---

## Prompt Universal de EmergÃªncia

Se nÃ£o souber o que estÃ¡ errado, cole isso:

```
Estou com um problema no OpenClaw e nÃ£o sei exatamente o que Ã©.
Sintoma: [DESCREVA O QUE ESTÃ ACONTECENDO]

Por favor:
1. Me ajuda a identificar a causa
2. Me diz o que fazer em linguagem simples
3. Me guia passo a passo pra resolver
4. Confirma quando estiver resolvido
```

---

## âš ï¸ Regra de Ouro

**NÃ£o tente resolver no chute.**

A sequÃªncia correta sempre Ã©:
1. Diagnosticar primeiro (o que estÃ¡ errado?)
2. Entender a causa (por quÃª aconteceu?)
3. Aplicar soluÃ§Ã£o (como corrigir?)
4. Confirmar que resolveu (funcionou?)

Pular etapas cria problemas novos em cima do antigo.

---

*Se nada resolver: descreva seu problema detalhadamente no grupo de suporte com:*
- *O que vocÃª tentou fazer*
- *O que aconteceu (print do erro se tiver)*
- *O que vocÃª jÃ¡ tentou*

---

*Ãšltima atualizaÃ§Ã£o: Fev/2026*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
