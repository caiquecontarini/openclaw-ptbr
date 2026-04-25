# Prompt â€” MÃ³dulo 8: Multi-Agentes

> Cole este prompt no chat do seu OpenClaw depois de assistir o MÃ³dulo 8.
> Anexe junto o arquivo: `prds/multi-agent-setup.md`
> âš ï¸ Nota: `shared/lessons/` referenciado abaixo = `shared/lessons.md` na estrutura real.

---

Acabei de assistir o MÃ³dulo 8 do curso sobre multi-agentes. Leia o PRD e me guie na criaÃ§Ã£o do meu primeiro time de agentes.

**O que preciso que vocÃª faÃ§a:**

1. **Avalie se eu preciso de multi-agentes agora** â€” se meu uso ainda Ã© simples, me diga honestamente que Ã© cedo. Multi-agentes sem fundaÃ§Ã£o = bagunÃ§a.

2. **Se fizer sentido, me ajude a criar 1-2 agentes extras:**
   - Me faÃ§a perguntas sobre que tarefas eu quero delegar
   - Crie o SOUL.md e AGENTS.md de cada agente
   - Configure no gateway (agents.list)

3. **Implemente o sistema de leveling:**
   - L1 Observer â†’ L2 Contributor â†’ L3 Operator â†’ L4 Trusted
   - Todo agente novo comeÃ§a em L1 (output revisado por mim)
   - Me explique como promover e rebaixar

4. **Configure o contexto compartilhado:**
   - TEAM.md â€” registry de todos os agentes
   - shared/outputs/ â€” resultados compartilhados
   - shared/lessons/ â€” aprendizados do time

5. **Defina a economia e demonstre o ciclo completo:**
   - Qual modelo pra cada agente (modelo principal: GPT-4o via ChatGPT; fallback: GPT-4o-mini)
   - Quando spawnar sub-agents vs fazer na main session
   - Me demonstre ao vivo o ciclo de orquestraÃ§Ã£o com sessions_yield:
     1. Spawna um sub-agent com sessions_spawn para uma task simples
     2. Chama sessions_yield para encerrar o turno limpo
     3. Mostra o resultado chegando na prÃ³xima mensagem
   - Explique a diferenÃ§a de tokens com e sem sessions_yield

6. **ACP bind (v2026.4+):** Se eu quiser vincular um agente secundÃ¡rio a um topic Telegram diferente do meu agente principal, me mostre o comando `/acp spawn codex --bind here`. Isso cria um agente isolado naquele topic, Ãºtil para um "agente escravo" que sÃ³ responde num topic especÃ­fico. Explique quando usar isso vs. sessions_spawn.

**Regras:**
- Menos Ã© mais â€” 2 agentes bem feitos > 6 agentes bagunÃ§ados
- Eu (humano) sempre no loop de decisÃµes importantes
- No final, me mostre o time completo e quem faz o quÃª

Vamos montar o time?


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
