# Guia Completo: TÃ³picos no Telegram + Arquitetura de Agentes

**Objetivo:** Ensinar a criar e organizar tÃ³picos no Telegram, configurar agentes para responder sem menÃ§Ã£o, e entender as diferenÃ§as arquiteturais entre **um agente MAIN compartilhado** vs **agentes isolados por tÃ³pico**.

---

## ðŸ“± Parte 1: Criando TÃ³picos no Telegram

### O que sÃ£o TÃ³picos (Topics)?

TÃ³picos sÃ£o **threads organizadas dentro de um grupo**. Cada tÃ³pico funciona como um canal separado, mas todos estÃ£o no mesmo grupo.

**Quando usar:**
- Separar projetos diferentes
- Organizar conversas por assunto (suporte, dev, ideias)
- Ter agentes especializados por contexto

### Passo a Passo: Criar Grupo com TÃ³picos

#### 1. Criar o Grupo

1. Abra o Telegram
2. Menu â†’ **Novo Grupo**
3. Nome: `Amora HQ` (ou o que preferir)
4. Adicione pelo menos 1 pessoa (vocÃª mesmo pode ser suficiente)
5. Finalize a criaÃ§Ã£o

#### 2. Transformar em Supergrupo

1. Abra as **configuraÃ§Ãµes do grupo** (clique no nome)
2. **Tipo do Grupo** â†’ **Grupo PÃºblico** (ou mantenha privado)
3. Defina um `@username` para o grupo (ex: `@amorahq_bruno`)
4. O Telegram automaticamente transforma em **Supergrupo**

> âš ï¸ **Importante:** SÃ³ supergrupos suportam tÃ³picos!

#### 3. Ativar TÃ³picos

1. ConfiguraÃ§Ãµes do grupo â†’ **TÃ³picos**
2. Toggle **"Ativar TÃ³picos"**
3. O Telegram cria automaticamente o tÃ³pico **"Geral"** (id: `1`)

#### 4. Criar TÃ³picos Adicionais

1. Na tela do grupo, clique no **Ã­cone de tÃ³picos** (canto superior)
2. **"Criar TÃ³pico"**
3. DÃª um nome: `Curso OpenClaw`, `Suporte`, `Dev`, etc.
4. Escolha um Ã­cone/emoji
5. Pronto! Cada tÃ³pico tem um **ID Ãºnico** (ex: `2638`, `2640`)

---

## ðŸ¤– Parte 2: Adicionando Agentes aos TÃ³picos

### OpÃ§Ã£o A: Adicionar o Bot ao Grupo

1. VÃ¡ em **@BotFather**
2. `/mybots` â†’ escolha seu bot
3. **Bot Settings â†’ Group Privacy â†’ Desativar "Privacy Mode"**
   - Isso permite o bot ver **todas as mensagens** do grupo
4. Adicione o bot ao grupo: `@seubotaqui`
5. Torne ele **administrador** (necessÃ¡rio para agir em tÃ³picos)

### OpÃ§Ã£o B: Usar Bot Existente (sem admin)

Se o bot NÃƒO for admin, ele sÃ³ responde quando **marcado** (`@bot mensagem`).

---

## âš™ï¸ Parte 3: Configurando Agentes para Responder SEM MenÃ§Ã£o

Por padrÃ£o, bots do Telegram sÃ³ respondem quando mencionados. Para habilitar **resposta automÃ¡tica em tÃ³picos especÃ­ficos**, vocÃª precisa configurar no `config.yaml`.

### Estrutura do Config

```yaml
agents:
  - id: amora-main
    model: openai/gpt-4o
    thinking: off
    workspaceDir: /root/.openclaw/workspace-meu-agente
    
    activation:
      surfaces:
        - surface: telegram
          mode: mention  # PadrÃ£o global: sÃ³ quando marcada
          
          overrides:
            # TÃ³pico "Curso OpenClaw" â€” responde TUDO
            - chat: "telegram:-1001234567890:topic:2638"
              mode: all
            
            # TÃ³pico "Suporte" â€” responde TUDO
            - chat: "telegram:-1001234567890:topic:2640"
              mode: all
            
            # TÃ³pico "Geral" â€” sÃ³ quando marcada
            - chat: "telegram:-1001234567890:topic:1"
              mode: mention
```

