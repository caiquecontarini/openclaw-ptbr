# PRD â€” Aula N-8: Telegram: Bot NÃ£o Responde no Grupo

> **NÃ­vel:** IntermediÃ¡rio / Troubleshooting  
> **DuraÃ§Ã£o estimada:** 10 minutos  
> **PrÃ©-requisito:** OpenClaw configurado, bot no Telegram funcionando em DM

---

## ðŸŽ¯ Objetivo da Aula

Ao final desta aula, o aluno serÃ¡ capaz de:

1. Entender por que o bot funciona em DM mas nÃ£o no grupo
2. Corrigir o privacy mode do BotFather
3. Configurar `groupPolicy` no OpenClaw
4. Descobrir o chat ID de qualquer grupo
5. Entender a diferenÃ§a entre `dmPolicy` e `groupPolicy`
6. Diagnosticar problemas de grupo sistematicamente

---

## ðŸŽ¬ ABERTURA (0:00 â€“ 0:45)

**[Bruno na tela, tom direto]**

> "Fala! Aula N-8 â€” uma das dÃºvidas mais comuns do curso: 'adicionei meu bot no grupo, mas ele nÃ£o responde'. Em 10 minutos vocÃª vai entender por que isso acontece e como resolver."

> "Spoiler: quase sempre sÃ£o 3 causas. Vou te mostrar as 3 e o diagnÃ³stico pra saber qual Ã© a sua."

---

## ðŸ“š SEÃ‡ÃƒO 1: Por Que o Bot NÃ£o Fala no Grupo (0:45 â€“ 3:00)

**[Tela: slide com 3 causas]**

> "O bot funciona em DM mas nÃ£o no grupo? Existem 3 causas possÃ­veis, e elas sÃ£o independentes â€” qualquer uma delas jÃ¡ basta para o bot ficar mudo:"

**Causa 1: Privacy Mode ATIVADO no BotFather (mais comum)**

> "Por padrÃ£o, o Telegram cria bots com 'privacy mode' ATIVADO. Isso significa que o bot NÃƒO RECEBE mensagens do grupo â€” ele sÃ³ recebe mensagens que comecem com `/comando` ou que mencionem diretamente o bot com @username."

> "Ã‰ uma medida de privacidade do Telegram. Mas pra um agente AI que deve participar das conversas, isso Ã© um problema."

**Causa 2: `groupPolicy` nÃ£o configurado no OpenClaw**

> "Mesmo que o bot receba as mensagens, o OpenClaw tem uma camada de seguranÃ§a prÃ³pria: por padrÃ£o, ele nÃ£o processa mensagens de grupos a menos que vocÃª configure explicitamente."

**Causa 3: Chat ID do grupo nÃ£o estÃ¡ no allowlist**

> "Se vocÃª usou `groupPolicy = allowlist`, precisa adicionar o chat ID do grupo especÃ­fico. Sem o ID correto, o OpenClaw ignora as mensagens mesmo com tudo configurado."

---

## ðŸ”§ FIX 1: BotFather â€” Desativar Privacy Mode (3:00 â€“ 5:00)

**[Tela: Telegram aberto no BotFather]**

> "Vamos resolver a Causa 1. Abre o Telegram e fala com o **@BotFather**."

```
1. Abra o chat com @BotFather
2. Envie: /setprivacy
3. BotFather vai listar seus bots â€” selecione o seu
4. Escolha: Disable
5. ConfirmaÃ§Ã£o: "Success! Privacy mode is disabled."
```

> "Agora o bot vai receber TODAS as mensagens do grupo, nÃ£o sÃ³ comandos. Isso Ã© necessÃ¡rio para o agente participar das conversas normalmente."

> "**AtenÃ§Ã£o:** ApÃ³s mudar o privacy mode, vocÃª precisa **remover o bot do grupo e adicionar de volta**. O Telegram sÃ³ aplica a nova configuraÃ§Ã£o quando o bot entra no grupo. Se o bot jÃ¡ estava no grupo, a mudanÃ§a nÃ£o vai funcionar atÃ© vocÃª fazer isso."

---

## ðŸ”§ FIX 2: Configurar groupPolicy no OpenClaw (5:00 â€“ 7:30)

**[Tela: Terminal]**

> "Agora vamos resolver a Causa 2 e 3 juntas. No terminal da VPS:"

