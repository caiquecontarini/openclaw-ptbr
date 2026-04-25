# Prompt â€” MÃ³dulo 1: Setup do OpenClaw

> Cole este prompt no chat do seu OpenClaw depois de assistir o MÃ³dulo 1.

---

Acabei de assistir o MÃ³dulo 1 do curso "Construa Seu AI COO". Preciso que vocÃª me guie no setup inicial do OpenClaw.

**O que preciso fazer:**

1. **Verificar meu ambiente** â€” Confira se Node.js, npm e as dependÃªncias estÃ£o instalados corretamente. Se algo faltar, me explique o que Ã© e me ajude a instalar.

2. **Configurar o provider** â€” Me ajude a configurar o OpenClaw com ChatGPT/OpenAI. O caminho recomendado Ã© via OAuth (login com conta ChatGPT Plus/Pro, sem precisar de API key). Se eu preferir usar API key da OpenAI, me ajude a configurar tambÃ©m e explique as diferenÃ§as. Depois, me explique como usar OpenRouter sÃ³ como camada opcional de experimentaÃ§Ã£o para testar outros LLMs.

3. **Ativar o perfil de ferramentas** â€” Execute `openclaw config set tools.profile full` e me explique por quÃª isso Ã© obrigatÃ³rio. Sem isso, vocÃª nÃ£o executa comandos â€” sÃ³ responde mensagens. Depois rode `openclaw config validate` pra confirmar que a configuraÃ§Ã£o estÃ¡ vÃ¡lida.

4. **Escolher o modelo** â€” Me explique a diferenÃ§a entre GPT-5.4, GPT-4o e GPT-4o-mini. Me recomende qual usar pra comeÃ§ar (considerando custo x qualidade). Configure a stack padrÃ£o do curso (GPT-5.4 â†’ GPT-4o â†’ GPT-4o-mini), e deixe OpenRouter sÃ³ para testes opcionais.

5. **Conectar ao Telegram** â€” Me guie passo a passo pra criar um bot no BotFather e conectar ao OpenClaw. Me explique por que Telegram com tÃ³picos Ã© melhor que WhatsApp (sessÃ£o Ãºnica vs mÃºltiplas). Use `openclaw channels login` e `openclaw channels status --probe` pra validar.

6. **Primeiro teste** â€” Depois de tudo configurado, rode um health check e confirme que tÃ¡ tudo funcionando. Inclua um teste de execuÃ§Ã£o de comando (ex: `echo "SHELL_TEST_OK"`) pra provar que o tools.profile full estÃ¡ ativo.

7. **OtimizaÃ§Ã£o inicial de tokens** â€” Configure a session initialization rule pra nÃ£o carregar 50KB de histÃ³rico a cada mensagem:
   - Carregar APENAS: SOUL.md, USER.md, IDENTITY.md, memory/YYYY-MM-DD.md
   - NÃƒO carregar automaticamente: MEMORY.md, histÃ³rico de sessÃµes, outputs anteriores
   - Usar `memory_search()` sob demanda quando precisar de contexto anterior

**Regras:**
- Me explique o PORQUÃŠ de cada passo antes de executar
- Se algo der erro, me explique o que aconteceu e como resolver
- No final, me diga quanto isso vai custar por mÃªs aproximadamente
- ReferÃªncia de custos: antes da otimizaÃ§Ã£o ~$2-3/dia, depois ~$0.10/dia

8. **Timezone (OBRIGATÃ“RIO se vai usar crons)** â€” Configure o timezone do gateway para que seus crons disparem no horÃ¡rio correto do Brasil. Sem isso, um cron configurado "Ã s 9h" vai disparar Ã s 12h (UTC):

```bash
sudo systemctl edit openclaw
# Adicione dentro de [Service]:
# Environment="OPENCLAW_TZ=America/Sao_Paulo"
sudo systemctl daemon-reload && sudo systemctl restart openclaw
```

**Comandos Ãºteis pra este mÃ³dulo:**
```
openclaw gateway start --mode local
openclaw config set tools.profile full
openclaw config validate
openclaw channels login
openclaw channels status --probe
openclaw models list --all
openclaw models set <model>
```

Vamos comeÃ§ar?


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
