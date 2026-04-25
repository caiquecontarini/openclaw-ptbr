# PRD â€” Aula N-2: Bot sem acesso ao shell â€” identificar e corrigir

**MÃ³dulo:** N â€” DiagnÃ³stico & Troubleshooting  
**Aula:** N-2  
**DuraÃ§Ã£o estimada:** 15 minutos  
**NÃ­vel:** IntermediÃ¡rio / Debug  
**Instrutor:** Bruno  
**Formato:** Screencast com narraÃ§Ã£o + slides/terminal ao vivo

---

## Objetivo da Aula

Ao final desta aula, o aluno serÃ¡ capaz de:
1. Identificar quando o agente perdeu acesso ao shell
2. Diagnosticar a causa exata do problema
3. Aplicar a correÃ§Ã£o correta em cada caso
4. Verificar que o acesso foi restaurado

---

## Roteiro de GravaÃ§Ã£o

### [00:00 â€“ 01:30] â€” ABERTURA

> **Bruno (cÃ¢mera ou voice-over):**

"Fala, pessoal! Bruno aqui. Nessa aula a gente vai resolver um dos problemas mais comuns que vejo acontecer com quem tÃ¡ comeÃ§ando a usar o OpenClaw: o agente para de executar comandos.

VocÃª pede pra ele instalar uma ferramenta. Ele diz 'nÃ£o consigo fazer isso'. VocÃª pede pra criar um arquivo. Ele diz 'nÃ£o tenho permissÃ£o'. Parece que o agente virou sÃ³ um chatbot â€” responde texto mas nÃ£o faz nada.

Isso tem causa. E tem soluÃ§Ã£o. Vou te mostrar as 5 causas mais comuns â€” incluindo a novidade da versÃ£o 3.2 que estÃ¡ pegando muita gente. Nos prÃ³ximos 15 minutos vocÃª vai aprender a identificar e corrigir cada uma.

Vamos lÃ¡!"

---

### [01:30 â€“ 03:00] â€” SINTOMAS DO PROBLEMA

> **Bruno (tela do terminal + agente aberto):**

"Primeiro, como saber que vocÃª estÃ¡ com esse problema?

Os sintomas clÃ¡ssicos sÃ£o esses:"

**[Mostrar na tela â€” lista de sintomas:]**

```
Sintoma 1: VocÃª pede ao agente pra rodar um comando e ele diz:
  â†’ "NÃ£o consigo executar comandos no seu sistema"
  â†’ "NÃ£o tenho acesso ao shell"
  â†’ "Essa ferramenta nÃ£o estÃ¡ disponÃ­vel"

Sintoma 2: O agente responde texto perfeitamente, mas qualquer
  tarefa que envolva o sistema operacional falha.

Sintoma 3: VocÃª recebe mensagens de erro como:
  â†’ "Permission denied"
  â†’ "exec: not in allowlist"
  â†’ "Sandbox restriction"
```

> "Se vocÃª tÃ¡ vendo qualquer um desses, o problema Ã© de permissÃ£o de acesso ao shell. Agora vamos entender por quÃª isso acontece â€” tem 4 causas principais."

---

### [03:00 â€“ 08:30] â€” AS 5 CAUSAS

#### âš ï¸ Causa 0 (NOVA, MAIS COMUM): `tools.profile = messaging` [03:00 â€“ 03:45]

> **Bruno:**

"Mas antes de qualquer coisa â€” desde a versÃ£o 3.2 do OpenClaw, a causa nÃºmero um do 'bot nÃ£o faz nada' mudou. E muita gente estÃ¡ caindo nessa agora.

Quando vocÃª configura o agente com `tools.profile = messaging`, o OpenClaw coloca o agente em modo mensageria â€” otimizado para responder texto no Telegram ou WhatsApp, mas sem acesso ao shell, sem exec, sem nada de sistema.

Ã‰ exatamente o que acontece quando vocÃª copia uma config de exemplo de bot Telegram e nÃ£o percebe que tem esse parÃ¢metro.

O sintoma Ã© claro: o agente responde fluentemente, parece esperto, mas quando vocÃª pede qualquer coisa que envolva o sistema operacional, ele diz 'nÃ£o consigo'.

A correÃ§Ã£o Ã© simples: remover o `tools.profile` ou trocÃ¡-lo para um perfil que inclua exec, como `full` ou `default`."

**[Mostrar config com o problema:]**
```json
{
  "agents": {
    "main": {
      "tools": {
        "profile": "messaging"
      }
    }
  }
}
```

