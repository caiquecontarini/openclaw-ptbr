# PRD â€” Aula N-4: LentidÃ£o do Bot no Telegram
## Debug e OtimizaÃ§Ã£o de Performance

**MÃ³dulo:** N â€” Troubleshooting  
**NÃ­vel:** IntermediÃ¡rio / Debug  
**DuraÃ§Ã£o estimada:** 15â€“20 minutos  
**Instrutor:** Bruno  
**Formato:** Screenshare + narraÃ§Ã£o (sem cÃ¢mera)

---

## ðŸŽ¯ Objetivo da Aula

Ao final, o aluno vai saber:
1. Diagnosticar por que o bot estÃ¡ lento (modelo, VPS ou Telegram?)
2. Identificar e resolver as 6 causas mais comuns de lentidÃ£o
3. Medir e monitorar o tempo de resposta via logs
4. Configurar o OpenClaw de forma otimizada para velocidade

---

## ðŸŽ¬ ROTEIRO DE GRAVAÃ‡ÃƒO

### INTRO (0:00 â€“ 1:30)

> **[Bruno fala, tela mostra o Telegram com bot demorando para responder]**

*"VocÃª manda uma mensagem pro seu bot no Telegram... e fica olhando o cursor piscando. 5 segundos. 10 segundos. 30 segundos. Nada."*

*"Se isso aconteceu com vocÃª, vocÃª nÃ£o estÃ¡ sozinho. Ã‰ uma das reclamaÃ§Ãµes mais comuns no curso. E o problema quase sempre tem soluÃ§Ã£o rÃ¡pida â€” mas Ã© preciso saber onde olhar."*

*"Nesta aula, vamos aprender a diagnosticar a lentidÃ£o de forma sistemÃ¡tica. Vou mostrar as 6 causas mais comuns, como identificar cada uma, e a soluÃ§Ã£o exata pra cada situaÃ§Ã£o."*

*"Bora? Abre o terminal junto comigo."*

---

### BLOCO 1: DIAGNÃ“STICO INICIAL â€” Ã‰ O MODELO, A VPS OU O TELEGRAM? (1:30 â€“ 4:00)

> **[Tela: terminal com `openclaw status` e depois logs do gateway]**

*"Antes de sair mexendo em config, a gente precisa entender o que estÃ¡ devagar. Existe uma sequÃªncia lÃ³gica aqui:"*

**[Mostre o fluxograma mentalmente enquanto fala:]**

*"Primeiro â€” o Telegram recebeu sua mensagem? O gateway processou ela? O modelo respondeu? VocÃª recebeu a resposta?"*

*"Cada etapa pode ter um gargalo diferente. Vamos comeÃ§ar pelo mais fÃ¡cil: o comando `openclaw status`."*

```bash
openclaw status
```

*"Esse comando mostra uso de CPU, RAM, e o estado dos processos ativos. Se a CPU tÃ¡ em 100% ou a RAM tÃ¡ quase zerada â€” vocÃª jÃ¡ tem sua resposta."*

*"Agora, pra ver onde o tempo estÃ¡ sendo gasto, a gente olha os logs do gateway:"*

```bash
# Logs em tempo real
openclaw gateway logs --follow

# Ou filtrar por tempo de resposta
openclaw gateway logs | grep "response_time"
```

*"Nos logs, vocÃª vai ver timestamps. Se o tempo entre 'received message' e 'sent to model' Ã© grande â€” Ã© processamento interno. Se o tempo entre 'model responded' e 'sent to telegram' Ã© grande â€” Ã© problema de rede ou webhook."*

*"Se ambos sÃ£o rÃ¡pidos mas o usuÃ¡rio nÃ£o recebe â€” o problema Ã© do Telegram mesmo. Raro, mas acontece."*

**[Pausa dramÃ¡tica]**

*"Agora que temos nosso toolkit de diagnÃ³stico, vamos Ã s causas. Tenho 6 pra te mostrar â€” da mais comum pra menos comum."*

---

### BLOCO 2: CAUSA 1 â€” CONTEXTO MUITO GRANDE (4:00 â€“ 6:00)

> **[Tela: `/status` mostrando contexto alto, ex: 85%]**

