# PRD: Como Integrar Suas Ferramentas â€” Skills & APIs

> Roteiro para gravaÃ§Ã£o da Aula Extra A
> PÃºblico: leigo total â€” nunca mexeu com API ou skill antes

---

## Objetivo da Aula

Ensinar como conectar o agente Ã s ferramentas que o aluno jÃ¡ usa (Notion, Google Calendar, Stripe, etc.) atravÃ©s de:
1. **Skills prontas** do ClawHub
2. **APIs diretas** (quando nÃ£o tem skill)
3. **Transformar conhecimento em skill customizada**

**Premissa:** O aluno nÃ£o sabe programar. Tudo tem que ser explicado como se fosse a primeira vez.

---

## Tempo estimado: 20-25 minutos

---

## Estrutura da Aula

### Bloco 1: Por que integrar? (3 min)

**O que mostrar:**
- Agente isolado vs agente conectado
- Exemplo visual: "Sem integraÃ§Ã£o, o agente Ã© cego. Com integraÃ§Ã£o, ele vÃª tudo."
- Case real: MGM Boss (Stripe + ChartMogul + Notion) e FLG Boss (YouTube + Instagram + Notion)

**Frase-chave:**
> "O agente sÃ³ Ã© Ãºtil se ele tiver acesso aos seus dados. Sem isso, ele Ã© sÃ³ um chatbot glorificado."

---

### Bloco 2: Skills do ClawHub â€” O jeito fÃ¡cil (7 min)

**O que Ã© uma skill:**
"Uma skill Ã© como um app que vocÃª instala no seu agente. AlguÃ©m jÃ¡ fez o trabalho pesado â€” vocÃª sÃ³ instala e usa."

**DemonstraÃ§Ã£o ao vivo:**

1. **Buscar skills disponÃ­veis**
   ```bash
   clawhub search notion
   ```
   Explicar: "O ClawHub Ã© tipo uma App Store de skills pra agentes."

2. **Instalar uma skill**
   ```bash
   clawhub install notion
   ```
   Explicar o que acontece:
   - Baixa o cÃ³digo da skill
   - Registra no OpenClaw
   - Agora o agente sabe usar Notion

3. **Ver skills instaladas**
   ```bash
   clawhub list
   ```

4. **Testar a skill** â€” mandar mensagem pro agente:
   > "Liste as tasks da database [ID da database] que estÃ£o com status 'In Progress'"

**Skills recomendadas pra mostrar:**
- `notion` â€” gestÃ£o de projetos
- `1password` â€” credenciais seguras
- `weather` â€” exemplo simples pra testar
- `github` â€” pra quem tem repo

---

### Bloco 2.5: gog CLI â€” Google Workspace de forma simples (2 min)

**gog CLI jÃ¡ vem instalado no OpenClaw (2026.4+).** Se precisar instalar manualmente:

```bash
# Instalar gog CLI
npm install -g gogcli
# ou via brew
brew install steipete/tap/gogcli

# Autenticar (um comando pra tudo: Calendar, Drive, Gmail, Docs, Sheets, Contacts)
gog auth credentials /path/to/client_secret.json
gog auth add voce@gmail.com --services gmail,calendar,drive,contacts,docs,sheets
gog auth list

# Usar
gog calendar events <calendarId> --from 2026-01-01 --to 2026-01-07
gog gmail search 'newer_than:7d'
gog drive search "minha pasta"
```

**O que o gog cobre (2026.4):**
- Gmail: busca, envio, reply, drafts (suporta HTML e stdin via `--body-file -`)
- Calendar: listar, criar, atualizar eventos com cores
- Drive: busca de arquivos
- Contacts: listar contatos
- Sheets: get, update, append, clear
- Docs: export e cat (leitura)

**Por que usar o gog?**
- Google Workspace completo em um CLI unificado â€” sem precisar criar projeto no Google Cloud Console manualmente
- AutenticaÃ§Ã£o via arquivo `client_secret.json` â€” o `gog auth` faz o fluxo OAuth inteiro
- Skills de Calendar, Drive e Gmail jÃ¡ usam gog por padrÃ£o
- Confirma antes de enviar email ou criar evento (safe by default)

> ðŸ’¡ Se vocÃª usa Google Workspace â€” o gog Ã© o caminho mais rÃ¡pido. Configure uma vez e o agente usa pra sempre.

---

