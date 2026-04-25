# Prompt do Aluno: TÃ³picos no Telegram + Arquitetura de Agentes

**Cole este prompt no chat com sua Amora:**

---

Amora, preciso da sua ajuda para configurar tÃ³picos no Telegram e entender a diferenÃ§a entre ter um agente MAIN compartilhado vs agentes isolados.

**Tarefas:**

1. **Me guiar na criaÃ§Ã£o de tÃ³picos no Telegram:**
   - Como transformar meu grupo em supergrupo
   - Como ativar e criar tÃ³picos
   - Como descobrir o chat ID de cada tÃ³pico

2. **Configurar vocÃª para responder sem menÃ§Ã£o em tÃ³picos especÃ­ficos:**
   - Mostrar como editar o `config.yaml` pra vocÃª responder automaticamente
   - Explicar o `mode: mention` vs `mode: all`
   - Testar se funcionou

3. **Me explicar as duas arquiteturas:**
   - **MAIN compartilhado** â€” um agente respondendo em mÃºltiplos tÃ³picos
   - **Agentes isolados** â€” um agente por tÃ³pico
   - Pros e contras de cada
   - Quando usar cada uma

4. **Impacto em:**
   - Workspace (onde ficam os arquivos?)
   - MemÃ³ria (MEMORY.md compartilhado ou isolado?)
   - Crons (heartbeats compartilhados ou isolados?)
   - SOUL.md, USER.md, TOOLS.md (globais ou por agente?)

5. **Me ajudar a decidir qual arquitetura usar:**
   - Fazer perguntas sobre meu caso de uso
   - Recomendar a melhor opÃ§Ã£o
   - Mostrar exemplo de config completo

**Contexto sobre mim:**
- [Descreva aqui: vocÃª trabalha sozinho? tem mÃºltiplos clientes? precisa de privacidade entre tÃ³picos? projetos relacionados ou isolados?]

**Exemplo:**
> "Sou freelancer e tenho 3 clientes. Cada cliente tem um tÃ³pico no meu grupo do Telegram. Preciso que dados de um cliente NUNCA apareÃ§am pra outro."

---

**Leia o guia completo em:**
`/root/.openclaw/workspace-curso-openclaw/prds/topicos-telegram-arquitetura.md`

**Depois de configurar:**
- Teste mandando mensagem nos tÃ³picos
- Verifique se vocÃª responde automaticamente (quando `mode: all`)
- Confirme que cada agente isolado **nÃ£o vÃª** o workspace dos outros
- Ajuste o SOUL.md de cada agente (se isolados)

**Se algo der errado:**
- `openclaw logs --tail 100` pra ver erros
- `openclaw gateway restart` pra aplicar mudanÃ§as no config
- Me chame no privado que te ajudo

TÃ¡ pronta pra comeÃ§ar?


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
