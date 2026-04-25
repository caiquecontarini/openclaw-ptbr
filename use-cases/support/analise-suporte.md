# ðŸŽ§ Use Case: AnÃ¡lise Inteligente de Suporte

> Identifique padrÃµes, bugs recorrentes e oportunidades nos tickets.

## O que faz

Conecta na sua ferramenta de suporte (Crisp, Intercom, Zendesk) e analisa:
- PadrÃµes nos tickets (quais problemas mais aparecem)
- Sentimento dos clientes (satisfaÃ§Ã£o, frustraÃ§Ã£o)
- Tempo de resposta e resoluÃ§Ã£o
- SugestÃµes de features baseadas em reclamaÃ§Ãµes
- Oportunidades de conteÃºdo (FAQ que vira post)

## Prompt

```
Quero que vocÃª analise meus tickets de suporte dos Ãºltimos [30/60/90] dias.

Minha ferramenta de suporte Ã© [CRISP/INTERCOM/ZENDESK].

Me entregue:
1. **Top 10 problemas mais reportados** â€” agrupados por categoria
2. **AnÃ¡lise de sentimento** â€” % de tickets positivos/neutros/negativos
3. **Bugs recorrentes** â€” issues que aparecem mais de 3x
4. **SugestÃµes de features** â€” o que os clientes estÃ£o pedindo
5. **Oportunidades de conteÃºdo** â€” perguntas frequentes que viram tutorial/post
6. **PadrÃµes de horÃ¡rio** â€” quando os tickets chegam (picos)
7. **Tempo mÃ©dio de resoluÃ§Ã£o** â€” e onde estÃ¡ lento

Formato: report estruturado com aÃ§Ãµes concretas pra cada insight.

Insight da Amora: "Crisp Ã© canal de vendas, nÃ£o sÃ³ suporte. Analise as perguntas prÃ©-venda tambÃ©m."
```

## Exemplo real

A Amora analisou 187 conversas do Crisp:
- 95% via WhatsApp
- "Vibe coding" dominava (172 menÃ§Ãµes)
- Pessoas travam na "Ãºltima milha" (deploy, config, go-live)
- Gerou 6 ideias de conteÃºdo direto dos tickets


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