### Como Descobrir o Chat ID

1. Mande uma mensagem **no tÃ³pico** marcando o bot
2. No terminal da VPS: `openclaw logs --tail 50`
3. Procure por: `chat_id: "telegram:-1001234567890:topic:2638"`
4. Copie esse ID e cole no config

### Aplicar a Config

```bash
openclaw gateway restart
```

Agora a Amora responde **automaticamente** nos tÃ³picos configurados com `mode: all`.

---

## ðŸ—ï¸ Parte 4: Arquitetura de Agentes â€” MAIN vs Isolados

Aqui estÃ¡ a **decisÃ£o mais importante** do curso: como organizar seus agentes?

---

### ðŸ”µ Arquitetura 1: **UM Agente MAIN Compartilhado**

**Como funciona:**
- **1 agente** (`amora-main`) responde em **mÃºltiplos tÃ³picos**
- Todos os tÃ³picos compartilham:
  - Mesmo **workspace**
  - Mesma **memÃ³ria** (`MEMORY.md`, `memory/2026-02-25.md`)
  - Mesmos **crons** (heartbeats, lembretes)
  - Mesmo **SOUL.md**, **USER.md**, **TOOLS.md**

**Exemplo de config:**

```yaml
agents:
  - id: amora-main
    workspaceDir: /root/.openclaw/workspace-meu-agente
    activation:
      surfaces:
        - surface: telegram
          mode: mention
          overrides:
            - chat: "telegram:-1001234567890:topic:2638"  # Suporte
              mode: all
            - chat: "telegram:-1001234567890:topic:1"     # Geral
              mode: mention
```

#### âœ… Vantagens

1. **Continuidade total** â€” A Amora lembra de TUDO que aconteceu em todos os tÃ³picos
2. **Economia de recursos** â€” 1 processo, 1 workspace, 1 memÃ³ria
3. **Crons Ãºnicos** â€” Heartbeats, lembretes, backups rodam 1 vez sÃ³
4. **Contexto cruzado** â€” "Aquele arquivo que vocÃª criou no tÃ³pico X" funciona
5. **Facilidade de setup** â€” SÃ³ um agente pra configurar

#### âŒ Desvantagens

1. **Contexto poluÃ­do** â€” Conversas de tÃ³picos diferentes se misturam no histÃ³rico
2. **Sem isolamento** â€” Se alguÃ©m faz merda num tÃ³pico, afeta todo o workspace
3. **Contexto explode rÃ¡pido** â€” MÃºltiplos tÃ³picos ativos = 100k tokens em dias
4. **Privacidade zero** â€” A Amora pode citar coisas de um tÃ³pico privado em outro pÃºblico
5. **Comportamento Ãºnico** â€” NÃ£o dÃ¡ pra ter "Amora TÃ©cnica" vs "Amora Criativa"

#### ðŸŽ¯ Quando usar

- **VocÃª Ã© o Ãºnico humano** usando os tÃ³picos
- Quer **continuidade total** entre conversas
- TÃ³picos sÃ£o **variaÃ§Ãµes do mesmo contexto** (projetos relacionados)
- NÃ£o se importa com **memory bleed** entre tÃ³picos

---

### ðŸŸ¢ Arquitetura 2: **Agentes Isolados por TÃ³pico**

**Como funciona:**
- **Cada tÃ³pico tem seu prÃ³prio agente** (`amora-curso`, `amora-suporte`, `amora-dev`)
- Cada agente tem:
  - **Workspace separado** (`/workspace-curso`, `/workspace-suporte`)
  - **MemÃ³ria isolada** (cada um tem seu `MEMORY.md`)
  - **Crons independentes** (cada um pode ter heartbeats diferentes)
  - **SOUL.md customizado** (comportamento especializado)

**Exemplo de config:**

