# Roteiro de GravaÃ§Ã£o â€” "Skills: O Sistema de Superpoderes do Seu Agente"
**Aula dedicada | ~25 min | MÃ³dulo 6 reformulado**

---

## Setup antes de gravar

- Terminal aberto com workspace da Amora visÃ­vel
- VS Code mostrando `skills/` com subpastas reais (content/, analytics/, operations/)
- ClawHub aberto no browser: clawhub.com
- GitHub aberto com um exemplo de skill de terceiro
- NotificaÃ§Ãµes desativadas

---

## BLOCO 1 â€” Abertura: Por que 1 agente > mÃºltiplos agentes (2 min)

**[CÃ‚MERA FRONTAL]**

> "Quando a galera comeÃ§a a usar OpenClaw de verdade, invariavelmente cai na mesma armadilha: comeÃ§a a criar agente pra tudo.
>
> Agente de conteÃºdo. Agente de mÃ©tricas. Agente de email. Agente de calendÃ¡rio.
>
> Parece que faz sentido. Na prÃ¡tica, Ã© um pesadelo.
>
> Por quÃª? Porque cada agente tem seu prÃ³prio contexto. VocÃª pede pra um criar um post, e outro nÃ£o sabe que o post foi criado. VocÃª toma uma decisÃ£o com um, o outro nÃ£o sabe. VocÃª vira o gerente de 8 agentes burros ao invÃ©s de ter 1 assistente inteligente.
>
> A forma certa Ã© outra: **1 agente com mÃºltiplos superpoderes.** Cada superpoder Ã© uma skill.
>
> Ã‰ exatamente isso que essa aula cobre."

---

## BLOCO 2 â€” O que Ã© uma skill (3 min)

**[COMPARTILHA TELA: VS Code, abre skills/ no workspace]**

> "Uma skill Ã© basicamente um manual de instruÃ§Ãµes + ferramentas que vocÃª dÃ¡ pro seu agente.
>
> Estrutura mÃ­nima:"

**[MOSTRAR: tree de uma skill real, ex: skills/content/carrossel-linkedin/]**

```
skills/
â””â”€â”€ content/
    â””â”€â”€ carrossel-linkedin/
        â””â”€â”€ SKILL.md
```

> "Ã‰ sÃ³ um arquivo SKILL.md. O agente lÃª esse arquivo quando vai executar a skill, entende o que pode fazer, e executa.
>
> Quando eu digo 'cria um carrossel de LinkedIn', o agente vai lÃ¡, lÃª a skill, e segue o processo definido. NÃ£o improvisa. NÃ£o alucina formato. Segue o que tÃ¡ escrito.
>
> Isso Ã© o ponto central: **skill = processo documentado que o agente executa de forma consistente.**"

**[MOSTRAR: abrir um SKILL.md real â€” conteÃºdo resumido]**

> "O arquivo tem: descriÃ§Ã£o do que a skill faz, quando usar, quais inputs ela precisa, e o passo a passo de execuÃ§Ã£o. Pode ter exemplos, regras de qualidade, o que for necessÃ¡rio."

---

## BLOCO 3 â€” Como organizar skills em pastas (3 min)

**[COMPARTILHA TELA: VS Code, Ã¡rvore completa de skills/]**

> "OrganizaÃ§Ã£o importa. Minha estrutura:"

**[MOSTRAR: tree das skills/ reais]**

```
skills/
â”œâ”€â”€ content/          â† tudo que produz conteÃºdo
â”‚   â”œâ”€â”€ carrossel-instagram/
â”‚   â”œâ”€â”€ carrossel-linkedin/
â”‚   â””â”€â”€ yt-hype/
â”œâ”€â”€ analytics/        â† mÃ©tricas e dados
â”‚   â”œâ”€â”€ chartmogul/
â”‚   â””â”€â”€ ga4/
â”œâ”€â”€ operations/       â† operaÃ§Ãµes recorrentes
â”‚   â”œâ”€â”€ notion-api/
â”‚   â”œâ”€â”€ crisp-wrapup/
â”‚   â””â”€â”€ planner-adhd/
â””â”€â”€ research/         â† pesquisa e inteligÃªncia
    â”œâ”€â”€ deep-research-protocol/
    â””â”€â”€ blogwatcher/
```

