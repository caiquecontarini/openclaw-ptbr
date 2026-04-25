# ðŸ‘¥ Use Case: AnÃ¡lise de Comunidade

> Entenda o que sua comunidade estÃ¡ falando, pedindo e sentindo.

## O que faz

Conecta na API da sua comunidade (Circle, Discord, Slack) e analisa:
- Hot topics (o que estÃ¡ gerando mais discussÃ£o)
- Perguntas frequentes (FAQ natural da comunidade)
- Membros mais ativos e influentes
- Spam e posts duplicados
- Trends emergentes
- Sentimento geral

## Prompt

```
Quero uma anÃ¡lise completa da minha comunidade nos Ãºltimos [30/60] dias.

Minha comunidade Ã© [CIRCLE/DISCORD/SLACK] com [NÃšMERO] membros.

Me entregue:

1. **Hot Topics** â€” os 10 assuntos mais discutidos, com volume de posts
2. **Perguntas Frequentes** â€” as 10 perguntas que mais aparecem (base pra FAQ/conteÃºdo)
3. **Membros destaque** â€” top 10 mais ativos e top 10 que mais ajudam outros
4. **Spam check** â€” posts duplicados, cross-posting excessivo, padrÃµes suspeitos
5. **Trends** â€” assuntos que estÃ£o CRESCENDO (nÃ£o os maiores, os que estÃ£o acelerando)
6. **Sentimento** â€” como estÃ¡ o clima? Positivo? Frustrado? Qual a vibe?
7. **Oportunidades** â€” ideias de conteÃºdo, features, ou aÃ§Ãµes baseadas nos dados

Formato: report com insights acionÃ¡veis, nÃ£o sÃ³ nÃºmeros.

Dica: cruze os dados da comunidade com os tickets de suporte pra ver padrÃµes completos.
```

## Exemplo real

A Amora analisou 345 posts da comunidade Micro-SaaS (20k membros):
- Spam puro: nÃ£o encontrado
- PadrÃµes de atenÃ§Ã£o: cross-posting e repetiÃ§Ã£o
- "150 MVPs em 60 dias" â€” dado que virou post LinkedIn viral
- Cruzamento com Crisp revelou: vibe coding domina em ambos


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
