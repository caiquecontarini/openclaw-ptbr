# Prompt â€” MÃ³dulo 5: IntegraÃ§Ãµes, Ferramentas e Crons

> Cole este prompt no chat do seu OpenClaw depois de assistir o MÃ³dulo 5.
> Anexe junto os arquivos: `prds/integrations-setup.md`, `configs/cron-examples.md`

---

Acabei de assistir o MÃ³dulo 5 do curso sobre integraÃ§Ãµes e crons. Leia o PRD de integraÃ§Ãµes e me guie.

**O que preciso que vocÃª faÃ§a:**

1. **Analise meu perfil** â€” baseado no que vocÃª jÃ¡ sabe sobre mim (USER.md), me recomende as 3-5 integraÃ§Ãµes mais Ãºteis pra comeÃ§ar

2. **Me guie na instalaÃ§Ã£o** de cada integraÃ§Ã£o, uma por vez:
   - Me explique o que ela faz e por que Ã© Ãºtil
   - Me ajude a configurar a API key de forma segura
   - Teste se funcionou

3. **Configure pelo menos 2 crons:**
   - Um lembrete/agenda (pra eu ver funcionando)
   - Um report automÃ¡tico (daily briefing ou mÃ©tricas)
   - Use SEMPRE: `sessionTarget: isolated` + `agentTurn` + `announce` (isso Ã© crÃ­tico pra funcionar!)

4. **Me explique os erros comuns:**
   - Por que `systemEvent` na main session nÃ£o funciona como esperado
   - Por que crons no mesmo horÃ¡rio causam problemas
   - Como config.patch afeta crons rodando

**Regras:**
- Comece com integraÃ§Ãµes simples (calendÃ¡rio, clima) antes das complexas
- Ferramentas de mÃ­dia sÃ£o built-in: `image_generate`, `video_generate` e `music_generate` estÃ£o disponÃ­veis de graÃ§a no OpenClaw â€” nÃ£o precisa de skill separada
- TODAS as credenciais vÃ£o no 1Password â€” zero hardcode nos arquivos
- Cuidado: systemd override sobrescreve .env â€” atualizar AMBOS ao trocar credenciais
- No final, me mostre os crons ativos e quando vÃ£o rodar

**Dica de produÃ§Ã£o:**
- Use Telegram com grupo + tÃ³picos como hub central
- Cada cron entrega no tÃ³pico certo â€” zero ruÃ­do
- Crons usam o mesmo modelo primÃ¡rio do agente â€” nÃ£o trocar modelo no cron isolado (causa `LiveSessionModelSwitchError`)
- Para produÃ§Ã£o do curso, mantenha a stack padrÃ£o em OpenAI (`openai/gpt-5.4`, `openai/gpt-4o`, `openai/gpt-4o-mini`)
- Use OpenRouter como camada de experimentaÃ§Ã£o para testar outros LLMs ou opÃ§Ãµes econÃ´micas sem trocar a narrativa principal do setup

**Comandos Ãºteis:**
```
openclaw channels status --probe
openclaw models fallbacks add <model>
openclaw models aliases add <alias> <model>
```

> **ðŸ“¡ Posicionamento de modelos (2026.4+):** No curso, OpenAI continua sendo a stack padrÃ£o. OpenRouter entra como caminho recomendado para experimentar outros modelos, por exemplo `openrouter/minimax/minimax-m2.7`, sem substituir o setup principal. Crons devem usar o mesmo modelo primÃ¡rio do agente que os dispatcha.

Vamos conectar ao mundo real?


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
