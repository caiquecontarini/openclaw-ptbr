# Prompt â€” Aula Extra A: Integrar Suas Ferramentas

> Cole este prompt no chat do seu agente depois de assistir a Aula Extra A.

---

Acabei de assistir a aula sobre integraÃ§Ã£o de ferramentas. Agora quero conectar meu agente Ã s ferramentas que eu uso no dia a dia.

**O que preciso fazer:**

## 1. Mapear minhas ferramentas

Me ajude a listar as ferramentas/plataformas que eu uso mais:
- GestÃ£o de projetos? (Notion, Trello, Asana, Monday...)
- Pagamentos? (Stripe, PayPal, Mercado Pago...)
- Analytics? (Google Analytics, Mixpanel, Amplitude...)
- CRM/Vendas? (HubSpot, Pipedrive, RD Station...)
- Email marketing? (ConvertKit, Mailchimp...)
- Social media? (Buffer, Later, Hootsuite...)
- Outras ferramentas crÃ­ticas?

Pra cada uma, me diga:
- âœ… Tem skill pronta no ClawHub? (`clawhub search nome`)
- âŒ Precisa integrar API direto?

## 2. Instalar skills prontas

Para as ferramentas que **tÃªm skill pronta**, me guie pra:
1. Instalar a skill (`clawhub install nome`)
2. Configurar credenciais (se necessÃ¡rio)
3. Testar se funciona
4. Documentar no TOOLS.md

## 3. Integrar APIs diretas

Para as ferramentas **sem skill pronta**, me guie pra:
1. Descobrir onde fica a API key na ferramenta
2. Guardar no 1Password (ou me ensinar a configurar 1Password se eu nÃ£o tiver)
3. Testar a API com vocÃª
4. Documentar no TOOLS.md com:
   - Nome da integraÃ§Ã£o
   - Item no 1Password
   - PermissÃµes (read/write)
   - LimitaÃ§Ãµes ou guardrails

## 4. Documentar tudo no TOOLS.md

Crie ou atualize meu `TOOLS.md` com:
- Lista de todas integraÃ§Ãµes ativas
- Como acessar cada uma
- Guardrails de seguranÃ§a (o que vocÃª pode/nÃ£o pode fazer)

## 5. Casos de uso prÃ¡ticos

Depois de tudo configurado, me sugira **3 casos de uso prÃ¡ticos** pra testar as integraÃ§Ãµes. Exemplos:
- "Me mostre meu MRR atual do Stripe"
- "Liste as tasks do Notion com status 'In Progress'"
- "Quantas visitas teve no site ontem?"

**Regras importantes:**

ðŸ”´ **NUNCA** colocar API keys direto no cÃ³digo ou config â€” sempre 1Password
ðŸ”´ **SEMPRE** me perguntar antes de fazer operaÃ§Ãµes de escrita (criar, atualizar, deletar)
ðŸ”´ **SEMPRE** documentar no TOOLS.md quando adicionar uma integraÃ§Ã£o nova

**Se eu nÃ£o tiver 1Password instalado:**
Me explique como instalar e configurar (ou me sugira alternativas como Bitwarden).

---

Vamos comeÃ§ar pelo mapeamento das minhas ferramentas. Me faÃ§a as perguntas e vamos integrando uma por uma.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