```yaml
agents:
  # Agente do tÃ³pico "Curso OpenClaw"
  - id: amora-curso
    model: openai/gpt-4o
    workspaceDir: /root/.openclaw/workspace-curso
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2638"
              mode: all
  
  # Agente do tÃ³pico "Suporte"
  - id: amora-suporte
    model: openai/gpt-4o-mini  # Mais barato
    workspaceDir: /root/.openclaw/workspace-suporte
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2640"
              mode: all
  
  # Agente do tÃ³pico "Dev"
  - id: amora-dev
    model: openai/gpt-5.4  # Mais poderoso
    thinking: on
    workspaceDir: /root/.openclaw/workspace-dev
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2641"
              mode: all
```

#### âœ… Vantagens

1. **Isolamento total** â€” Cada tÃ³pico tem sua prÃ³pria sandbox
2. **EspecializaÃ§Ã£o** â€” Agente de suporte usa Haiku (barato), Dev usa Opus (poderoso)
3. **SOUL.md customizado** â€” "Amora Professora" no curso, "Amora DevOps" no suporte
4. **Privacidade** â€” Dados de um tÃ³pico **nunca vazam** para outro
5. **Contexto limpo** â€” Cada agente sÃ³ vÃª mensagens do seu tÃ³pico
6. **Controle granular** â€” Crons diferentes por agente (ex: heartbeat sÃ³ no suporte)
7. **Escalabilidade** â€” Adicionar novo tÃ³pico = novo agente, sem poluir os existentes

#### âŒ Desvantagens

1. **Zero continuidade** â€” Agentes nÃ£o sabem o que aconteceu em outros tÃ³picos
2. **Custo maior** â€” MÃºltiplos processos rodando (mais RAM, mais API calls)
3. **Crons duplicados** â€” Se 3 agentes tÃªm heartbeat, rodam 3x
4. **Setup complexo** â€” Precisa criar workspace + config pra cada agente
5. **Sem compartilhamento** â€” Arquivo criado no tÃ³pico X nÃ£o existe no Y

#### ðŸŽ¯ Quando usar

- **MÃºltiplos humanos** usando tÃ³picos diferentes
- Precisa de **privacidade entre tÃ³picos** (cliente A vs cliente B)
- Quer **comportamentos especializados** (suporte vs desenvolvimento)
- TÃ³picos tÃªm **contextos completamente diferentes**
- Quer **modelos diferentes por tÃ³pico** (Haiku no suporte, Opus no dev)

---

## ðŸ“Š ComparaÃ§Ã£o Direta

| Aspecto | MAIN Compartilhado | Agentes Isolados |
|---------|-------------------|------------------|
| **MemÃ³ria** | Compartilhada entre tÃ³picos | Isolada por tÃ³pico |
| **Workspace** | 1 Ãºnico workspace | 1 workspace por agente |
| **SOUL.md** | Comportamento global | Personalizado por tÃ³pico |
| **USER.md** | 1 humano, contexto unificado | Pode ter USER.md diferente |
| **TOOLS.md** | Ferramentas globais | Ferramentas por agente |
| **Crons** | Rodam 1x (compartilhados) | Rodam N vezes (por agente) |
| **Heartbeats** | 1 heartbeat global | 1 heartbeat por agente |
| **Contexto** | Cruza entre tÃ³picos | Nunca cruza |
| **Privacidade** | Zero â€” tudo vaza | Total â€” isolamento completo |
| **Custo (API)** | Mais barato | Mais caro |
| **Custo (RAM)** | 1 processo | N processos |
| **Setup** | Simples (1 agente) | Complexo (N agentes) |
| **Uso ideal** | Projetos relacionados | Contextos isolados |

---

## ðŸ› ï¸ Parte 5: ConfiguraÃ§Ã£o AvanÃ§ada

### HÃ­brido: MAIN + Agentes Especializados

VocÃª pode **misturar** as duas arquiteturas:

```yaml
agents:
  # Agente MAIN â€” responde no privado e no "Geral"
  - id: amora-main
    workspaceDir: /root/.openclaw/workspace-meu-agente
    activation:
      surfaces:
        - surface: telegram
          mode: mention  # PadrÃ£o: sÃ³ quando marcada
          overrides:
            - chat: "telegram:1983085858"  # Privado com Bruno
              mode: all
  
  # Agente especializado â€” sÃ³ no tÃ³pico "Curso"
  - id: amora-curso
    model: openai/gpt-4o
    workspaceDir: /root/.openclaw/workspace-curso
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2638"
              mode: all
  
  # Agente especializado â€” sÃ³ no tÃ³pico "Suporte"
  - id: amora-suporte
    model: openai/gpt-4o-mini
    workspaceDir: /root/.openclaw/workspace-suporte
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2640"
              mode: all
```