*"Causa nÃºmero 1, e de longe a mais comum: contexto cheio."*

*"Lembra que a Aula Extra E explica como o contexto funciona? Aqui estÃ¡ o impacto prÃ¡tico: quanto mais tokens no contexto, mais o modelo precisa processar a cada mensagem. Uma conversa com 80% do contexto usado pode ser 3 a 5 vezes mais lenta que uma conversa nova."*

*"Ã‰ como um documento Word com 500 pÃ¡ginas abertas â€” toda operaÃ§Ã£o fica pesada."*

*"DiagnÃ³stico rÃ¡pido:"*

```
# Qualquer canal (Telegram, WhatsApp, etc.)
/status
```

*"Se aparecer '75%+' â€” vocÃª encontrou sua causa."*

**SoluÃ§Ã£o imediata:**

*"VocÃª tem duas opÃ§Ãµes:"*

```
/compact   â† resume o histÃ³rico, libera espaÃ§o, mantÃ©m contexto
/new       â† comeÃ§a sessÃ£o nova (perde histÃ³rico, comeÃ§a do zero)
```

*"`/compact` Ã© pra quando vocÃª quer continuar de onde parou. `/new` Ã© pra quando quer um pizarro limpo."*

*"Pra evitar que isso aconteÃ§a no futuro, configure compactaÃ§Ã£o automÃ¡tica:"*

```json
{
  "sessions": {
    "main": {
      "autoCompact": {
        "enabled": true,
        "thresholdPercent": 75
      }
    }
  }
}
```

---

### BLOCO 3: CAUSA 2 â€” MODELO MUITO PESADO (6:00 â€“ 8:00)

> **[Tela: arquivo de config com modelo configurado]**

*"Causa nÃºmero 2: vocÃª tÃ¡ usando um canhÃ£o pra matar formiga."*

*"Claude Opus Ã© o modelo mais inteligente. Mas 'mais inteligente' tambÃ©m significa 'mais lento e mais caro'. Se vocÃª configurou Opus pra absolutamente tudo â€” pra responder 'oi, tudo bem?' E pra rodar crons de notificaÃ§Ã£o â€” vocÃª estÃ¡ pagando caro e esperando mais do que precisa."*

*"A regra de ouro Ã©:"*

- **Sonnet** â†’ conversas normais, o dia a dia
- **Haiku** â†’ crons, alertas automÃ¡ticos, tarefas simples e repetitivas  
- **Opus** â†’ anÃ¡lise profunda, cÃ³digo complexo, quando qualidade > velocidade

*"Como configurar isso no openclaw.json:"*

```json
{
  "sessions": {
    "main": {
      "model": "gpt-4o"
    }
  },
  "crons": {
    "defaultModel": "gpt-4o-mini"
  }
}
```

*"E pra trocar o modelo na hora, sem editar config:"*

```
/model sonnet    â† muda pra Sonnet nessa sessÃ£o
/model haiku     â† muda pra Haiku
```

*"VocÃª vai sentir a diferenÃ§a na prÃ¡tica. Haiku responde em 1-2 segundos. Opus pode demorar 10-15s pra anÃ¡lises complexas. Use o certo pra cada trabalho."*

---

### BLOCO 4: CAUSA 3 â€” VPS FRACA (8:00 â€“ 9:30)

> **[Tela: `openclaw status` mostrando CPU/RAM, ou `htop`]**

*"Causa nÃºmero 3: o servidor em si tÃ¡ engasgado."*

*"A maioria dos alunos do curso comeÃ§a com um VPS de entrada â€” 1GB RAM, 1 vCPU compartilhada. Isso funciona pro inÃ­cio, mas quando vocÃª comeÃ§a a empilhar: gateway rodando, crons ativos, skills pesadas, heartbeats frequentes â€” pode nÃ£o ter headroom suficiente."*

*"Como diagnosticar:"*

```bash
openclaw status      # visÃ£o geral do OpenClaw
htop                 # uso em tempo real de CPU/RAM
free -h              # memÃ³ria disponÃ­vel
df -h                # espaÃ§o em disco (swap issue)
```

