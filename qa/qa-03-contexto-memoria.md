# â“ Q&A â€” Contexto & MemÃ³ria (Token, /compact, /new)

> Linguagem simples. Sem terminal. Cole o prompt no seu bot e ele resolve.

---

## "Meu bot ficou lento e as respostas pioraram muito"

**O que provavelmente aconteceu:** A conversa ficou longa demais. Imagine tentar lembrar de TUDO que vocÃª fez nos Ãºltimos 6 meses de uma vez sÃ³ â€” o cÃ©rebro trava. Com o bot Ã© igual.

**O que fazer:**
Cole esse prompt no seu bot:

```
Estou sentindo que vocÃª ficou mais lento e as respostas pioraram.
Me diz:
1. Qual Ã© o tamanho atual do contexto? (use /status)
2. EstÃ¡ perto do limite?
3. O que vocÃª recomenda: /compact ou /new?
4. Qual a diferenÃ§a entre os dois pra mim decidir?
```

---

## "Qual a diferenÃ§a entre /compact e /new? Tenho medo de perder tudo"

**Em linguagem simples:**

| | /compact | /new |
|---|---|---|
| **O que faz** | Resume a conversa atual | ComeÃ§a uma conversa zerada |
| **Perde memÃ³ria?** | NÃ£o â€” resume, nÃ£o apaga | A conversa some, mas arquivos de memÃ³ria ficam |
| **Quando usar** | Conversa longa mas quer continuar | Quer um comeÃ§o fresco |
| **Analogia** | Tirar uma foto do que aconteceu | Abrir um caderno novo |

**Resposta curta:** Use `/compact` primeiro. Se ainda estiver lento depois, use `/new`.

**Importante:** Mesmo com `/new`, o bot lembra de vocÃª! Ele tem arquivos de memÃ³ria (MEMORY.md, memory/) que persistem entre conversas.

---

## "O bot 'esqueceu' algo que eu tinha contado"

**O que aconteceu:** Ou a conversa foi compactada e aquela informaÃ§Ã£o nÃ£o ficou no resumo, ou foi iniciada uma sessÃ£o nova.

**O que fazer:**
Cole esse prompt no seu bot:

```
VocÃª parece ter esquecido [DESCREVA O QUE ELE ESQUECEU].
Me ajuda a recuperar isso:
1. Verifica seus arquivos de memÃ³ria (MEMORY.md, memory/)
2. Essa informaÃ§Ã£o estÃ¡ salva em algum lugar?
3. Se nÃ£o estiver, vou te recontar agora: [REESCREVA A INFORMAÃ‡ÃƒO]
4. Por favor, salva isso no arquivo de memÃ³ria adequado pra nÃ£o esquecer mais.
```

---

## "Apareceu um erro de 'token limit' ou 'context too long'"

**O que aconteceu:** A conversa ultrapassou o limite de memÃ³ria do modelo. Ã‰ como tentar colocar 10 litros em um copo de 2 litros.

**O que fazer imediatamente:**
Cole esse prompt no seu bot:

```
Apareceu um erro de limite de contexto/tokens.
Precisa que vocÃª:
1. FaÃ§a um /compact agora para resumir a conversa
2. Me confirme quando terminar
3. Continue de onde paramos depois do compact
```

**Para evitar que aconteÃ§a de novo:**
Cole esse prompt:

```
Quero configurar a compactaÃ§Ã£o automÃ¡tica pra vocÃª nunca mais estourar o limite.
Me guia como configurar o "compaction: { mode: default }" no meu openclaw.json.
Explica o que cada opÃ§Ã£o faz antes de eu aplicar.
```

---

## "O que Ã© memÃ³ria vetorial? Preciso disso?"

**Em linguagem simples:** Ã‰ uma forma do bot guardar muita informaÃ§Ã£o e encontrar a parte certa na hora certa â€” como um Ã­ndice de livro inteligente.

**Precisa?** Provavelmente nÃ£o agora. A maioria dos alunos usa muito bem sÃ³ com os arquivos de memÃ³ria normais (MEMORY.md). A memÃ³ria vetorial Ã© para casos avanÃ§ados com muita informaÃ§Ã£o.

**Se quiser entender mais:**
Cole esse prompt no seu bot:

```
Me explica de forma bem simples:
1. O que sÃ£o os arquivos MEMORY.md e memory/ que vocÃª usa?
2. O que seria "memÃ³ria vetorial" e quando faz sentido?
3. Para o meu uso atual, o que vocÃª recomenda?
```

---

*Ãšltima atualizaÃ§Ã£o: Fev/2026*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