### Bloco 3: APIs diretas â€” Quando nÃ£o tem skill (8 min)

**CenÃ¡rio:** "E se nÃ£o existir uma skill pronta pro Stripe? Ou pro seu CRM interno?"

**Case real: Integrar Stripe no MGM Boss**

**Passo a passo (mostrar o processo, nÃ£o sÃ³ o resultado):**

1. **Conseguir a API key**
   - Ir em dashboard.stripe.com â†’ Developers â†’ API Keys
   - Copiar a "Secret key" (comeÃ§a com `sk_live_` ou `sk_test_`)
   - **NUNCA** colocar direto no cÃ³digo ou config

2. **Guardar no 1Password** (seguranÃ§a!)
   ```bash
   # Se tiver a CLI do 1Password instalada
   op item create --category=api-credential \
     --title="Stripe MGM" \
     --vault="Meu Vault" \
     secret_key="sk_live_..."
   ```
   Ou manualmente pelo app/web.

3. **Recuperar quando o agente precisar** â€” mostrar como o agente faz isso:
   > "Agente, pegue a Stripe key do 1Password e me mostre meu MRR atual."

   Por trÃ¡s dos panos, o agente vai:
   ```bash
   STRIPE_KEY=$(op item get "Stripe MGM" --vault "Meu Vault" --field secret_key --reveal)
   curl https://api.stripe.com/v1/balance \
     -u "$STRIPE_KEY:"
   ```

4. **Registrar no TOOLS.md** â€” documentar a integraÃ§Ã£o:
   ```markdown
   ### Stripe (Pagamentos MGM)
   - **Item 1PW:** `Stripe MGM`
   - **Vault:** Meu Vault
   - **Acesso:** Read livre, Write = aprovaÃ§Ã£o do Bruno
   ```

**Explicar o fluxo:**
> "1Password â†’ Agente pega credencial â†’ Usa API â†’ Retorna resultado. Sua senha nunca fica exposta."

---

### Bloco 3.5: PDF Tool Nativo â€” jÃ¡ disponÃ­vel no seu agente (1 min)

**Sem instalar nada â€” jÃ¡ funciona:**

> "Desde a versÃ£o 3.2, seu agente consegue analisar PDFs diretamente. Nenhuma skill, nenhuma configuraÃ§Ã£o."

**Demonstrar ao vivo:**
- Arrastar um PDF para o chat (ou mencionar o path)
- Pedir: "Analise este contrato e me diga os pontos crÃ­ticos"
- Mostrar o agente extraindo informaÃ§Ãµes do PDF em tempo real

**Casos de uso prÃ¡ticos:**
- Analisar boletos e notas fiscais
- Resumir relatÃ³rios longos
- Extrair dados de planilhas em PDF
- Revisar contratos (com alerta: agente nÃ£o Ã© advogado!)

**Detalhes tÃ©cnicos (breve):**
- Suporte nativo: OpenAI (GPT-4o) como primÃ¡rio, Google (Gemini) e Anthropic (Claude) como secundÃ¡rios
- Multimodal nativo â€” extrai texto e imagens automaticamente
- Limite: atÃ© 10 PDFs por mensagem
- Ferramenta: `pdf` tool (primeira classe no OpenClaw)

---

### Bloco 4: Transformar conhecimento em skill (5 min)

**CenÃ¡rio:** "E se vocÃª usar uma ferramenta nichada que ninguÃ©m mais usa? Tipo um CRM interno da sua empresa?"

**Mostrar o conceito (nÃ£o precisa implementar ao vivo):**

Uma skill Ã© sÃ³ uma pasta com:
- `SKILL.md` â€” instruÃ§Ãµes pro agente
- Scripts auxiliares (se necessÃ¡rio)

**Exemplo simples â€” Skill "CRM da Empresa X":**

Criar pasta:
```bash
mkdir -p ~/.openclaw/skills/crm-empresa-x
```

Criar `SKILL.md`:
```markdown
# Skill: CRM da Empresa X

Acesso Ã  API interna do CRM.

## Credenciais
- API Key: 1Password â†’ "CRM Empresa X API Key"
- Base URL: https://crm.empresax.com.br/api/v1

## Endpoints principais

### Listar leads
GET /leads?status=active
Header: Authorization: Bearer {API_KEY}

### Criar lead
POST /leads
Body: {"name": "...", "email": "...", "phone": "..."}

## Como usar
O agente deve:
1. Pegar a API key do 1Password
2. Fazer chamadas via curl ou fetch
3. Parsear a resposta JSON
```