> "Categorias claras. Quando vou criar uma skill nova, primeiro me pergunto: qual categoria? Se nÃ£o existe categoria pra ela, pode ser que seja uma categoria nova â€” ou que eu precisaria criar antes.
>
> Por que isso importa? Porque quando vocÃª tem 20, 30 skills, sem organizaÃ§Ã£o vocÃª perde tempo achando o que tem disponÃ­vel. E mais importante: o agente tambÃ©m fica confuso.
>
> A regra que uso: **cada skill resolve uma coisa bem feita.** Skill de carrossel de Instagram â‰  skill de carrossel de LinkedIn â€” porque o formato, tom e estrutura sÃ£o completamente diferentes."

---

## BLOCO 4 â€” Como pedir pro agente executar uma skill (2 min)

**[CÃ‚MERA FRONTAL â†’ COMPARTILHA TELA: terminal com agente]**

> "Duas formas:"

**[DEMO AO VIVO: digitar os dois exemplos]**

> "Forma simples â€” vocÃª sÃ³ pede:"

```
"Cria um carrossel de LinkedIn sobre o crescimento do Metricaas"
```

> "O agente identifica que existe a skill de carrossel LinkedIn, lÃª o SKILL.md automaticamente, e executa.
>
> Forma explÃ­cita â€” quando quer garantir qual skill usar:"

```
"Usa a skill carrossel-linkedin pra criar um carrossel sobre..."
```

> "O agente vai direto pra aquela skill especÃ­fica.
>
> **Importante:** o agente sÃ³ usa a skill se ela estiver na pasta skills/ do workspace. Ele nÃ£o inventa. Se a skill nÃ£o existe, ele ou improvisa â€” o que Ã© menos consistente â€” ou te diz que nÃ£o tem aquela skill."

---

## BLOCO 5 â€” Todo processo repetitivo vira skill (3 min)

**[CÃ‚MERA FRONTAL]**

> "Essa Ã© a mentalidade que muda o jogo.
>
> Toda vez que vocÃª faz a mesma coisa mais de duas vezes com seu agente, vocÃª tem um candidato a skill.
>
> Exemplos concretos:"

**[MOSTRAR NA TELA â€” lista simples]**

> "- VocÃª toda semana pede um relatÃ³rio de mÃ©tricas â†’ skill de weekly-metrics
> - VocÃª toda vez que grava um vÃ­deo pede tÃ­tulo, descriÃ§Ã£o e tags â†’ skill yt-hype
> - VocÃª toda vez que tem uma reuniÃ£o pede um brief de prep â†’ skill meeting-prep
> - VocÃª todo mÃªs analisa o churn â†’ skill churn-analysis
>
> Por que transformar em skill e nÃ£o sÃ³ repetir o prompt?
>
> Porque quando estÃ¡ na skill, o processo estÃ¡ documentado, testado, tem critÃ©rios de qualidade definidos. VocÃª nÃ£o precisa lembrar de detalhe. O agente nÃ£o improvisa. E quando vocÃª quiser melhorar o processo, muda a skill â€” e muda pra sempre.
>
> Pensa assim: **um prompt Ã© um pedido. Uma skill Ã© um processo.**"

---

## BLOCO 6 â€” Sub-agentes executam skills especÃ­ficas (2 min)

**[CÃ‚MERA FRONTAL]**

> "Quando vocÃª usa sub-agentes â€” que Ã© quando o agente principal delega uma tarefa pra um agente isolado rodar em background â€” a melhor prÃ¡tica Ã©: o sub-agente tem um escopo claro e executa uma skill especÃ­fica.
>
> Errado:"

**[MOSTRAR NA TELA]**

> âŒ "Spawna um agente pra 'cuidar do conteÃºdo'"

> "Certo:"

> âœ… "Spawna um agente pra executar a skill carrossel-linkedin com esse input"

> "A diferenÃ§a: o agente solto vai tomar decisÃµes aleatÃ³rias. O agente com skill tem um processo definido, inputs claros, e output previsÃ­vel.
>
> Sub-agentes sÃ£o Ã³timos pra tarefas paralelas e longas. Mas sempre com escopo fechado. Um sub-agente sem skill Ã© um freelancer sem briefing."

---

## BLOCO 7 â€” Backup das suas skills (2 min)

**[COMPARTILHA TELA: terminal]**

