# ðŸ’° Custos â€” Breakdown Real de Rodar um Agente AI

> Quanto custa na prÃ¡tica, com otimizaÃ§Ãµes aplicadas.

---

## Infraestrutura

| Item | Custo/mÃªs | Notas |
|------|-----------|-------|
| VPS Hostinger KVM 1 | ~R$25-50 | 2 vCPU, 4GB RAM, Ubuntu 24.04 |
| VPS Hostinger KVM 2 | ~R$39-60 | 2 vCPU, 8GB RAM (recomendado pra multi-agent) |
| DomÃ­nio (opcional) | ~R$5-10 | Pra Mission Control |
| Cloudflare Tunnel | GrÃ¡tis | Acesso remoto seguro |
| **Subtotal infra** | **R$25-60** | |

## API do Modelo (Anthropic)

### Sem otimizaÃ§Ã£o (tudo Opus)
| Uso | Custo/dia | Custo/mÃªs |
|-----|-----------|-----------|
| InteraÃ§Ã£o diÃ¡ria | ~$2-3 | ~$70-90 |
| 17 crons | ~$1-2 | ~$30-60 |
| Heartbeats | ~$0.50 | ~$15 |
| **Total** | **~$3-5** | **~$100-150** |

### Com otimizaÃ§Ã£o (split inteligente) âœ…
| Uso | Modelo | Custo/dia | Custo/mÃªs |
|-----|--------|-----------|-----------|
| InteraÃ§Ã£o (chat) | Opus | ~$0.50-1.00 | ~$15-30 |
| Crons execuÃ§Ã£o | Sonnet | ~$0.10-0.20 | ~$3-6 |
| Heartbeats | Haiku | ~$0.01-0.02 | ~$0.30-0.60 |
| Heartbeats | Ollama local | $0 | $0 |
| **Total otimizado** | | **~$0.60-1.20** | **~$18-36** |

### Economia
| MÃ©trica | Antes | Depois |
|---------|-------|--------|
| Custo diÃ¡rio | $3-5 | $0.60-1.20 |
| Custo mensal | $100-150 | $18-36 |
| **Economia** | | **~75-80%** |

### Dica: Assinatura Anthropic
- Plano Pro ($20/mÃªs) inclui uso generoso do Claude
- Se usar via assinatura em vez de API, custo cai drasticamente
- Bruno usa assinatura e nunca estourou o limite

## APIs e Ferramentas Externas

| Ferramenta | Custo/mÃªs | Pra quÃª |
|------------|-----------|---------|
| 1Password | GrÃ¡tis (pessoal) ou $3 | Gerenciar credenciais |
| RapidAPI | GrÃ¡tis (free tier) | Proxy pra YouTube, Instagram, X |
| Apify | GrÃ¡tis ($5 crÃ©dito/mÃªs) | YouTube transcripts (~714 vÃ­deos) |
| Brave Search API | GrÃ¡tis (2k buscas/mÃªs) | Web search |
| Google APIs | GrÃ¡tis | Calendar, Drive, YouTube Data |
| OpenAI (Whisper) | ~$1-3 | TranscriÃ§Ã£o de Ã¡udio |
| **Subtotal APIs** | **$0-10** | Maioria tem free tier |

## Custo Total Estimado

### Iniciante (1 agente, uso moderado)
| Item | Custo/mÃªs |
|------|-----------|
| VPS KVM 1 | R$25-50 |
| API Anthropic (otimizado) | R$90-180 (~$18-36) |
| APIs externas | R$0-25 |
| **Total** | **R$115-255/mÃªs** |
| **Por dia** | **~R$4-8** |

> "Menos que um cafÃ© por dia pra ter um assistente AI 24/7"

### AvanÃ§ado (6 agentes, 22 crons, stack completo)
| Item | Custo/mÃªs |
|------|-----------|
| VPS KVM 2 | R$39-60 |
| API Anthropic (otimizado) | R$180-360 (~$36-72) |
| APIs externas | R$25-50 |
| Supabase (MC) | GrÃ¡tis (free tier) |
| **Total** | **R$244-470/mÃªs** |
| **Por dia** | **~R$8-16** |

> "O equivalente a 1/10 de um funcionÃ¡rio CLT, trabalhando 24/7"

## Comparativo com Alternativas

| SoluÃ§Ã£o | Custo/mÃªs | Disponibilidade | PersonalizaÃ§Ã£o |
|---------|-----------|-----------------|----------------|
| **OpenClaw otimizado** | R$115-255 | 24/7 | Total |
| Assistente freelancer | R$2.000-5.000 | HorÃ¡rio comercial | MÃ©dia |
| FuncionÃ¡rio CLT | R$3.000-8.000 | HorÃ¡rio comercial | Alta |
| ChatGPT Pro | R$100 | Sob demanda | Baixa |
| N8N + Zapier | R$200-500 | 24/7 (limitado) | MÃ©dia |

## Dicas de Economia

1. **Sonnet pra crons** â€” 90% de economia vs Opus
2. **Haiku pra heartbeats** â€” ou Ollama local (grÃ¡tis)
3. **Session initialization** â€” 8KB vs 50KB = 80% menos tokens
4. **Rate limits** â€” previne runaway de automaÃ§Ãµes
5. **Free tiers** â€” RapidAPI, Apify, Brave, Google APIs sÃ£o generosos
6. **Assinatura vs API** â€” assinatura Anthropic pode ser mais barato pra uso pessoal

---

*Valores baseados em produÃ§Ã£o real â€” Fev/2026*
*CÃ¢mbio aproximado: $1 = R$5*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