**Registrar a skill:**
```bash
openclaw skills register ~/.openclaw/skills/crm-empresa-x
```

**Testar:**
> "Agente, me liste os leads ativos no CRM."

**Explicar:**
> "VocÃª nÃ£o precisa saber programar. SÃ³ precisa saber onde estÃ¡ a documentaÃ§Ã£o da API e copiar pra dentro do SKILL.md. O agente faz o resto."

---

### Bloco 5: Cases reais â€” FLG e MGM (3 min)

**Mostrar os dois workspaces lado a lado:**

**MGM Boss (`workspace-mgm-boss`):**
- **TOOLS.md aberto** â€” mostrar as integraÃ§Ãµes documentadas:
  - Supabase (banco de dados)
  - Stripe (pagamentos)
  - ChartMogul (mÃ©tricas SaaS)
  - PostHog (analytics)
  - Notion (sprint board)
  - Google Analytics + Search Console (SEO)

**FLG Boss (`workspace-flg-boss`):**
- **TOOLS.md aberto** â€” mostrar:
  - YouTube Data API + Analytics API
  - Instagram via RapidAPI
  - LinkedIn via RapidAPI
  - Twitter/X Bearer Token
  - Tella.tv (gravaÃ§Ãµes)
  - Figma (design)
  - Notion (calendÃ¡rio editorial)

**Frase-chave:**
> "Esses dois agentes veem TUDO que acontece nos meus negÃ³cios. E eu nÃ£o preciso abrir 15 abas todo dia."

---

### Bloco 6: Checklist prÃ¡tico pra integrar qualquer ferramenta (2 min)

**Roteiro que o aluno pode seguir:**

1. âœ… A ferramenta tem API? (procurar "API documentation" no Google)
2. âœ… Existe skill pronta no ClawHub? (`clawhub search nome-da-ferramenta`)
3. âœ… Se sim â†’ instalar e testar
4. âœ… Se nÃ£o â†’ seguir o fluxo:
   - Pegar API key na ferramenta
   - Guardar no 1Password
   - Documentar no TOOLS.md
   - Testar com o agente
5. âœ… Se for recorrente â†’ criar uma skill customizada

---

## Alertas de SeguranÃ§a (enfatizar)

ðŸ”´ **NUNCA** colocar API keys direto no cÃ³digo ou config
ðŸ”´ **NUNCA** commitar credenciais no Git
ðŸ”´ **SEMPRE** usar 1Password (ou similar)
ðŸ”´ **SEMPRE** definir permissÃµes (read-only quando possÃ­vel)

**Exemplo real do MGM:**
> "No MGM Boss, o agente pode LER dados do Stripe Ã  vontade. Mas pra fazer um refund ou cancelar uma subscription, ele PRECISA pedir aprovaÃ§Ã£o minha. Isso estÃ¡ documentado no TOOLS.md e ele respeita."

---

## Checkpoint da Aula

Ao final, o aluno deve saber:
- [ ] O que Ã© uma skill e onde encontrar
- [ ] Como instalar uma skill do ClawHub
- [ ] Como integrar uma API direto (sem skill pronta)
- [ ] Onde guardar credenciais (1Password)
- [ ] Como documentar integraÃ§Ãµes no TOOLS.md
- [ ] Como criar uma skill customizada (conceito)

---

## Prompt que vai no PDF

Vai estar no arquivo `prompts/modulo-extra-a-integracoes.md`.

---

## Troubleshooting Comum

### "gog: command not found"
```bash
npm install -g gogcli
# ou
brew install steipete/tap/gogcli
```

### "clawhub: command not found"
```bash
npm install -g clawhub
```

### "Skill instalou mas agente nÃ£o sabe usar"
```bash
# Verificar se registrou
openclaw skills list
# Se nÃ£o aparece, registrar manualmente
openclaw skills register ~/.openclaw/skills/nome-da-skill
# Reiniciar gateway
openclaw gateway restart
```

### "API retorna 401 Unauthorized"
- Verificar se a API key estÃ¡ certa
- Verificar se expirou
- Verificar se tem permissÃµes suficientes

---

*Esta aula Ã© o divisor de Ã¡guas: antes dela, o aluno tem um agente isolado. Depois, tem um agente que vÃª tudo.*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
