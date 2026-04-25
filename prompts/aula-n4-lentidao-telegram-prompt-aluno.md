# Prompt do Aluno â€” Aula N-4: LentidÃ£o do Bot no Telegram

**Como usar:** Cole este prompt diretamente no seu agente OpenClaw para iniciar uma sessÃ£o interativa de diagnÃ³stico e resoluÃ§Ã£o da lentidÃ£o do bot.

---

## ðŸ“‹ PROMPT PRINCIPAL

```
Meu bot no Telegram estÃ¡ lento â€” Ã s vezes demora 30 segundos ou mais pra responder, e Ã s vezes parece que trava. 

Quero fazer um diagnÃ³stico completo com vocÃª. Me guia pelo processo passo a passo, como na Aula N-4 do curso.

Para cada etapa:
1. Me diz qual comando rodar ou qual config verificar
2. Me explica o que procurar no resultado
3. Aguarda eu colar a saÃ­da
4. Analisa e me diz se essa Ã© a causa

Vamos comeÃ§ar pelo diagnÃ³stico inicial. Qual Ã© o primeiro passo?
```

---

## ðŸ” PROMPTS DE DIAGNÃ“STICO POR CAUSA

Use os prompts abaixo conforme o diagnÃ³stico avanÃ§ar:

### Se suspeitar de contexto cheio:

```
Vou rodar /status agora e te mostrar o resultado.
[cole o resultado do /status]

Ã‰ o contexto? O que vocÃª recomenda â€” /compact ou /new? Me explica a diferenÃ§a antes de eu decidir.
```

### Se suspeitar de modelo pesado:

```
Me mostra como ver qual modelo estÃ¡ configurado agora e como trocar 
para usar Sonnet nas conversas e Haiku nos crons. 
Quero entender o impacto real no tempo de resposta.
```

### Se suspeitar de VPS fraca:

```
Me ajuda a interpretar a saÃ­da do `openclaw status` e do `htop`.
O que os nÃºmeros me dizem sobre se minha VPS aguenta a carga atual?
```

### Se suspeitar de crons simultÃ¢neos:

```
Roda mentalmente: se eu tiver 4 crons todos Ã s 09:00, o que acontece 
no servidor? Me mostra como escalonar eles e como listar os crons ativos.
```

### Se suspeitar de heartbeat agressivo:

```
Meu heartbeat estÃ¡ configurado a cada X minutos. 
Qual Ã© o intervalo ideal? E devo usar Haiku pra ele? Por quÃª?
```

### Para ativar streaming parcial:

```
Quero ativar o streaming parcial no Telegram pra melhorar a percepÃ§Ã£o 
de velocidade. Me mostra exatamente onde e como configurar isso no openclaw.json.
```

---

## âœ… PROMPT DE VERIFICAÃ‡ÃƒO FINAL

ApÃ³s implementar as mudanÃ§as:

```
Implementei as mudanÃ§as que vocÃª sugeriu. Agora vamos verificar se funcionou:

1. Como eu testo se o bot ficou mais rÃ¡pido de forma objetiva?
2. O que devo monitorar nas prÃ³ximas 24 horas para confirmar que estÃ¡ estÃ¡vel?
3. Tem alguma configuraÃ§Ã£o de "prevenÃ§Ã£o" que vocÃª recomenda pra nÃ£o ter esse problema de novo?

Me faz um resumo das mudanÃ§as que fizemos e do que cada uma resolve.
```

---

## ðŸ“Š PROMPT DE EXERCÃCIO PRÃTICO

Para praticar o diagnÃ³stico de forma estruturada:

```
Vou te dar uma situaÃ§Ã£o hipotÃ©tica e vocÃª me guia no diagnÃ³stico:

SituaÃ§Ã£o: Bot funcionando bem por semanas. De repente, hoje Ã  tarde comeÃ§a a 
demorar 20-30s em toda mensagem. Ã‰ o mesmo horÃ¡rio em que eu adicionei 3 novos 
crons de monitoramento e aumentei o heartbeat de 30 para 5 minutos.

Sem olhar os logs ainda â€” quais sÃ£o as hipÃ³teses mais provÃ¡veis? 
Em que ordem eu deveria investigar e por quÃª?
```

---

## ðŸ’¡ DICAS DE USO

- **Cole resultados reais:** Quando o agente pedir saÃ­da de um comando, cole o resultado real do seu terminal. O diagnÃ³stico fica muito mais preciso.
- **Um problema por vez:** Se tiver mÃºltiplas causas, resolva uma por vez e teste antes de passar pra prÃ³xima.
- **Salve as mudanÃ§as:** ApÃ³s cada alteraÃ§Ã£o no `openclaw.json`, recarregue o gateway com `openclaw gateway restart`.
- **MeÃ§a antes e depois:** Anote o tempo mÃ©dio de resposta antes das mudanÃ§as para comparar depois.

---

*Prompt criado para a Aula N-4 do Curso OpenClaw | NÃ­vel: IntermediÃ¡rio*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
