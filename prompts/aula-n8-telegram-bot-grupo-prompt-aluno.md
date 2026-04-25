# Prompt do Aluno â€” Aula N-8: Telegram Bot NÃ£o Responde no Grupo

> **Como usar:** Copie o prompt abaixo e cole no chat do seu agente OpenClaw apÃ³s assistir a aula.

---

## ðŸ“‹ Prompt Principal

```
OlÃ¡! Assisti a aula N-8 sobre configuraÃ§Ã£o de bot em grupos do Telegram.

Estou tentando fazer meu bot funcionar em um grupo, mas [ele nÃ£o responde / sÃ³ responde comandos / responde Ã s vezes].

Me ajude a:
1. Diagnosticar o problema especÃ­fico no meu caso
2. Aplicar os fixes necessÃ¡rios
3. Verificar que funcionou

Vamos comeÃ§ar com o diagnÃ³stico?
```

---

## ðŸ” ExercÃ­cio 1 â€” DiagnÃ³stico Completo

```
Por favor, faÃ§a um diagnÃ³stico completo do meu setup de bot para grupos:

1. Verifique a configuraÃ§Ã£o atual:
   - `openclaw config get channels.telegram.groupPolicy`
   - `openclaw config get channels.telegram.groupAllowlist`
   
2. Me diga qual das 3 causas Ã© mais provÃ¡vel:
   - Privacy mode ativado no BotFather
   - groupPolicy nÃ£o configurado
   - Chat ID nÃ£o estÃ¡ no allowlist

3. Cheque os logs por mensagens de grupo:
   `openclaw gateway logs | tail -50`

ApÃ³s o diagnÃ³stico, me diga exatamente o que preciso fazer.
```

---

## ðŸ¤– ExercÃ­cio 2 â€” Fix do Privacy Mode

```
Preciso verificar e corrigir o privacy mode do meu bot.

Por favor, me guie pelo processo completo:
1. Como verificar se o privacy mode estÃ¡ ativado (sinal no comportamento do bot)
2. Passo a passo para desativar via BotFather:
   - Qual comando enviar ao BotFather
   - O que selecionar quando ele perguntar
   - Como confirmar que foi desativado
3. Por que preciso remover e re-adicionar o bot ao grupo
4. Como confirmar que a mudanÃ§a funcionou

(Se jÃ¡ verificou e o privacy mode estÃ¡ desativado, me confirme isso e vamos para o prÃ³ximo passo)
```

---

## âš™ï¸ ExercÃ­cio 3 â€” Configurar groupPolicy

```
Quero configurar o groupPolicy do OpenClaw corretamente.

Por favor:
1. Explique a diferenÃ§a entre groupPolicy = "allowlist" e "open"
2. Configure o allowlist (recomendado para seguranÃ§a):
   `openclaw config set channels.telegram.groupPolicy allowlist`
3. Me ajude a descobrir o chat ID do meu grupo:
   - Execute `openclaw gateway logs | grep -i "chat_id"` 
   - Ou me diga outro mÃ©todo se nÃ£o aparecer
4. ApÃ³s encontrar o ID, configure o allowlist:
   `openclaw config set channels.telegram.groupAllowlist "[-100XXXXXXXXXX]"`
5. Reinicie o gateway: `openclaw gateway restart`
6. Teste: envie uma mensagem no grupo e verifique nos logs

(Meu grupo Ã©: [DESCREVA SEU GRUPO â€” ex: "grupo familiar de 5 pessoas"])
```

---

## ðŸ“ ExercÃ­cio 4 â€” Descobrir Chat ID na PrÃ¡tica

