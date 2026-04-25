# â“ Q&A â€” Auth & Modelo (API, Claude, Troca de Provedor)

> Linguagem simples. Sem terminal. Cole o prompt no seu bot e ele resolve.

---

## "Meu bot parou de responder / ficou lento de repente"

**O que provavelmente aconteceu:** O serviÃ§o do Claude (Anthropic) colocou sua conta em cooldown temporÃ¡rio. Ã‰ normal â€” acontece quando hÃ¡ muitas chamadas em pouco tempo.

**O que fazer:**
Cole esse prompt no seu bot:

```
Verifica o status do gateway pra mim. Quero saber: 
1. Se o modelo configurado estÃ¡ respondendo
2. Se tem algum erro de autenticaÃ§Ã£o ou cooldown
3. O que vocÃª recomenda fazer agora
```

**Se o bot tambÃ©m nÃ£o responder:** Espere 5â€“10 minutos e tente de novo. O cooldown Ã© automÃ¡tico e passa sozinho.

---

## "Apareceu erro 401 â€” o que significa isso?"

**Em linguagem simples:** O bot tentou se identificar pro serviÃ§o de IA e a senha estava errada ou vencida. Ã‰ como tentar entrar numa festa com um convite expirado.

**O que fazer:**
Cole esse prompt no seu bot:

```
Apareceu um erro 401 de autenticaÃ§Ã£o. Me ajuda a diagnosticar:
1. A chave de API estÃ¡ configurada corretamente?
2. O .env estÃ¡ sendo lido pelo gateway?
3. O serviÃ§o do systemd tem algum override antigo que pode estar sobrescrevendo a chave nova?
Me diz o que encontrar e o que devo corrigir.
```

---

## "NÃ£o sei se devo usar API key ou assinar o plano Claude.ai"

**DiferenÃ§a simples:**

| | Assinatura Claude.ai | API Key (Anthropic) |
|---|---|---|
| **Pra quÃª serve** | Usar o chat no site/app | Conectar ao OpenClaw |
| **PreÃ§o** | R$ 100â€“550/mÃªs | Paga pelo uso (R$ 0,10â€“R$ 5 por 1M tokens) |
| **Funciona no OpenClaw?** | âŒ NÃ£o diretamente | âœ… Sim |

**Resumo:** Para usar no OpenClaw, vocÃª precisa da **API Key** (console.anthropic.com), nÃ£o da assinatura do chat.

**âš ï¸ Aviso importante sobre bloqueios:** Algumas contas da Anthropic estÃ£o sendo bloqueadas no momento. NÃ£o temos controle sobre isso â€” Ã© uma decisÃ£o deles. Se sua conta foi bloqueada, o curso ensina como usar o **ChatGPT (OpenAI) como alternativa**. Muitos alunos estÃ£o usando assim sem problema.

---

## "Quero trocar do Claude para o ChatGPT (ou vice-versa)"

**O que fazer:**
Cole esse prompt no seu bot:

```
Quero trocar o modelo que vocÃª usa. Me guia passo a passo:
1. Como pego minha API key da OpenAI (ou Anthropic)
2. Como atualizo o .env com a nova chave
3. Como configuro o modelo no openclaw.json
4. Como reinicio o gateway pra aplicar a mudanÃ§a
Explica como se eu nunca tivesse feito isso antes.
```

---

## "Quanto custa usar o Claude / ChatGPT no OpenClaw?"

**ReferÃªncia de preÃ§os (Fev/2026 â€” consulte sempre o site oficial):**

| Modelo | Plano | PreÃ§o aprox/mÃªs |
|---|---|---|
| Claude Haiku | API | Muito barato (~R$ 1â€“5) |
| Claude Sonnet | API | Moderado (~R$ 15â€“50) |
| Claude Opus | API | Caro (~R$ 80â€“200) |
| GPT-4o mini | API | Muito barato (~R$ 1â€“5) |
| GPT-4o | API | Moderado (~R$ 20â€“80) |

**Nossa recomendaÃ§Ã£o:**
- Use **Haiku ou GPT-4o mini** para tarefas automÃ¡ticas (lembretes, crons)
- Use **Sonnet ou GPT-4o** para conversas do dia a dia
- Reserve o **Opus** para quando realmente precisar de profundidade

**Dica:** Com otimizaÃ§Ã£o, a maioria dos alunos gasta entre R$ 20â€“80/mÃªs.

---

*Ãšltima atualizaÃ§Ã£o: Fev/2026*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