**[Mostrar a correÃ§Ã£o:]**
```json
{
  "agents": {
    "main": {
      "tools": {
        "profile": "default"
      }
    }
  }
}
```

> "Ou simplesmente remova a chave `tools.profile` â€” o padrÃ£o jÃ¡ inclui exec."

#### Causa 1: Ferramenta `exec` nÃ£o estÃ¡ no allowlist [03:45 â€“ 04:45]

> **Bruno:**

"A causa mais comum. O OpenClaw controla quais ferramentas cada agente pode usar. Se a ferramenta `exec` nÃ£o estiver na lista de ferramentas permitidas, o agente simplesmente nÃ£o consegue rodar comandos.

Isso acontece quando alguÃ©m configura o agente de forma restrita â€” talvez pra um agente de suporte que nÃ£o devia ter acesso ao sistema. Faz sentido nesse contexto, mas nÃ£o faz sentido se vocÃª quer um agente que executa tarefas.

A correÃ§Ã£o vai estar na configuraÃ§Ã£o do allowlist. Vou mostrar como daqui a pouco."

#### Causa 2: Sandbox ativo sem permissÃ£o correta [04:00 â€“ 05:00]

> **Bruno:**

"A segunda causa Ã© o sandbox. O OpenClaw tem um sistema de sandbox que isola a execuÃ§Ã£o de comandos. Dependendo de como tÃ¡ configurado, o agente pode estar rodando num ambiente isolado que nÃ£o deixa comandos passarem.

O sandbox tem trÃªs modos:
- `off` â€” sem sandbox, acesso total ao sistema
- `non-main` â€” sandbox ativo sÃ³ pra sub-agentes
- `all` â€” sandbox ativo pra todos os agentes, incluindo o principal

Se vocÃª colocou `all` sem configurar as permissÃµes de sandbox corretamente, o agente principal tambÃ©m fica preso.

A diferenÃ§a entre esses modos importa. Vou mostrar na configuraÃ§Ã£o."

#### Causa 3: Security mode "deny" [05:00 â€“ 06:00]

> **Bruno:**

"A terceira causa Ã© o security mode. O OpenClaw tem um parÃ¢metro chamado `security` que controla como o agente lida com execuÃ§Ã£o de comandos. Quando esse parÃ¢metro estÃ¡ configurado como `deny`, o agente bloqueia qualquer tentativa de executar comandos no sistema.

Esse modo existe por uma razÃ£o: seguranÃ§a. Em alguns casos vocÃª quer um agente que sÃ³ lÃª, nÃ£o que executa. Mas se vocÃª configurou isso por engano no agente errado, ele vai ficar travado.

A soluÃ§Ã£o Ã© simples: mudar o security mode para `allowlist` ou `full`."

#### Causa 4: BotFather privacy mode â€” bot nÃ£o responde no grupo [06:00 â€“ 07:00]

> **Bruno:**

"Essa causa Ã© especÃ­fica pra quem usa o agente em grupos do Telegram. VocÃª adiciona o bot ao grupo, manda mensagem â€” nada. O bot responde em DM normalmente, mas no grupo, silÃªncio total.

O culpado Ã© o **Group Privacy Mode** do BotFather. Por padrÃ£o, quando vocÃª cria um bot no BotFather, ele vem com privacy mode ATIVO. Isso significa que o bot sÃ³ recebe mensagens que comeÃ§am com `/comando` â€” mensagens normais no grupo sÃ£o invisÃ­veis pra ele.

Como corrigir:"

**[Mostrar passo a passo:]**
```
1. Abra @BotFather no Telegram
2. Envie: /mybots
3. Selecione seu bot
4. Clique em "Bot Settings"
5. Clique em "Group Privacy"
6. Clique em "Turn off"
7. ConfirmaÃ§Ã£o: "Privacy mode is disabled"

IMPORTANTE: remova e adicione o bot ao grupo novamente
para as novas permissÃµes valerem.
```

> "Depois de desativar o privacy mode e re-adicionar o bot, ele comeÃ§a a receber todas as mensagens do grupo. Simples assim."

#### Causa 5: Path do shell nÃ£o encontrado [07:00 â€“ 08:00]

> **Bruno:**

"A quinta causa Ã© menos comum mas acontece especialmente em VPS â€” o OpenClaw nÃ£o consegue encontrar o shell do sistema.

Em ambientes Linux padrÃ£o, o shell fica em `/bin/bash` ou `/bin/sh`. Mas em algumas distribuiÃ§Ãµes minimalistas, containers Docker, ou VPS mal configurados, o path pode ser diferente. Ou o usuÃ¡rio que roda o OpenClaw nÃ£o tem permissÃ£o pra usar o shell.

