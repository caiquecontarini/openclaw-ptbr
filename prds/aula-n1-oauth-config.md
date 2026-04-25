# PRD â€” Aula N-1: Configurar Credenciais â€” ChatGPT OAuth (PadrÃ£o) + OpenAI API Key

> **NÃ­vel:** Iniciante / Setup
> **DuraÃ§Ã£o estimada:** 15â€“20 minutos
> **PrÃ©-requisito:** OpenClaw instalado, acesso Ã  internet, conta ChatGPT (Plus ou Pro)
> **Atualizado:** ChatGPT OAuth como caminho recomendado (2026-04)

---

## ðŸŽ¯ Objetivo da Aula

Ao final desta aula, o aluno serÃ¡ capaz de:

1. Configurar o OpenClaw com **ChatGPT/OpenAI via OAuth** (recomendado â€” 1 clique, sem API key)
2. Configurar **OpenAI API Key** como fallback de controle fino
3. Entender quando usar **OpenRouter** para testar outros LLMs sem sair da stack principal
4. Configurar **Anthropic API Key** opcionalmente, apenas se quiser Claude de forma direta
5. Configurar as credenciais no OpenClaw via `openclaw auth login`
6. Verificar se a configuraÃ§Ã£o estÃ¡ funcionando com `openclaw status`
7. Diagnosticar e resolver os **erros mais comuns** de autenticaÃ§Ã£o

---

## ðŸ“‹ Script de GravaÃ§Ã£o â€” SeÃ§Ã£o por SeÃ§Ã£o

### ðŸŽ¬ ABERTURA (0:00 â€“ 2:00)

**[Bruno na tela, tom direto]**

> "Fala, pessoal! Aula N-1 do curso OpenClaw â€” configurar credenciais. Essa Ã© a aula onde a maioria das pessoas trava, e o objetivo aqui Ã© acabar com essa dÃºvida de vez."

> "Vou te mostrar o caminho mais simples: usar sua conta do ChatGPT que vocÃª jÃ¡ tem. Sim â€” se vocÃª jÃ¡ paga R$99/mÃªs de ChatGPT Plus, o OpenClaw pode usar essa mesma conta via OAuth. Um clique, sem API key, sem configurar billing separado."

> "TambÃ©m vou mostrar como configurar via API key direta, que Ã© Ãºtil pra quem quer mais controle. E, se vocÃª quiser experimentar outros LLMs depois, o caminho recomendado Ã© adicionar OpenRouter como camada de testes, sem mexer no fluxo principal do curso."

---

### ðŸ“š SEÃ‡ÃƒO 1: Os dois caminhos de autenticaÃ§Ã£o (2:00 â€“ 5:00)

**[Tela: diagrama comparativo]**

> "Existem dois caminhos pra conectar o OpenClaw na OpenAI:"

| Caminho | Como funciona | Melhor pra |
|---------|-------------|-----------|
| **OAuth (recomendado)** | 1 clique no navegador, usa sua assinatura existente | Quem jÃ¡ tem ChatGPT Plus/Pro |
| **API Key** | Gera chave na plataforma, cola no terminal | Quem quer controle fino de gasto, usa mÃºltiplos modelos |

> "O OAuth Ã© mais simples. A API Key Ã© mais flexÃ­vel. Os dois funcionam â€” escolhe o que faz mais sentido pra vocÃª."

---

### ðŸ” SEÃ‡ÃƒO 2: ChatGPT OAuth â€” O caminho recomendado (5:00 â€“ 10:00)

**[Tela: terminal + navegador lado a lado]**

> "Vamos pelo OAuth. Esse Ã© o caminho mais simples."

> "No terminal, digita:"

```bash
openclaw auth login --provider openai
```

> "O OpenClaw vai abrir o navegador automaticamente. Faz login com sua conta ChatGPT â€” pode ser Plus ou Pro. Autoriza o acesso."

> "Na tela que aparecer, confirma. O terminal vai mostrar algo como:"

