# PRD â€” Aula N-7: Quanto Custa e Qual Modelo Usar

> **NÃ­vel:** IntermediÃ¡rio  
> **DuraÃ§Ã£o estimada:** 15 minutos  
> **PrÃ©-requisito:** OpenClaw instalado e funcionando, pelo menos um provider configurado

---

## ðŸŽ¯ Objetivo da Aula

Ao final desta aula, o aluno serÃ¡ capaz de:

1. Entender a diferenÃ§a entre **assinatura** e **API Key** e quando usar cada uma
2. Comparar os principais modelos de IA por **preÃ§o e capacidade**
3. Escolher o modelo certo para cada tipo de tarefa (economizando atÃ© 95%)
4. Configurar **modelos diferentes por funÃ§Ã£o** (heartbeat, chat, anÃ¡lise)
5. Estimar o **gasto mensal real** do seu setup
6. Colocar **limites de gasto** para nunca ser surpreendido

---

## ðŸ“‹ Script de GravaÃ§Ã£o â€” SeÃ§Ã£o por SeÃ§Ã£o

### ðŸŽ¬ ABERTURA (0:00 â€“ 1:00)

**[Bruno na tela, tom direto]**

> "Fala, pessoal! Aula N-7 â€” custos e modelos. Essa Ã© a aula que vai te salvar de um susto na fatura."

> "JÃ¡ vi aluno gastar $200 num Ãºnico dia de teste. JÃ¡ vi outro rodando o mesmo setup por $8/mÃªs. A diferenÃ§a? Escolha de modelo. Em 15 minutos vocÃª vai entender tudo."

---

### ðŸ’³ SEÃ‡ÃƒO 1: Assinatura vs API Key â€” Qual Usar? (1:00 â€“ 4:30)

**[Tela: slide comparativo]**

> "Primeira decisÃ£o: vocÃª vai usar assinatura mensal ou API Key com pay-per-use?"

**[Mostrar na tela:]**

| | Assinatura (ChatGPT Plus/Pro) | API Key (pay-per-use) |
|---|---|---|
| **Custo fixo** | Valor mensal do seu plano | $0 se nÃ£o usar |
| **Controle de gasto** | Limitado ao plano | âœ… Total |
| **Funciona com OpenClaw** | âœ… Sim, via OAuth OpenAI | âœ… Sim |
| **Ideal para** | Setup rÃ¡pido, uso no mesmo ecossistema | Agentes, automaÃ§Ã£o, controle fino |
| **Risco de surpresa** | Baixo | MÃ©dio sem limites |

> "O fluxo padrÃ£o do curso Ã©: **OpenAI primeiro**. OAuth Ã© o caminho mais rÃ¡pido pra comeÃ§ar. API Key Ã© o caminho mais flexÃ­vel quando vocÃª quer medir custo, trocar modelo e automatizar com mais controle."

> "Se quiser testar outros modelos alÃ©m da stack padrÃ£o, use OpenRouter como camada de experimentaÃ§Ã£o. Anthropic fica como comparaÃ§Ã£o opcional, nÃ£o como fallback principal do curso."

---

### ðŸ“Š SEÃ‡ÃƒO 2: Tabela de Modelos e PreÃ§os (4:30 â€“ 8:00)

**[Tela: tabela comparativa]**

> "Agora vamos falar de dinheiro concreto. Os modelos sÃ£o cobrados por tokens â€” pedaÃ§os de texto de ~4 caracteres. O preÃ§o Ã© por 1 milhÃ£o de tokens."

| Modelo | PreÃ§o Input (M tokens) | PreÃ§o Output (M tokens) | Velocidade | Qualidade |
|--------|----------------------|------------------------|------------|-----------|
| **GPT-5.4** | $2.50 | $15 | MÃ©dio | â­â­â­â­â­ |
| **GPT-4o** | $2.50 | $10 | MÃ©dio | â­â­â­â­ |
| **GPT-4o-mini** | $0.15 | $0.60 | RÃ¡pido | â­â­â­ |
| **Gemini 3.1 Pro** | $1.25 | $5 | MÃ©dio | â­â­â­â­ |
| **Mistral Small** | $0.10 | $0.30 | Muito rÃ¡pido | â­â­ |

> "Uma mensagem tÃ­pica usa ~500 tokens de input + ~200 tokens de output. Vamos fazer a conta com a stack padrÃ£o do curso:"

> "Com GPT-5.4: $2.50/M Ã— 0.0005M + $15/M Ã— 0.0002M = $0.00125 + $0.003 = **$0.00425 por mensagem**"
> "Com GPT-4o-mini: $0.15/M Ã— 0.0005M + $0.60/M Ã— 0.0002M = $0.000075 + $0.00012 = **$0.000195 por mensagem**"

> "DiferenÃ§a: **mais de 20x mais barato** com GPT-4o-mini para tarefas simples."

