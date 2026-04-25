# â“ Q&A â€” Arquitetura OpenClaw (CÃ©rebro, BraÃ§os, Subagentes)

> Linguagem simples. Sem terminal. Cole o prompt no seu bot e ele resolve.

---

## "Qual a diferenÃ§a entre o cÃ©rebro e os braÃ§os do agente?"

**Em linguagem simples:**

Pensa assim: vocÃª Ã© o **chefe**. O OpenClaw Ã© sua **empresa**.

- **CÃ©rebro (Gateway)** = O escritÃ³rio central. Recebe seus pedidos, toma decisÃµes, coordena tudo.
- **BraÃ§os (Tools/Skills)** = Os funcionÃ¡rios especializados. Um faz busca na web, outro acessa o calendÃ¡rio, outro manda mensagem.
- **Subagentes** = Freelancers contratados pra tarefas especÃ­ficas. Trabalham em paralelo e entregam resultado.

**Analogia completa:**
> VocÃª manda: "Pesquisa os melhores restaurantes perto de mim pra hoje Ã  noite e coloca no meu calendÃ¡rio."
> - O **cÃ©rebro** entende o pedido
> - O **braÃ§o de busca** procura os restaurantes
> - O **braÃ§o de calendÃ¡rio** cria o evento
> - Tudo acontece de forma coordenada

---

## "O que Ã© um subagente e quando usar?"

**Em linguagem simples:** Um subagente Ã© como contratar um assistente temporÃ¡rio pra fazer uma tarefa especÃ­fica enquanto vocÃª continua fazendo outra coisa.

**Quando usar:**
- Tarefas que demoram muito (pesquisa longa, anÃ¡lise de muitos dados)
- Tarefas paralelas (enquanto um pesquisa, outro escreve)
- Tarefas de risco (melhor deixar um "assistente" testar antes do "chefe" executar)

**O que fazer:**
Cole esse prompt no seu bot:

```
Quero entender quando vale usar subagentes no meu caso.
Me explica:
1. O que diferencia um subagente de uma tarefa normal?
2. Para o que eu uso o bot hoje, faz sentido usar subagentes?
3. Se sim, me dÃ¡ um exemplo prÃ¡tico de como ficaria?
```

---

## "Devo usar o OpenClaw ou o n8n para automatizar?"

**DiferenÃ§a simples:**

| | OpenClaw | n8n |
|---|---|---|
| **Melhor pra** | Tarefas que precisam de raciocÃ­nio e linguagem natural | Fluxos fixos e previsÃ­veis (se X entÃ£o Y) |
| **Exemplo** | "Resumir emails importantes e me avisar os urgentes" | "Quando receber email com assunto X, salvar no sheet" |
| **Precisa de** | VPS + API de IA | Servidor ou conta cloud |
| **Curva de aprendizado** | MÃ©dia (tem IA te ajudando) | MÃ©dia (interface visual) |

**Resposta curta:** Use OpenClaw quando precisar de julgamento humano. Use n8n quando o fluxo for sempre igual.

**Eles podem trabalhar juntos:** n8n dispara um webhook â†’ OpenClaw recebe e decide o que fazer.

---

## "Como sei se meu agente estÃ¡ funcionando corretamente?"

**O que fazer:**
Cole esse prompt no seu bot:

```
Faz um diagnÃ³stico completo de saÃºde do meu agente:
1. O gateway estÃ¡ rodando corretamente?
2. Todas as ferramentas (tools) estÃ£o funcionando?
3. A memÃ³ria estÃ¡ sendo salva corretamente?
4. Tem algum cron ou automaÃ§Ã£o com problema?
5. O que vocÃª recomenda verificar regularmente?
Me dÃ¡ um resumo do status geral.
```

---

## "Posso ter mais de um agente? Como funciona?"

**Em linguagem simples:** Sim! Ã‰ como ter uma equipe de assistentes especializados.

**Exemplos:**
- **Agente Principal:** Faz tudo, Ã© o seu assistente pessoal
- **Agente de Trabalho:** SÃ³ cuida de emails e tarefas profissionais
- **Agente de ConteÃºdo:** Especializado em criar posts e textos

**O que fazer:**
Cole esse prompt no seu bot:

```
Quero entender como ter mÃºltiplos agentes funciona.
Me explica:
1. Como cada agente Ã© configurado?
2. Eles compartilham memÃ³ria ou sÃ£o separados?
3. Quanto isso aumenta o custo?
4. Faz sentido pro meu uso atual ter mais de um?
```

---

*Ãšltima atualizaÃ§Ã£o: Fev/2026*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