*"Sinais de alerta:"*
- RAM disponÃ­vel < 200MB
- CPU consistently > 80%
- Swap sendo usado (isso Ã© pÃ©ssimo pra performance)

*"SoluÃ§Ãµes, em ordem de custo:"*

1. **GrÃ¡tis:** Otimize o que tÃ¡ rodando (prÃ³ximas causas)
2. **~$5/mÃªs:** Upgrade pra 2GB RAM (Hetzner, DigitalOcean, etc.)
3. **Reorganize:** Mova crons pesados pra horÃ¡rios de menos carga

---

### BLOCO 5: CAUSA 4 â€” MUITOS CRONS SIMULTÃ‚NEOS (9:30 â€“ 11:00)

> **[Tela: config de crons, vÃ¡rios com mesmo horÃ¡rio]**

*"Causa nÃºmero 4: todos os seus crons acordam ao mesmo tempo."*

*"Imagina que vocÃª tem 5 crons configurados. Todos pra Ã s 09:00. O sistema acorda, tenta rodar os 5 ao mesmo tempo, todos fazem chamadas pro modelo, todos competem pelo mesmo CPU e memÃ³ria. A sessÃ£o principal fica esperando na fila."*

*"DiagnÃ³stico: liste seus crons ativos:"*

```bash
openclaw cron list
```

*"Se vocÃª ver vÃ¡rios com horÃ¡rios idÃªnticos ou muito prÃ³ximos â€” encontrou o problema."*

*"SoluÃ§Ã£o: escalone os horÃ¡rios:"*

```json
{
  "crons": [
    { "name": "daily-summary", "schedule": "0 9 * * *" },
    { "name": "weather-check", "schedule": "5 9 * * *" },
    { "name": "news-digest", "schedule": "10 9 * * *" },
    { "name": "task-reminder", "schedule": "15 9 * * *" }
  ]
}
```

*"Separe ao menos 5 minutos entre crons pesados. Ou espalhe ao longo do dia â€” nem tudo precisa ser Ã s 9h."*

---

### BLOCO 6: CAUSA 5 â€” SKILLS PESADAS (11:00 â€“ 12:30)

> **[Tela: AGENTS.md ou config de skills]**

*"Causa nÃºmero 5: skills que demoram pra carregar em todo turno."*

*"Algumas skills leem arquivos grandes, fazem chamadas de rede, ou executam cÃ³digo pesado toda vez que sÃ£o invocadas. Se vocÃª tem skills assim configuradas pra carregar automaticamente em cada mensagem â€” vocÃª estÃ¡ pagando esse custo em todo request."*

*"DiagnÃ³stico: olhe o seu AGENTS.md ou configuraÃ§Ã£o de skills:"*

```bash
# Quais skills estÃ£o sendo carregadas automaticamente?
cat /root/.openclaw/workspace-*/AGENTS.md | grep -i skill
```

*"SoluÃ§Ãµes:"*

1. **Carregamento sob demanda:** Configure a skill pra carregar sÃ³ quando necessÃ¡rio, nÃ£o em todo turno
2. **Cache local:** Se a skill busca dados externos, adicione cache (ex: buscar clima sÃ³ a cada 30min)
3. **Revise a lista:** VocÃª realmente precisa de todas as skills ativas? Desative as que nÃ£o usa

```json
{
  "skills": {
    "loadOnDemand": true,
    "autoload": ["weather"]
  }
}
```

---

### BLOCO 7: CAUSA 6 â€” HEARTBEATS MUITO FREQUENTES (12:30 â€“ 13:30)

> **[Tela: configuraÃ§Ã£o de heartbeat]**

*"Causa nÃºmero 6: heartbeat acelerado demais."*

*"O heartbeat Ã© a checagem periÃ³dica que o agente faz â€” email, calendÃ¡rio, notificaÃ§Ãµes. Se vocÃª configurou isso pra checar a cada 5 minutos, vocÃª tem 12 invocaÃ§Ãµes do modelo por hora. Em background. Competindo com suas conversas."*

*"DiagnÃ³stico:"*

```bash
# Ver configuraÃ§Ã£o atual de heartbeat
cat ~/.openclaw/config.json | grep -A 5 heartbeat
```