A correÃ§Ã£o Ã© configurar o path correto do shell na configuraÃ§Ã£o do agente."

---

### [08:00 â€“ 08:30] â€” FLUXOGRAMA DE DIAGNÃ“STICO

> **Bruno:**

"Antes de entrar no diagnÃ³stico passo a passo, deixa eu te mostrar o mapa mental. Quando o bot nÃ£o faz nada, siga essa ordem:"

**[Mostrar fluxograma na tela:]**

```
Bot nÃ£o executa comandos?
         â”‚
         â–¼
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  tools.profile = messaging?    â”‚ â”€â”€YESâ”€â”€â–¶ Remover ou trocar para "default"
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
         â”‚ NO
         â–¼
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  Bot em grupo e nÃ£o responde?  â”‚ â”€â”€YESâ”€â”€â–¶ BotFather â†’ desativar Group Privacy
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
         â”‚ NO
         â–¼
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  sandbox = "all" ?             â”‚ â”€â”€YESâ”€â”€â–¶ Mudar para "off" ou "non-main"
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
         â”‚ NO
         â–¼
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  security = "deny" ?           â”‚ â”€â”€YESâ”€â”€â–¶ Mudar para "allowlist"
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
         â”‚ NO
         â–¼
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  "exec" no allowlist?          â”‚ â”€â”€NOâ”€â”€â”€â–¶ Adicionar "exec" ao allowlist
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
         â”‚ YES
         â–¼
    openclaw gateway restart
         â”‚
         â–¼
    echo "SHELL_TEST_OK"
         â”‚
    â”Œâ”€â”€â”€â”€â”´â”€â”€â”€â”€â”
   OK?      Falhou?
    â”‚           â”‚
  Resolvido   Ver logs
              gateway
```

> "Testa nessa ordem. A causa 0 â€” o tools.profile â€” resolve 60% dos casos que aparecem no grupo."

---

### [08:30 â€“ 09:00] â€” TESTE RÃPIDO

> **Bruno (mostrando terminal):**

"Antes de mergulhar no diagnÃ³stico, tem um teste rÃ¡pido que vocÃª pode fazer. PeÃ§a pro seu agente executar isso:"

**[Mostrar no terminal/chat:]**
```
execute: echo test
```

> "Se o agente responder com 'test', ele tem acesso ao shell. Se der erro, vocÃª tem um dos problemas que acabamos de ver. Simples assim."

---

### [08:00 â€“ 10:30] â€” COMO DIAGNOSTICAR

> **Bruno (tela do terminal):**

"Agora vamos ao diagnÃ³stico. Passo a passo:"

#### Passo 1: Verificar os logs do gateway

```bash
openclaw gateway logs --tail 50
```

> "Procure por mensagens como `exec blocked`, `not in allowlist`, `sandbox restriction` ou `permission denied`. O log vai te dizer exatamente o que estÃ¡ bloqueando."

#### Passo 2: Verificar a configuraÃ§Ã£o do agente

```bash
cat ~/.openclaw/config.json
```

ou, se estiver num workspace especÃ­fico:

```bash
cat openclaw.json
```

> "VocÃª precisa checar trÃªs coisas nesse arquivo: o `allowlist` de tools, o parÃ¢metro `sandbox`, e o `security` mode. Vou mostrar como cada um deve estar configurado."

#### Passo 3: Usar o diagnÃ³stico interativo

> "VocÃª tambÃ©m pode colar o prompt de diagnÃ³stico que disponibilizamos junto com esta aula â€” ele vai guiar o agente a verificar a prÃ³pria configuraÃ§Ã£o e identificar o problema automaticamente."

---

### [10:30 â€“ 13:00] â€” COMO CORRIGIR CADA CAUSA

> **Bruno (editor de cÃ³digo aberto com o config):**

"Agora a parte boa â€” as correÃ§Ãµes. Vou mostrar cada uma."

#### CorreÃ§Ã£o 1: Adicionar `exec` ao allowlist

```json
{
  "agents": {
    "main": {
      "tools": {
        "allowlist": ["exec", "read", "write", "edit", "web_search", "web_fetch"]
      }
    }
  }
}
```

> "Simples. Adicione `exec` na lista. Se nÃ£o existia a chave `tools`, crie ela. Salve o arquivo e reinicie o gateway."

#### CorreÃ§Ã£o 2: Ajustar configuraÃ§Ã£o de sandbox

