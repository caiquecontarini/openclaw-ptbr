# â“ Q&A â€” Telegram (Config, Allowlist, Privacidade)

> Linguagem simples. Sem terminal. Cole o prompt no seu bot e ele resolve.

---

## "Qualquer pessoa consegue mandar mensagem pro meu bot e ele responde"

**O que aconteceu:** Seu bot estÃ¡ configurado como "aberto" â€” qualquer pessoa que descobrir o username dele pode usar. Ã‰ como deixar a porta da sua casa aberta.

**O que fazer:**
Cole esse prompt no seu bot:

```
Meu bot estÃ¡ respondendo qualquer pessoa. Preciso restringir isso.
Me ajuda a:
1. Descobrir qual Ã© o meu ID numÃ©rico do Telegram
2. Configurar o dmPolicy para "allowlist" 
3. Adicionar meu ID na lista de permitidos
4. Confirmar que ficou certo testando
Explica tudo passo a passo.
```

---

## "Meu bot nÃ£o me responde mais depois que configurei a allowlist"

**O que provavelmente aconteceu:** VocÃª colocou a allowlist mas esqueceu de incluir o SEU prÃ³prio ID â€” ou digitou errado.

**O que fazer:**
Cole esse prompt no seu bot (via outro canal, como chat direto se tiver):

```
NÃ£o consigo mais mandar mensagem pro meu bot principal. 
Acho que me tranquei fora da allowlist.
Me ajuda a verificar:
1. Qual Ã© o meu ID do Telegram? (me diz como descobrir)
2. Como vejo quem estÃ¡ na allowlist atual?
3. Como adiciono meu ID corretamente?
```

**Como descobrir seu ID do Telegram:** Mande `/start` para @userinfobot no Telegram â€” ele te responde com seu ID numÃ©rico.

---

## "Bot nÃ£o funciona em grupo / tÃ³pico"

**O que fazer:**
Cole esse prompt no seu bot:

```
Meu bot nÃ£o estÃ¡ respondendo no grupo/tÃ³pico do Telegram.
Me ajuda a verificar:
1. O Privacy Mode do bot estÃ¡ desativado? (precisa estar desativado pra funcionar em grupo)
2. O ID do grupo estÃ¡ na configuraÃ§Ã£o de canais permitidos?
3. Tem alguma configuraÃ§Ã£o de "allowFrom" ou "allowedIds" que precisa atualizar?
Me guia passo a passo.
```

**Dica rÃ¡pida:** No BotFather, envie `/mybots` â†’ selecione seu bot â†’ `Bot Settings` â†’ `Group Privacy` â†’ `Turn off`. Isso resolve 80% dos problemas em grupo.

---

## "Apareceu um erro com allowedIds ou allowFrom â€” o que mudou?"

**O que aconteceu:** O OpenClaw atualizou o formato da configuraÃ§Ã£o. VersÃµes antigas usavam `allowedIds` ou `allowFrom` â€” a versÃ£o atual usa `dmPolicy: "allowlist"` com `allowedUsers`.

**O que fazer:**
Cole esse prompt no seu bot:

```
Minha configuraÃ§Ã£o do Telegram tem "allowedIds" ou "allowFrom" que parecem ser de uma versÃ£o antiga.
Me ajuda a:
1. Identificar qual formato estou usando
2. Migrar para o formato atual (dmPolicy + allowedUsers)
3. Verificar se a config ficou correta
4. Reiniciar o gateway pra aplicar
```

---

## "Como adiciono mais pessoas pra poderem usar meu bot?"

**O que fazer:**
Cole esse prompt no seu bot:

```
Quero adicionar uma nova pessoa para poder usar meu bot.
O ID do Telegram dela Ã©: [COLOQUE O ID AQUI]
Me guia como adicionar ela na allowlist corretamente.
```

**Como a pessoa descobre o ID dela:** Ela manda `/start` pro @userinfobot no Telegram.

---

*Ãšltima atualizaÃ§Ã£o: Fev/2026*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
