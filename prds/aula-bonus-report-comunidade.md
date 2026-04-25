# PRD â€” Aula BÃ´nus: Report de Comunidade com IA

> **NÃ­vel:** IntermediÃ¡rio
> **DuraÃ§Ã£o estimada:** 15â€“18 minutos
> **PrÃ©-requisito:** OpenClaw instalado, pelo menos um grupo conectado ao MyGroupMetrics (ou qualquer fonte de dados de mensagens)

---

## ðŸŽ¯ Objetivo da Aula

Ao final desta aula, o aluno vai entender que o OpenClaw pode:

1. Conectar em qualquer banco de dados com mensagens (Supabase, API REST)
2. Analisar automaticamente o humor, as dÃºvidas e os padrÃµes da comunidade
3. Gerar um relatÃ³rio visual completo â€” HTML + PDF â€” sem escrever uma linha de cÃ³digo manualmente
4. Entregar esse relatÃ³rio todo na sua caixa de entrada, toda semana, sem interaÃ§Ã£o

**Ã‚ngulo da aula:** O resultado primeiro. O cÃ³digo Ã© sÃ³ a prova de que Ã© simples.

---

## ðŸ“‹ Script de GravaÃ§Ã£o â€” SeÃ§Ã£o por SeÃ§Ã£o

---

### ðŸŽ¬ ABERTURA (0:00 â€“ 1:30)

**[Bruno na tela com o PDF do report aberto ao lado]**

> "Fala, pessoal. Olha esse PDF aqui."

> "Esse relatÃ³rio chegou pra mim ontem, de manhÃ£, sem eu pedir nada. Ele me mostra: humor da comunidade essa semana, quais dÃºvidas mais repetiram, que horas o grupo mais ativa, quem sÃ£o os alunos que mais ajudam os outros."

> "14.725 mensagens analisadas. Quatro grupos de WhatsApp. Quatro semanas de dados. E eu nÃ£o fiz absolutamente nada."

> "Nessa aula eu vou te mostrar como eu fiz isso â€” e mais importante: como vocÃª vai fazer igual para a sua comunidade."

---

### ðŸ“Š SEÃ‡ÃƒO 1: O problema que isso resolve (1:30 â€“ 4:00)

**[Bruno na cÃ¢mera, tom de conversa]**

> "Deixa eu te fazer uma pergunta rÃ¡pida."

> "VocÃª tem grupo de WhatsApp de alunos, clientes, comunidade? Quantas mensagens por semana? 200? 500? 2.000?"

> "Agora me diz: vocÃª consegue responder essas perguntas sem abrir o grupo agora?"

**[Mostrar na tela â€” slide com as 4 perguntas]**

> "Qual foi o humor da comunidade essa semana â€” as pessoas estÃ£o animadas ou frustradas?"
> "Qual dÃºvida apareceu mais de trÃªs vezes nos Ãºltimos 7 dias?"
> "Que horas do dia o grupo mais engaja â€” quando eu devo fixar comunicados?"
> "Quem sÃ£o os membros que mais ajudam os outros â€” meus potenciais moderadores?"

> "A maioria dos criadores nÃ£o consegue responder nenhuma das quatro. Porque essas respostas estÃ£o enterradas em milhares de mensagens."

> "O OpenClaw lÃª tudo isso, analisa e entrega as respostas toda segunda de manhÃ£."

---

### ðŸ” SEÃ‡ÃƒO 2: Como funciona em 3 passos (4:00 â€“ 7:00)

**[Tela: diagrama simples com 3 blocos]**

> "O processo inteiro tem trÃªs partes. E cada parte o agente faz sozinho."

**Passo 1 â€” Buscar os dados**

> "O agente se conecta na sua base de dados â€” no meu caso Ã© o Supabase do MyGroupMetrics. Busca todas as mensagens dos Ãºltimos 30 dias. Com paginaÃ§Ã£o, porque bancos de dados grandes devolvem os dados em pedaÃ§os."

