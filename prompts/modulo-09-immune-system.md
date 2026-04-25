# Prompt â€” MÃ³dulo 9: Sistema ImunolÃ³gico

> Cole este prompt no chat do seu OpenClaw depois de assistir o MÃ³dulo 9.
> Anexe junto o arquivo: `prds/immune-system.md`

---

Acabei de assistir o MÃ³dulo 9 do curso sobre o sistema imunolÃ³gico. "Agents are 30% of the work. The other 70% is the immune system." Leia o PRD e me guie.

**O que preciso que vocÃª faÃ§a:**

1. **Watchdog de crons** â€” Configure um cron que monitora se os outros crons estÃ£o executando. Se algum falhar, retry automÃ¡tico atÃ© 3x. Se falhar 3x, me avisa.

2. **Feedback Loops** â€” Me ajude a configurar um sistema de approve/reject:
   - Quando vocÃª me sugerir algo e eu rejeitar, anote o motivo
   - Consulte essas anotaÃ§Ãµes antes de sugerir novamente
   - Me mostre como isso funciona na prÃ¡tica

3. **Monitoramento de custos:**
   - Configure o split de modelos (GPT-4o-mini pra heartbeats, GPT-4o pra crons e interaÃ§Ã£o direta)
   - Configure rate limits e budgets pra prevenir runaway
   - Me mostre quanto estou gastando por dia/semana

4. **Audit de seguranÃ§a periÃ³dico:**
   - Configure um cron semanal de security audit
   - Rode um agora pra eu ver o resultado

5. **Backup antes de mudanÃ§as:**
   - Crie uma regra: antes de qualquer mudanÃ§a estrutural, salvar backup + ROLLBACK.md
   - Me mostre como reverter se algo der errado

6. **openclaw secrets audit (v2026.3.2+):** Rode `openclaw secrets audit` para checar se hÃ¡ credenciais expostas no workspace. Isso Ã© crÃ­tico antes de compartilhar arquivos ou fazer backup.

7. **Sub-agents: sessions_yield (v2026.3.13+):** Quando spawnar sub-agents, use sessions_yield para encerrar o turno limpo e receber os resultados na prÃ³xima mensagem â€” nunca deixe um sub-agent no limbo silencioso.

**Regras:**
- Esse mÃ³dulo Ã© o que separa "tÃ´ brincando" de "tÃ´ em produÃ§Ã£o"
- Me explique cada proteÃ§Ã£o e qual problema ela previne
- No final, rode um health check completo e me dÃª o score

Vamos construir a imunidade?


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