```
âœ… OAuth completo
ðŸ“§ Conta: seu-email@exemplo.com
ðŸ”— Provider: openai (OpenAI)
ðŸ“Š Plano: ChatGPT Plus
â° Validade: ~30 dias (renova automaticamente)
```

> "Pronto. Sem chave pra copiar, sem billing pra configurar. VocÃª jÃ¡ tem tudo."

> "**Importante:** o OAuth usa a assinatura existente. Se vocÃª tem ChatGPT Plus, o OpenClaw vai usar o mesmo modelo que vocÃª tem acesso no chat. NÃ£o gasta nada adicional."

---

### ðŸ”‘ SEÃ‡ÃƒO 2.5: OpenAI API Key â€” O caminho flexÃ­vel (10:00 â€“ 14:00)

**[Tela: browser em platform.openai.com]**

> "Se vocÃª prefere API Key â€” seja por controle de gasto, seja porque quer usar modelos que nÃ£o estÃ£o no Plus â€” vamos configurar."

> "Acesse **platform.openai.com/api-keys** e clica em **'Create new secret key'**."

> "DÃ¡ um nome (ex: `openclaw`), copia a chave. ComeÃ§a com `sk-proj-` ou `sk-`. **Copia agora â€” nÃ£o aparece de novo.**"

> "Verifica se tem crÃ©dito em **Billing â†’ Usage**."

> "Volta pro terminal:"

```bash
openclaw config set provider openai
# O OpenClaw vai pedir a chave
```

> "Cole a chave. Pronto."

> "**Dica:** API Key dÃ¡ acesso a todos os modelos da OpenAI, incluindo os mais novos. Mas precisa gerenciar crÃ©ditos."

> "Se a sua meta Ã© testar Gemini, Claude, Llama e outras opÃ§Ãµes sem reescrever seu setup principal, o caminho recomendado Ã© ligar OpenRouter depois. Assim vocÃª mantÃ©m OpenAI como base do curso e usa OpenRouter sÃ³ para experimentaÃ§Ã£o."

---

### ðŸ”‘ SEÃ‡ÃƒO 3: Anthropic API Key â€” O caminho opcional (14:00 â€“ 17:00)

**[Tela: browser em console.anthropic.com]**

> "Se vocÃª quer comparar com Claude especificamente, a Anthropic continua opcional. A Anthropic **nÃ£o tem OAuth funcional** para a maioria dos planos â€” entÃ£o Ã© API Key direto. Para testar vÃ¡rios LLMs sem trocar a narrativa principal do curso, prefira OpenRouter; Anthropic direta faz sentido quando Claude for uma escolha consciente."

> "Acesse **console.anthropic.com** (nÃ£o claude.ai â€” Ã© outro sistema)."

> "Se vocÃª tem plano Pro ($20/mÃªs): atenÃ§Ã£o â€” assinatura Pro e API sÃ£o **sistemas de billing separados**. VocÃª pode ter Pro no chat e nÃ£o ter acesso Ã  API. Verifica em Settings â†’ Billing."

> "Se nÃ£o tiver billing, adiciona um cartÃ£o ou crÃ©ditos."

> "Clica em **API Keys â†’ Create Key**. Copia imediatamente."

> "No terminal:"

```bash
openclaw auth login --provider anthropic
# Escolhe "API Key" (nÃ£o OAuth â€” nÃ£o funciona pra maioria)
# Cole a chave
```

> "**Resumo rÃ¡pido:** ChatGPT OAuth = mais simples. Anthropic API Key = mais trabalho mas acesso ao Claude."

---

### âœ… SEÃ‡ÃƒO 4: Verificando tudo com `openclaw status` (17:00 â€“ 19:00)

**[Tela: Terminal]**

> "Pra confirmar que tÃ¡ tudo certo:"

```bash
openclaw status
```

> "SaÃ­da esperada:"

