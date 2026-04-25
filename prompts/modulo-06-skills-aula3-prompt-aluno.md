# Prompt do Aluno â€” M06 Aula 3: Crie suas skills com o /criar-skill

> Use este prompt no seu agente depois de assistir a aula bÃ´nus.

---

## ðŸ“¦ Passo 1 â€” O /criar-skill jÃ¡ vem com o OpenClaw

A skill `skill-creator` jÃ¡ faz parte das skills oficiais. Verifique:

```bash
openclaw skills list | grep skill-creator
```

Se precisar instalar:
```bash
clawhub install skill-creator
```

O comando `/criar-skill` fica disponÃ­vel automaticamente no chat do agente â€” nenhum clone manual necessÃ¡rio.

---

## ðŸŽ¯ O que vocÃª vai praticar

Usar o `/criar-skill` nos dois modos: capturar um processo que jÃ¡ resolveram juntos, e criar uma skill nova a partir de uma ideia que vocÃª ainda nÃ£o sabe estruturar.

---

## Caminho A â€” VocÃª acabou de resolver algo. NÃ£o deixa sumir.

Use logo depois de uma conversa onde vocÃªs resolveram um problema juntos:

```
/criar-skill
```

SÃ³ isso. O agente lÃª o histÃ³rico, extrai o processo e propÃµe a skill completa.

**Quando usar:** Sempre que uma conversa levou mais de 10 minutos pra resolver algo. Se foi trabalhoso uma vez, vai ser de novo â€” a menos que vire skill.

---

## Caminho B â€” VocÃª tem uma ideia. Quer estruturar.

```
/criar-skill quero [descreva sua ideia em 1 frase]
```

**Exemplos reais para testar:**

```
/criar-skill quero gerar um resumo semanal das minhas mÃ©tricas mais importantes
```

```
/criar-skill quero criar briefings de reuniÃ£o antes de cada call importante
```

```
/criar-skill quero responder comentÃ¡rios do Instagram mantendo meu tom de voz
```

```
/criar-skill quero analisar concorrentes e me dar os 3 pontos principais
```

O agente vai fazer perguntas pra entender o processo â€” responda naturalmente. No final, ele propÃµe a skill completa e vocÃª aprova o deploy.

---

## Desafio da aula

Crie **pelo menos 2 skills** esta semana:

1. **Uma do Caminho A** â€” Pense num problema que vocÃª jÃ¡ resolveu com o agente recentemente. Recrie a conversa e use `/criar-skill` no final.

2. **Uma do Caminho B** â€” Pense num processo que vocÃª faz manualmente hoje e gostaria que o agente assumisse. Use `/criar-skill quero [sua ideia]`.

---

## Pergunta para cada skill que vocÃª criar

Antes de aprovar o deploy, responda:

- O trigger faz sentido? (Consigo acionar naturalmente?)
- O output Ã© o que eu esperava?
- Tem algum detalhe importante que ficou faltando?

Se sim para os trÃªs â€” aprova. Se nÃ£o, pede pro agente ajustar antes de salvar.

---

## Lembre-se

> "Qualquer processo que vocÃª repete mais de 2 vezes Ã© candidato a skill."

Toda vez que vocÃª se pegar explicando algo pro agente de novo â€” Ã© sinal de que falta uma skill.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