```bash
# Configurar polÃ­tica para grupos
# allowlist = sÃ³ responde em grupos especÃ­ficos (recomendado)
openclaw config set channels.telegram.groupPolicy allowlist

# Adicionar o chat ID do grupo ao allowlist
# (Veja a seÃ§Ã£o abaixo para descobrir o chat ID)
openclaw config set channels.telegram.groupAllowlist "[-100XXXXXXXXXX]"
```

> "Se tiver mais de um grupo:"
```bash
openclaw config set channels.telegram.groupAllowlist "[-100111111111, -100222222222]"
```

> "Para permitir qualquer grupo sem allowlist (menos seguro):"
```bash
openclaw config set channels.telegram.groupPolicy open
```

> "Recomendo `allowlist` â€” vocÃª controla exatamente em quais grupos o agente atua."

---

## ðŸ” Como Descobrir o Chat ID do Grupo (7:30 â€“ 8:30)

**[Tela: Terminal + Telegram]**

> "Para descobrir o chat ID do seu grupo, siga estes passos:"

```bash
# 1. Adicione o bot ao grupo (se ainda nÃ£o fez)
# 2. Envie qualquer mensagem no grupo
# 3. Verifique os logs do OpenClaw
openclaw gateway logs | grep "chat_id"
# ou
openclaw gateway logs | tail -50
```

> "Nos logs vocÃª vai ver algo como:"
```
Received message from chat_id: -1001234567890, user: JoÃ£o
```

> "O chat ID de grupos comeÃ§a com `-100` seguido de nÃºmeros. Anote esse ID â€” Ã© ele que vai no allowlist."

> "Dica alternativa: adicione o bot @userinfobot ao grupo, mande `/start`, ele retorna o ID do grupo tambÃ©m."

---

## ðŸ“˜ SEÃ‡ÃƒO 5: dmPolicy vs groupPolicy â€” A DiferenÃ§a (8:30 â€“ 9:30)

**[Tela: comparativo]**

> "Essa Ã© uma confusÃ£o comum. Deixa eu esclarecer de vez:"

| | dmPolicy | groupPolicy |
|---|---|---|
| **Controla** | Mensagens diretas (DM/privadas) | Mensagens em grupos |
| **Default** | allowlist | nÃ£o configurado |
| **Escopo** | 1-para-1 com vocÃª | Muitos usuÃ¡rios no mesmo chat |
| **Risco** | AlguÃ©m comandar seu agente | Agente ativo em grupos nÃ£o autorizados |

> "SÃ£o dois guardiÃµes independentes. O `dmPolicy` cuida da sua conversa privada com o bot. O `groupPolicy` cuida de quando o bot estÃ¡ em grupos."

> "VocÃª pode ter: DM aberta (sÃ³ vocÃª) + grupos no allowlist. Ou DM sÃ³ para vocÃª + nenhum grupo ativo. A combinaÃ§Ã£o depende do seu caso de uso."

---

## ðŸ—ºï¸ SEÃ‡ÃƒO 6: DiagnÃ³stico Passo a Passo (Fluxograma)

```
Bot adicionado ao grupo mas nÃ£o responde
â”‚
â”œâ”€â”€ [1] Privacy mode estÃ¡ ATIVO?
â”‚   â†’ Teste: envie /start ou /help no grupo
â”‚   â†’ Se o bot RESPONDE a comandos mas ignora mensagens normais â†’ Privacy mode ATIVO
â”‚   â†’ FIX: BotFather â†’ /setprivacy â†’ Disable â†’ Remover e re-adicionar bot ao grupo
â”‚
â”œâ”€â”€ [2] groupPolicy configurado?
â”‚   â†’ Teste: openclaw config get channels.telegram.groupPolicy
â”‚   â†’ Se retornar vazio ou "none" â†’ nÃ£o configurado
â”‚   â†’ FIX: openclaw config set channels.telegram.groupPolicy allowlist
â”‚
â”œâ”€â”€ [3] Chat ID no allowlist?
â”‚   â†’ Teste: openclaw config get channels.telegram.groupAllowlist
â”‚   â†’ Verifique se o ID do grupo estÃ¡ na lista
â”‚   â†’ FIX: openclaw config set channels.telegram.groupAllowlist "[-100XXXXXXX]"
â”‚
â””â”€â”€ [4] Ainda nÃ£o funciona?
    â†’ openclaw gateway logs | tail -100
    â†’ Procure mensagens de erro relacionadas ao chat
    â†’ openclaw gateway restart
```

---

## ðŸ’¡ SEÃ‡ÃƒO 7: TÃ³picos (Forum Mode) â€” ReferÃªncia

