# Roteiro de GravaÃ§Ã£o â€” "MemÃ³ria 2.0"
**Aula nova separada | ~20 min | AtualizaÃ§Ã£o MarÃ§o 2026**

---

## Setup antes de gravar

- Abrir terminal com workspace limpo (sessÃ£o nova)
- Ter aberto: VS Code com `memory/` visÃ­vel, terminal lateral
- Deixar `memory/sessions/` com 2â€“3 arquivos visÃ­veis (para mostrar o diÃ¡rio)
- Desativar notificaÃ§Ãµes

---

## BLOCO 1 â€” Abertura (1:30 min)

**[CÃ‚MERA FRONTAL]**

> "Galera, memÃ³ria 2.0. Se vocÃª assistiu a aula de fundaÃ§Ã£o, lembra que a gente configurou o sistema de memÃ³ria, os arquivos decisions, lessons, pendingâ€¦ e na hora de testar o memory search, travou pedindo chave de API do OpenAI.
>
> Duas coisas aconteceram desde entÃ£o. Primeiro: esse bug foi corrigido. O memory search agora funciona nativamente, sem precisar de nenhuma chave externa. Segundo: eu aprendi â€” usando o meu prÃ³prio agente todo dia â€” que a estrutura de pastas que a gente criou na primeira aula funciona, mas tem uns ajustes que fazem diferenÃ§a enorme.
>
> Essa aula cobre os dois. Ã‰ curta. Uns 20 minutos. E vocÃª vai sair com o sistema de memÃ³ria do seu agente rodando de verdade."

---

## BLOCO 2 â€” O que o agente carrega vs. busca (4 min)

**[CÃ‚MERA FRONTAL â†’ COMPARTILHA TELA: terminal]**

> "Antes de qualquer coisa, preciso deixar isso muito claro, porque muda como vocÃª pensa na estrutura:"

**[MOSTRAR NA TELA: digitar `/status` no agente e mostrar output]**

> "Toda sessÃ£o nova, o agente carrega automaticamente 5 coisas:
> SOUL.md, USER.md, AGENTS.md, MEMORY.md â€” e as notas de hoje e ontem.
>
> SÃ³ isso. Mais nada.
>
> Tudo o mais â€” decisions, lessons, projetos, integraÃ§Ãµes â€” fica FORA do contexto. O agente vai buscar quando precisar. Isso Ã© a busca semÃ¢ntica, e jÃ¡ vou mostrar como funciona."

**[MOSTRAR: estrutura de pastas no VS Code]**

> "O MEMORY.md â€” o Ã­ndice â€” Ã© o Ãºnico arquivo que estÃ¡ sempre presente. E ele nÃ£o guarda conteÃºdo. Ele aponta onde o conteÃºdo estÃ¡. Olha aqui o meu:"

**[MOSTRAR: MEMORY.md aberto â€” seÃ§Ãµes com links para os arquivos de memÃ³ria]**

> "Ã‰ um mapa. NÃ£o Ã© o territÃ³rio."

---

## BLOCO 3 â€” Estrutura de subpastas (4 min)

**[COMPARTILHA TELA: VS Code, Ã¡rvore de pastas memory/]**

> "Na aula de fundaÃ§Ã£o a gente criou tudo na raiz da pasta memory. Decisions.md, lessons.md, pending.md, tudo junto. Funciona â€” mas quando o volume cresce, a busca semÃ¢ntica comeÃ§a a trazer contexto misturado.
>
> O que eu uso hoje:"

**[MOSTRAR: tree da pasta memory/ no terminal]**

```
memory/
â”œâ”€â”€ context/
â”‚   â”œâ”€â”€ decisions.md
â”‚   â”œâ”€â”€ lessons.md
â”‚   â”œâ”€â”€ people.md
â”‚   â””â”€â”€ business-context.md
â”œâ”€â”€ projects/
â”‚   â”œâ”€â”€ metricaas.md
â”‚   â”œâ”€â”€ comunidade-ai.md
â”‚   â””â”€â”€ mission-control-apis.md
â”œâ”€â”€ content/
â”‚   â”œâ”€â”€ voice/linkedin.md
â”‚   â””â”€â”€ voice/youtube.md
â”œâ”€â”€ integrations/
â”‚   â”œâ”€â”€ telegram-map.md
â”‚   â””â”€â”€ credentials-map.md
â””â”€â”€ sessions/
    â”œâ”€â”€ 2026-03-14.md
    â””â”€â”€ 2026-03-12-mission-control.md
```

> "Subpastas por categoria. A lÃ³gica Ã© simples: quando eu pergunto 'qual o status do Metricaas?', o agente busca em projects/ e encontra exatamente o arquivo certo. Se tivesse tudo num projects.md gigante, ele traria contexto do MGM, da Comunidade IA, de tudo junto.
>
> Projetos separados por arquivo. Isso Ã© a mudanÃ§a mais importante."

**[MOSTRAR: abrir metricaas.md â€” conteÃºdo real do arquivo]**

> "Cada projeto tem: status atual, prÃ³ximas aÃ§Ãµes, pendÃªncias. O agente atualiza quando vocÃª pede. Na prÃ³xima sessÃ£o, ele encontra tudo aqui."

---

## BLOCO 4 â€” Como a busca semÃ¢ntica funciona (4 min)

**[CÃ‚MERA FRONTAL â†’ COMPARTILHA TELA: terminal com agente]**