> "Suas skills sÃ£o ativos. Se vocÃª perder o workspace, perde todo o processo que documentou.
>
> Duas formas de backup:"

**[MOSTRAR: comando git]**

> "A mais simples: Git. Seu workspace jÃ¡ Ã© um repositÃ³rio. Commita e faz push:"

```bash
cd ~/seu-workspace
git add skills/
git commit -m "backup skills $(date +%Y-%m-%d)"
git push
```

> "RepositÃ³rio privado no GitHub, acesso sÃ³ seu.
>
> Segunda opÃ§Ã£o: script de backup automÃ¡tico. VocÃª configura uma cron pra rodar de madrugada e fazer push automaticamente. Tem um script de exemplo no workspace de referÃªncia do curso.
>
> A regra de ouro: **skill que nÃ£o estÃ¡ no Git nÃ£o existe.** Um crash de disco, um workspace corrompido â€” e vocÃª perde meses de processo documentado. NÃ£o deixa isso acontecer."

---

## BLOCO 7b â€” Demo real: skill de Meta Ads (2 min)

**[COMPARTILHA TELA: VS Code â†’ skills/analytics/meta-ads/SKILL.md]**

> "Antes de falar de seguranÃ§a, quero mostrar como uma skill de analytics real funciona na prÃ¡tica.
>
> Essa Ã© a skill de Meta Ads que rodo todo dia pra acompanhar as vendas da Pixel EducaÃ§Ã£o â€” a empresa do curso. Vou abrir o SKILL.md:"

**[MOSTRAR: SKILL.md aberto â€” credenciais com XXXX]**

> "Olha aqui: o token do Meta e o ID da conta estÃ£o como `XXXX`. Nunca no cÃ³digo â€” sempre via 1Password. O agente busca em runtime.
>
> O que ela gera? Um dashboard como esse:"

**[MOSTRAR: arquivo exemplo-output-meta-ads.html no browser]**

> "Receita total, split por produto â€” OpenClaw Minicurso separado do Micro-SaaS PRO â€” taxa de reembolso, ROAS das campanhas. Gerado automaticamente, enviado pro Telegram todo dia Ã s 8h.
>
> Isso Ã© o que uma skill bem feita entrega. VocÃª descreve o processo uma vez â€” e o agente executa toda vez que vocÃª pedir, ou no horÃ¡rio que vocÃª configurar."

---

## BLOCO 8 â€” Skills de terceiros: como usar com seguranÃ§a (4 min)

**[COMPARTILHA TELA: clawhub.com aberto no browser]**

> "O ClawHub Ã© o marketplace de skills da comunidade OpenClaw. VocÃª encontra skills prontas pra instalar.
>
> Mas antes de instalar qualquer coisa, uma regra inviolÃ¡vel:"

**[CÃ‚MERA FRONTAL â€” tom sÃ©rio]**

> "Leia o cÃ³digo. Sempre.
>
> Uma skill tem acesso ao seu workspace, pode rodar comandos, pode ler arquivos. Skill maliciosa pode exfiltrar credenciais, deletar dados, executar qualquer coisa.
>
> O protocolo manual bÃ¡sico:"

**[COMPARTILHA TELA: terminal]**

```bash
git clone https://github.com/usuario/skill-nome /tmp/review-skill
cat /tmp/review-skill/SKILL.md
grep -r "curl" /tmp/review-skill/
grep -r "rm -rf" /tmp/review-skill/
grep -r "eval" /tmp/review-skill/
```

> "Funciona. Mas tem uma forma melhor.
>
> O Adrylan â€” um dos alunos mais avanÃ§ados do curso â€” criou uma skill que audita outras skills. Ela Ã© baseada no OWASP ASI Top 10 de 2026, no scanner Snyk e no Aguara. Nove categorias de verificaÃ§Ã£o: prompt injection, exfiltraÃ§Ã£o de dados, cÃ³digo malicioso, credenciais hardcoded, engenharia social...
>
> VocÃª instala ela uma vez â€” e a partir daÃ­, toda vez que encontrar uma skill nova, vocÃª cola o conteÃºdo e pede: 'audita essa skill'. O agente roda o checklist completo e te dÃ¡ um relatÃ³rio: limpo, atenÃ§Ã£o ou crÃ­tico.
>
> O SKILL.md completo tÃ¡ no material bÃ´nus no Drive. **Ã‰ a primeira skill que vocÃª deve instalar â€” antes de qualquer outra.**"

