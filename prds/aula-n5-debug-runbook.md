# PRD â€” Aula N-5: Debug Passo a Passo â€” Runbook PadrÃ£o de DiagnÃ³stico

**MÃ³dulo:** N â€” Troubleshooting & ManutenÃ§Ã£o  
**Aula:** N-5  
**DuraÃ§Ã£o estimada:** 25â€“30 minutos  
**NÃ­vel:** IntermediÃ¡rio / AvanÃ§ado  
**Formato:** Screencast com terminal ao vivo + slides de apoio  

---

## Objetivo da Aula

Ao final desta aula, o aluno saberÃ¡ seguir um runbook sistemÃ¡tico de 5 etapas para diagnosticar e resolver qualquer problema no OpenClaw â€” seja um bot silencioso, credenciais invÃ¡lidas, configuraÃ§Ã£o quebrada ou um erro desconhecido que precisa ser escalado.

---

## Roteiro de GravaÃ§Ã£o

### [00:00â€“02:00] Abertura

**Script (Bruno fala):**

> "OlÃ¡, pessoal! Nesta aula vamos falar de algo que todo mundo precisa em algum momento: debug. O OpenClaw Ã© robusto, mas coisas acontecem â€” um bot para de responder, uma chave de API expira, o gateway trava. E quando isso acontece sem vocÃª saber por onde comeÃ§ar... vira caos.
>
> EntÃ£o hoje eu vou te dar o meu runbook pessoal. Cinco etapas, em ordem. VocÃª segue do comeÃ§o ao fim e, na minha experiÃªncia, isso resolve 95% dos problemas. Vamos lÃ¡."

**O que mostrar na tela:**
- Diagrama das 5 etapas (slide de abertura)
- Terminal limpo, pronto para uso

---

### [02:00â€“06:00] Etapa 1: Triagem Inicial â€” O Bot Responde?

**Script:**

> "A primeira etapa Ã© a triagem. Antes de mexer em qualquer coisa, vocÃª precisa entender _o que_ exatamente estÃ¡ errado. Existem trÃªs cenÃ¡rios distintos, e cada um aponta para um caminho diferente.
>
> **CenÃ¡rio A: O bot estÃ¡ completamente silencioso.** VocÃª mandou mensagem, esperou, nada aconteceu. Isso quase sempre significa que o gateway nÃ£o estÃ¡ rodando. O gateway Ã© o processo que fica escutando as mensagens e roteando para o modelo de IA. Se ele cair, o bot simplesmente para de existir. A soluÃ§Ã£o Ã© imediata â€” vamos ver na Etapa 2.
>
> **CenÃ¡rio B: O bot responde, mas com uma mensagem de erro.** Ã“timo! Isso significa que o gateway estÃ¡ de pÃ©. Agora vocÃª precisa _ler_ a mensagem de erro. Parece Ã³bvio, mas muita gente entra em pÃ¢nico e sai reiniciando tudo sem ler o que estÃ¡ escrito. O erro geralmente te diz exatamente o que fazer: chave invÃ¡lida, rate limit atingido, arquivo de configuraÃ§Ã£o com problema.
>
> **CenÃ¡rio C: O bot responde, mas lento â€” muito lento.** Esse Ã© um problema de performance, nÃ£o de configuraÃ§Ã£o. Eu cobri isso na aula N-4. Se o seu bot estÃ¡ demorando 30 segundos para responder, pula para lÃ¡. Aqui a gente foca em erros, nÃ£o em lentidÃ£o.
>
> EntÃ£o antes de continuar: qual dos trÃªs cenÃ¡rios vocÃª estÃ¡ vivendo? Isso define tudo."

**O que mostrar na tela:**
- Fluxograma de decisÃ£o: Silencioso / Erro / Lento
- DemonstraÃ§Ã£o: mandar mensagem no Telegram e mostrar cada tipo de resposta (ou ausÃªncia dela)

---

### [06:00â€“12:00] Etapa 2: Verificar o Gateway

**Script:**

> "Se o bot estÃ¡ silencioso, comeÃ§a aqui. O comando Ã© simples:"

```bash
openclaw gateway status
```

> "Esse comando te diz se o processo do gateway estÃ¡ rodando ou nÃ£o. Se a saÃ­da mostrar algo como `stopped` ou `inactive`, vocÃª sabe o problema. Reinicia:

```bash
openclaw gateway restart
```

> "Se o gateway estava parado, provavelmente ele volta e o bot comeÃ§a a funcionar imediatamente. Testa rÃ¡pido â€” manda um 'olÃ¡' lÃ¡.
>
> Mas e se o gateway reinicia, mas o problema persiste? AÃ­ vocÃª precisa olhar os logs. Os logs do OpenClaw ficam em:

```bash
~/.openclaw/logs/gateway.log
```

> "Para ver as Ãºltimas linhas em tempo real, usa:

```bash
tail -f ~/.openclaw/logs/gateway.log
```

> "Agora, o que vocÃª estÃ¡ procurando nos logs? Existem quatro sinais de alerta que eu sempre busco:
>
> **1. `auth error` ou `unauthorized`** â€” Significa que a API key nÃ£o estÃ¡ sendo aceita. Vai direto para a Etapa 3.
>
> **2. `rate limit exceeded`** â€” VocÃª esgotou o limite de requisiÃ§Ãµes do seu plano. Pode ser um pico de uso, um loop acidental, ou o plano precisando ser upgradado. Espere alguns minutos e tente novamente.
>
> **3. `context error` ou `context length exceeded`** â€” A conversa ficou longa demais para o modelo processar. VocÃª precisa limpar o histÃ³rico da sessÃ£o ou ajustar o limite de contexto na configuraÃ§Ã£o.
>
> **4. `connection refused` ou `timeout`** â€” Problema de rede ou o endpoint da API estÃ¡ fora. Verifica sua conexÃ£o e o status da API do seu provedor (OpenAI, OpenRouter, etc.).
>
> Vou mostrar ao vivo como ler um log real e identificar esses sinais."

**O que mostrar na tela:**
- `openclaw gateway status` com saÃ­da de stopped/running
- `openclaw gateway restart` e output
- `tail -f ~/.openclaw/logs/gateway.log` com exemplos de cada tipo de erro destacados

---

### [12:00â€“17:00] Etapa 3: Verificar Credenciais

**Script:**

> "Chegamos na causa mais comum de problemas: credenciais. A API key expirou, foi rotacionada, ou simplesmente foi copiada errada. ComeÃ§a com o diagnÃ³stico:

```bash
openclaw status
```

> "Esse comando lista todos os modelos configurados e o status de cada um. VocÃª vai ver algo como:

```
Models configured:
  âœ“ openai/gpt-5.4   [active]
  âœ— openai/gpt-4o             [auth error]
```

> "Se algum modelo estÃ¡ com `auth error`, a chave estÃ¡ invÃ¡lida ou ausente.
>
> O teste mais simples Ã© mandar uma mensagem curta â€” literalmente 'olÃ¡' â€” e ver o que acontece. Se vocÃª receber `401 Unauthorized` nos logs, a chave estÃ¡ errada. Se receber `429 Too Many Requests`, Ã© rate limit.
>
> Esses dois erros parecem iguais para o usuÃ¡rio â€” o bot nÃ£o responde â€” mas a soluÃ§Ã£o Ã© completamente diferente:
>
> - **401 / auth error:** VocÃª precisa reautenticar. A chave estÃ¡ invÃ¡lida.
> - **429 / rate limit:** A chave Ã© vÃ¡lida, mas vocÃª usou demais. Espere e tente de novo.
>
> Para reautenticar, vai no painel do provedor, gera uma nova chave, e atualiza no OpenClaw:

```bash
openclaw config set api_key <sua-nova-chave>
openclaw gateway restart
```

> "Depois do restart, testa novamente. Na minha experiÃªncia, 60% dos problemas que chegam no suporte se resolvem aqui."

**O que mostrar na tela:**
- `openclaw status` com exemplos de modelos ativos e com erro
- ComparaÃ§Ã£o visual: 401 vs 429 nos logs
- DemonstraÃ§Ã£o de como atualizar a chave e reiniciar

---

### [17:00â€“22:00] Etapa 4: Verificar ConfiguraÃ§Ã£o

**Script:**

> "Se chegou atÃ© aqui e ainda nÃ£o resolveu, o problema estÃ¡ na configuraÃ§Ã£o. O OpenClaw tem um comando novo que eu recomendo fortemente usar _antes_ de qualquer restart:

```bash
openclaw config validate
```

> "Esse comando lÃª o seu `openclaw.json`, verifica a sintaxe, e aponta exatamente onde estÃ¡ o erro â€” com nÃºmero de linha e tudo. Muito melhor do que reiniciar e ficar olhando pra uma tela branca tentando adivinhar.
>
> Os erros mais comuns que eu vejo no `openclaw.json`:
>
> **1. VÃ­rgula sobrando ou faltando** â€” JSON Ã© impiedoso. Uma vÃ­rgula a mais no final de um objeto jÃ¡ quebra tudo.
>
> **2. Campo obrigatÃ³rio ausente** â€” `model`, `channel`, ou `token` faltando no bloco de configuraÃ§Ã£o.
>
> **3. ReferÃªncia a arquivo que nÃ£o existe** â€” O `openclaw.json` apontando para um AGENTS.md num caminho que nÃ£o existe.
>
> Falando em AGENTS.md: esse arquivo tambÃ©m pode causar problemas. Os erros mais comuns sÃ£o:
>
> - **IndentaÃ§Ã£o quebrada** â€” O AGENTS.md usa markdown. Um bloco de cÃ³digo mal fechado pode bagunÃ§ar o parsing.
> - **ReferÃªncia circular** â€” Uma skill que importa outra que importa a primeira.
> - **InstruÃ§Ã£o conflitante** â€” Duas regras que se contradizem. O modelo fica preso tentando obedecer as duas.
>
> Skills tambÃ©m podem ter conflito. Se vocÃª adicionou uma skill nova e o bot comeÃ§ou a se comportar de forma estranha, testa removendo a skill temporariamente para isolar o problema.
>
> Depois de corrigir qualquer coisa no arquivo de configuraÃ§Ã£o, sempre valida antes de reiniciar:

```bash
openclaw config validate && openclaw gateway restart
```

> "O `&&` garante que o restart sÃ³ acontece se a validaÃ§Ã£o passar. Boa prÃ¡tica."

**O que mostrar na tela:**
- `openclaw config validate` com saÃ­da de sucesso e com erro
- Exemplos de `openclaw.json` quebrado vs correto (diff lado a lado)
- Exemplo de AGENTS.md com problema de formataÃ§Ã£o

---

### [22:00â€“27:00] Etapa 5: Escalar o Problema

**Script:**

> "Se vocÃª chegou atÃ© aqui e ainda nÃ£o conseguiu resolver, o problema Ã© mais complexo. NÃ£o Ã© vergonha nenhuma â€” o importante agora Ã© pedir ajuda da forma certa.
>
> Tem uma ferramenta especÃ­fica para isso:

```bash
openclaw doctor
```

> "O `doctor` faz uma checagem completa do ambiente: versÃ£o do OpenClaw, integridade dos arquivos de configuraÃ§Ã£o, status dos modelos, permissÃµes de arquivo, variÃ¡veis de ambiente. Ele gera um relatÃ³rio que vocÃª pode compartilhar.
>
> Mas antes de postar no grupo de suporte, existe uma etiqueta importante: **nunca compartilhe suas chaves de API.** O `openclaw doctor` automaticamente mascara credenciais no output, mas se vocÃª for copiar logs manualmente, revise antes.
>
> O que coletar antes de pedir ajuda:
>
> **1. VersÃ£o do OpenClaw:**

```bash
openclaw --version
```

> **2. Output do `openclaw doctor`** (jÃ¡ com credenciais mascaradas)
>
> **3. Os Ãºltimos 50 logs do gateway:**

```bash
tail -50 ~/.openclaw/logs/gateway.log
```

> **4. Sua config sem credenciais:**

```bash
openclaw config export --mask-secrets
```

> "Com essas quatro coisas, qualquer pessoa do suporte consegue te ajudar em minutos. Sem isso, a conversa vira um interrogatÃ³rio e demora muito mais.
>
> No grupo de suporte, cole tudo em um Ãºnico bloco de cÃ³digo, descreva o que vocÃª fez antes do problema aparecer, e qual das 5 etapas do runbook vocÃª jÃ¡ executou. Isso economiza o tempo de todo mundo."

