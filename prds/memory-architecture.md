# PRD: Arquitetura de MemÃ³ria (Atualizado MarÃ§o 2026)

> Jogue este arquivo no agente: "Implementa esta arquitetura de memÃ³ria"

## Contexto

Agentes AI esquecem tudo a cada sessÃ£o. Sem memÃ³ria estruturada, vocÃª repete contexto todo dia. Esta arquitetura resolve isso com uma estrutura em subpastas que permite busca semÃ¢ntica precisa.

**Novidade MarÃ§o 2026:** `memory_search` agora funciona nativamente â€” sem precisar de chave de API externa (OpenAI/Gemini). A busca por embedding Ã© built-in.

**âš ï¸ Breaking v2026.3.13 â€” MEMORY.md obrigatÃ³rio em maiÃºsculas:** O agente carrega apenas um arquivo de memÃ³ria raiz. `MEMORY.md` (maiÃºsculas) tem prioridade; `memory.md` (minÃºsculas) sÃ³ Ã© usado quando `MEMORY.md` nÃ£o existe. Se vocÃª criou `memory.md` antes da v3.13, renomeie:

```bash
mv memory.md MEMORY.md
```

**Comportamento pÃ³s-compaction (v2026.3.13):** ApÃ³s compaction automÃ¡tica, o Ã­ndice de memÃ³ria Ã© reindexado de forma assÃ­ncrona. Se o agente parecer "esquecer" algo logo apÃ³s uma compaction â€” aguarde alguns segundos e tente `memory_search` novamente. Isso Ã© normal e temporÃ¡rio.

## O que o agente carrega vs. busca

| Sempre carregado na sessÃ£o | Buscado sob demanda |
|---------------------------|---------------------|
| SOUL.md, USER.md, AGENTS.md | memory/context/decisions.md |
| MEMORY.md (Ã­ndice) | memory/context/lessons.md |
| memory/sessions/ (hoje + ontem) | memory/projects/*.md |
| | skills/ (qualquer skill) |

## Tarefas

### 1. Criar estrutura de subpastas

```bash
mkdir -p memory/context memory/projects memory/sessions memory/integrations
```

### 2. Criar os arquivos de contexto

| Arquivo | PropÃ³sito |
|---------|-----------|
| `memory/context/decisions.md` | DecisÃµes permanentes e irreversÃ­veis |
| `memory/context/lessons.md` | LiÃ§Ãµes aprendidas, erros, padrÃµes |
| `memory/context/people.md` | Equipe, parceiros, contatos â€” como interagir com cada um |
| `memory/context/business-context.md` | Contexto do negÃ³cio, produtos, clientes |

**RetenÃ§Ã£o de liÃ§Ãµes:**
- ðŸ”’ EstratÃ©gicas = permanentes (filosofia, padrÃµes de arquitetura)
- â³ TÃ¡ticas = expiram em 30 dias (bugs, workarounds temporÃ¡rios)

### 3. Criar projetos individuais

Em vez de um `projects.md` gigante, um arquivo por projeto:

```
memory/projects/
â”œâ”€â”€ meu-saas.md          â† MRR atual, prÃ³ximas features, pendÃªncias
â”œâ”€â”€ lanÃ§amento-maio.md   â† status, checklist, responsÃ¡veis
â””â”€â”€ produto-b.md
```

**Por que separado?** A busca semÃ¢ntica acha o projeto certo sem trazer contexto de outros projetos junto.

### 4. Criar MEMORY.md (Ã­ndice)

Na raiz do workspace. Ã‰ o mapa â€” nÃ£o duplica conteÃºdo, apenas referencia:

```markdown
# MEMORY.md

## Contexto
- DecisÃµes: memory/context/decisions.md
- LiÃ§Ãµes: memory/context/lessons.md
- Pessoas: memory/context/people.md

## Projetos ativos
- [Nome do Projeto]: memory/projects/nome.md

## IntegraÃ§Ãµes
- Mapa de ferramentas: memory/integrations/
```

### 5. Configurar ciclo de memÃ³ria no AGENTS.md

```
Regras de memÃ³ria:
1. Notas diÃ¡rias: criar memory/sessions/YYYY-MM-DD.md a cada sessÃ£o relevante
2. Projetos: um arquivo separado por projeto em memory/projects/
3. INVIOLÃVEL: antes de compactar â†’ extrair liÃ§Ãµes, decisÃµes e pendÃªncias
4. Feedback: ao rejeitar sugestÃ£o â†’ salvar motivo em memory/feedback/
```

### 6. Configurar busca semÃ¢ntica

O agente usa dois tools:
- `memory_search("termo")` â€” busca semÃ¢ntica em todos os arquivos (~400 tokens/chunk)
- `memory_get("arquivo.md", linha_inÃ­cio)` â€” lÃª sÃ³ o trecho relevante

**Funciona nativamente** desde MarÃ§o 2026. NÃ£o precisa de chave externa.

### 7. Configurar feedback loops (avanÃ§ado)

```
memory/feedback/
â”œâ”€â”€ content.json    â† sugestÃµes de conteÃºdo aprovadas/rejeitadas
â”œâ”€â”€ tasks.json      â† preferÃªncias de execuÃ§Ã£o de tarefas
â””â”€â”€ tone.json       â† ajustes de tom e estilo
```

Formato:
```json
{
  "entries": [
    {
      "date": "2026-03-14",
      "context": "Sugeri post LinkedIn com linguagem formal",
      "decision": "reject",
      "reason": "Tom muito corporativo â€” prefere direto e conversacional",
      "tags": ["linkedin", "tom"]
    }
  ]
}
```

### 8. Configure dreaming (experimental, opt-in)

O OpenClaw tem um sistema de consolidaÃ§Ã£o automÃ¡tica de memÃ³ria que funciona em segundo plano â€” o **Dreaming**.

**As 3 fases do ciclo:**

| Fase | O que faz | Escreve em MEMORY.md? |
|------|-----------|----------------------|
| ðŸŒ… **Light** | Coleta sinais recentes das sessÃµes e notas diÃ¡rias, separa ruÃ­do do relevante | NÃ£o |
| ðŸŒ™ **Deep** | Pontua candidatos e promove os melhores para `MEMORY.md` | âœ… Sim |
| ðŸ’¤ **REM** | Extrai temas recorrentes e gera resumo narrativo | NÃ£o |

**Output:** Depois de cada ciclo, escreve um **Dream Diary** em `DREAMS.md` (ou `dreams.md`). Ã‰ leitura humana â€” nÃ£o Ã© fonte de promoÃ§Ã£o.

**Como ativar:**
- Na sessÃ£o: `/dreaming` â€” roda o ciclo completo
- `/dreaming --dry-run` â€” mostra o que faria sem executar

**Nota:** Dreaming vem desabilitado por padrÃ£o. Ative se quiser que o agente promova memÃ³rias automaticamente entre sessÃµes.

## Como pedir para salvar

| âŒ NÃ£o funciona | âœ… Funciona |
|----------------|------------|
| "Lembra disso" | "Salva em memory/context/decisions.md" |
| "Guarda essa info" | "Adiciona em memory/projects/nome.md" |
| "NÃ£o esquece que..." | "Registra em memory/sessions/hoje como liÃ§Ã£o" |

## Resultado Esperado

1. Estrutura criada com subpastas organizadas
2. MEMORY.md como Ã­ndice apontando para tudo
3. Teste: fechar sessÃ£o â†’ abrir nova â†’ perguntar algo salvo â†’ agente encontra via memory_search


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
