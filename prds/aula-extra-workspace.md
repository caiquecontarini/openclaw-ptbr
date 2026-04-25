# PRD â€” Aula Extra: Organize as Pastas do Seu Agente Para Escalar

> **Tipo:** Aula extra (material HTML + prompt de execuÃ§Ã£o)
> **NÃ­vel:** IntermediÃ¡rio
> **PrÃ©-requisito:** OpenClaw instalado, SOUL.md e USER.md configurados, pelo menos 1 semana de uso
> **Material:** `aula-extra-workspace-v2.html` (leitura) + prompt do aluno (execuÃ§Ã£o)

---

## ðŸŽ¯ O que essa aula entrega

O aluno lÃª o material HTML e depois cola o prompt no agente. O agente **executa** â€” nÃ£o explica, faz:

1. **DiagnÃ³stico** do workspace atual (o que estÃ¡ certo, o que estÃ¡ errado)
2. **CriaÃ§Ã£o** da estrutura de pastas completa (memory/, skills/, reports/, archive/)
3. **MigraÃ§Ã£o** de arquivos soltos para os destinos corretos
4. **AtualizaÃ§Ã£o dos arquivos raiz** â€” insere no TOOLS.md a tabela de "onde salvar cada output", atualiza MEMORY.md como Ã­ndice
5. **OrganizaÃ§Ã£o de skills** por categoria de trabalho (nÃ£o por ferramenta)
6. **ConfiguraÃ§Ã£o de projetos** â€” cada projeto aponta para sua fonte de verdade de tasks
7. **Teste de sanidade** â€” cria um output, salva no lugar certo, confirma que memory_search encontra

---

## ðŸ“‹ Problema que resolve

Workspace desorganizado causa:
- Agente nÃ£o sabe onde salvar outputs â†’ pergunta toda vez ou joga na raiz
- memory_search retorna lixo â†’ agente perde contexto entre sessÃµes
- Skills sem categoria â†’ impossÃ­vel auditar ou encontrar
- Arquivos raiz desatualizados â†’ agente age como se integraÃ§Ãµes/skills nÃ£o existissem
- Sem regra de destino â†’ cada sessÃ£o cria estrutura diferente

---

## ðŸ—ï¸ Estrutura-alvo que o prompt implementa

```
workspace/
â”œâ”€â”€ SOUL.md, IDENTITY.md, USER.md, MEMORY.md     â† 7 arquivos raiz (jÃ¡ existem)
â”œâ”€â”€ AGENTS.md, TOOLS.md, HEARTBEAT.md
â”‚
â”œâ”€â”€ memory/
â”‚   â”œâ”€â”€ context/         â† decisions.md, lessons.md, people.md
â”‚   â”œâ”€â”€ projects/        â† um .md por projeto ativo + _index.md
â”‚   â”œâ”€â”€ integrations/    â† credentials-map.md, acessos, IDs
â”‚   â””â”€â”€ sessions/        â† YYYY-MM-DD.md (diÃ¡rio de sessÃ£o)
â”‚
â”œâ”€â”€ skills/              â† subpastas por categoria de trabalho
â”‚   â”œâ”€â”€ {categoria}/     â† cada skill em {categoria}/SKILL.md
â”‚   â””â”€â”€ _registry.md     â† Ã­ndice por categoria
â”‚
â”œâ”€â”€ reports/             â† outputs consultÃ¡veis
â”‚   â”œâ”€â”€ business/
â”‚   â””â”€â”€ misc/
â”‚
â”œâ”€â”€ scripts/             â† scripts operacionais
â”œâ”€â”€ projects/            â† PRDs de projetos grandes
â””â”€â”€ archive/             â† rascunhos, temporÃ¡rios, obsoletos
```

---

## âœ… CritÃ©rios de sucesso

O prompt funcionou quando:

1. âœ… Nenhum arquivo solto na raiz alÃ©m dos 7 de identidade
2. âœ… Estrutura de pastas criada (memory/context, memory/projects, memory/sessions, skills/, reports/, archive/)
3. âœ… TOOLS.md contÃ©m tabela "Onde Salvar Cada Output"
4. âœ… MEMORY.md funciona como Ã­ndice (aponta para memory/, nÃ£o duplica conteÃºdo)
5. âœ… Skills organizadas por categoria com _registry.md
6. âœ… O agente salva um output no destino correto sem perguntar
7. âœ… memory_search encontra o output salvo

---

## ðŸ“ Regras do prompt

- O prompt **executa**, nÃ£o ensina. O material HTML jÃ¡ ensinou.
- Se o aluno jÃ¡ tem estrutura parcial â†’ o agente **adapta**, nÃ£o destrÃ³i
- Arquivos existentes sÃ£o **movidos**, nunca deletados
- Cada arquivo movido â†’ log de "de onde saiu â†’ pra onde foi â†’ por quÃª"
- A tabela de destinos no TOOLS.md Ã© **adaptada** ao contexto do aluno (categorias de reports)
- Skills com menos de 2 por categoria â†’ juntar em "general" atÃ© ter volume

---

## ðŸ”— Arquivos relacionados

- **Material HTML:** `reports/misc/aula-extra-workspace-v2.html`
- **Prompt do aluno:** `memory/curso-openclaw/prompts/aula-extra-workspace-prompt-aluno.md`
- **ReferÃªncia real:** Workspace da Amora (workspace-meu-agente)


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
