# â“ Q&A â€” Comparativo de LLMs (Claude, ChatGPT e outros)

> Guia de referÃªncia: qual modelo usar, quanto custa, o que recomendamos.

---

## Qual modelo devo usar no OpenClaw?

**Nossa recomendaÃ§Ã£o geral:**

| SituaÃ§Ã£o | Modelo recomendado | Por quÃª |
|---|---|---|
| Conversa do dia a dia | Claude Sonnet ou GPT-4o | Ã“timo equilÃ­brio qualidade/custo |
| Tarefas automÃ¡ticas (crons, lembretes) | Claude Haiku ou GPT-4o mini | Muito barato, rÃ¡pido o suficiente |
| AnÃ¡lises complexas, decisÃµes importantes | Claude Opus | MÃ¡xima qualidade, use com moderaÃ§Ã£o |
| Quando Claude estÃ¡ bloqueado | GPT-4o | Excelente alternativa |

---

## Comparativo de PreÃ§os e Planos

### Claude (Anthropic)

| Plano | PreÃ§o aprox. | O que inclui |
|---|---|---|
| Claude.ai Free | GrÃ¡tis | Uso limitado no chat (nÃ£o serve pro OpenClaw) |
| Claude.ai Pro | ~R$ 100/mÃªs | Uso no chat â€” **nÃ£o conecta diretamente ao OpenClaw** |
| Claude.ai Max | ~R$ 550/mÃªs | Uso intenso no chat â€” **nÃ£o conecta diretamente ao OpenClaw** |
| **API Anthropic** | Pay-per-use | âœ… **O que funciona no OpenClaw** |

**Custo real da API (estimativa mensal com uso moderado):**
- Haiku (automaÃ§Ãµes): ~R$ 2â€“10/mÃªs
- Sonnet (uso diÃ¡rio): ~R$ 20â€“80/mÃªs
- Opus (uso intenso): ~R$ 100â€“300/mÃªs

> âš ï¸ **AtenÃ§Ã£o sobre bloqueios:** A Anthropic estÃ¡ bloqueando algumas contas novas no momento. NÃ£o temos controle sobre isso. Se a sua conta foi bloqueada, use o ChatGPT como alternativa â€” o curso ensina os dois jeitos e ambos funcionam muito bem.

---

### ChatGPT / OpenAI

| Plano | PreÃ§o aprox. | O que inclui |
|---|---|---|
| ChatGPT Free | GrÃ¡tis | Uso limitado no chat (nÃ£o serve pro OpenClaw) |
| ChatGPT Plus | ~R$ 100/mÃªs | GPT-4o no chat â€” **nÃ£o conecta diretamente ao OpenClaw** |
| ChatGPT Pro | ~R$ 1.000/mÃªs | Uso intenso + o1 pro â€” **nÃ£o conecta diretamente ao OpenClaw** |
| **API OpenAI** | Pay-per-use | âœ… **O que funciona no OpenClaw** |

**Custo real da API (estimativa mensal com uso moderado):**
- GPT-4o mini (automaÃ§Ãµes): ~R$ 2â€“8/mÃªs
- GPT-4o (uso diÃ¡rio): ~R$ 15â€“60/mÃªs
- o1 (anÃ¡lises complexas): ~R$ 80â€“250/mÃªs

---

## Qual a diferenÃ§a entre assinar o Claude.ai e usar a API?

**Analogia simples:**

- **Assinar o Claude.ai/ChatGPT** = Comer num restaurante. VocÃª usa o cardÃ¡pio deles, no ambiente deles.
- **Usar a API** = Comprar os ingredientes e cozinhar em casa. VocÃª integra onde quiser.

O OpenClaw Ã© como a sua cozinha â€” ele precisa dos **ingredientes** (API), nÃ£o do restaurante pronto.

---

## Posso usar outros modelos alÃ©m de Claude e ChatGPT?

Sim! O OpenClaw suporta vÃ¡rios provedores:

| Modelo | Provedor | Destaque |
|---|---|---|
| Gemini | Google | Bom pra contextos muito longos |
| Mistral | Mistral AI | OpÃ§Ã£o europeia, boa privacidade |
| Llama (local) | Ollama | **GrÃ¡tis**, roda na sua mÃ¡quina |
| Deepseek | Deepseek | Muito barato, boa qualidade |

**Para descobrir o que estÃ¡ disponÃ­vel:**
Cole esse prompt no seu bot:

```
Quais modelos de IA o OpenClaw suporta atualmente?
Me recomenda qual seria o melhor pro meu uso com base no que vocÃª sabe sobre mim.
Considera tanto qualidade quanto custo.
```

---

## Como trocar o modelo que meu bot usa?

Cole esse prompt no seu bot:

```
Quero trocar o modelo que vocÃª usa para [MODELO QUE QUER].
Me guia:
1. Como pego a API key do novo provedor?
2. Como atualizo a configuraÃ§Ã£o?
3. Como testo se ficou funcionando?
Explica passo a passo sem usar comandos de terminal difÃ­ceis.
```

---

*Ãšltima atualizaÃ§Ã£o: Fev/2026 â€” PreÃ§os aproximados, consulte sempre o site oficial dos provedores.*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
