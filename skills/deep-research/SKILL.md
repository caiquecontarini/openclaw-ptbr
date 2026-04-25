---
name: deep-research-protocol
description: >
  Protocolo estruturado de pesquisa profunda com mÃºltiplas fontes, sÃ­ntese e relatÃ³rio
  acionÃ¡vel. Use quando o Bruno pedir pesquisa detalhada, anÃ¡lise de mercado, investigaÃ§Ã£o
  de tema ou benchmarking. Acionar quando: "pesquisa sobre", "deep research", "investiga",
  "analisa o mercado de", "benchmark", "quero entender melhor", "pesquisa profunda",
  "me dÃ¡ um overview de", "anÃ¡lise de concorrentes". Para pesquisas complexas (>30min),
  spawnar como sub-agent.
metadata:
  author: amora-cos
  version: 1.0.0
  domain: shared
  owner: main
---

# Deep Research Protocol â€” Skill de Pesquisa Profunda

## O que Ã©

Protocolo estruturado para pesquisa profunda. Combina mÃºltiplas fontes, sintetiza findings, e entrega relatÃ³rio acionÃ¡vel.

## Protocolo de Pesquisa

### 1. Enquadramento (2 min)
- Qual a pergunta exata?
- Qual decisÃ£o essa pesquisa vai informar?
- Qual nÃ­vel de profundidade? (Quick scan vs Deep dive)

### 2. Coleta Multi-fonte

**Fontes primÃ¡rias (usar nesta ordem):**
1. `web_search` â€” busca geral (Brave)
2. `web_fetch` â€” extrair conteÃºdo de URLs relevantes
3. **Perplexity** â€” busca com AI-powered answers e citaÃ§Ãµes (API key no 1Password: "Perplexity API")
   ```bash
   PERPLEXITY_API_KEY=$(op item get "Perplexity API" --vault "Meu Vault" --field credential --reveal)
   node /root/.openclaw/workspace/skills/perplexity/scripts/search.mjs "query"
   ```
4. Knowledge Base â€” se tiver conteÃºdo relevante jÃ¡ ingestado

**Fontes especializadas:**
- Reddit/HackerNews â€” opiniÃ£o de comunidade tÃ©cnica
- Twitter/X â€” sinais em tempo real
- YouTube â€” anÃ¡lises longas e tutoriais
- GitHub â€” repos e projetos open source

### 3. SÃ­ntese

Para cada fonte:
- **Fato** â€” o que Ã© confirmÃ¡vel
- **OpiniÃ£o** â€” o que Ã© interpretaÃ§Ã£o
- **Sinal** â€” o que sugere tendÃªncia

### 4. RelatÃ³rio

**Formato padrÃ£o:**

```markdown
# [Tema] â€” Deep Research
Data: DD/MM/YYYY

## TL;DR (3-5 bullets)

## Contexto
[Por que estamos pesquisando isso]

## Findings
### [Subtema 1]
- Finding + fonte
### [Subtema 2]
- Finding + fonte

## AnÃ¡lise
[Cruzamento dos findings, padrÃµes identificados]

## RecomendaÃ§Ã£o
[O que fazer com essa informaÃ§Ã£o]

## Fontes
[Lista de URLs consultadas]
```

### 5. Salvamento
- Salvar em `memory/research-YYYY-MM-DD-[slug].md`
- Se relevante pra Knowledge Base â†’ ingestar

## NÃ­veis de Profundidade

| NÃ­vel | Tempo | Fontes | Output |
|-------|-------|--------|--------|
| Quick scan | 5-10 min | 3-5 URLs | 1 parÃ¡grafo + bullets |
| Standard | 15-30 min | 8-12 URLs | RelatÃ³rio 1-2 pÃ¡ginas |
| Deep dive | 30-60 min | 15-20+ URLs | RelatÃ³rio 3-5 pÃ¡ginas |

## Quando spawnar sub-agent

Se a pesquisa Ã© deep dive (>30min) ou Bruno quer continuar trabalhando enquanto pesquisa roda:
- Spawnar via `sessions_spawn` com task detalhada
- Sub-agent entrega relatÃ³rio quando pronto
- Amora review e envia pro Bruno

## Vieses a evitar

- Confirmation bias â€” buscar contra-argumentos ativamente
- Recency bias â€” verificar se tendÃªncias sÃ£o reais ou hype
- Survivorship bias â€” buscar casos de fracasso, nÃ£o sÃ³ sucesso
- Authority bias â€” expert disse â‰  Ã© verdade


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
