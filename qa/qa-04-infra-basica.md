# â“ Q&A â€” Infraestrutura BÃ¡sica (Porta, SSH, ConexÃ£o)

> Linguagem simples. Sem terminal. Cole o prompt no seu bot e ele resolve.

---

## "Apareceu 'address already in use' ou 'port in use'"

**O que aconteceu:** Tem outro programa usando a mesma porta que o OpenClaw quer usar. Ã‰ como duas pessoas tentando usar a mesma cadeira ao mesmo tempo.

**O que fazer:**
Cole esse prompt no seu bot:

```
Apareceu um erro de "port already in use" ou "address already in use".
Me ajuda a resolver:
1. Qual porta estÃ¡ em conflito?
2. Qual processo estÃ¡ usando essa porta?
3. Como resolver â€” parar o processo que estÃ¡ atrapalhando ou mudar a porta do OpenClaw?
4. Como confirmar que resolveu?
```

---

## "O bot nÃ£o conecta / 'localhost refused connection'"

**O que aconteceu:** O gateway (o programa principal do OpenClaw) provavelmente nÃ£o estÃ¡ rodando, ou estÃ¡ em uma porta diferente da que vocÃª estÃ¡ tentando acessar.

**O que fazer:**
Cole esse prompt no seu bot (se tiver acesso por outro canal):

```
Estou com problema de conexÃ£o â€” "connection refused" no localhost.
Me ajuda a diagnosticar:
1. O gateway do OpenClaw estÃ¡ rodando?
2. Em qual porta ele deveria estar?
3. Como verificar o status sem usar muito o terminal?
4. Como reiniciar o gateway de forma segura?
```

**Se nÃ£o conseguir acessar o bot de jeito nenhum:** Tente acessar o painel do OpenClaw pelo Mission Control ou pelo link que vocÃª configurou no setup.

---

## "Apareceu 'command not found' quando tento usar algo"

**O que aconteceu:** O programa que vocÃª quer usar nÃ£o estÃ¡ instalado, ou o caminho nÃ£o estÃ¡ configurado corretamente.

**O que fazer:**
Cole esse prompt no seu bot:

```
Apareceu "command not found" quando tentei usar [NOME DO COMANDO].
Me ajuda:
1. Esse comando deveria estar instalado no OpenClaw?
2. Como instalar se nÃ£o estiver?
3. Como verificar se estÃ¡ no caminho certo?
```

---

## "NÃ£o sei como acessar meu servidor remotamente"

**O que aconteceu:** VocÃª precisa se conectar Ã  sua VPS de qualquer lugar com seguranÃ§a.

**O que fazer:**
Cole esse prompt no seu bot:

```
Preciso acessar meu servidor remotamente de forma segura.
Me explica de forma bem simples:
1. O que Ã© um tÃºnel SSH e pra que serve?
2. Como configuro acesso seguro via Tailscale ou Cloudflare Tunnel?
3. Qual Ã© mais fÃ¡cil pra iniciante?
4. Me guia pelo processo de configuraÃ§Ã£o passo a passo.
```

**Dica:** Tailscale Ã© a opÃ§Ã£o mais simples pra iniciantes â€” instala em 5 minutos e funciona como uma VPN pessoal gratuita.

---

## "Minha VPS estÃ¡ lenta / usando muita memÃ³ria"

**O que fazer:**
Cole esse prompt no seu bot:

```
Minha VPS parece estar lenta ou usando muita memÃ³ria/CPU.
Me ajuda a diagnosticar:
1. Quais processos estÃ£o consumindo mais recursos?
2. Tem algum agente ou cron rodando desnecessariamente?
3. O que posso fazer pra reduzir o consumo?
4. Quando faz sentido fazer upgrade da VPS?
```

---

*Ãšltima atualizaÃ§Ã£o: Fev/2026*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