---

## BLOCO 9 â€” Skills do Claude Code funcionam no OpenClaw? (2 min)

**[CÃ‚MERA FRONTAL]**

> "Pergunta frequente: tenho skills do Claude Code, funcionam no OpenClaw?
>
> Resposta curta: depende.
>
> Skills do Claude Code â€” os arquivos CLAUDE.md â€” tÃªm um formato diferente. SÃ£o instruÃ§Ãµes pro agente de como se comportar num projeto de cÃ³digo especÃ­fico. NÃ£o sÃ£o o mesmo conceito de skill do OpenClaw.
>
> Para adaptar:
> 1. O conteÃºdo de instruÃ§Ã£o geralmente Ã© aproveitÃ¡vel â€” vocÃª pega o contexto e regras e coloca num SKILL.md do OpenClaw
> 2. Scripts bash que o Claude Code usa geralmente rodam no OpenClaw sem modificaÃ§Ã£o â€” o ambiente de execuÃ§Ã£o Ã© compatÃ­vel
> 3. O que nÃ£o funciona direto sÃ£o integraÃ§Ãµes especÃ­ficas do Claude Code (MCP servers, por exemplo) â€” aÃ­ precisa adaptar pro equivalente OpenClaw
>
> Na prÃ¡tica: se vocÃª tem um prompt elaborado que usa no Claude Code, vira um SKILL.md no OpenClaw. O comportamento vai ser equivalente."

---

## BLOCO 10 â€” Encerramento (1 min)

**[CÃ‚MERA FRONTAL]**

> "Resumindo:
>
> Um agente com skills > mÃºltiplos agentes. Contexto unificado, processo consistente.
>
> Cada processo repetitivo vira skill. Prompt Ã© pedido, skill Ã© processo.
>
> Sub-agente sem skill = freelancer sem briefing. Sempre dÃª escopo claro.
>
> Backup no Git. Skills sÃ£o ativos, trate como cÃ³digo.
>
> Skill de terceiro: leia o cÃ³digo antes. Sempre.
>
> O material completo â€” lista de skills por perfil, checklist de seguranÃ§a e o prompt de instalaÃ§Ã£o â€” tÃ¡ no Drive, link na descriÃ§Ã£o."

---

## Checklist prÃ©-gravaÃ§Ã£o

- [ ] VS Code com `skills/` aberto mostrando categorias reais
- [ ] `skills/analytics/meta-ads/SKILL.md` aberto (credenciais como XXXX)
- [ ] `reports/misc/exemplo-output-meta-ads.html` aberto no browser (dashboard de vendas)
- [ ] Terminal pronto pra demo do clone + grep de seguranÃ§a
- [ ] clawhub.com aberto no browser
- [ ] SKILL.md da skill-audit pronto pra mostrar (material bÃ´nus)
- [ ] Script de backup git pronto no terminal
- [ ] NotificaÃ§Ãµes desativadas

## Timings aproximados

| Bloco | ConteÃºdo | Tempo |
|-------|----------|-------|
| 1 | Abertura: 1 agente > mÃºltiplos | 2:00 |
| 2 | O que Ã© uma skill | 3:00 |
| 3 | OrganizaÃ§Ã£o em pastas | 3:00 |
| 4 | Como pedir pra executar | 2:00 |
| 5 | Todo processo vira skill | 3:00 |
| 6 | Sub-agentes + skills | 2:00 |
| 7 | Backup no Git | 2:00 |
| 7b | Demo real: skill Meta Ads | 2:00 |
| 8 | Skills de terceiros + skill-audit bÃ´nus | 4:00 |
| 9 | Claude Code â†’ OpenClaw | 2:00 |
| 10 | Encerramento | 1:00 |
| **Total** | | **~26 min** |

## Links para colocar na descriÃ§Ã£o

- ClawHub: https://clawhub.com
- Skills por perfil (PDF): Drive â†’ Curso OpenClaw â†’ aula-06-skills â†’ skills-by-profile.pdf
- Prompt de instalaÃ§Ã£o: Drive â†’ aula-06-skills â†’ prompts â†’ modulo-06-skills.md


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