```json
{
  "agents": {
    "main": {
      "sandbox": "off"
    }
  }
}
```

> "Para o agente principal, use `sandbox: off`. Se quiser sandboxing em sub-agentes mas nÃ£o no principal, use `non-main`. SÃ³ use `all` se vocÃª entende bem as implicaÃ§Ãµes e configurou as permissÃµes de sandbox corretamente."

**Tabela explicativa:**

| Valor       | Comportamento |
|-------------|---------------|
| `off`       | Sem sandbox â€” acesso total ao sistema |
| `non-main`  | Sandbox sÃ³ em sub-agentes |
| `all`       | Sandbox em todos â€” **inclui agente principal** |

#### CorreÃ§Ã£o 3: Ajustar security mode

```json
{
  "agents": {
    "main": {
      "security": "allowlist"
    }
  }
}
```

> "Mude de `deny` para `allowlist`. Com `allowlist`, sÃ³ os comandos e ferramentas na sua lista permitida vÃ£o funcionar â€” Ã© seguro e funcional. `full` desabilita restriÃ§Ãµes mas sÃ³ use se souber o que estÃ¡ fazendo."

#### CorreÃ§Ã£o 4: Configurar path do shell

```json
{
  "agents": {
    "main": {
      "shell": "/bin/bash"
    }
  }
}
```

> "Se o shell nÃ£o estÃ¡ sendo encontrado, especifique o path completo. No Ubuntu/Debian Ã© `/bin/bash`, em alguns Alpine/containers pode ser `/bin/sh`. Rode `which bash` ou `which sh` no terminal pra confirmar o path correto."

---

### [13:00 â€“ 14:30] â€” CHECKLIST DE VERIFICAÃ‡ÃƒO PÃ“S-CORREÃ‡ÃƒO

> **Bruno:**

"Depois de aplicar qualquer correÃ§Ã£o, siga esse checklist:"

**[Mostrar na tela:]**

```
CHECKLIST PÃ“S-CORREÃ‡ÃƒO

â–¡ 1. Reiniciar o gateway:
     openclaw gateway restart

â–¡ 2. Verificar status do gateway:
     openclaw gateway status

â–¡ 3. Testar acesso bÃ¡sico â€” pedir pro agente:
     execute: echo "shell funcionando"

â–¡ 4. Testar criaÃ§Ã£o de arquivo:
     execute: touch /tmp/teste-openclaw && echo "OK"

â–¡ 5. Verificar logs por erros residuais:
     openclaw gateway logs --tail 20

â–¡ 6. Testar uma tarefa real simples:
     "liste os arquivos do diretÃ³rio atual"
```

---

### [14:30 â€“ 15:00] â€” ENCERRAMENTO

> **Bruno:**

"Pronto! Agora vocÃª sabe identificar e corrigir os cinco tipos de problema que tiram o acesso ao shell do seu agente.

Pra recapitular:
- Causa 0 (mais comum!): `tools.profile = messaging` â†’ remova ou troque para `default`
- Causa 1: `exec` nÃ£o estÃ¡ no allowlist â†’ adicione na lista de tools
- Causa 2: Sandbox mal configurado â†’ ajuste o modo de sandbox
- Causa 3: Security mode `deny` â†’ mude para `allowlist`
- Causa 4: Bot no grupo sem resposta â†’ desativar Group Privacy no BotFather
- Causa 5: Shell nÃ£o encontrado â†’ configure o path correto

Use o prompt de diagnÃ³stico que deixamos disponÃ­vel pra vocÃª fazer esse processo de forma interativa com o prÃ³prio agente.

Qualquer dÃºvida, joga no grupo. AtÃ© a prÃ³xima!"

---

## Notas de ProduÃ§Ã£o

- **Mostrar terminal ao vivo** ao explicar logs e config
- **Editor de cÃ³digo** aberto ao mostrar as correÃ§Ãµes JSON
- **Destacar** as linhas relevantes no config com zoom ou destaque
- **Demonstrar** o teste rÃ¡pido (`echo test`) ao vivo pra mostrar o agente funcionando depois da correÃ§Ã£o
- **Adicionar captions/legendas** nas partes tÃ©cnicas

## Assets NecessÃ¡rios

- [ ] Arquivo `openclaw.json` de exemplo (com erro deliberado)
- [ ] VersÃ£o corrigida do `openclaw.json`
- [ ] Screenshot dos logs com mensagem de erro
- [ ] GIF/video do teste `echo test` funcionando

---

*PRD gerado em 2026-03-04 Â· Curso OpenClaw Â· Pixel EducaÃ§Ã£o*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
