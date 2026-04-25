# Prompt â€” MÃ³dulo 4: Sistema de MemÃ³ria (Atualizado MarÃ§o 2026)

> Cole este prompt no chat do seu OpenClaw depois de assistir o MÃ³dulo 4.
> Anexe junto os arquivos: `prds/memory-architecture.md`, `templates/MEMORY-template.md`, `templates/HEARTBEAT-template.md` e a pasta `templates/memory/`

---

Acabei de assistir o MÃ³dulo 4 do curso sobre memÃ³ria. Leia o PRD de arquitetura de memÃ³ria e me guie na implementaÃ§Ã£o.

**O que preciso que vocÃª faÃ§a:**

1. **Me explique como funciona sua memÃ³ria** â€” quero entender o problema (Alzheimer entre sessÃµes) e a soluÃ§Ã£o (memÃ³ria em camadas)

2. **Crie a estrutura de memÃ³ria** organizada em subpastas:
   ```
   memory/
   â”œâ”€â”€ MEMORY.md              â† Ã­ndice geral (Ãºnico arquivo sempre carregado)
   â”œâ”€â”€ context/
   â”‚   â”œâ”€â”€ decisions.md       â† regras permanentes e irreversÃ­veis
   â”‚   â”œâ”€â”€ lessons.md         â† erros e aprendizados
   â”‚   â”œâ”€â”€ people.md          â† equipe, parceiros, contatos
   â”‚   â””â”€â”€ business-context.md
   â”œâ”€â”€ projects/              â† um arquivo por projeto ativo
   â”œâ”€â”€ sessions/              â† diÃ¡rio: um arquivo por dia (YYYY-MM-DD.md)
   â””â”€â”€ integrations/          â† mapa de ferramentas, IDs, acessos
   ```

3. **Configure a regra de extraÃ§Ã£o antes de compactaÃ§Ã£o** â€” NUNCA compactar sem extrair liÃ§Ãµes, decisÃµes e pendÃªncias primeiro. Isso Ã© INVIOLÃVEL.

4. **Explique o que Ã© carregado vs. buscado sob demanda:**
   - Carregado sempre: `SOUL.md`, `USER.md`, `AGENTS.md`, `MEMORY.md`, sessÃµes de hoje + ontem
   - Buscado sob demanda: todos os outros arquivos via `memory_search`

5. **Configure o memory search** â€” busca semÃ¢ntica nativa (nÃ£o precisa de chave de API externa):
   - `memory_search()` para busca por significado em todos os arquivos
   - `memory_get()` para puxar sÃ³ o trecho especÃ­fico (econÃ´mico em tokens)
   - Funciona nativamente desde MarÃ§o 2026 â€” sem OpenAI/Gemini embedding

6. **Ensine como salvar corretamente** â€” mostre exemplos prÃ¡ticos:
   - âŒ "Lembra disso" (mental note â€” morre na prÃ³xima sessÃ£o)
   - âœ… "Salva em memory/context/decisions.md como decisÃ£o permanente"
   - âœ… "Registra em memory/projects/meu-projeto.md"

7. **Configure feedback loops** â€” JSONs em `memory/feedback/` que capturam approve/reject:
   - O agente consulta ANTES de sugerir novamente
   - NÃ£o repete erros â€” evoluÃ§Ã£o real

**Regras:**
- Me explique cada arquivo e PRA QUE SERVE antes de criar
- Me mostre um exemplo prÃ¡tico de como uma decisÃ£o vira memÃ³ria permanente
- Regra INVIOLÃVEL: antes de CADA compactaÃ§Ã£o, rodar checklist de extraÃ§Ã£o (lessons, decisions, people, projects, pending)
- Teste a busca semÃ¢ntica: feche a sessÃ£o, abra uma nova e pergunte algo que foi salvo

**CritÃ©rio rÃ¡pido â€” o que vai onde:**

| O que Ã© | Arquivo |
|---------|---------|
| DecisÃ£o que nÃ£o pode mudar | `memory/context/decisions.md` |
| Erro que nÃ£o pode repetir | `memory/context/lessons.md` |
| Status de projeto | `memory/projects/nome-do-projeto.md` |
| Aguardando seu input | `memory/pending.md` |
| O que aconteceu hoje | `memory/sessions/YYYY-MM-DD.md` |

Vamos criar sua memÃ³ria?


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