> "Se o seu grupo usa **tÃ³picos** (grupos com forum mode ativado), hÃ¡ uma configuraÃ§Ã£o adicional. O bot precisa ser admin do grupo para ter acesso a todos os tÃ³picos, e vocÃª pode precisar configurar quais tÃ³picos o agente monitora."

> "Para configuraÃ§Ã£o detalhada de tÃ³picos, consulte a **Aula Extra C** â€” ela cobre o forum mode completo com exemplos prÃ¡ticos."

---

## ðŸ“‹ ConfiguraÃ§Ã£o Completa (ReferÃªncia RÃ¡pida)

```bash
# 1. BotFather: /setprivacy â†’ Disable (no Telegram)
# 2. Remover e re-adicionar o bot ao grupo

# 3. Configurar groupPolicy
openclaw config set channels.telegram.groupPolicy allowlist

# 4. Adicionar chat ID do grupo
openclaw config set channels.telegram.groupAllowlist "[-100XXXXXXXXXX]"

# 5. Verificar configuraÃ§Ã£o
openclaw config get channels.telegram.groupPolicy
openclaw config get channels.telegram.groupAllowlist

# 6. Reiniciar gateway
openclaw gateway restart

# 7. Checar logs
openclaw gateway logs | tail -30
```

---

## âœ… Checklist Final do Aluno

- [ ] Privacy mode desativado no BotFather (`/setprivacy â†’ Disable`)
- [ ] Bot removido e re-adicionado ao grupo apÃ³s mudanÃ§a de privacy mode
- [ ] Chat ID do grupo descoberto (comeÃ§a com `-100...`)
- [ ] `groupPolicy = allowlist` configurado
- [ ] Chat ID adicionado ao `groupAllowlist`
- [ ] Gateway reiniciado
- [ ] Teste: mensagem enviada no grupo â†’ bot respondeu âœ…

---

## ðŸš¨ Erros Comuns

| Sintoma | Causa | SoluÃ§Ã£o |
|---------|-------|---------|
| Bot responde `/start` mas ignora mensagens | Privacy mode ATIVADO | BotFather â†’ /setprivacy â†’ Disable |
| Bot nÃ£o responde nada no grupo | groupPolicy nÃ£o configurado | `openclaw config set channels.telegram.groupPolicy allowlist` |
| groupPolicy configurado mas nÃ£o responde | Chat ID nÃ£o estÃ¡ no allowlist | Adicione o ID correto ao groupAllowlist |
| Bot funciona em DM, mudo no grupo | Qualquer das 3 causas | Seguir fluxograma de diagnÃ³stico |
| ApÃ³s mudanÃ§a de privacy mode, ainda mudo | Bot ainda no grupo com config antiga | Remover bot do grupo e adicionar de volta |
| Chat ID invÃ¡lido | Copiou ID errado | Ver logs: `openclaw gateway logs | grep chat_id` |

---

## â“ DÃºvidas Frequentes

**1. Preciso remover o bot e adicionar de volta sempre que mudar o privacy mode?**

> Sim. O Telegram processa a configuraÃ§Ã£o de privacy mode no momento em que o bot entra no grupo. MudanÃ§as retroativas nÃ£o se aplicam â€” precisa sair e entrar de novo.

**2. Posso ter groupPolicy = open?**

> Sim, mas nÃ£o recomendo para uso geral. Com `open`, o agente responde em qualquer grupo onde estiver adicionado â€” qualquer pessoa que adicione o bot a um grupo pode usÃ¡-lo. Prefira `allowlist`.

**3. O bot pode ser admin do grupo?**

> Sim, e Ã© necessÃ¡rio para alguns recursos (deletar mensagens, acessar todos os tÃ³picos em forum mode). Para uso bÃ¡sico de resposta, ser membro comum Ã© suficiente.

**4. Funciona com grupos grandes (centenas de pessoas)?**

> Tecnicamente sim. Mas pense no custo: cada mensagem no grupo vai para o agente. Com 200 pessoas no grupo e muitas mensagens por dia, o custo de tokens pode ser alto. Configure bem o `groupPolicy` e considere usar `groupMentionOnly` (o bot sÃ³ responde quando @mencionado) para grupos grandes.

**5. TÃ³picos (forum mode) exigem configuraÃ§Ã£o extra?**

> Sim. Consulte a Aula Extra C para configuraÃ§Ã£o completa de forum mode com tÃ³picos.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