> "Agora o que mudou de verdade. Na aula antiga, o memory search exigia chave de API do OpenAI pra funcionar. Isso gerou muita confusÃ£o. Aluno configurava tudo certo, chegava nessa parte, travava.
>
> NÃ£o precisa mais. Funciona nativamente."

**[DEMO AO VIVO: abrir sessÃ£o nova no terminal]**

> "Deixa eu mostrar. SessÃ£o nova â€” contexto zerado. Nenhum arquivo de projeto carregado."

**[DIGITAR: "qual o status atual do Metricaas?"]**

> "O agente vai buscar nos arquivos... olha aqui â€” ele usou o memory_search, encontrou o arquivo projects/metricaas.md, e trouxe exatamente o trecho relevante. Sem eu ter aberto nada manualmente."

**[MOSTRAR O OUTPUT â€” agente encontrando a info]**

> "Isso Ã© busca semÃ¢ntica. NÃ£o Ã© grep, nÃ£o Ã© palavra-chave exata. Ele entende o significado. Se eu perguntar 'como estÃ¡ meu SaaS de mÃ©tricas', ele vai achar o mesmo arquivo.
>
> Dois tools por baixo dos panos:
> - `memory_search` â€” busca em tudo, traz os chunks mais relevantes
> - `memory_get` â€” lÃª sÃ³ as linhas especÃ­ficas que precisa
>
> VocÃª nÃ£o precisa chamar esses tools manualmente. O agente usa automaticamente quando vocÃª pergunta algo."

---

## BLOCO 5 â€” Como pedir para salvar (3 min)

**[CÃ‚MERA FRONTAL]**

> "Maior erro de quem comeÃ§a: achar que o agente vai lembrar sozinho.
>
> NÃ£o vai. Se nÃ£o estÃ¡ em arquivo, nÃ£o existe na prÃ³xima sessÃ£o.
>
> A diferenÃ§a:"

**[MOSTRAR NA TELA â€” slide simples ou digitar no terminal]**

> "âŒ 'Lembra disso' â†’ morre quando vocÃª fechar a janela
> âœ… 'Salva em memory/context/decisions.md' â†’ permanente"

**[DEMO AO VIVO: digitar uma decisÃ£o e pedir pra salvar]**

> "Vou tomar uma decisÃ£o agora: todas as integraÃ§Ãµes novas precisam ter documentaÃ§Ã£o antes de ir pra produÃ§Ã£o. Vou pedir pra salvar:"

**[DIGITAR: "Ficou decidido: toda integraÃ§Ã£o nova precisa ter documentaÃ§Ã£o antes de ir pra produÃ§Ã£o. Salva em memory/context/decisions.md como decisÃ£o permanente."]**

**[MOSTRAR: agente abrindo o arquivo e salvando]**

> "Feito. SessÃ£o nova, esse contexto vai estar lÃ¡.
>
> CritÃ©rio rÃ¡pido de onde salvar:
> - DecisÃ£o que nÃ£o muda â†’ context/decisions.md
> - Erro que nÃ£o pode repetir â†’ context/lessons.md
> - Status de projeto â†’ projects/nome.md
> - Aguardando seu input â†’ pending.md"

---

## BLOCO 6 â€” Encerramento (1:30 min)

**[CÃ‚MERA FRONTAL]**

> "Recapitulando o que mudou:
>
> Um â€” busca semÃ¢ntica funciona nativamente, sem chave de API.
>
> Dois â€” subpastas por categoria. Projects com um arquivo por projeto. Context separado de integrations separado de sessions.
>
> TrÃªs â€” o agente sÃ³ carrega automaticamente SOUL, USER, AGENTS, MEMORY e as sessÃµes de hoje e ontem. Todo o resto Ã© sob demanda.
>
> Quatro â€” para salvar, vocÃª precisa ser explÃ­cito. 'Salva em memory/context/decisions.md'. Sem isso, nÃ£o existe.
>
> O material desta aula tÃ¡ no Drive â€” tem o guia em PDF com a estrutura completa, o prompt pra vocÃª pedir pro agente reorganizar a memÃ³ria, e o PRD atualizado. Linka na descriÃ§Ã£o.
>
> Qualquer dÃºvida, manda no grupo. AtÃ© a prÃ³xima."

---

## Checklist prÃ©-gravaÃ§Ã£o

- [ ] SessÃ£o nova aberta no terminal (contexto zerado)
- [ ] VS Code com `memory/` visÃ­vel e arquivos reais (metricaas.md, decisions.md)
- [ ] MEMORY.md aberto em outra aba
- [ ] NotificaÃ§Ãµes desativadas
- [ ] Testou a demo do memory_search antes de gravar

## Timings aproximados

| Bloco | ConteÃºdo | Tempo |
|-------|----------|-------|
| 1 | Abertura | 1:30 |
| 2 | Carrega vs. busca | 4:00 |
| 3 | Estrutura de subpastas | 4:00 |
| 4 | Busca semÃ¢ntica (demo) | 4:00 |
| 5 | Como salvar (demo) | 3:00 |
| 6 | Encerramento | 1:30 |
| **Total** | | **~18 min** |

## Links para colocar na descriÃ§Ã£o

- Material do aluno (PDF): Drive â†’ Curso OpenClaw â†’ aula-04-memoria â†’ modulo-04-memoria.pdf
- Prompt de implementaÃ§Ã£o: Drive â†’ aula-04-memoria â†’ prompts â†’ modulo-04-memoria.md
- PRD atualizado: Drive â†’ aula-04-memoria â†’ prd â†’ memory-architecture.md


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