> "Resultado: 14.725 mensagens num arquivo JSON na memÃ³ria do agente."

**Passo 2 â€” Analisar**

> "Com os dados em mÃ£os, o agente aplica anÃ¡lises. Sentimento: quais mensagens sÃ£o positivas, quais sÃ£o negativas, com exemplos reais para vocÃª entender por quÃª. TÃ³picos: o que mais aparece â€” instalaÃ§Ã£o, erros, cases de sucesso, custos. PadrÃµes: horÃ¡rios, dias da semana, quem responde mais, quem some."

> "Tudo isso sem biblioteca de machine learning. Python puro, dicionÃ¡rio de palavras calibrado para o seu contexto."

**Passo 3 â€” Entregar**

> "O agente gera um HTML completo â€” dark theme, grÃ¡ficos em CSS, 14 seÃ§Ãµes â€” converte em PDF pelo Chrome e manda direto no Telegram. Eu recebo o arquivo aqui, e posso mandar pros alunos se quiser."

---

### ðŸ§  SEÃ‡ÃƒO 3: A Skill â€” a memÃ³ria do processo (7:00 â€“ 10:00)

**[Tela: o arquivo SKILL.md aberto no editor]**

> "Agora vou te mostrar a parte mais importante. NÃ£o Ã© o cÃ³digo â€” Ã© a Skill."

> "Toda vez que o agente acorda pra gerar o relatÃ³rio, ele lÃª esse arquivo aqui. A Skill Ã© a memÃ³ria do processo â€” estÃ¡ documentado onde buscar os dados, como analisar, qual formato gerar, onde salvar, como entregar."

> "Se eu nÃ£o tivesse isso, o agente esqueceria tudo entre uma sessÃ£o e outra. Com a Skill, ele sempre faz igual. Toda semana. Sem variaÃ§Ã£o."

**[Mostrar a estrutura do SKILL.md]**

> "Olha a estrutura: o que a skill faz, quando usar, os grupos que ela analisa com os IDs, como buscar as credenciais no 1Password â€” nunca senha hardcoded â€”, o processo passo a passo, e no final: guardrail. SÃ³ leitura. Zero escrita no banco sem autorizaÃ§Ã£o."

> "Isso aqui Ã© o que transforma uma tarefa que eu fiz uma vez em um processo que roda para sempre."

---

### â° SEÃ‡ÃƒO 4: O Cron â€” set and forget (10:00 â€“ 12:30)

**[Tela: cron list no terminal ou na interface]**

> "Com a Skill pronta, criar o cron Ã© a parte mais rÃ¡pida."

> "Pedi pro agente: 'Cria um cron pra rodar essa skill toda segunda Ã s 9h.' Ele verificou se o horÃ¡rio estava livre, configurou e pronto."

**[Mostrar a config do cron]**

> "Repara no detalhe: sessionTarget isolated. A tarefa roda numa sessÃ£o separada â€” nÃ£o polui o histÃ³rico do meu chat principal. E o delivery: announce para o topic do Telegram. O resultado chega aqui, no grupo certo."

> "Desde que configurei, nÃ£o precisei pensar mais nisso. Chega toda segunda. Leio em dois minutos. Tenho o panorama completo da semana."

---

### ðŸŒ SEÃ‡ÃƒO 5: Adapte para o seu contexto (12:30 â€“ 15:30)

**[Bruno na cÃ¢mera]**

> "Agora a pergunta que vocÃª estÃ¡ fazendo: 'Bruno, mas eu nÃ£o tenho MyGroupMetrics. Isso funciona pra mim?'"

> "Sim. VocÃª precisa de trÃªs coisas:"

**[Mostrar na tela â€” lista simples]**

> "Primeiro: uma fonte de dados com mensagens acessÃ­vel por API â€” pode ser Supabase, Crisp, Zendesk, qualquer coisa que tenha endpoint REST."

> "Segundo: saber quais campos tem nessa tabela â€” criado_em, mensagem, usuÃ¡rio. TrÃªs campos jÃ¡ sÃ£o suficientes."