```
âœ… OpenClaw Status
â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
Provider: OpenAI (OAuth)     âœ… Connected
Provider: Anthropic (API Key) âœ… Connected
â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
All providers configured âœ“
```

> "Se aparecer Connected â€” perfeito! PrÃ³xima seÃ§Ã£o pra troubleshootings."

---

### ðŸ”§ SEÃ‡ÃƒO 5: Erros Comuns e Como Resolver (19:00 â€“ 22:00)

**[Tela: Slides com erros]**

**[Erro 1]**

> "**'OAuth access denied' ou 'Authorization failed'** â€” o login OAuth foi cancelado ou a conta nÃ£o tem permissÃ£o. Tenta de novo: `openclaw auth login --provider openai`. Verifica se aceitou todos os termos."

**[Erro 2]**

> "**'Invalid API Key'** â€” a chave tÃ¡ errada, expirou ou foi revogada. Vai no console do provider, cria uma nova."

**[Erro 3]**

> "**'HTTP 402 Payment Required'** â€” sem billing. Anthropic: console.anthropic.com â†’ Billing. OpenAI API: platform.openai.com â†’ Billing â†’ crÃ©ditos."

**[Erro 4]**

> "**'Insufficient credits'** â€” OpenAI API sem crÃ©ditos. Adiciona em platform.openai.com â†’ Billing."

**[Erro 5]**

> "**Rate limit (HTTP 429)** â€” limite temporÃ¡rio do provider. Espera 1-5 minutos. Considere modelos mais econÃ´micos (GPT-4o-mini) se acontecer muito."

**[Erro 6]**

> "**'model_not_available'** â€” modelo nÃ£o disponÃ­vel no seu plano. Tenta com `gpt-4o-mini` ou `gpt-4o`."

---

### ðŸŽ¯ ENCERRAMENTO (22:00 â€“ 23:00)

> "Resumo da aula: o caminho mais simples Ã© ChatGPT/OpenAI via OAuth â€” 1 clique, usa sua assinatura existente. OpenAI API Key entra quando vocÃª quer mais controle. Configuramos com `openclaw auth login`, verificamos com `openclaw status`."

> "Pra testar outros LLMs, o caminho recomendado do curso Ã© OpenRouter como camada de experimentaÃ§Ã£o. Anthropic direta continua opcional, nÃ£o o fallback principal."

> "PrÃ³xima aula: a gente comeÃ§a a usar de verdade!"

---

## ðŸ› ï¸ Passo a Passo TÃ©cnico Detalhado

### 1. ChatGPT OAuth (Recomendado)

```bash
# Passo 1: No terminal
openclaw auth login --provider openai

# Passo 2: O navegador abre â€” faz login no ChatGPT
# Aceita a autorizaÃ§Ã£o

# Passo 3: ConfirmaÃ§Ã£o no terminal
# âœ… OAuth completo
```

### 2. OpenAI API Key (Fallback)

