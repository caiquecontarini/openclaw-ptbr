# Prompt do Aluno â€” Aula Extra: Organize as Pastas do Seu Agente Para Escalar

> **Como usar:** Cole o prompt abaixo no chat do seu agente OpenClaw depois de ler o material da aula.

---

## ðŸ“‹ Prompt Principal

```
Acabei de ler o material sobre organizaÃ§Ã£o de workspace do curso OpenClaw. Quero que vocÃª organize meu workspace agora.

Siga estas 5 fases na ordem. FaÃ§a cada uma e me mostre o resultado antes de ir pra prÃ³xima.

---

**FASE 1 â€” DIAGNÃ“STICO**

FaÃ§a um scan completo do meu workspace:
1. Liste tudo na raiz â€” identifique o que NÃƒO deveria estar aqui (sÃ³ os 7 arquivos de identidade ficam na raiz: SOUL.md, IDENTITY.md, USER.md, MEMORY.md, AGENTS.md, TOOLS.md, HEARTBEAT.md)
2. Verifique quais dos 7 arquivos raiz existem e quais faltam
3. Verifique se existem as pastas: memory/, skills/, reports/, archive/
4. Dentro de memory/, verifique: context/, projects/, integrations/, sessions/

Me mostre um relatÃ³rio de saÃºde:
- ðŸŸ¢ OK
- ðŸŸ¡ Pode melhorar
- ðŸ”´ Precisa de atenÃ§Ã£o

---

**FASE 2 â€” CRIAR ESTRUTURA + MOVER ARQUIVOS**

Baseado no diagnÃ³stico:

1. Crie as pastas que faltam:
   - memory/context/
   - memory/projects/
   - memory/integrations/
   - memory/sessions/
   - skills/ (com subpastas por categoria de trabalho â€” sugira 3-5 categorias baseadas no meu uso)
   - reports/ (com subpastas: business/, misc/ â€” sugira outras se fizer sentido)
   - archive/

2. Mova todo arquivo que estÃ¡ fora do lugar para o destino correto. Para cada arquivo movido, me diga: de onde saiu â†’ pra onde foi â†’ por quÃª.

3. Se algum dos 7 arquivos raiz nÃ£o existe, crie um template mÃ­nimo pra eu preencher depois.

---

**FASE 3 â€” ATUALIZAR TOOLS.md**

Adicione ao meu TOOLS.md uma seÃ§Ã£o "Onde Salvar Cada Output" com esta tabela (adapte as categorias pro meu contexto):

| Tipo de arquivo | Destino |
|----------------|---------|
| Report / anÃ¡lise | reports/{categoria}/ |
| Dashboard HTML | reports/{categoria}/ |
| PDF / imagem entregÃ¡vel | reports/{categoria}/ |
| Screenshot / temporÃ¡rio | archive/imgs/ |
| PRD de projeto | projects/{nome}/PRD.md |
| Skill nova | skills/{categoria}/SKILL.md |
| Script operacional | scripts/{categoria}/ |
| Doc obsoleto | archive/ |
| MemÃ³ria de projeto | memory/projects/{nome}.md |
| DecisÃ£o permanente | memory/context/decisions.md |
| DiÃ¡rio de sessÃ£o | memory/sessions/YYYY-MM-DD.md |

Se eu jÃ¡ tenho seÃ§Ãµes no TOOLS.md, integre â€” nÃ£o sobrescreva.

---

**FASE 4 â€” ATUALIZAR MEMORY.md**

FaÃ§a o MEMORY.md funcionar como Ã­ndice:

1. Se nÃ£o existe, crie com:
   - SeÃ§Ã£o "Estrutura de MemÃ³ria" (tabela: pasta â†’ o que contÃ©m)
   - SeÃ§Ã£o "Mapa de MemÃ³ria" (tabela: "estou buscando X" â†’ "onde encontrar")
2. Se jÃ¡ existe, reorganize pra seguir esse formato
3. MEMORY.md deve ser LEVE (50-100 linhas) â€” sÃ³ aponta para os arquivos, nunca duplica conteÃºdo

---

**FASE 5 â€” ORGANIZAR SKILLS + TESTE**

1. Liste minhas skills atuais (se existirem)
2. Mova cada skill pra skills/{categoria}/ baseado no tipo de trabalho
3. Crie um _registry.md em cada categoria listando as skills
4. Se nÃ£o tenho skills ainda, crie a estrutura vazia

Depois teste tudo:
5. Crie um relatÃ³rio simples de teste e salve seguindo a tabela do TOOLS.md
6. Use memory_search pra confirmar que encontra
7. Me mostre o resultado: "Perguntei onde salvar X â†’ salvei em Y â†’ busquei e encontrei âœ…"

---

No final, me dÃª um resumo:
- Quantos arquivos movidos e pra onde
- Quais pastas criadas
- O que mudou nos arquivos raiz
- O que eu ainda preciso preencher manualmente
```

---

## ðŸ”„ Prompt de ManutenÃ§Ã£o Mensal

> Use 1x/mÃªs pra manter o workspace saudÃ¡vel.

```
FaÃ§a uma auditoria mensal do meu workspace:

1. Tem arquivo na raiz que nÃ£o deveria estar?
2. Alguma pasta cresceu demais e precisa de subcategorias?
3. Tem algo em archive/ que pode ser deletado?
4. Algum projeto em memory/projects/ que jÃ¡ terminou?
5. TOOLS.md e MEMORY.md estÃ£o sincronizados com a estrutura real?
6. Alguma skill sem documentaÃ§Ã£o ou sem _registry.md?

Me dÃª um relatÃ³rio de saÃºde com aÃ§Ãµes recomendadas. Execute as que forem Ã³bvias sem perguntar.
```


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
