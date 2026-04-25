# PRD â€” Aula N-6: VPS vs Mac Mini â€” Quando Usar Cada Infraestrutura

**MÃ³dulo:** NÃºcleo (N)  
**Aula:** N-6  
**DuraÃ§Ã£o estimada:** 15â€“20 minutos  
**NÃ­vel:** Iniciante / Setup  
**Instrutor:** Bruno  

---

## ðŸŽ¯ Objetivo da Aula

Ao final desta aula, o aluno deve conseguir decidir com confianÃ§a qual infraestrutura usar para rodar o OpenClaw: VPS na nuvem ou Mac Mini local.

## ðŸ“‹ PrÃ©-requisitos

- Ter assistido N-1 a N-5 (introduÃ§Ã£o ao OpenClaw e configuraÃ§Ã£o bÃ¡sica)
- Saber o que Ã© SSH (nÃ£o precisa dominar, sÃ³ saber que existe)

---

## ðŸŽ¬ ROTEIRO DE GRAVAÃ‡ÃƒO

### [00:00 â€“ 01:30] ABERTURA â€” A DÃºvida Que Todo Mundo Tem

**[Bruno na cÃ¢mera, tom casual, como se tivesse batendo papo]**

> "Fala pessoal. Se vocÃª chegou atÃ© essa aula, provavelmente vocÃª jÃ¡ testou o OpenClaw e tÃ¡ pensando: *'Mas onde eu vou rodar isso de verdade?'* Laptop Ã© bom pra testar, mas fica travado. VocÃª nÃ£o pode desligar. E se vocÃª usa o agente o dia todo, precisa de algo mais robusto.
>
> Essa Ã© a pergunta que eu recebo toda semana: *VPS ou Mac Mini?*
>
> E a resposta honesta Ã©: depende do seu caso. Mas eu vou te dar um framework pra decidir em menos de 5 minutos. Vamos lÃ¡."

---

### [01:30 â€“ 05:00] PARTE 1 â€” O Que Ã‰ VPS e Quando Usar

**[Tela compartilhada: slides ou browser mostrando Hostinger/DigitalOcean]**

> "VPS significa *Virtual Private Server* â€” basicamente Ã© um computador que fica ligado em um datacenter em algum lugar do mundo. VocÃª paga uma mensalidade baixa e tem acesso remoto via terminal.
>
> Pensa assim: vocÃª contrata o computador de outra pessoa, mas tem controle total dele."

**[Mostra lista na tela]**

> "As vantagens do VPS sÃ£o claras:
>
> **Primeiro: custo baixo.** VocÃª consegue um VPS decente por 20, 30 dÃ³lares por mÃªs. Ã€s vezes menos. Hostinger tem planos que comeÃ§am em 10 dÃ³lares.
>
> **Segundo: sempre ligado.** VocÃª nÃ£o precisa se preocupar com queda de luz, computador travado, nada disso. O servidor fica rodando 24/7.
>
> **Terceiro: acesso de qualquer lugar.** VocÃª tÃ¡ no celular, no cafÃ©, em viagem â€” vocÃª acessa o seu agente de qualquer lugar com internet.
>
> **Quarto: sem manutenÃ§Ã£o fÃ­sica.** NÃ£o tem hardware pra cuidar. Queimou alguma coisa, Ã© problema do datacenter."

> "Mas VPS tambÃ©m tem desvantagens. A principal: vocÃª vai usar a API de algum modelo de IA, seja Claude, GPT, o que for. Seus dados *passam* por servidores de terceiros. Se vocÃª lida com informaÃ§Ã£o muito sensÃ­vel, isso pode ser um ponto.
>
> Outra coisa: a performance Ã© limitada pelo plano que vocÃª pagou. Se vocÃª precisa rodar modelos locais pesados como Llama, um VPS bÃ¡sico nÃ£o vai dar conta."

---

### [05:00 â€“ 08:30] PARTE 2 â€” O Que Ã‰ Mac Mini e Quando Usar

**[Corte pra cÃ¢mera ou slide com imagem de Mac Mini]**

> "Mac Mini Ã© um computador da Apple. Pequeno, silencioso, bem eficiente. E nos Ãºltimos anos, com os chips M1, M2, M3 e M4, ele ficou absurdamente poderoso.
>
> A grande sacada do Mac Mini Ã© que vocÃª pode rodar modelos de IA *localmente*. Sem API. Sem custo de token. Seus dados ficam na sua mÃ¡quina."

> "As vantagens do Mac Mini pra rodar OpenClaw:
>
> **Poder local real.** Um Mac Mini M4 Pro, por exemplo, consegue rodar modelos de 30, 70 bilhÃµes de parÃ¢metros com velocidade razoÃ¡vel. Isso significa agente funcionando mesmo sem internet.
>
> **Privacidade total.** Nada sai da sua rede local. Se vocÃª lida com dados de clientes, contratos, informaÃ§Ãµes sigilosas, isso muda tudo.
>
> **Zero latÃªncia de rede.** O agente responde na velocidade da mÃ¡quina, nÃ£o depende de ping pra servidor.
>
> **Uma vez comprado, nÃ£o paga mais.** NÃ£o tem mensalidade. Compra uma vez e usa por anos."