**Vantagens:**
- MAIN mantÃ©m contexto pessoal (privado com vocÃª)
- Agentes especializados ficam isolados
- Melhor dos dois mundos

---

## ðŸ§  Parte 6: Impacto na MemÃ³ria e Contexto

### CenÃ¡rio 1: MAIN Compartilhado

**Estrutura de memÃ³ria:**

```
/root/.openclaw/workspace-meu-agente/
â”œâ”€â”€ MEMORY.md               â† Contexto global (lido em TODAS sessÃµes)
â”œâ”€â”€ memory/
â”‚   â”œâ”€â”€ 2026-02-25.md       â† Log diÃ¡rio (mistura TODOS os tÃ³picos)
â”‚   â”œâ”€â”€ 2026-02-26.md
```

**Quando a Amora responde no tÃ³pico "Curso":**
1. LÃª `MEMORY.md` (contexto global)
2. LÃª `memory/2026-02-25.md` (conversas de TODOS os tÃ³picos)
3. Responde com **contexto completo**

**Problema:**
- Se vocÃª falou sobre "projeto secreto X" no tÃ³pico "Dev" de manhÃ£
- E alguÃ©m pergunta no tÃ³pico "Curso" Ã  tarde
- A Amora **pode citar o projeto secreto** (memory bleed)

---

### CenÃ¡rio 2: Agentes Isolados

**Estrutura de memÃ³ria:**

```
/root/.openclaw/workspace-curso/
â”œâ”€â”€ MEMORY.md               â† Contexto APENAS do curso
â”œâ”€â”€ memory/
â”‚   â”œâ”€â”€ 2026-02-25.md       â† Log APENAS do tÃ³pico Curso

/root/.openclaw/workspace-suporte/
â”œâ”€â”€ MEMORY.md               â† Contexto APENAS do suporte
â”œâ”€â”€ memory/
â”‚   â”œâ”€â”€ 2026-02-25.md       â† Log APENAS do tÃ³pico Suporte
```

**Quando amora-curso responde:**
1. LÃª `MEMORY.md` do workspace-curso
2. LÃª `memory/2026-02-25.md` do workspace-curso
3. **NÃ£o tem acesso** ao workspace-suporte

**BenefÃ­cio:**
- Zero vazamento de contexto
- Cada agente sÃ³ sabe o que aconteceu no seu tÃ³pico

---

## ðŸ”„ Parte 7: Impacto nos Crons

### MAIN Compartilhado

```yaml
# /root/.openclaw/config.yaml
cron:
  jobs:
    - name: "Heartbeat Global"
      schedule:
        kind: every
        everyMs: 1800000  # 30 min
      payload:
        kind: systemEvent
        text: "Read HEARTBEAT.md if it exists..."
      sessionTarget: main
      delivery:
        mode: announce
        channel: telegram
        to: "1983085858"  # Privado com Bruno
```

**Como funciona:**
- Roda **1 vez a cada 30 min**
- Usa o **workspace global** (`/workspace-meu-agente`)
- Pode checar coisas de **todos os tÃ³picos** (emails, calendÃ¡rio, etc.)
- Economiza API calls (1 heartbeat vs 3)

---

### Agentes Isolados

```yaml
cron:
  jobs:
    # Heartbeat do agente "Curso"
    - name: "Heartbeat Curso"
      schedule:
        kind: every
        everyMs: 3600000  # 60 min
      payload:
        kind: agentTurn
        message: "Checar se tem novas perguntas no curso"
        agentId: amora-curso
      sessionTarget: isolated
      delivery:
        mode: announce
        channel: telegram
        to: "-1001234567890:topic:2638"
    
    # Heartbeat do agente "Suporte"
    - name: "Heartbeat Suporte"
      schedule:
        kind: every
        everyMs: 1800000  # 30 min
      payload:
        kind: agentTurn
        message: "Checar tickets pendentes"
        agentId: amora-suporte
      sessionTarget: isolated
      delivery:
        mode: announce
        channel: telegram
        to: "-1001234567890:topic:2640"
```

