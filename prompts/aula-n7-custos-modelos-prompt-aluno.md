# Prompt do Aluno â€” Aula N-7: Quanto Custa e Qual Modelo Usar

> **Como usar:** Copie o prompt abaixo e cole no chat do seu agente OpenClaw apÃ³s assistir a aula.

---

## ðŸ“‹ Prompt Principal

```
OlÃ¡! Acabei de assistir a aula N-7 do curso OpenClaw sobre custos e modelos de IA.

Preciso da sua ajuda para:
1. Verificar quais modelos estÃ£o configurados no meu setup
2. Otimizar a configuraÃ§Ã£o para economizar sem perder qualidade
3. Entender quanto estou gastando (ou vou gastar)

Vamos comeÃ§ar com um diagnÃ³stico da minha configuraÃ§Ã£o de modelos?
```

---

## ðŸ§ª ExercÃ­cio 1 â€” DiagnÃ³stico de Modelos Configurados

```
Por favor, verifique minha configuraÃ§Ã£o atual de modelos:

1. Execute `openclaw config get model` â€” qual Ã© o modelo padrÃ£o?
2. Execute `openclaw config get heartbeat.model` â€” tem modelo especÃ­fico para heartbeat?
3. Me diga se estou usando o modelo certo ou se devo otimizar
4. Calcule o custo estimado por mensagem com o modelo atual

Baseado na tabela de preÃ§os:
- GPT-4o-mini: ~$0.15/$0.60 por M tokens
- GPT-4o: $2.50/$10 por M tokens  
- GPT-5.4: $2.50/$15 por M tokens
- Gemini 3.1 Pro: $1.25/$5 por M tokens
```

---

## ðŸ’° ExercÃ­cio 2 â€” Calcular Gasto Mensal Estimado

```
Quero estimar quanto vou gastar por mÃªs. Me ajude com esse cÃ¡lculo:

Meu uso estimado:
- Heartbeats: [X] vezes por hora, [Y] horas por dia
- Mensagens diretas: [Z] por dia
- AnÃ¡lises longas: [W] por semana

Para cada tipo de uso:
1. Qual modelo deveria usar?
2. Qual o custo estimado por execuÃ§Ã£o?
3. Qual o custo mensal total desse item?

Ao final, some tudo e me dÃª um total mensal estimado.
(Preencha os valores acima com o seu uso real ou estimado)
```

---

## âš™ï¸ ExercÃ­cio 3 â€” Configurar Modelos Otimizados

```
Quero configurar modelos diferentes para diferentes situaÃ§Ãµes no meu OpenClaw.

Por favor, me guie pelos comandos para:
1. Configurar `openai/gpt-4o` como modelo padrÃ£o para interaÃ§Ãµes
2. Configurar `openai/gpt-4o-mini` para heartbeats (econÃ´mico)
3. Separar `openai/gpt-5.4` para anÃ¡lises mais pesadas, quando fizer sentido
4. Verificar que as configuraÃ§Ãµes ficaram corretas
5. Me dizer o impacto estimado no custo mensal dessa mudanÃ§a

Execute os comandos e confirme cada passo.
```

---

## ðŸ›¡ï¸ ExercÃ­cio 4 â€” Configurar Limites de Gasto

```
Preciso configurar proteÃ§Ãµes para nÃ£o ter surpresas na fatura.

Por favor:
1. Me diga como configurar o limite de gasto mensal no platform.openai.com (instruÃ§Ãµes passo a passo)
2. Configure o rateLimit no OpenClaw: `openclaw config set rateLimit.requestsPerHour 100`
3. Me ensine a verificar o gasto atual com `openclaw usage report`
4. Sugira um limite de gasto adequado para o meu perfil de uso

Queremos garantir que se algo der errado (loop infinito, bug em skill), o dano financeiro seja limitado.
```

---

## ðŸ“Š ExercÃ­cio 5 â€” ComparaÃ§Ã£o Real de Custo: Haiku vs Sonnet vs Opus

```
Quero ver na prÃ¡tica a diferenÃ§a de custo entre os modelos.

Por favor, me faÃ§a uma demonstraÃ§Ã£o:
1. Crie uma tarefa de heartbeat simples (ex: "verifique se hÃ¡ emails urgentes e responda em 1 linha")
2. Estime o custo dessa tarefa em cada modelo: GPT-4o-mini, GPT-4o e GPT-5.4
3. Calcule quanto isso significa em 30 dias com 2 heartbeats por hora

Mostre o cÃ¡lculo detalhado para eu entender por que o GPT-4o-mini Ã© tÃ£o importante para tarefas repetitivas.
```

---

## ðŸ” ExercÃ­cio 6 â€” AnÃ¡lise do Uso Real (se jÃ¡ estiver usando hÃ¡ algum tempo)

```
JÃ¡ estou usando o OpenClaw hÃ¡ algum tempo e quero analisar meu uso real.

Por favor:
1. Execute `openclaw usage report` e me mostre o resultado
2. Identifique qual modelo estou usando mais
3. Calcule se estaria gastando menos com uma configuraÃ§Ã£o mais otimizada
4. Sugira ajustes na minha configuraÃ§Ã£o baseado no uso real

Se `openclaw usage report` nÃ£o estiver disponÃ­vel, me explique como ver o uso no console da OpenAI. Se eu estiver testando outros modelos, inclua tambÃ©m como ver isso no OpenRouter.
```

---

## âœ… VerificaÃ§Ã£o Final de Aprendizado

```
Para encerrar os exercÃ­cios da aula N-7, me faÃ§a um quiz rÃ¡pido com 5 perguntas sobre:
- Quando usar GPT-4o-mini vs GPT-4o vs GPT-5.4
- Como o preÃ§o por token funciona na prÃ¡tica
- Como configurar modelos diferentes por funÃ§Ã£o
- Como se proteger de gastos inesperados
- DiferenÃ§a entre assinatura e API Key

ApÃ³s eu responder, me dÃª feedback sobre o que acertei e o que preciso revisar.
```

---

## ðŸ’¡ Dica RÃ¡pida

> Se quiser uma anÃ¡lise rÃ¡pida do seu setup atual:

```
FaÃ§a um diagnÃ³stico completo do meu setup de custos:
1. Modelos configurados atualmente
2. FrequÃªncia de heartbeats ativos
3. Custo mensal estimado com a configuraÃ§Ã£o atual
4. SugestÃ£o de otimizaÃ§Ã£o se aplicÃ¡vel
5. Alerta se alguma configuraÃ§Ã£o pode causar custo excessivo
```


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
