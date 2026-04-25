# Prompt do Aluno â€” Aula N-1: Configurar API Key

> **Como usar:** Copie o prompt abaixo e cole no chat do seu agente OpenClaw apÃ³s assistir a aula.
>
> âš ï¸ **Nota:** Esta aula configura credenciais no OpenClaw. O caminho recomendado Ã© **ChatGPT OAuth** (1 clique, usa sua assinatura existente). TambÃ©m mostra API Key direta como alternativa.

---

## ðŸ“‹ Prompt Principal

```
OlÃ¡! Acabei de assistir a aula N-1 do curso OpenClaw sobre configuraÃ§Ã£o de API Keys. 

Preciso da sua ajuda para:
1. Verificar se minha configuraÃ§Ã£o estÃ¡ correta
2. Fazer os exercÃ­cios prÃ¡ticos da aula
3. Resolver qualquer problema que encontrar

Vamos comeÃ§ar com um diagnÃ³stico completo da minha configuraÃ§Ã£o?
```

---

## ðŸ§ª ExercÃ­cio 1 â€” DiagnÃ³stico da ConfiguraÃ§Ã£o

```
Por favor, faÃ§a um diagnÃ³stico completo da minha configuraÃ§Ã£o atual do OpenClaw:

1. Execute `openclaw status` e me mostre o resultado
2. Identifique quais providers estÃ£o configurados (OpenAI/ChatGPT, Anthropic, Google, etc.)
3. Para cada provider, verifique se o status Ã© "Connected"
4. Me diga se hÃ¡ algum problema ou alerta

ApÃ³s o diagnÃ³stico, me explique o que cada parte do output significa.
```

---

## ðŸ”‘ ExercÃ­cio 2 â€” Configurar API Key (fluxo principal)

```
Quero configurar minha API Key no OpenClaw usando o fluxo correto.

Por favor, me guie pelo processo:
1. Me explique a diferenÃ§a entre ChatGPT/OpenAI via OAuth, OpenAI API Key e OpenRouter â€” quando uso cada um?
2. Me guie para obter minha API Key da OpenAI (platform.openai.com)
3. Configure a key no OpenClaw usando o fluxo atual mais seguro
4. Se fizer sentido, me explique como adicionar OpenRouter depois para testar outros LLMs
5. Confirme que estÃ¡ funcionando com `openclaw status`

Importante: NÃ£o hardcode a key em nenhum arquivo de cÃ³digo ou .env â€” use o config do OpenClaw ou `openclaw secrets`.
```

---

## ðŸ” ExercÃ­cio 3 â€” VerificaÃ§Ã£o de SeguranÃ§a das Credenciais

```
Quero verificar se minhas credenciais estÃ£o armazenadas de forma segura.

Por favor:
1. Execute `openclaw secrets audit` para verificar se hÃ¡ credenciais expostas
2. Verifique as permissÃµes do arquivo ~/.openclaw/config.json (deve ser 600)
3. Se estiver em um projeto git, verifique se config.json estÃ¡ no .gitignore
4. Confirme que NÃƒO hÃ¡ API keys hardcodadas em arquivos de cÃ³digo ou .env

Se houver algum problema, use `openclaw secrets apply` para migrar as credenciais para o local correto.
```

---

## ðŸ”— ExercÃ­cio 4 â€” Teste Real de Conectividade

```
Agora vamos testar se as credenciais funcionam de verdade, nÃ£o sÃ³ se estÃ£o configuradas.

Por favor, faÃ§a um teste real:
1. Tente uma chamada simples Ã  API da OpenAI (se configurada)
2. Confirme qual modelo estÃ¡ sendo usado
3. Me mostre o resultado â€” seja sucesso ou erro especÃ­fico

Se o teste falhar, me ajude a diagnosticar o problema com detalhes.
```

---

## ðŸš¨ ExercÃ­cio 5 â€” Troubleshooting Guiado (use se tiver problemas)

```
Estou com um problema na minha configuraÃ§Ã£o. 

[DESCREVA SEU ERRO AQUI â€” por exemplo:]
- "Aparece 'Invalid API Key' quando tento usar o Claude"
- "openclaw status mostra 'Not configured'"
- "Aparece 'Unauthorized' ou '401' ao testar"
- "A key foi aceita mas o modelo nÃ£o responde"

Preciso de ajuda para resolver isso passo a passo. Por favor:
1. Explique o que esse erro significa
2. Me dÃª os passos exatos para resolver
3. Me ajude a verificar se funcionou apÃ³s cada passo
```

---

## ðŸ“Š ExercÃ­cio 6 â€” Entendendo Rate Limits vs Credencial InvÃ¡lida

```
Quero entender a diferenÃ§a entre rate limit e credencial invÃ¡lida na prÃ¡tica.

Por favor, me explique:
1. Como identificar um erro de rate limit (qual mensagem, qual HTTP status)
2. Como identificar um erro de credencial invÃ¡lida (qual mensagem, qual HTTP status)
3. O que fazer em cada caso
4. Como verificar meu plano/cota atual nos providers que configurei

TambÃ©m quero saber: existe algum comando do OpenClaw para ver meu uso atual de tokens/requisiÃ§Ãµes?
```

---

## ðŸ”„ ExercÃ­cio 7 â€” ReconfiguraÃ§Ã£o (se precisar trocar a chave)

```
Quero praticar o processo de reconfiguraÃ§Ã£o, como se precisasse trocar minha API Key.

Por favor, me guie pelo processo completo:
1. Como rotacionar (substituir) uma API Key sem interromper o serviÃ§o
2. Qual comando usar para atualizar as credenciais no OpenClaw
3. Como verificar que a nova chave estÃ¡ funcionando
4. Boas prÃ¡ticas: usar `openclaw secrets` para armazenar, nunca colocar em .env ou cÃ³digo

NÃ£o precisa executar de verdade â€” sÃ³ me explique o processo passo a passo.
```

---

## âœ… VerificaÃ§Ã£o Final de Aprendizado

```
Para encerrar os exercÃ­cios da aula N-1, me faÃ§a um quiz rÃ¡pido com 5 perguntas sobre:
- DiferenÃ§a entre OAuth, OpenAI API Key e OpenRouter
- Onde as credenciais devem ser armazenadas (spoiler: openclaw secrets ou config)
- Como interpretar o openclaw status
- Como distinguir rate limit de credencial invÃ¡lida
- Boas prÃ¡ticas de seguranÃ§a com API Keys

ApÃ³s eu responder, me dÃª um feedback detalhado sobre o que acertei e o que preciso revisar.
```

---

## ðŸ’¡ Dica de Uso

> Se vocÃª ainda nÃ£o configurou suas credenciais e estÃ¡ vendo erros, use este prompt mais direto:

```
Preciso configurar minha API Key do OpenClaw do zero. 
Tenho minha API Key da OpenAI em mÃ£os (obtida em platform.openai.com).

Por favor, me guie passo a passo pelo processo completo, desde o terminal atÃ© verificar que estÃ¡ funcionando. Estou usando [Linux/Mac/Windows â€” escolha um].

Lembre: quero usar API Key diretamente, nÃ£o OAuth.
```

---

*Prompt para Aula N-1 Â· Curso OpenClaw Â· Pixel EducaÃ§Ã£o*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