**Como funciona:**
- Cada agente tem **seu prÃ³prio heartbeat**
- Rodam em **workspaces separados**
- **Mais API calls**, mas **contexto focado**

---

## ðŸ§ª Parte 8: Casos de Uso Reais

### Caso 1: Freelancer com MÃºltiplos Clientes

**Problema:** Precisa separar contexto de cada cliente (privacidade).

**SoluÃ§Ã£o:** Agentes isolados

```yaml
agents:
  - id: amora-cliente-a
    workspaceDir: /workspace-cliente-a
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2638"
              mode: all
  
  - id: amora-cliente-b
    workspaceDir: /workspace-cliente-b
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2640"
              mode: all
```

**BenefÃ­cios:**
- Cliente A **nunca vÃª** dados do Cliente B
- SOUL.md customizado por cliente (ex: "Fale formal com Cliente A")
- Modelos diferentes (Haiku pra suporte, Opus pra dev)

---

### Caso 2: Projetos Pessoais Relacionados

**Problema:** VocÃª trabalha em 3 projetos, mas sÃ£o todos seus (ex: blog, app, curso).

**SoluÃ§Ã£o:** MAIN compartilhado

```yaml
agents:
  - id: amora-main
    workspaceDir: /workspace-meu-agente
    activation:
      surfaces:
        - surface: telegram
          mode: mention
          overrides:
            - chat: "telegram:-1001234567890:topic:1"    # Blog
              mode: all
            - chat: "telegram:-1001234567890:topic:2"    # App
              mode: all
            - chat: "telegram:-1001234567890:topic:3"    # Caso 3: HÃ­brido â€” Pessoal + Profissional

**Problema:** VocÃª quer **privacidade** entre trabalho e vida pessoal.

**SoluÃ§Ã£o:** HÃ­brido

```yaml
agents:
  # Agente pessoal â€” privado + tÃ³pico "Vida"
  - id: amora-pessoal
    workspaceDir: /workspace-pessoal
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:1983085858"                # Privado
              mode: all
            - chat: "telegram:-1001234567890:topic:1"    # TÃ³pico "Vida"
              mode: all
  
  # Agente profissional â€” tÃ³pico "Trabalho"
  - id: amora-trabalho
    model: openai/gpt-5.4
    workspaceDir: /workspace-trabalho
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2"    # TÃ³pico "Trabalho"
              mode: all
```

**BenefÃ­cios:**
- Zero vazamento entre vida pessoal e trabalho
- Modelos diferentes (Haiku pessoal, Opus profissional)
- Comportamento especializado (SOUL.md diferente)

---

## ðŸš¨ Parte 9: Armadilhas Comuns

### Armadilha 1: Misturar Chat IDs

**Erro:**
```yaml
- chat: "telegram:-1001234567890"  # ID do grupo (sem :topic:)
  mode: all
```

**Resultado:** Amora responde em **TODOS os tÃ³picos** do grupo (caos).

**CorreÃ§Ã£o:**
```yaml
- chat: "telegram:-1001234567890:topic:2638"  # ID especÃ­fico do tÃ³pico
  mode: all
```

---

### Armadilha 2: Esquecer de Tornar o Bot Admin

**Erro:** Adicionar bot ao grupo mas **nÃ£o dar permissÃ£o de admin**.

**Resultado:** Bot nÃ£o consegue ler mensagens em tÃ³picos (sÃ³ no "Geral").

**CorreÃ§Ã£o:**
1. ConfiguraÃ§Ãµes do grupo â†’ **Administradores**
2. Adicione o bot
3. Ative permissÃ£o: **"Gerenciar TÃ³picos"**

---

### Armadilha 3: Agentes Isolados Compartilhando Workspace

**Erro:**
```yaml
agents:
  - id: amora-curso
    workspaceDir: /workspace-meu-agente  # âŒ Mesmo workspace
  - id: amora-suporte
    workspaceDir: /workspace-meu-agente  # âŒ Mesmo workspace
