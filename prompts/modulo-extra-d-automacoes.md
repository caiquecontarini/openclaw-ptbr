# Prompt do Aluno: Automações Evolutivas

**Cole este prompt no chat com sua Amora:**

---

Amora, preciso da sua ajuda para transformar uma tarefa repetitiva em automação seguindo o ciclo de evolução.

**Tarefa que quero automatizar:**
[Descreva aqui — ex: "Fazer backup do Notion toda sexta", "Postar no LinkedIn toda segunda", "Gerar relatório de vendas semanal"]

**Me guia nos 5 estágios:**

1. **Manual Puro:**
   - Me ajuda a fazer a tarefa manualmente agora
   - Anotar os passos enquanto faço
   - Descobrir onde demora, onde posso errar

2. **Skill Documentada:**
   - Criar `skills/[nome-tarefa]/SKILL.md` com checklist completo
   - Incluir comandos, URLs, notas importantes
   - Deixar claro o suficiente pra eu fazer sem pensar

3. **Alias/Atalho:**
   - Criar script executável (`run.sh` ou `.py`)
   - Automatizar passos mecânicos (download, upload, processamento)
   - Manter decisões humanas (quando rodar, o que fazer com resultado)
   - Criar alias no `.bashrc` pra rodar rápido

4. **Heartbeat Check:**
   - Adicionar check no meu `HEARTBEAT.md`
   - Você me lembra quando tá na hora de fazer
   - Verificar última vez que rodou (se aplicável)

5. **Cron Automático:**
   - **(Só se fizer sentido!)** Criar cron job
   - Rodar sozinho no horário certo
   - Me avisar no Telegram quando terminar (sucesso ou erro)

**Contexto:**
- Frequência: [diário / semanal / mensal]
- Timing: [flexível / fixo — ex: "toda sexta 18h"]
- Passos: [manual / parcialmente automátivel / 100% automátivel]
- Importância: [se falhar, não é grave / crítico]

**Me ajuda a decidir:**
- Vale a pena automatizar completamente?
- Ou alias + heartbeat já resolve?
- Tem risco de over-engineering?

**Leia o guia completo em:**
`/root/.openclaw/workspace-curso-openclaw/prds/automacoes-evolutivas.md`

**Entregáveis esperados:**
1. ✅ `skills/[tarefa]/SKILL.md` documentado
2. ✅ Script executável testado
3. ✅ Alias criado no `.bashrc`
4. ✅ Check adicionado no `HEARTBEAT.md`
5. ✅ (Opcional) Cron configurado se fizer sentido

Bora começar?