*"SoluÃ§Ã£o â€” ajuste o intervalo:"*

```json
{
  "heartbeat": {
    "enabled": true,
    "intervalMinutes": 30,
    "model": "gpt-4o-mini"
  }
}
```

*"Regra de ouro: heartbeat a cada 30 minutos Ã© suficiente pra 95% dos casos. E sempre use Haiku pro heartbeat â€” Ã© rÃ¡pido e barato."*

---

### BLOCO 8: QUANDO O PROBLEMA Ã‰ DO TELEGRAM (13:30 â€“ 14:30)

> **[Tela: logs mostrando model response time vs delivery time]**

*"Existe uma sÃ©tima causa que nÃ£o Ã© culpa do seu setup: o Telegram em si."*

*"Eventualmente â€” especialmente em regiÃµes mais afastadas dos datacenters do Telegram, ou durante picos de trÃ¡fego na plataforma â€” as mensagens demoram na rede antes de chegarem ao webhook. Ou antes de serem entregues de volta."*

*"Como identificar: os logs do gateway vÃ£o mostrar tempo de resposta normal do modelo, mas delay grande na entrega:"*

```
[15:23:01] Message received
[15:23:01] Sent to model
[15:23:04] Model responded (3s) â† normal
[15:23:09] Delivered to Telegram (5s) â† suspeito
```

*"Nesse caso, a soluÃ§Ã£o de curto prazo Ã© ativar o streaming parcial:"*

```json
{
  "channels": {
    "telegram": {
      "streaming": "partial"
    }
  }
}
```

*"Com streaming parcial, o usuÃ¡rio comeÃ§a a ver o texto chegando enquanto o modelo ainda estÃ¡ gerando. A resposta completa pode demorar o mesmo tempo â€” mas a percepÃ§Ã£o de velocidade melhora muito. Ã‰ a diferenÃ§a entre 'o bot nÃ£o respondeu' e 'o bot estÃ¡ digitando'."*

---

### RECAP E CONCLUSÃƒO (14:30 â€“ 16:00)

> **[Tela: fluxograma de diagnÃ³stico ou slides de resumo]**

*"Vamos recapitular o que vimos hoje:"*

*"Quando o bot estiver lento, siga esta ordem:"*

1. **`openclaw status`** â†’ CPU/RAM OK?
2. **`/status` no chat** â†’ contexto acima de 75%? â†’ `/compact` ou `/new`
3. **Logs do gateway** â†’ onde estÃ¡ o delay?
4. **Modelo** â†’ Opus onde deveria ser Sonnet?
5. **Crons** â†’ muitos no mesmo horÃ¡rio?
6. **Heartbeat** â†’ intervalos muito curtos?
7. **Skills** â†’ algo carregando em todo turno?
8. **Streaming** â†’ ativar `partial` se o problema for percepÃ§Ã£o

*"A boa notÃ­cia: na maioria dos casos, o problema Ã© contexto cheio ou modelo errado â€” e ambos se resolvem em menos de 2 minutos."*

*"Valeu, pessoal! Na prÃ³xima aula vamos falar sobre como configurar alertas pra te avisar antes que o bot fique lento. AtÃ© lÃ¡!"*

---

## ðŸ“‹ CHECKLIST PRÃ‰-GRAVAÃ‡ÃƒO

- [ ] Terminal aberto com gateway rodando
- [ ] Bot configurado no Telegram (para demo)
- [ ] Arquivo `openclaw.json` de exemplo preparado
- [ ] Logs do gateway com exemplos reais de timing
- [ ] Screenshare em monitor com resoluÃ§Ã£o 1920x1080
- [ ] Microfone testado, sem ruÃ­do de fundo
- [ ] GravaÃ§Ã£o de tela: OBS ou Loom

## ðŸ“ ASSETS NECESSÃRIOS

- Fluxograma de diagnÃ³stico (incluÃ­do no HTML da aula)
- Tabela de causas/soluÃ§Ãµes (incluÃ­da no HTML da aula)
- Exemplos de log do gateway (simulados se necessÃ¡rio)

---

*PRD gerado em: 2026-03-04 | VersÃ£o: 1.0*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
