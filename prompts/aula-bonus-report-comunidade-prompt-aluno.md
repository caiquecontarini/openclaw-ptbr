# Prompt do Aluno â€” Aula BÃ´nus: Report de Comunidade

> Copie, adapte as partes entre colchetes e mande para o seu agente OpenClaw.

---

## Prompt Principal

```
Quero criar um relatÃ³rio semanal automÃ¡tico das mensagens da minha comunidade.

**Minha fonte de dados:**
[Descreva onde ficam as mensagens. Exemplos:
- "Tenho um Supabase com tabela 'messages'. Campos: created_at, content, user_name, chat_id"
- "Uso o MyGroupMetrics â€” meu user_owner Ã© [seu ID]"
- "Tenho acesso Ã  API do Crisp com workspace_id [seu ID]"
- "Tenho um CSV exportado do grupo â€” posso fazer upload"]

**Grupos/canais a analisar:**
[Liste os grupos ou canais. Exemplos:
- "Grupo WhatsApp Alunos â€” chat_id: 120363xxxxxxxx"
- "Canal Telegram Clientes â€” @meucanal"
- "Workspace Crisp â€” todos os tickets"]

**Credenciais:**
[As credenciais estÃ£o no 1Password? Se sim, informe o nome do item e o vault.
Se nÃ£o, me avise que eu te oriento a guardar antes de continuar.]

**O que quero no relatÃ³rio:**
- Sentimento geral da semana (positivo / negativo / neutro)
- DÃºvidas e temas mais frequentes
- HorÃ¡rios de pico de atividade
- Quem mais ajuda os outros (possÃ­veis embaixadores)
- ComparaÃ§Ã£o com as semanas anteriores

**Formato de entrega:**
- HTML dark theme com grÃ¡ficos visuais
- Convertido em PDF
- Enviado aqui no Telegram toda segunda Ã s 9h

**O que preciso que vocÃª faÃ§a:**
1. Criar uma Skill em skills/research/report-[nome-comunidade]/ com todo o processo documentado
2. Testar a conexÃ£o com minha fonte de dados
3. Gerar o primeiro relatÃ³rio agora para eu ver como fica
4. Criar o cron para rodar automaticamente toda segunda Ã s 9h

GUARDRAIL: apenas leitura nos dados. Nenhuma escrita, atualizaÃ§Ã£o ou deleÃ§Ã£o sem minha autorizaÃ§Ã£o explÃ­cita.
```

---

## VariaÃ§Ãµes por Fonte de Dados

### Se vocÃª usa MyGroupMetrics (Supabase MGM)

```
Minha fonte de dados Ã© o Supabase do MyGroupMetrics.
As credenciais estÃ£o no 1Password com o nome "Supabase MGM", vault "Meu Vault".
Campos relevantes da tabela interactions: created_at, message, user_name, chat_id, response_to.

Meus grupos:
- [Nome do grupo 1] â€” chat_id: [ID do grupo no WhatsApp]
- [Nome do grupo 2] â€” chat_id: [ID do grupo no WhatsApp]

Meu group_owner no banco Ã©: [seu ID de usuÃ¡rio no MGM]
```

### Se vocÃª usa Crisp

```
Minha fonte de dados Ã© o Crisp.
As credenciais (website_id e token) estÃ£o no 1Password como "Crisp API", vault "Meu Vault".
Quero analisar todas as conversas dos Ãºltimos 30 dias do workspace.
```

### Se vocÃª tem Supabase prÃ³prio

```
Tenho um Supabase prÃ³prio.
URL e service_key estÃ£o no 1Password como "[Nome do Item]", vault "[Nome do Vault]".
Tabela: [nome da tabela]
Campos: [created_at ou equivalente], [campo de texto], [campo de usuÃ¡rio], [campo de grupo/canal se houver]
```

### Se vocÃª tem sÃ³ um CSV

```
Tenho um arquivo CSV com o histÃ³rico do grupo.
Vou fazer upload agora. Depois de analisar, quero que vocÃª crie um processo para eu poder atualizar o CSV toda semana e gerar o novo relatÃ³rio.
Campos no CSV: [liste as colunas]
```

---

## O que esperar depois de mandar o prompt

O agente vai:

1. **Confirmar a conexÃ£o** â€” vai testar o acesso Ã  sua fonte de dados e te dizer quantas mensagens encontrou
2. **Criar a Skill** â€” vai documentar todo o processo em `skills/research/report-[nome]/SKILL.md`
3. **Gerar o primeiro relatÃ³rio** â€” HTML + PDF direto no chat para vocÃª ver e aprovar
4. **Criar o cron** â€” vai verificar se segunda Ã s 9h estÃ¡ livre e configurar o agendamento

Se algo nÃ£o funcionar (credencial errada, estrutura de tabela diferente), o agente vai te pedir as informaÃ§Ãµes que faltam antes de continuar.

---

## Dicas

**Calibre o sentimento para o seu nicho**

Depois do primeiro relatÃ³rio, se os percentuais nÃ£o parecerem certos, peÃ§a:
```
O sentimento positivo estÃ¡ alto demais / baixo demais. 
Me mostra quais mensagens foram classificadas como positivas e negativas.
Quero ajustar o dicionÃ¡rio de palavras.
```

**Adicione tÃ³picos especÃ­ficos da sua Ã¡rea**

```
Quero que o relatÃ³rio identifique tambÃ©m mensagens sobre [seu tÃ³pico especÃ­fico].
Palavras-chave: [lista de palavras]
```

**Mude a frequÃªncia**

```
Em vez de semanal, quero relatÃ³rio mensal â€” todo dia 1 Ã s 8h.
Ajusta o cron para: 0 8 1 * *
```


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