> "Mas tem desvantagens claras:
>
> **Custo inicial alto.** Um Mac Mini M4 bÃ¡sico comeÃ§a em 600 dÃ³lares. O M4 Pro, que realmente faz diferenÃ§a pra IA, estÃ¡ na faixa de 1.400 a 2.000 dÃ³lares.
>
> **VocÃª precisa mantÃª-lo ligado.** Se cair a luz, desligar acidentalmente, ou precisar reiniciar, o agente vai offline.
>
> **Setup mais complexo.** VocÃª precisa configurar acesso remoto, manter o sistema, resolver problemas de hardware se aparecerem."

---

### [08:30 â€“ 11:00] PARTE 3 â€” Tabela Comparativa

**[Tela compartilhada: tabela visual]**

> "Deixa eu colocar isso lado a lado pra ficar mais claro."

| CritÃ©rio | VPS | Mac Mini |
|---|---|---|
| **Custo mensal** | $10â€“$30/mÃªs | ~$0 (hardware pago) |
| **Custo inicial** | Zero | $600â€“$2.000+ |
| **Setup** | MÃ©dio (SSH + CLI) | Mais complexo (acesso remoto local) |
| **ManutenÃ§Ã£o** | MÃ­nima | VocÃª cuida do hardware |
| **Performance** | Limitada ao plano | Alta (M4 Ã© muito poderoso) |
| **Privacidade** | API de terceiros | Dados locais |
| **Modelos locais** | NÃ£o (geralmente) | Sim |
| **Acesso remoto** | Nativo | Precisa configurar |
| **Disponibilidade** | 99.9%+ garantido | Depende de vocÃª |
| **Ideal para** | ComeÃ§ar, freelancer | Empresa, privacidade |

> "Olhando assim, fica mais fÃ¡cil de decidir. Mas deixa eu falar sobre os perfis de usuÃ¡rio."

---

### [11:00 â€“ 13:30] PARTE 4 â€” CenÃ¡rios de Uso: Qual Ã‰ o Seu?

**[CÃ¢mera, tom direto]**

> "Eu vou falar sobre trÃªs perfis que aparecem bastante nos alunos do curso."

**CenÃ¡rio 1: Freelancer Solo**
> "VocÃª trabalha sozinho. Usa o agente pra organizar tarefas, responder clientes, gerar relatÃ³rios. NÃ£o tem dado ultra-sensÃ­vel. Quer comeÃ§ar rÃ¡pido e gastar pouco.
>
> **RecomendaÃ§Ã£o: VPS.** Custa 15â€“20 dÃ³lares por mÃªs, fica sempre ligado, vocÃª acessa de qualquer lugar. Perfeito."

**CenÃ¡rio 2: Empresa Pequena**
> "VocÃª tem uma equipe de 2 a 10 pessoas. Lida com dados de clientes, contratos, informaÃ§Ãµes financeiras. Privacidade Ã© importante. JÃ¡ tem estrutura de TI mÃ­nima.
>
> **RecomendaÃ§Ã£o: Mac Mini.** O investimento inicial compensa pela privacidade e pelo poder de processamento. VocÃª pode rodar modelos locais pra dados sensÃ­veis."

**CenÃ¡rio 3: Uso Pessoal / Hobby**
> "VocÃª quer experimentar, aprender, ver o que o OpenClaw pode fazer. NÃ£o tem necessidade crÃ­tica de uptime.
>
> **RecomendaÃ§Ã£o: VPS bÃ¡sico ou atÃ© o prÃ³prio computador.** NÃ£o precisa gastar muito ainda. Testa, aprende, depois decide."

---

### [13:30 â€“ 16:00] PARTE 5 â€” ConfiguraÃ§Ã£o BÃ¡sica de Cada OpÃ§Ã£o

**[Tela compartilhada: terminal]**

> "Agora vou mostrar como vocÃª *comeÃ§a* em cada caso. NÃ£o Ã© aula de setup completo â€” isso tem aula separada â€” mas quero te dar uma noÃ§Ã£o do que esperar."

**VPS â€” O Fluxo BÃ¡sico:**
> "Com VPS, vocÃª vai:
>
> 1. Contratar o servidor (Hostinger, DigitalOcean, Contabo)
> 2. Conectar via SSH: `ssh root@seu-ip`
> 3. Instalar o OpenClaw com o comando de instalaÃ§Ã£o
> 4. Configurar seu agente
>
> Ã‰ isso. Em 30 a 60 minutos vocÃª tÃ¡ funcionando. Sem dor de cabeÃ§a com hardware."