> "Anthropic continua Ãºtil como comparaÃ§Ã£o opcional, e OpenRouter Ã© o melhor jeito de experimentar esses modelos sem trocar a narrativa principal do curso."

---

### ðŸŽ¯ SEÃ‡ÃƒO 3: Qual Modelo Para Cada SituaÃ§Ã£o? (8:00 â€“ 11:00)

**[Tela: cards de recomendaÃ§Ã£o]**

> "A estratÃ©gia Ã©: use o modelo MÃNIMO que resolve o problema."

**Heartbeats e Crons:**

> "Heartbeat Ã© quando o agente acorda sozinho pra checar emails, calendÃ¡rio, notificaÃ§Ãµes. Essas tarefas sÃ£o simples â€” verificar, categorizar, decidir se precisa te avisar."
> "**Use GPT-4o-mini** â€” Ã© o modelo econÃ´mico da stack padrÃ£o do curso. Para tarefas repetitivas, ele entrega o melhor custo-benefÃ­cio sem sacrificar velocidade."

**InteraÃ§Ã£o DiÃ¡ria (mensagens no Telegram):**

> "Quando vocÃª manda uma mensagem pro agente e quer uma resposta Ãºtil â€” pesquisa, organizaÃ§Ã£o, anÃ¡lise leve."
> "**Use GPT-4o** â€” ele Ã© o ponto ideal da stack padrÃ£o para conversa diÃ¡ria: mais barato que o flagship e muito forte para uso geral."

**AnÃ¡lise Complexa:**

> "Quando vocÃª precisa analisar um documento longo, tomar uma decisÃ£o difÃ­cil, ou escrever algo importante."
> "**Use GPT-5.4** â€” mas sÃ³ quando precisa. Ele Ã© o topo da stack padrÃ£o do curso para contexto longo, decisÃµes e escrita importante."

**ExperimentaÃ§Ã£o e comparaÃ§Ã£o:**

> "Gemini 3.1 Pro Ã© uma excelente alternativa econÃ´mica. Claude pode entrar como comparaÃ§Ã£o opcional. Se quiser testar esses caminhos sem mexer no setup principal, use OpenRouter como camada de experimentaÃ§Ã£o."

---

### âš™ï¸ SEÃ‡ÃƒO 4: Como Configurar Modelo por FunÃ§Ã£o (11:00 â€“ 13:00)

**[Tela: Terminal]**

> "O OpenClaw permite configurar modelos diferentes por funÃ§Ã£o. Isso Ã© poderoso."

```bash
# Modelo padrÃ£o para interaÃ§Ãµes do dia a dia
openclaw config set model openai/gpt-5.4

# Modelo especÃ­fico para heartbeats (econÃ´mico)
openclaw config set heartbeat.model openai/gpt-4o-mini

# Modelo para anÃ¡lises pesadas (opcional, usar com moderaÃ§Ã£o)
openclaw config set analysis.model openai/gpt-5.4
```

> "Dessa forma, o agente usa GPT-4o-mini automaticamente nos heartbeats, GPT-4o para conversa diÃ¡ria e GPT-5.4 quando vocÃª realmente pedir anÃ¡lise pesada."

> "Para verificar a configuraÃ§Ã£o atual:"

```bash
openclaw config get model
openclaw config get heartbeat.model
```

---

### ðŸ’° SEÃ‡ÃƒO 5: Exemplo Real de Gasto Mensal (13:00 â€“ 14:30)

**[Tela: breakdown de custos]**

> "Vamos montar um setup real e calcular:"

| Uso | Quantidade/mÃªs | Modelo | Custo estimado |
|-----|---------------|--------|----------------|
| Heartbeats (2x/hora, 16h/dia) | ~960 execuÃ§Ãµes | GPT-4o-mini | ~$1 |
| Mensagens diÃ¡rias (10/dia) | ~300 mensagens | GPT-4o | ~$4 |
| AnÃ¡lises semanais | ~4 anÃ¡lises longas | GPT-5.4 | ~$6 |
| Crons e automaÃ§Ãµes | ~200 execuÃ§Ãµes | GPT-4o-mini | ~$1 |
| **Total estimado** | | | **~$12/mÃªs** |

> "Setup moderado, agente funcionando 24/7 com heartbeats ativos: **~$12 a $25/mÃªs**. Se vocÃª usar intensamente, pode passar disso, mas a stack padrÃ£o jÃ¡ nasce com controle de custo muito melhor."

> "Compare com: manter uma assinatura isolada sem automaÃ§Ã£o, ou depender de execuÃ§Ã£o manual. Com OpenAI como base, OpenRouter para experimentos e Anthropic opcional, vocÃª monta um stack profissional por uma fraÃ§Ã£o do custo de operaÃ§Ã£o humana."

---

