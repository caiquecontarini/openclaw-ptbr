# Prompt Guiado â€” Aula BÃ´nus: Multi-Agent OS v2.0

> Anexe junto os arquivos: `prds/multi-agent-v2.md`, `prds/multi-agent-setup.md`, `templates/BOSS-WORKSPACE/` (todos os 8 arquivos), `templates/WORKER-WORKSPACE/` (todos os 6 arquivos)
> âš ï¸ Nota: `TOOLS-SHARED.md` e `shared/lessons/` no PRD v2 foram reorganizados na v2.1. Ver nota no topo do PRD.

---

```
Acabei de assistir a aula bÃ´nus sobre Multi-Agent OS v2.0 â€” a evoluÃ§Ã£o de um agente Ãºnico para uma organizaÃ§Ã£o completa com Chief of Staff, Bosses e Workers. Leia os PRDs e templates que estou anexando e me guie na migraÃ§Ã£o.

## O QUE PRECISO

### Fase 1: DiagnÃ³stico (antes de mudar qualquer coisa)

1. **Analise meu setup atual:**
   - Quantos agentes eu tenho?
   - Quem faz o quÃª?
   - Onde estÃ£o os gargalos? (agente sobrecarregado, context rot, custo descontrolado)

2. **Identifique meus domÃ­nios:**
   - Me faÃ§a perguntas sobre meu trabalho/negÃ³cio
   - Baseado nas respostas, sugira 3-5 domÃ­nios para bosses
   - Explique POR QUE cada domÃ­nio faz sentido separado

3. **Plano de migraÃ§Ã£o personalizado:**
   - Qual a ordem ideal dos bosses? (comeÃ§ar pelo mais crÃ­tico)
   - Quais workers cada boss precisa? (Watcher vs Maker)
   - Estimativa de custo mensal

### Fase 2: Foundation (executar)

4. **Backup obrigatÃ³rio:**
   - FaÃ§a backup completo do workspace atual
   - Confirme que Ã© restaurÃ¡vel antes de prosseguir

5. **Promover CoS:**
   - Atualize seu prÃ³prio SOUL.md: de COO/Hub para Chief of Staff
   - Defina claramente o que vocÃª PARA de fazer vs. o que continua
   - Atualize HEARTBEAT.md para foco em governance

6. **Criar shared/:**
   - Estrutura completa: context/, governance/, costs/, audit/, templates/, outputs/, lessons/
   - TEAM.md como fonte de verdade
   - USER.md canonical que todos herdam
   - TOOLS-SHARED.md com integraÃ§Ãµes compartilhadas
   - Governance docs: daily digest template, cross-boss protocol, quality gates, escalation rules
   - Scripts: cost tracking, context sync

7. **Ativar governance Day 1:**
   - Cron: daily digest (manhÃ£)
   - Cron: kill switch (noite)
   - Me mostre os crons criados e explique cada um

### Fase 3: Primeiro Boss

8. **Criar Boss A (o mais prioritÃ¡rio):**
   - Criar workspace usando template BOSS-WORKSPACE
   - Personalizar SOUL.md com domÃ­nio especÃ­fico
   - Configurar binding Telegram (topic prÃ³prio)
   - Adicionar ao agents.list
   - Cron: summary do boss (horÃ¡rio que faz sentido)

9. **Criar Workers do Boss A:**
   - Para cada worker, decidir: Watcher ou Maker?
   - Watchers: criar workspace + heartbeat
   - Makers: criar workspace (sem heartbeat â€” spawnados sob demanda)

10. **Teste crÃ­tico:**
    - Testar spawn chain: CoS â†’ Boss â†’ Worker
    - Testar que o boss responde no topic dele
    - Testar que o daily digest inclui o boss
    - SÃ“ avance para o Boss B depois que Boss A funcionar 100%

### Fase 4: Expandir

11. **Repetir para Boss B e Boss C:**
    - Mesmo processo do Boss A
    - Testar cross-boss communication
    - Validar que governance acompanha

12. **Hardening:**
    - Context sync automÃ¡tico (cron semanal)
    - Performance review semanal
    - Ajustar workers: remover os que nÃ£o usam, adicionar os que faltam
    - Revisar custos: algum agente caro demais vs. valor que entrega?

## REGRAS

- SEMPRE backup antes de cada etapa
- NUNCA pular o teste â€” se Boss A nÃ£o funciona, nÃ£o crie Boss B
- Governance Ã© Dia 1, nÃ£o "depois"
- ComeÃ§ar com 2-3 bosses, NUNCA 5 de uma vez
- Worker idle (Maker) = $0 â€” nÃ£o tenha medo de criar, mas tambÃ©m nÃ£o crie sem necessidade
- Todo agente novo comeÃ§a L1 (Observer) â€” confianÃ§a se ganha
- Se algo der errado: rollback do backup, respirar, tentar de novo

## FORMATO

Para cada passo:
1. Explique O QUE vai fazer e POR QUE
2. PeÃ§a minha confirmaÃ§Ã£o
3. Execute
4. Mostre o resultado
5. Confirme se posso avanÃ§ar

NÃ£o automatize tudo de uma vez. Quero entender cada decisÃ£o.
```


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