```bash
# Conectar ao VPS
ssh root@123.456.789.0

# Instalar OpenClaw (exemplo)
curl -fsSL https://openclaw.com/install.sh | bash

# Iniciar o agente
openclaw start
```

**Mac Mini â€” O Fluxo BÃ¡sico:**
> "Com Mac Mini, vocÃª vai:
>
> 1. Ligar o Mac Mini e conectar na rede
> 2. Ativar Compartilhamento Remoto nas PreferÃªncias do Sistema
> 3. Instalar o OpenClaw normalmente
> 4. Configurar acesso remoto (SSH ou VNC)
> 5. Opcionalmente instalar Ollama pra modelos locais
>
> Ã‰ um pouco mais longo, mas vocÃª faz uma vez."

---

### [16:00 â€“ 17:30] PARTE 6 â€” Quando Migrar e o Setup HÃ­brido

**[CÃ¢mera, tom consultivo]**

> "Uma pergunta que aparece bastante: *quando devo migrar de VPS pro Mac Mini (ou vice-versa)?*"

**Migrar de VPS para Mac Mini quando:**
> "VocÃª comeÃ§ou com VPS, o negÃ³cio cresceu, e agora vocÃª lida com dados de clientes que nÃ£o podem ir pra cloud. Ou vocÃª comeÃ§a a querer rodar modelos locais pesados. Ou o custo mensal do VPS comeÃ§a a parecer alto comparado com investir uma vez no hardware."

**Migrar de Mac Mini para VPS quando:**
> "O Mac Mini tÃ¡ gerando problemas de disponibilidade â€” cai a luz, alguÃ©m desliga acidentalmente. Ou vocÃª precisa de acesso 100% garantido de qualquer lugar do mundo. Nesse caso, ou vocÃª resolve o problema de infraestrutura do Mac Mini, ou usa um VPS como camada extra."

**O Setup HÃ­brido:**
> "Meu setup favorito pra quem jÃ¡ tem Mac Mini: usa o Mac Mini como servidor principal â€” pra dados sensÃ­veis, modelos locais â€” e mantÃ©m um VPS pequeno como backup e ponto de acesso externo. Se o Mac Mini cair, o VPS ainda funciona pra tarefas bÃ¡sicas.
>
> Ã‰ o melhor dos dois mundos. Mas custa um pouco mais e adiciona complexidade."

---

### [17:30 â€“ 18:30] FECHAMENTO â€” RecomendaÃ§Ã£o do Bruno

**[CÃ¢mera, direto ao ponto]**

> "EntÃ£o, minha recomendaÃ§Ã£o final:
>
> **Se vocÃª tÃ¡ comeÃ§ando agora: VPS.** Simples assim. Ã‰ mais barato pra comeÃ§ar, mais fÃ¡cil de configurar, e vocÃª vai aprender sem se preocupar com hardware.
>
> **Se vocÃª jÃ¡ usa o OpenClaw hÃ¡ algum tempo, tem dados sensÃ­veis, ou quer o mÃ¡ximo de performance: Mac Mini M4 Pro.**
>
> **Se vocÃª quer o melhor setup possÃ­vel e pode investir: Mac Mini + VPS como backup.**
>
> NÃ£o existe resposta errada. Existe a resposta certa pro seu momento.
>
> Na prÃ³xima aula, vamos configurar o VPS do zero â€” do contrato atÃ© o agente rodando. AtÃ© lÃ¡!"

---

## ðŸ“Š Estrutura de TÃ³picos

1. IntroduÃ§Ã£o â€” a dÃºvida comum (1,5 min)
2. O que Ã© VPS â€” prÃ³s e contras (3,5 min)
3. O que Ã© Mac Mini â€” prÃ³s e contras (3,5 min)
4. Tabela comparativa (2,5 min)
5. CenÃ¡rios de uso (2,5 min)
6. ConfiguraÃ§Ã£o bÃ¡sica de cada (2,5 min)
7. Quando migrar + hÃ­brido (1,5 min)
8. RecomendaÃ§Ã£o final (1 min)

**Total:** ~19 minutos

---

## ðŸŽ¨ Assets NecessÃ¡rios

- [ ] Slide com tabela comparativa (HTML/Notion ou Figma)
- [ ] Terminal mostrando comandos de SSH e instalaÃ§Ã£o
- [ ] Screenshot de painel Hostinger/DigitalOcean
- [ ] Imagem Mac Mini M4 (site Apple ou foto prÃ³pria)

## ðŸ“¦ EntregÃ¡veis Relacionados

- `docs/aula-n6-vps-vs-macmini.html` â€” Material de apoio visual
- `docs/aula-n6-vps-vs-macmini.pdf` â€” VersÃ£o para download
- `prompts/aula-n6-vps-vs-macmini-prompt-aluno.md` â€” Prompt pÃ³s-aula


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