```

**Resultado:** Agentes pisam um no outro (arquivos sobrescritos, memÃ³ria compartilhada).

**CorreÃ§Ã£o:**
```yaml
agents:
  - id: amora-curso
    workspaceDir: /workspace-curso  # âœ… Workspace isolado
  - id: amora-suporte
    workspaceDir: /workspace-suporte  # âœ… Workspace isolado
```

---

### Armadilha 4: Crons no Agente Errado

**Erro:** Criar cron para `amora-curso` mas tentar acessar dados de `amora-suporte`.

**Resultado:** Cron nÃ£o encontra os arquivos (workspaces diferentes).

**CorreÃ§Ã£o:** Certifique-se que o cron **usa o agentId correto**:

```yaml
cron:
  jobs:
    - name: "Checar curso"
      payload:
        kind: agentTurn
        message: "Checar novas perguntas"
        agentId: amora-curso  # âœ… Usa o workspace correto
```

---

## ðŸ“ Parte 10: Checklist de DecisÃ£o

### Perguntas pra se fazer:

1. **Privacidade Ã© crÃ­tica?**
   - âŒ NÃ£o â†’ MAIN compartilhado
   - âœ… Sim â†’ Agentes isolados

2. **Os tÃ³picos tÃªm contextos relacionados?**
   - âœ… Sim (ex: projetos pessoais) â†’ MAIN compartilhado
   - âŒ NÃ£o (ex: clientes diferentes) â†’ Agentes isolados

3. **Precisa de comportamentos especializados?**
   - âŒ NÃ£o â†’ MAIN compartilhado
   - âœ… Sim (ex: Amora Professora vs DevOps) â†’ Agentes isolados

4. **Quer economizar recursos (RAM/API)?**
   - âœ… Sim â†’ MAIN compartilhado
   - âŒ NÃ£o â†’ Agentes isolados

5. **Contexto cruzado Ã© Ãºtil ou perigoso?**
   - Ãštil (ex: "lembra daquela ideia?") â†’ MAIN compartilhado
   - Perigoso (ex: vazamento de dados) â†’ Agentes isolados

---

## ðŸŽ¯ RecomendaÃ§Ã£o Final

**Para iniciantes:**
- Comece com **MAIN compartilhado**
- Ã‰ mais simples, econÃ´mico, e "just works"
- Migre pra isolado quando sentir a dor (poluiÃ§Ã£o de contexto, privacidade)

**Para avanÃ§ados:**
- Use **agentes isolados** desde o inÃ­cio
- Custa mais, mas escala melhor
- Especialmente se trabalha com mÃºltiplos clientes/projetos

**Para a maioria:**
- **HÃ­brido** Ã© o sweet spot
- MAIN pra contexto pessoal
- Isolados pra contextos profissionais/privados

---

## ðŸ› ï¸ Parte 11: Exemplo de Setup Completo

### Estrutura de Grupo

```
Amora HQ (Telegram Group)
â”œâ”€â”€ ðŸ“Œ Geral (id: 1) â€” sÃ³ quando marcada
â”œâ”€â”€ ðŸ“š Curso OpenClaw (id: 2638) â€” agente isolado, responde tudo
â”œâ”€â”€ ðŸ› ï¸ Suporte (id: 2640) â€” agente isolado, responde tudo
â””â”€â”€ ðŸ’¬ Bruno Privado (chat: 1983085858) â€” MAIN, responde tudo
```

### Config Completo

```yaml
# /root/.openclaw/config.yaml

agents:
  # Agente MAIN â€” privado com Bruno
  - id: amora-main
    model: openai/gpt-4o
    thinking: off
    workspaceDir: /root/.openclaw/workspace-meu-agente
    activation:
      surfaces:
        - surface: telegram
          mode: mention
          overrides:
            - chat: "telegram:1983085858"  # Privado
              mode: all

  # Agente do Curso â€” isolado
  - id: amora-curso
    model: openai/gpt-4o
    thinking: off
    workspaceDir: /root/.openclaw/workspace-curso
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2638"
              mode: all

  # Agente de Suporte â€” isolado, modelo barato
  - id: amora-suporte
    model: openai/gpt-4o-mini
    thinking: off
    workspaceDir: /root/.openclaw/workspace-suporte
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1001234567890:topic:2640"
              mode: all