> "Terceiro: pedir pro agente criar a Skill adaptada para o seu contexto."

**[Mostrar o prompt do aluno na tela]**

> "Tem um prompt no material da aula. VocÃª copia, adapta com seus dados, manda pro agente. Ele vai criar a Skill, testar a conexÃ£o, gerar o primeiro relatÃ³rio e montar o cron. Em menos de uma hora vocÃª tem o processo rodando."

> "Comunidade de clientes, grupo de alunos, canal de suporte â€” qualquer coisa que gere mensagens vira inteligÃªncia acionÃ¡vel."

---

### ðŸŽ¯ FECHAMENTO (15:30 â€“ 17:00)

**[Bruno na cÃ¢mera, tom de encerramento]**

> "Deixa eu resumir o que aconteceu aqui."

> "Eu tinha 14.725 mensagens que eu nunca ia ler. Agora toda segunda de manhÃ£ eu sei exatamente o que estÃ¡ acontecendo na comunidade: o que trava os alunos, quem estÃ¡ evoluindo, quando o grupo pulsa, o que precisa de atenÃ§Ã£o."

> "Isso nÃ£o Ã© anÃ¡lise â€” Ã© inteligÃªncia operacional. Ã‰ a diferenÃ§a entre gerir uma comunidade no escuro e gerir com dados."

> "O processo inteiro â€” conexÃ£o, anÃ¡lise, relatÃ³rio, entrega â€” estÃ¡ documentado numa Skill de uma pÃ¡gina. Roda automaticamente. NÃ£o depende de mim."

> "Na prÃ³xima aula a gente vai ver como criar Skills do zero para qualquer processo recorrente que vocÃª queira automatizar. AtÃ© lÃ¡."

---

## ðŸ–¥ï¸ O que mostrar na tela (guia de screen)

| Momento | O que mostrar |
|---------|--------------|
| Abertura | PDF do report aberto â€” a cÃ¢mera vÃª Bruno e o PDF lado a lado |
| SeÃ§Ã£o 1 | Slide com as 4 perguntas que a maioria nÃ£o consegue responder |
| SeÃ§Ã£o 2 | Diagrama: 3 blocos (Buscar â†’ Analisar â†’ Entregar) |
| SeÃ§Ã£o 2 (detalhe) | Briefly: terminal mostrando "Total: 14.725 mensagens" |
| SeÃ§Ã£o 3 | SKILL.md aberto no editor â€” scroll lento |
| SeÃ§Ã£o 4 | `cron list` no terminal + config do cron |
| SeÃ§Ã£o 5 | Prompt do aluno (material da aula) na tela |
| Fechamento | Bruno na cÃ¢mera, encerramento direto |

---

## âš ï¸ Pontos de atenÃ§Ã£o para a gravaÃ§Ã£o

- **NÃ£o entrar em detalhes de cÃ³digo Python** â€” mencionar que existe, mostrar brevemente se quiser, mas nÃ£o explicar linha por linha
- **Mostrar o PDF real** na abertura â€” o impacto visual Ã© o gancho
- **Pronunciar "MyGroupMetrics"** como contexto do caso, mas deixar claro que funciona com outras fontes
- **Mencionar paginaÃ§Ã£o** apenas como "o agente sabe como buscar os dados em pedaÃ§os" â€” sem detalhes tÃ©cnicos
- **Guardrail** â€” mencionar brevemente que a Skill tem regra de sÃ³ leitura. Passa confianÃ§a para o aluno

---

## ðŸ“ Arquivos da Aula

| Arquivo | Destino Drive |
|---------|--------------|
| HTML do material | Aulas extras / Materiais Aulas Extras / html/ |
| PDF do material | Aulas extras / Materiais Aulas Extras / pdf/ |
| Prompt do aluno | Aulas extras / Materiais Aulas Extras / |
| Exemplo de report (PDF) | Aulas extras / use-cases/ |


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