1. Acesse [platform.openai.com/api-keys](https://platform.openai.com/api-keys)
2. Clique em **"Create new secret key"**
3. Nome: `openclaw`
4. **COPIE A CHAVE** â€” nÃ£o aparece de novo
5. Verifique crÃ©ditos em **Billing â†’ Usage**

```bash
openclaw config set provider openai
# Cole a chave quando solicitado
```

### 3. OpenRouter para testar outros LLMs (Recomendado para experimentaÃ§Ã£o)

1. Acesse [openrouter.ai](https://openrouter.ai)
2. Crie sua conta e gere uma API key
3. Use essa chave quando quiser testar outros modelos mantendo OpenAI como base do curso
4. Trate OpenRouter como camada de experimentaÃ§Ã£o, nÃ£o como substituiÃ§Ã£o obrigatÃ³ria do setup inicial

### 4. Anthropic API Key (Opcional)

1. Acesse [console.anthropic.com](https://console.anthropic.com)
2. Verifique billing em **Settings â†’ Billing**
3. **API Keys â†’ Create Key**
4. **COPIE A CHAVE** â€” nÃ£o aparece de novo
5. Configure no terminal:
```bash
openclaw auth login --provider anthropic
# Escolha API Key (nÃ£o OAuth)
# Cole a chave
```

### 4. Verificar

```bash
openclaw status
# SaÃ­da: All providers configured âœ…
```

### 5. Onde as Credenciais sÃ£o Armazenadas

| SO | Caminho |
|----|---------|
| Linux / macOS | `~/.openclaw/config.json` |
| Windows | `C:\Users\<SeuNome>\.openclaw\config.json` |

> ðŸ”’ **SeguranÃ§a:** Esse arquivo nunca vai pro git. **Nunca commite esse arquivo.**

---

## ðŸš¨ Tabela de Erros Comuns + SoluÃ§Ã£o

| Erro | Causa | SoluÃ§Ã£o |
|------|-------|---------|
| `OAuth access denied` | Login OAuth cancelado | `openclaw auth login --provider openai` de novo |
| `Invalid API Key` | Chave errada/expirada | Recriar chave no console do provider |
| `HTTP 402 Payment Required` | Sem billing ativo | Adicionar cartÃ£o/crÃ©ditos no provider |
| `Insufficient credits` | OpenAI sem crÃ©ditos | platform.openai.com â†’ Billing â†’ crÃ©ditos |
| `HTTP 429 Too Many Requests` | Rate limit temporÃ¡rio | Esperar 1-5 min. Considerar modelo menor |
| `model_not_available` | Modelo indisponÃ­vel no plano | Trocar para `gpt-4o-mini` |
| Chave funciona mas agente nÃ£o responde | `tools.profile = messaging` | `openclaw config set tools.profile full` |

---

## âœ… Checklist Final do Aluno

- [ ] ChatGPT OAuth configurado (`openclaw auth login --provider openai`) â€” **recomendado**
- [ ] (Opcional) OpenAI API Key configurada
- [ ] (Opcional) Anthropic API Key configurada
- [ ] `openclaw status` mostrando Connected
- [ ] Primeiros testes realizados com sucesso
- [ ] `~/.openclaw/config.json` nÃ£o estÃ¡ no git

---

## â“ DÃºvidas Frequentes

**1. Qual provider eu preciso configurar?**

> SÃ³ um Ã© suficiente. **ChatGPT/OpenAI via OAuth Ã© o mais simples** â€” usa sua assinatura existente. Se depois quiser testar outros modelos, adicione OpenRouter como etapa extra. Anthropic direta fica opcional.

**2. OAuth e API Key â€” qual a diferenÃ§a de custo?**

> OAuth usa sua assinatura existente (Plus R$99/mÃªs ou Pro). NÃ£o gasta mais. API Key cobra por uso real (~$5-15/mÃªs com uso moderado).

**3. Posso usar os dois (ChatGPT + Claude)?**

> Sim! Configure os dois providers. O OpenClaw pode usar os dois. VocÃª escolhe qual usar por padrÃ£o.

**4. Minha assinatura Pro da Anthropic funciona pro OAuth do OpenClaw?**

> NÃ£o. A Anthropic bloqueou OAuth para planos Pro. O que funciona Ã© API Key direta. Por isso o ChatGPT/OpenAI OAuth continua sendo o caminho mais simples, e OpenRouter vira a opÃ§Ã£o mais prÃ¡tica para experimentaÃ§Ã£o multi-modelo.

**5. Como trocar o provider padrÃ£o depois?**

> `openclaw config set model openai/gpt-5.4` (padrÃ£o do curso), ou troque temporariamente por outro modelo sÃ³ quando estiver testando via OpenRouter ou Anthropic opcional.

**6. O OpenClaw almacena minhas chaves na nuvem?**

> NÃ£o. Chaves ficam em `~/.openclaw/config.json` â€” localmente. O OpenClaw nÃ£o envia credenciais pra servidores externos.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