cron:
  jobs:
    # Heartbeat MAIN â€” sÃ³ pro Bruno
    - name: "Heartbeat Pessoal"
      schedule:
        kind: every
        everyMs: 1800000  # 30 min
      payload:
        kind: systemEvent
        text: "Read HEARTBEAT.md..."
      sessionTarget: main
      delivery:
        mode: announce
        channel: telegram
        to: "1983085858"
    
    # Heartbeat Curso â€” checks a cada 1h
    - name: "Heartbeat Curso"
      schedule:
        kind: every
        everyMs: 3600000
      payload:
        kind: agentTurn
        message: "Checar novas dÃºvidas no curso"
        agentId: amora-curso
      sessionTarget: isolated
      delivery:
        mode: announce
        channel: telegram
        to: "-1001234567890:topic:2638"
```

### Estrutura de Workspaces

```
/root/.openclaw/
â”œâ”€â”€ workspace-meu-agente/           # MAIN (pessoal)
â”‚   â”œâ”€â”€ SOUL.md                # "Seja Ã­ntima, casual, use gÃ­rias"
â”‚   â”œâ”€â”€ USER.md                # Contexto do Bruno
â”‚   â”œâ”€â”€ MEMORY.md              # MemÃ³ria pessoal
â”‚   â”œâ”€â”€ memory/
â”‚   â”‚   â””â”€â”€ 2026-02-25.md
â”‚   â””â”€â”€ HEARTBEAT.md           # Checks pessoais
â”‚
â”œâ”€â”€ workspace-curso/           # Agente isolado
â”‚   â”œâ”€â”€ SOUL.md                # "Seja professora, didÃ¡tica, paciente"
â”‚   â”œâ”€â”€ USER.md                # Perfil dos alunos
â”‚   â”œâ”€â”€ MEMORY.md              # DÃºvidas comuns, decisÃµes do curso
â”‚   â”œâ”€â”€ memory/
â”‚   â”‚   â””â”€â”€ 2026-02-25.md
â”‚   â””â”€â”€ HEARTBEAT.md           # Checar novas perguntas
â”‚
â””â”€â”€ workspace-suporte/         # Agente isolado
    â”œâ”€â”€ SOUL.md                # "Seja tÃ©cnica, objetiva, rÃ¡pida"
    â”œâ”€â”€ USER.md                # Perfil dos clientes
    â”œâ”€â”€ MEMORY.md              # Tickets resolvidos, bugs conhecidos
    â”œâ”€â”€ memory/
    â”‚   â””â”€â”€ 2026-02-25.md
    â””â”€â”€ HEARTBEAT.md           # Checar tickets pendentes
```

---

## ðŸŽ“ ConclusÃ£o

### Resumo do Resumo

**MAIN Compartilhado = MemÃ³ria Total, Zero Privacidade**
- Use quando contexto cruzado Ã© desejÃ¡vel
- Economiza recursos
- Ideal pra projetos pessoais relacionados

**Agentes Isolados = Privacidade Total, Zero MemÃ³ria Cruzada**
- Use quando contexto cruzado Ã© perigoso
- Custa mais recursos
- Ideal pra mÃºltiplos clientes/contextos

**HÃ­brido = Melhor dos Dois Mundos**
- MAIN pra uso pessoal
- Isolados pra contextos profissionais
- Recomendado pra maioria dos casos

---

**Proximos Passos:**
1. Decidir qual arquitetura usar
2. Criar os tÃ³picos no Telegram
3. Configurar o `config.yaml`
4. Testar cada tÃ³pico
5. Ajustar SOUL.md de cada agente
6. Configurar crons (se necessÃ¡rio)

**DÃºvidas?**
- Revise a seÃ§Ã£o de **Checklist de DecisÃ£o**
- Teste com 1-2 tÃ³picos primeiro
- Migre gradualmente se precisar mudar de arquitetura

---

**Ãšltima dica:** NÃ£o existe "arquitetura errada" â€” existe a que funciona **pra vocÃª**. Teste, aprenda, ajuste. Ã‰ assim que se constrÃ³i um sistema sob medida.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
