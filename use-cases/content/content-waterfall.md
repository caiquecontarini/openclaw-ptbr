# ðŸŽ¬ Use Case: Content Waterfall

> Um vÃ­deo vira 10+ peÃ§as de conteÃºdo em mÃºltiplas plataformas.

## O que faz

Pega um vÃ­deo gravado (YouTube, Tella, Loom) e automaticamente gera:
- Post LinkedIn (formato longo, storytelling)
- Thread X/Twitter (5-8 tweets)
- Carrossel Instagram (slides com design)
- Newsletter (formato editorial)
- Reels/Shorts (roteiro de 60s)
- Tweets avulsos (insights isolados)

## Como a Amora faz isso

1. Transcreve o vÃ­deo (Whisper API ou Apify)
2. Extrai os insights principais
3. Adapta pra cada plataforma (tom, formato, limitaÃ§Ãµes)
4. Gera todas as peÃ§as
5. Agenda publicaÃ§Ã£o (Late API ou manual)

## Prompt

```
Acabei de gravar um vÃ­deo sobre [TEMA]. Aqui estÃ¡ a transcriÃ§Ã£o:

[COLE A TRANSCRIÃ‡ÃƒO OU LINK DO VÃDEO]

Quero que vocÃª aplique o Content Waterfall:

1. Extraia os 5-7 insights principais do vÃ­deo
2. Gere as seguintes peÃ§as de conteÃºdo:
   - 1 post LinkedIn (formato storytelling, 1200-1500 caracteres, gancho forte na primeira linha)
   - 1 thread X/Twitter (5-8 tweets, primeiro tweet Ã© o gancho)
   - 1 roteiro de Reel/Short (60 segundos, formato: hook + conteÃºdo + CTA)
   - 1 bloco de newsletter (formato editorial, 300-500 palavras)
   - 3 tweets avulsos (insights isolados, cada um independente)

Regras:
- Use MEU tom de voz (consulte USER.md)
- Cada plataforma tem formato diferente â€” adapte
- LinkedIn: profissional mas humano, sem hashtags excessivas
- Twitter: direto, provocativo, opiniÃ£o forte
- Reel: visual, dinÃ¢mico, gancho nos primeiros 3 segundos
- Newsletter: mais profundo, contexto, bastidores

Me mostre todas as peÃ§as e pergunte se quer ajustar algo antes de finalizar.
```

## Resultado esperado

De 1 vÃ­deo de 20 minutos â†’ 7+ peÃ§as prontas pra publicar em ~10 minutos.

## Dica

Configure um cron pra rodar o waterfall automaticamente toda vez que um novo vÃ­deo Ã© detectado no Tella/YouTube.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
