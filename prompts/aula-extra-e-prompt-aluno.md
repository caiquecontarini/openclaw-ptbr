# Prompt do Aluno: Aula Extra E â€” Gerenciamento de Contexto & MemÃ³ria

> **Cole este prompt no chat com seu agente OpenClaw para praticar os conceitos da aula.**

---

OlÃ¡! Vou praticar gerenciamento de contexto e memÃ³ria com vocÃª.

**Objetivo:** Aprender a usar `/status`, `/compact`, `/new`, entender compactaÃ§Ã£o automÃ¡tica e como a memÃ³ria funciona entre sessÃµes.

Por favor, me guie atravÃ©s dos seguintes exercÃ­cios:

---

## ExercÃ­cio 1: Entendendo o `/status`

1. Me mostre como usar o comando `/status`
2. Me explique o que cada informaÃ§Ã£o significa:
   - Modelo atual
   - Uso de contexto (tokens e %)
   - Custo (se disponÃ­vel)
   - Tempo de sessÃ£o
3. Me diga: em qual % de contexto eu deveria comeÃ§ar a me preocupar?

---

## ExercÃ­cio 2: Simulando Crescimento de Contexto

Vamos fazer uma conversa longa para encher o contexto (nÃ£o precisa ser Ãºtil, sÃ³ pra praticar):

1. Me conte uma histÃ³ria sobre como vocÃª foi criado (use bastante texto)
2. Depois, me explique como funciona um LLM em detalhes tÃ©cnicos (de novo, bastante texto)
3. Depois disso, rode `/status` de novo e me mostre quanto o contexto cresceu

**Pergunta reflexiva:** Por que conversas longas aumentam tanto o contexto?

---

## ExercÃ­cio 3: CompactaÃ§Ã£o Manual

1. Me mostre como usar o comando `/compact`
2. Rode `/status` antes e depois para eu ver a diferenÃ§a
3. Me explique:
   - O que foi preservado?
   - O que foi resumido?
   - VocÃª ainda lembra da nossa conversa anterior?

---

## ExercÃ­cio 4: DiferenÃ§a entre `/compact` e `/new`

1. Me explique a diferenÃ§a entre:
   - Compactar a sessÃ£o (`/compact`)
   - Iniciar sessÃ£o nova (`/new`)

2. Me dÃª exemplos de quando usar cada um:
   - 3 situaÃ§Ãµes para `/compact`
   - 3 situaÃ§Ãµes para `/new`

---

## ExercÃ­cio 5: Testando `/new`

**Antes de fazer `/new`:**
1. Me ajude a criar um arquivo `memory/teste-aula-e.md` com:
   - Resumo do que praticamos atÃ© agora
   - Uma decisÃ£o fictÃ­cia importante: "Projeto X deve usar Python 3.11"
   - Data e hora atual

**Agora faÃ§a `/new`**

**Depois do `/new`:**
1. VocÃª ainda lembra de mim?
2. VocÃª lembra do que conversamos antes?
3. VocÃª consegue acessar o arquivo `memory/teste-aula-e.md`?
4. Me explique o que aconteceu: o que vocÃª perdeu e o que vocÃª manteve?

---

## ExercÃ­cio 6: CompactaÃ§Ã£o AutomÃ¡tica

Me explique como configurar compactaÃ§Ã£o automÃ¡tica no OpenClaw:

1. Qual arquivo eu preciso editar?
2. Quais parÃ¢metros eu devo configurar?
3. Qual threshold vocÃª recomenda? (70%, 75%, 80%?)
4. Quais sÃ£o as vantagens e desvantagens de ativar?

---

## ExercÃ­cio 7: Hierarquia de MemÃ³ria

Me desenhe (em texto/ASCII) a hierarquia de memÃ³ria do OpenClaw:

1. Contexto da sessÃ£o (temporÃ¡rio)
2. MemÃ³ria recente (memory/*.md)
3. MemÃ³ria de longo prazo (MEMORY.md)

E me explique:
- O que acontece com cada nÃ­vel quando uso `/compact`?
- O que acontece com cada nÃ­vel quando uso `/new`?
- Como vocÃª decide o que salvar em cada nÃ­vel?

---

## ExercÃ­cio 8: Troubleshooting

Me ajude a resolver estes problemas fictÃ­cios:

**Problema 1:** "Fiz `/new` e o agente nÃ£o lembra do projeto que comeÃ§amos ontem"
- O que pode ter acontecido?
- Como eu resolvo?

**Problema 2:** "Meu contexto tÃ¡ em 95% e `/compact` sÃ³ liberou 10%"
- O que devo fazer?
- Como prevenir isso no futuro?

**Problema 3:** "ApÃ³s compactar, o agente esqueceu uma decisÃ£o importante"
- Por que isso acontece?
- Como eu garanto que decisÃµes importantes nÃ£o se percam?

---

## ExercÃ­cio 9: EstratÃ©gia Pessoal

Com base no meu uso (vocÃª pode me perguntar como eu pretendo usar o OpenClaw), me recomende:

1. Devo ativar auto-compact? Com qual threshold?
2. Com que frequÃªncia devo usar `/new`?
3. Devo monitorar contexto ativamente ou deixar no automÃ¡tico?
4. Dicas especÃ­ficas para economizar custo de API

---

## ExercÃ­cio 10: Checklist Final

Me crie um checklist personalizado de boas prÃ¡ticas de gestÃ£o de contexto que eu possa imprimir e deixar do lado do computador. Algo tipo:

**Antes de comeÃ§ar:**
- [ ] ...

**Durante o trabalho:**
- [ ] ...

**Ao terminar:**
- [ ] ...

---

## ReflexÃ£o Final

Depois de fazer todos esses exercÃ­cios, me responda:

1. Qual Ã© a diferenÃ§a prÃ¡tica entre `/compact` e `/new`?
2. Por que compactaÃ§Ã£o automÃ¡tica Ã© importante?
3. Como memÃ³ria funciona entre sessÃµes?
4. Qual Ã© a maior liÃ§Ã£o que vocÃª aprendeu sobre gestÃ£o de contexto?

---

**Obrigado por me guiar! ðŸš€**

Agora eu sei:
âœ… Usar `/status`, `/compact`, `/new` com confianÃ§a  
âœ… Configurar compactaÃ§Ã£o automÃ¡tica  
âœ… Entender a hierarquia de memÃ³ria  
âœ… Gerenciar contexto de forma proativa  
âœ… Economizar custo de API  

---

*Se tiver dÃºvidas adicionais durante os exercÃ­cios, sinta-se livre para perguntar!*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