### ðŸš¨ SEÃ‡ÃƒO 6: Troubleshooting â€” "Minha Conta Zerou" (14:30 â€“ 15:00)

**[Tela: como colocar limites]**

> "Isso acontece quando um loop de cÃ³digo ou skill mal configurada faz milhares de chamadas sem querer. Como se proteger:"

**Na OpenAI:**
```
platform.openai.com â†’ Settings â†’ Billing â†’ Usage Limits
â†’ "Monthly spend limit" â†’ Defina um valor (ex: $50)
â†’ "Notification threshold" â†’ Defina um alerta (ex: $25)
```

**No OpenClaw:**
```bash
# Limitar requests por hora (proteÃ§Ã£o contra loops)
openclaw config set rateLimit.requestsPerHour 100

# Ver gasto estimado acumulado do mÃªs
openclaw usage report
```

> "Configure esses limites **antes** de comeÃ§ar a usar intensamente. Ã‰ o cinto de seguranÃ§a â€” vocÃª espera nÃ£o precisar, mas vai ficar feliz que existe."

---

## ðŸ› ï¸ ConfiguraÃ§Ã£o Recomendada Para Iniciantes

```bash
# Setup bÃ¡sico e econÃ´mico para comeÃ§ar
openclaw config set model openai/gpt-5.4
openclaw config set heartbeat.model openai/gpt-4o-mini

# Verificar configuraÃ§Ã£o
openclaw config get model
openclaw config get heartbeat.model
```

E no platform.openai.com:
- Monthly spend limit: $50
- Notification at: $25

---

## ðŸ“Š Tabela Completa de Modelos (ReferÃªncia RÃ¡pida)

| Modelo | Input/Output ($/M) | Uso Ideal | Evitar Para |
|--------|-------------------|-----------|-------------|
| GPT-5.4 | $2.50/$15 | AnÃ¡lise profunda, decisÃµes importantes | Heartbeats e tarefas repetitivas |
| GPT-4o | $2.50/$10 | Conversa diÃ¡ria, pesquisa, cÃ³digo | Volume muito alto e tarefas triviais |
| GPT-4o-mini | $0.15/$0.60 | Heartbeats, crons, classificaÃ§Ã£o | AnÃ¡lises complexas e escrita crÃ­tica |
| Gemini 3.1 Pro | $1.25/$5 | Alternativa econÃ´mica para comparar resultados | â€” |
| Mistral Small | $0.10/$0.30 | Routing e classificaÃ§Ã£o simples | Qualquer tarefa que exige raciocÃ­nio |
| Claude (opcional) | Varia | ComparaÃ§Ã£o qualitativa ou casos especÃ­ficos | Virar fallback principal do curso |

---

## âœ… Checklist Final do Aluno

- [ ] Entende a diferenÃ§a entre assinatura e API Key
- [ ] Modelo padrÃ£o configurado: `openclaw config set model openai/gpt-5.4`
- [ ] Modelo de heartbeat configurado: `openclaw config set heartbeat.model openai/gpt-4o-mini`
- [ ] Limite de gasto configurado no platform.openai.com
- [ ] NotificaÃ§Ã£o de gasto configurada (threshold)
- [ ] `openclaw usage report` testado e funcionando

---

## â“ DÃºvidas Frequentes

**1. Posso trocar de modelo a qualquer hora?**

> Sim. `openclaw config set model NOVO-MODELO` e pronto. VÃ¡lido a partir da prÃ³xima mensagem.

**2. O Mistral Ã© muito mais barato â€” por que nÃ£o usar sempre?**

> Qualidade inferior para raciocÃ­nio complexo. Para classificaÃ§Ã£o simples funciona; para conversa diÃ¡ria, o mÃ­nimo recomendado da stack padrÃ£o Ã© GPT-4o-mini, e para interaÃ§Ã£o principal vale mais usar GPT-4o.

**3. Gemini Ã© confiÃ¡vel para uso com OpenClaw?**

> Sim, desde a v2026.3.2. Boa alternativa econÃ´mica. Ã‰ um Ã³timo candidato para comparaÃ§Ã£o via OpenRouter, sem virar o caminho principal do curso.

**4. Como saber exatamente quanto gastei?**

> `openclaw usage report` mostra breakdown por modelo. Platform.openai.com mostra em tempo real com grÃ¡ficos para a API da OpenAI. Se estiver testando outros modelos, OpenRouter oferece um dashboard separado para experimentaÃ§Ã£o.

**5. Haiku Ã© "burro"?**

> NÃ£o! Para tarefas estruturadas (checar emails, classificar mensagens, responder perguntas simples), Haiku Ã© excelente. Ele fica atrÃ¡s em raciocÃ­nio multi-step e criatividade. Para 80% das tarefas de automaÃ§Ã£o, Ã© mais que suficiente.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
