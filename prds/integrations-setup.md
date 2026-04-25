# PRD: Setup de IntegraÃ§Ãµes

> Jogue este arquivo no agente: "Configura estas integraÃ§Ãµes seguindo o PRD"

## Contexto

Um agente sem integraÃ§Ãµes Ã© sÃ³ um chatbot. Estas sÃ£o as integraÃ§Ãµes mais Ãºteis por categoria.

## NÃ­vel 1 â€” Essenciais (fazer primeiro)

### Google Calendar
```bash
# gog CLI jÃ¡ vem instalado no OpenClaw (2026.4+)
# Se precisar instalar manualmente:
npm install -g gogcli
# ou
brew install steipete/tap/gogcli

# Autenticar (Google Workspace completo)
gog auth credentials /path/to/client_secret.json
gog auth add SEU_EMAIL@gmail.com --services gmail,calendar,drive,contacts,docs,sheets
gog auth list
```
- Permite: ver compromissos, criar/atualizar eventos, lembretes
- Cron sugerido: checar agenda a cada heartbeat
- **gog CLI (2026.4+)** Ã© o caminho recomendado: autenticaÃ§Ã£o via arquivo `client_secret.json` do Google Cloud Console â€” menos configuraÃ§Ã£o manual, mesmo acesso completo ao Google Workspace (Calendar, Drive, Gmail, Docs, Sheets, Contacts).

> ðŸ’¡ **gog CLI** Ã© o caminho recomendado para Google Workspace: configura uma vez e o agente usa pra sempre. Suporta Google Workspace completo â€” Calendar, Drive, Gmail, Docs, Sheets e Contacts.

### Telegram (jÃ¡ configurado no setup)
- Criar grupo com tÃ³picos para organizar conversas
- TÃ³picos sugeridos: Geral, ConteÃºdo, MÃ©tricas, Operacional
- dmPolicy: SEMPRE allowlist

## NÃ­vel 2 â€” Produtividade

### Google Drive
```bash
gog drive search "minha pasta" --account=SEU_EMAIL@gmail.com
```
- Upload/download de arquivos
- Ãštil para compartilhar reports, docs, planilhas

### Notion API
- Criar integraÃ§Ã£o em https://www.notion.so/my-integrations
- Guardar API key no 1Password
- Ãštil para: kanban, base de conteÃºdo, CRM

### 1Password CLI
```bash
# Instalar
# Ver: https://developer.1password.com/docs/cli/get-started/

# Uso
op item get "Nome do Item" --field credential --reveal
```
- TODA credencial deve viver no 1Password
- Nunca hardcodar API keys em arquivos

## NÃ­vel 3 â€” ConteÃºdo & MÃ©tricas

### YouTube (Data API + OAuth)
- Criar projeto no Google Cloud Console
- Habilitar YouTube Data API v3
- Gerar OAuth credentials
- Permite: listar vÃ­deos, ver analytics, agendar uploads

### Social Media via RapidAPI
- Cloud IPs sÃ£o bloqueados por Instagram, X, LinkedIn
- RapidAPI funciona como proxy:
  - Instagram Statistics API (50 req/mÃªs free)
  - X/Twitter API45 (1000 req/mÃªs free)
  - Fresh LinkedIn Scraper
- Cadastro: https://rapidapi.com

### Brave Search
- API para pesquisa web
- JÃ¡ vem configurado no OpenClaw (verificar)

## NÃ­vel 3.2 â€” GeraÃ§Ã£o de MÃ­dia (Built-in, sem skill)

### image_generate, video_generate, music_generate
Estas ferramentas sÃ£o **primeira classe no OpenClaw** â€” nenhuma skill extra ou API key extra necessÃ¡ria.

```
# Gerar imagem
image_generate(prompt="Um carrossel de LinkedIn sobre automaÃ§Ã£o de agentes")

# Gerar vÃ­deo (built-in)
video_generate(prompt="...", durationSeconds=5, size="1280x720")

# Gerar mÃºsica (built-in)
music_generate(prompt="ambient technology background music", durationSeconds=30)
```
- **image_generate:** OpenAI (DALL-E) como primÃ¡rio, Google Imagen como secundÃ¡rio
- **video_generate:** Built-in via provedores configurados (Hunyuan, Wan, etc.)
- **music_generate:** Built-in via provedores configurados
- **Importante:** nÃ£o sÃ£o skills â€” sÃ£o ferramentas nativas do OpenClaw, disponÃ­veis diretamente

## NÃ­vel 3.5 â€” PDF Nativo (Built-in desde 3.2)

### PDF Tool Nativo
Agentes OpenClaw analisam documentos PDF **nativamente** â€” sem precisar instalar nada.

```
# O agente simplesmente faz:
Analise este PDF: /caminho/para/documento.pdf
```

- **Suportado por:** OpenAI (GPT-4o) como primÃ¡rio, Google Gemini e Anthropic Claude como secundÃ¡rios
- **Multimodal nativo:** extrai texto e imagens automaticamente
- **Uso prÃ¡tico:** contratos, relatÃ³rios, notas fiscais, planilhas PDF
- **Limite:** atÃ© 10 PDFs por chamada
- Ferramenta: `pdf` tool â€” primeira classe no OpenClaw, nenhuma configuraÃ§Ã£o extra

> ðŸ’¡ Casos de uso reais: o agente analisa boletos, extrai dados de NFs para o Notion, resume relatÃ³rios longos automaticamente.

## NÃ­vel 4 â€” AvanÃ§ado

### ChartMogul (se tiver SaaS)
- MÃ©tricas de MRR, churn, LTV
- Cron semanal para report

### Crisp / Intercom (se tiver suporte)
- AnÃ¡lise de conversas
- Insights de conteÃºdo a partir de dÃºvidas reais

## Crons Essenciais

ApÃ³s configurar integraÃ§Ãµes, criar crons:

| Cron | FrequÃªncia | O que faz |
|------|-----------|-----------|
| Check agenda | A cada heartbeat | Compromissos prÃ³ximos |
| MÃ©tricas sociais | Semanal | Puxar dados das redes |
| RevisÃ£o semanal | Sexta | Revisar projetos e pendÃªncias |

**REGRA CRÃTICA para crons:**
```
sessionTarget: "isolated"
payload.kind: "agentTurn"
delivery: { mode: "announce" }
```
NUNCA usar `systemEvent` + `main` â€” dispara mas nÃ£o executa.

## Resultado Esperado

Agente conectado Ã s suas ferramentas principais, com pelo menos 2 crons rodando.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