**O que mostrar na tela:**
- `openclaw doctor` com output completo
- `openclaw --version`
- `openclaw config export --mask-secrets`
- Template de post no grupo de suporte

---

### [27:00â€“30:00] Encerramento â€” Tabela de Erros & Primeiros Socorros

**Script:**

> "Antes de terminar, dois recursos que vocÃª vai querer ter sempre Ã  mÃ£o.
>
> O primeiro Ã© a tabela de erros mais comuns â€” estÃ¡ no material de apoio desta aula. Cola no favoritos.
>
> O segundo Ã© o checklist de primeiros socorros: cinco comandos que resolvem 80% dos problemas. Quando o bot parar de funcionar, roda esses cinco na ordem, e na maioria das vezes um deles jÃ¡ resolve:

```bash
# 1. Ver status geral
openclaw status

# 2. Ver status do gateway
openclaw gateway status

# 3. Reiniciar o gateway
openclaw gateway restart

# 4. Validar configuraÃ§Ã£o
openclaw config validate

# 5. DiagnÃ³stico completo
openclaw doctor
```

> "Salva isso. Imprime se precisar. Ã‰ o seu kit de ferramentas de debug.
>
> Nos vemos na prÃ³xima aula. Se tiver dÃºvida, o grupo de suporte estÃ¡ lÃ¡."

---

## Tabela de Erros Mais Comuns

| Erro | Sintoma | Causa | SoluÃ§Ã£o |
|------|---------|-------|---------|
| `401 Unauthorized` | Bot silencioso ou erro na resposta | API key invÃ¡lida ou expirada | Gerar nova chave, `openclaw config set api_key <nova>`, restart |
| `429 Too Many Requests` | Bot silencioso por um perÃ­odo | Rate limit atingido | Aguardar 1-5 minutos, reduzir frequÃªncia de uso |
| `Gateway stopped` | Bot completamente silencioso | Processo do gateway travou ou crashou | `openclaw gateway restart` |
| `Context length exceeded` | Erro apÃ³s conversa longa | HistÃ³rico de conversa muito extenso | Limpar histÃ³rico ou ajustar `max_context` na config |
| `Connection refused` | Erro de conexÃ£o nos logs | Rede instÃ¡vel ou endpoint fora | Verificar internet, checar status do provedor |
| `JSON parse error` | Gateway falha ao iniciar | `openclaw.json` com erro de sintaxe | `openclaw config validate`, corrigir JSON |
| `File not found` | Gateway falha ao iniciar | Caminho de arquivo inexistente na config | Verificar todos os caminhos no `openclaw.json` |
| `Skill conflict` | Comportamento errÃ¡tico do bot | Duas skills com instruÃ§Ãµes conflitantes | Remover skill recÃ©m-adicionada, isolar problema |
| `AGENTS.md parse error` | Bot ignora instruÃ§Ãµes | AGENTS.md mal formatado (bloco de cÃ³digo aberto) | Fechar todos os blocos de cÃ³digo no AGENTS.md |
| `Model not found` | Erro ao processar mensagem | Nome do modelo incorreto na config | Verificar nomenclatura exata no `openclaw status` |

---

## Checklist de Primeiros Socorros

- [ ] `openclaw status` â€” ver estado geral dos modelos
- [ ] `openclaw gateway status` â€” confirmar se o gateway estÃ¡ rodando
- [ ] `openclaw gateway restart` â€” reiniciar o gateway
- [ ] `openclaw config validate` â€” validar o arquivo de configuraÃ§Ã£o
- [ ] `openclaw doctor` â€” diagnÃ³stico completo do ambiente

---

## Notas de ProduÃ§Ã£o

- **Ambiente de gravaÃ§Ã£o:** Terminal com fonte grande (16px+), tema escuro
- **Mostrar erros reais:** Preparar arquivos de configuraÃ§Ã£o propositalmente quebrados para demonstraÃ§Ã£o
- **Pausar nos momentos-chave:** ApÃ³s cada comando, aguardar o output aparecer completamente antes de falar
- **Material de apoio:** HTML desta aula deve estar linkado na descriÃ§Ã£o do vÃ­deo
- **Thumbnail:** Imagem com "5 etapas" e Ã­cone de bug/ferramentas


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