```
Preciso descobrir o chat ID do meu grupo do Telegram.

Por favor, me guie por TODOS os mÃ©todos disponÃ­veis:

MÃ©todo 1 â€” Via logs do OpenClaw:
- Como enviar uma mensagem de teste no grupo
- Onde exatamente o chat ID aparece nos logs
- Formato do comando correto para filtrar

MÃ©todo 2 â€” Via @userinfobot:
- Como usar esse bot para descobrir o ID
- O que fazer com a informaÃ§Ã£o que ele retorna

MÃ©todo 3 â€” Via Telegram API (se necessÃ¡rio):
- Como usar a URL da API para ver updates recentes

Qual mÃ©todo Ã© mais fÃ¡cil para iniciantes?
```

---

## ðŸ”„ ExercÃ­cio 5 â€” dmPolicy vs groupPolicy na PrÃ¡tica

```
Quero entender de vez a diferenÃ§a entre dmPolicy e groupPolicy.

Por favor:
1. Mostre minha configuraÃ§Ã£o atual dos dois:
   - `openclaw config get channels.telegram.dmPolicy`
   - `openclaw config get channels.telegram.groupPolicy`
   
2. Me explique o que cada configuraÃ§Ã£o atual significa na prÃ¡tica:
   - Quem consegue mandar mensagem privada pro bot?
   - Em quais grupos o bot responde?
   
3. Me recomende a configuraÃ§Ã£o ideal para seguranÃ§a:
   - dmPolicy para uso pessoal (sÃ³ eu)
   - groupPolicy para um grupo especÃ­fico que eu quero

4. Se precisar ajustar, me dÃª os comandos exatos.
```

---

## ðŸ—ºï¸ ExercÃ­cio 6 â€” Fluxograma de DiagnÃ³stico (use se ainda tiver problemas)

```
Ainda nÃ£o consegui fazer o bot funcionar no grupo. Vamos ser sistemÃ¡ticos.

Por favor, me leve pelo fluxograma de diagnÃ³stico passo a passo:

Passo 1: O bot responde no grupo quando manda /start?
[Sim â†’ Passo 2] [NÃ£o â†’ Privacy mode ou bot nÃ£o estÃ¡ no grupo]

Passo 2: O groupPolicy estÃ¡ configurado?
[Sim â†’ Passo 3] [NÃ£o â†’ configurar groupPolicy]

Passo 3: O chat ID do grupo estÃ¡ no allowlist?
[Sim â†’ Passo 4] [NÃ£o â†’ adicionar chat ID]

Passo 4: O gateway foi reiniciado apÃ³s as mudanÃ§as?
[Sim â†’ ver logs] [NÃ£o â†’ openclaw gateway restart]

Para cada passo, execute o diagnÃ³stico e me diga o resultado. Vamos resolver isso juntos.
```

---

## âœ… VerificaÃ§Ã£o Final de Aprendizado

```
Para encerrar os exercÃ­cios da aula N-8, me faÃ§a um quiz rÃ¡pido com 5 perguntas sobre:
- O que Ã© privacy mode e quando causa problemas
- DiferenÃ§a entre dmPolicy e groupPolicy
- Como descobrir o chat ID de um grupo
- Por que precisa remover e re-adicionar o bot ao mudar o privacy mode
- Quando usar groupPolicy "open" vs "allowlist"

ApÃ³s eu responder, me dÃª feedback sobre o que acertei e o que preciso revisar.
```

---

## ðŸ’¡ Prompt de EmergÃªncia (se nada funcionar)

> Se vocÃª tentou tudo e o bot ainda nÃ£o responde no grupo:

```
Meu bot NÃƒO estÃ¡ respondendo no grupo e jÃ¡ tentei de tudo. Me ajude com um debug completo:

1. Execute `openclaw gateway logs | tail -100` e analise tudo
2. Verifique se hÃ¡ erros relacionados ao Telegram
3. Verifique se o webhook estÃ¡ funcionando: `openclaw provider status telegram`
4. Me mostre TODA a configuraÃ§Ã£o atual do canal Telegram:
   `openclaw config get channels.telegram`
5. Baseado no que encontrar, me dÃª a soluÃ§Ã£o especÃ­fica

Estou disposto a seguir qualquer passo â€” sÃ³ preciso que o bot funcione no grupo.
```


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
