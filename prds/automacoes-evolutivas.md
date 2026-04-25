# Aula: AutomaÃ§Ãµes Evolutivas â€” Do Manual ao AutomÃ¡tico

**Objetivo:** Ensinar o aluno a **evoluir uma tarefa manual em automaÃ§Ã£o completa**, seguindo o fluxo natural de maturidade de um processo.

**DuraÃ§Ã£o:** 25-30 minutos

---

## ðŸŽ¯ Conceito Central

**AutomaÃ§Ã£o nÃ£o comeÃ§a com cÃ³digo. ComeÃ§a com repetiÃ§Ã£o.**

O erro clÃ¡ssico: tentar automatizar algo que vocÃª fez 1 vez. O jeito certo:

1. **Fazer manual** (1-3x) â€” aprender o processo
2. **Documentar como skill** â€” capturar o conhecimento
3. **Criar atalhos** â€” reduzir fricÃ§Ã£o
4. **Adicionar checks** â€” detectar quando fazer
5. **Automatizar completamente** â€” deixar rodar sozinho

---

## ðŸ“š Estrutura da Aula

### Parte 1: O Ciclo de EvoluÃ§Ã£o (5 min)

**Explicar os 5 estÃ¡gios:**

#### EstÃ¡gio 1: Manual Puro
- **Quando:** Tarefa nova, ainda aprendendo
- **Como:** VocÃª faz, descobre os passos, anota mentalmente
- **Exemplo:** "Baixar backup do Notion toda sexta"

#### EstÃ¡gio 2: Skill Documentada
- **Quando:** JÃ¡ fez 2-3x, sabe os passos
- **Como:** Cria `SKILL.md` com checklist ou script
- **Exemplo:** Criar `/skills/notion-backup/SKILL.md`

#### EstÃ¡gio 3: Alias/Atalho
- **Quando:** Faz toda semana, quer economizar tempo
- **Como:** Criar alias bash ou funÃ§Ã£o rÃ¡pida
- **Exemplo:** `alias backup-notion="./skills/notion-backup/run.sh"`

#### EstÃ¡gio 4: Heartbeat Check
- **Quando:** Ã€s vezes esquece de fazer
- **Como:** Adicionar check no `HEARTBEAT.md`
- **Exemplo:** "Sexta-feira? Lembrar de fazer backup."

#### EstÃ¡gio 5: Cron AutomÃ¡tico
- **Quando:** Processo 100% previsÃ­vel
- **Como:** Cron job roda sozinho, sÃ³ notifica se der erro
- **Exemplo:** Cron roda toda sexta 18h, manda resultado no Telegram

---

### Parte 2: Caso Real â€” Backup do Notion (10 min)

**Vamos seguir o fluxo completo com exemplo prÃ¡tico.**

#### Passo 1: Manual Puro (Semana 1)

**Contexto:** VocÃª quer fazer backup semanal do Notion.

**Como faz:**
1. Abrir Notion no navegador
2. Settings â†’ Export All Workspace Content
3. Escolher formato (Markdown + CSV)
4. Baixar o ZIP
5. Subir no Google Drive (pasta `/Backups/Notion/`)

**Descobertas:**
- Demora ~2 min pra exportar
- ZIP fica com nome tipo `Export-2026-02-25.zip`
- Precisa lembrar de fazer toda sexta

**âš ï¸ Ainda nÃ£o automatiza! SÃ³ aprende o processo.**

---

#### Passo 2: Skill Documentada (Semana 2)

**VocÃª fez pela 3Âª vez. Hora de documentar.**

Criar: `/root/.openclaw/workspace-meu-agente/skills/notion-backup/SKILL.md`

```markdown
# Notion Backup

**FrequÃªncia:** Toda sexta-feira, 18h

## Checklist Manual

1. **Exportar do Notion:**
   - Ir em [Notion Settings](https://www.notion.so/my-settings)
   - Export â†’ Export All Workspace Content
   - Formato: Markdown & CSV
   - Aguardar export (~2 min)
   - Baixar ZIP

2. **Upload no Google Drive:**
   ```bash
   # Assumindo ZIP estÃ¡ em ~/Downloads/Export-YYYY-MM-DD.zip
   gog drive upload ~/Downloads/Export-*.zip \
     --parent 1aB2cD3eF4gH5iJ6kL7mN8oP9qR0  # ID da pasta Backups/Notion
   ```

3. **Limpar Downloads:**
   ```bash
   rm ~/Downloads/Export-*.zip
   ```

## Notas

- Export demora ~2 min (workspace grande)
- Notion limita exports (nÃ£o fazer mais que 1x/dia)
- Manter Ãºltimos 4 backups no Drive (1 mÃªs)
```

**BenefÃ­cio:** Agora vocÃª tem um checklist. NÃ£o esquece passos.

---

#### Passo 3: Alias/Atalho (Semana 3)

**Problema:** Toda sexta vocÃª lÃª o checklist e digita os comandos.

**SoluÃ§Ã£o:** Criar script executÃ¡vel.

Criar: `/root/.openclaw/workspace-meu-agente/skills/notion-backup/run.sh`

```bash
#!/bin/bash
set -e

echo "ðŸ”„ Iniciando backup do Notion..."

# VariÃ¡veis
BACKUP_DIR="$HOME/Downloads"
DRIVE_FOLDER_ID="1aB2cD3eF4gH5iJ6kL7mN8oP9qR0"  # Pasta Backups/Notion
DATE=$(date +%Y-%m-%d)

# Passo 1: Avisar pra fazer export manual
echo "ðŸ“‹ Passo 1: Exportar do Notion"
echo "   1. Abra: https://www.notion.so/my-settings"
echo "   2. Export â†’ Export All Workspace Content"
echo "   3. Formato: Markdown & CSV"
echo "   4. Aguarde o download (~2 min)"
echo ""
read -p "âœ… Export concluÃ­do? (pressione Enter quando baixar o ZIP)"

# Passo 2: Encontrar o ZIP mais recente
LATEST_ZIP=$(ls -t $BACKUP_DIR/Export-*.zip 2>/dev/null | head -1)

if [ -z "$LATEST_ZIP" ]; then
  echo "âŒ Erro: Nenhum Export-*.zip encontrado em $BACKUP_DIR"
  exit 1
fi

echo "ðŸ“¦ Arquivo encontrado: $(basename $LATEST_ZIP)"

# Passo 3: Upload pro Drive
echo "â˜ï¸  Fazendo upload pro Google Drive..."
export GOG_KEYRING_PASSWORD=$(op item get "GOG Keyring" --vault "Meu Vault" --field password --reveal)
gog drive upload "$LATEST_ZIP" --parent "$DRIVE_FOLDER_ID" --account seu-email@exemplo.com

# Passo 4: Limpar Downloads
echo "ðŸ—‘ï¸  Limpando Downloads..."
rm "$LATEST_ZIP"

echo "âœ… Backup concluÃ­do!"
echo "ðŸ“… PrÃ³ximo backup: sexta-feira, $(date -d 'next friday' +%Y-%m-%d)"
```

Tornar executÃ¡vel:
```bash
chmod +x /root/.openclaw/workspace-meu-agente/skills/notion-backup/run.sh
```

Criar alias no `.bashrc`:
```bash
alias backup-notion="/root/.openclaw/workspace-meu-agente/skills/notion-backup/run.sh"
```

**BenefÃ­cio:** Agora vocÃª sÃ³ roda `backup-notion` â€” o script guia vocÃª.

---

#### Passo 4: Heartbeat Check (Semana 4)

**Problema:** Ã€s vezes esquece de rodar na sexta.

**SoluÃ§Ã£o:** Adicionar check no `HEARTBEAT.md`.

Editar: `/root/.openclaw/workspace-meu-agente/HEARTBEAT.md`

```markdown
## Checks Semanais

### Sexta-feira (18h-20h)

- [ ] **Backup do Notion** â€” Se nÃ£o fez hoje, avisar
  - Comando: `backup-notion`
  - Verificar: Ãšltimo backup no Drive (`gog drive search "name contains 'Export-'" --max 1`)
  - Se Ãºltimo backup > 7 dias â†’ avisar
```

No heartbeat (cron que roda a cada 30 min), a Amora vai:
1. Verificar se Ã© sexta-feira entre 18h-20h
2. Checar Ãºltimo backup no Drive
3. Se faz > 7 dias â†’ **te avisar**: "Hey, faz tempo que nÃ£o faz backup do Notion. Quer rodar agora?"

**BenefÃ­cio:** VocÃª nÃ£o esquece. A Amora te cutuca.

---

#### Passo 5: Cron AutomÃ¡tico (Semana 6)

**Problema:** Mesmo com lembrete, vocÃª tem que fazer manualmente.

**SoluÃ§Ã£o:** Automatizar o export usando browser automation.

Criar: `/root/.openclaw/workspace-meu-agente/skills/notion-backup/auto-export.sh`

```bash
#!/bin/bash
set -e

# VariÃ¡veis
WORKSPACE_DIR="/root/.openclaw/workspace-meu-agente"
BACKUP_DIR="$HOME/Downloads"
DRIVE_FOLDER_ID="1aB2cD3eF4gH5iJ6kL7mN8oP9qR0"
DATE=$(date +%Y-%m-%d)

echo "ðŸ¤– Backup automÃ¡tico do Notion â€” $DATE"

# Passo 1: Usar browser automation pra exportar
cd $WORKSPACE_DIR
cat > /tmp/notion-export.js <<'EOF'
// Script de automaÃ§Ã£o (roda no browser via Playwright/Puppeteer)
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch();
  const page = await browser.newPage();
  
  // Login no Notion (assumindo cookies salvos)
  await page.goto('https://www.notion.so/my-settings');
  
  // Clicar em Export
  await page.click('text=Export all workspace content');
  
  // Escolher formato
  await page.click('text=Markdown & CSV');
  
  // Confirmar export
  await page.click('button:has-text("Export")');
  
  // Aguardar download (~2 min)
  await page.waitForTimeout(120000);
  
  await browser.close();
})();
EOF

# Rodar script (assumindo Node.js + Playwright instalados)
node /tmp/notion-export.js

# Passo 2: Aguardar ZIP aparecer
echo "â³ Aguardando export..."
sleep 30

# Passo 3: Upload pro Drive
LATEST_ZIP=$(ls -t $BACKUP_DIR/Export-*.zip 2>/dev/null | head -1)
if [ -z "$LATEST_ZIP" ]; then
  echo "âŒ Erro: Export falhou"
  exit 1
fi

echo "â˜ï¸  Upload: $(basename $LATEST_ZIP)"
export GOG_KEYRING_PASSWORD=$(op item get "GOG Keyring" --vault "Meu Vault" --field password --reveal)
gog drive upload "$LATEST_ZIP" --parent "$DRIVE_FOLDER_ID" --account seu-email@exemplo.com

# Passo 4: Limpar
rm "$LATEST_ZIP"
rm /tmp/notion-export.js

echo "âœ… Backup automÃ¡tico concluÃ­do!"
```

**Criar cron job no OpenClaw:**

```yaml
# /root/.openclaw/config.yaml
cron:
  jobs:
    - name: "Backup Notion Semanal"
      schedule:
        kind: cron
        expr: "0 18 * * 5"  # Sexta-feira, 18h
        tz: "America/Sao_Paulo"
      payload:
        kind: agentTurn
        message: "Rodar backup automÃ¡tico do Notion: /root/.openclaw/workspace-meu-agente/skills/notion-backup/auto-export.sh"
      sessionTarget: isolated
      delivery:
        mode: announce
        channel: telegram
        to: "1983085858"  # Seu chat privado
```

**BenefÃ­cio:** Roda sozinho toda sexta 18h. VocÃª sÃ³ recebe notificaÃ§Ã£o de sucesso (ou erro).

---

### Parte 3: Quando Parar em Cada EstÃ¡gio (5 min)

**Nem tudo precisa virar automaÃ§Ã£o completa.** Aqui vai o bom senso:

#### Fique no EstÃ¡gio 1 (Manual) quando:
- âœ… Tarefa rara (< 1x/mÃªs)
- âœ… Processo ainda mudando
- âœ… Precisa de decisÃ£o humana a cada vez
- **Exemplo:** Renovar domÃ­nio (1x/ano)

#### Fique no EstÃ¡gio 2 (Skill) quando:
- âœ… Tarefa mensal, mas complexa
- âœ… Passos mudam de vez em quando
- âœ… Quer documentaÃ§Ã£o, nÃ£o velocidade
- **Exemplo:** Deploy de app (mensal, mas cada vez Ã© diferente)

#### Fique no EstÃ¡gio 3 (Alias) quando:
- âœ… Tarefa semanal, sempre igual
- âœ… Quer rapidez, mas precisa decidir QUANDO fazer
- âœ… Contexto importa (ex: sÃ³ faz se bateu meta da semana)
- **Exemplo:** RelatÃ³rio semanal de vendas

#### Use EstÃ¡gio 4 (Heartbeat) quando:
- âœ… Tarefa semanal, Ã s vezes esquece
- âœ… Timing flexÃ­vel (entre 18h-20h, por ex.)
- âœ… Quer lembrete, nÃ£o automaÃ§Ã£o forÃ§ada
- **Exemplo:** Revisar emails importantes da semana

#### Use EstÃ¡gio 5 (Cron) quando:
- âœ… Tarefa semanal/diÃ¡ria, 100% previsÃ­vel
- âœ… Timing fixo (toda sexta 18h, todo dia 9h)
- âœ… Zero decisÃ£o humana necessÃ¡ria
- âœ… Quer esquecer que existe
- **Exemplo:** Backup de banco de dados, scraping diÃ¡rio

---

### Parte 4: Outros Exemplos de EvoluÃ§Ã£o (5 min)

#### Exemplo 1: Post Semanal no LinkedIn

**EvoluÃ§Ã£o:**
1. **Manual:** Escreve post no Notion, copia pro LinkedIn (semana 1-2)
2. **Skill:** Checklist de "como escrever post" (`skills/linkedin-post/SKILL.md`)
3. **Alias:** Script que lÃª Notion, formata, e **abre draft** no LinkedIn
4. **Heartbeat:** Segunda-feira 10h, Amora pergunta: "JÃ¡ escreveu o post da semana?"
5. **Cron:** Segunda 10h, Amora sugere tÃ³picos baseado em analytics + publica draft

#### Exemplo 2: RelatÃ³rio de Vendas

**EvoluÃ§Ã£o:**
1. **Manual:** Baixa CSV do Stripe, faz pivot no Excel (semana 1-3)
2. **Skill:** Script Python que baixa CSV, gera grÃ¡ficos (`skills/sales-report/run.py`)
3. **Alias:** `alias vendas="python skills/sales-report/run.py"`
4. **Heartbeat:** Sexta 17h, Amora pergunta: "Quer o relatÃ³rio de vendas?"
5. **Cron:** Sexta 17h, gera relatÃ³rio, manda PDF no Telegram automaticamente

#### Exemplo 3: Limpeza de Email

**EvoluÃ§Ã£o:**
1. **Manual:** Marca como lido, arquiva, deleta spam (diÃ¡rio)
2. **Skill:** Regras de filtro documentadas (`skills/email-cleanup/SKILL.md`)
3. **Alias:** Script que roda filtros (`cleanup-email`)
4. **Heartbeat:** Todo dia 8h, Amora mostra: "23 emails nÃ£o lidos. Rodar cleanup?"
5. **Cron:** Todo dia 8h, roda filtros, arquiva newsletters, sÃ³ alerta se tiver > 5 importantes

---

### Parte 5: Como Decidir Se Deve Automatizar (5 min)

**Use a regra dos 5 minutos:**

```
Tempo economizado = (minutos por tarefa) Ã— (vezes por mÃªs) Ã— 12 meses
Tempo pra automatizar = X horas

Se (tempo economizado em 1 ano) > (tempo pra automatizar Ã— 3)
  â†’ Vale a pena
```

**Exemplo:**
- Backup do Notion: 5 min/semana = 4h/ano
- Automatizar: 2h (script + browser automation)
- 4h > (2h Ã— 3)? **NÃƒO** â€” melhor ficar no alias/heartbeat

**Mas considere:**
- **Erro humano:** Se vocÃª sempre esquece â†’ automaÃ§Ã£o vale
- **Custo de falha:** Backup crÃ­tico? AutomaÃ§Ã£o vale (paz de espÃ­rito)
- **Aprendizado:** Quer aprender browser automation? Vale mesmo que nÃ£o economize tempo

---

## ðŸŽ“ ExercÃ­cio PrÃ¡tico

**Tarefa pro aluno:**

1. **Escolher 1 tarefa repetitiva** que vocÃª faz toda semana
2. **Documentar como skill** (`skills/nome-tarefa/SKILL.md`)
3. **Criar alias** ou script simples
4. **Adicionar check no HEARTBEAT.md**
5. **(Opcional)** Criar cron se for 100% automÃ¡tivel

**EntregÃ¡veis:**
- Arquivo `SKILL.md` da tarefa escolhida
- Script executÃ¡vel (`.sh` ou `.py`)
- Trecho do `HEARTBEAT.md` com o check
- Screenshot do resultado (se tiver cron, mostrar log)

---

## ðŸ“‹ Checklist de AutomaÃ§Ã£o

**Antes de automatizar, responda:**

- [ ] **JÃ¡ fiz isso manualmente 3+ vezes?** (senÃ£o, volte pro EstÃ¡gio 1)
- [ ] **Os passos sÃ£o sempre os mesmos?** (senÃ£o, fique no EstÃ¡gio 2)
- [ ] **Demora > 5 min toda vez?** (senÃ£o, alias jÃ¡ resolve)
- [ ] **EsqueÃ§o de fazer com frequÃªncia?** (heartbeat resolve)
- [ ] **Timing Ã© fixo (ex: toda sexta 18h)?** (sÃ³ aqui vale cron)
- [ ] **Zero decisÃ£o humana necessÃ¡ria?** (se precisar escolher algo, nÃ£o automatize completamente)

Se marcou TUDO â†’ automaÃ§Ã£o completa faz sentido.
Se marcou 3-4 â†’ heartbeat + alias jÃ¡ resolve.
Se marcou < 3 â†’ fique na skill documentada.

---

## ðŸš¨ Armadilhas Comuns

### Armadilha 1: Automatizar Cedo Demais

**Erro:** Criar cron na primeira vez que faz a tarefa.

**Problema:** Processo muda, automaÃ§Ã£o quebra, vocÃª perde tempo corrigindo.

**SoluÃ§Ã£o:** FaÃ§a manual 3x. Documente. AÃ­ automatize.

---

### Armadilha 2: Over-Engineering

**Erro:** Criar sistema complexo com retry, logs, dashboards pra tarefa de 2 min.

**Problema:** Gastou 10h pra economizar 1h/ano.

**SoluÃ§Ã£o:** Use a regra dos 5 minutos. Se nÃ£o valer, fique no alias.

---

### Armadilha 3: Esquecer de Monitorar

**Erro:** Cron roda, falha silenciosamente, vocÃª nÃ£o percebe.

**Problema:** Acha que tÃ¡ funcionando, mas nÃ£o tÃ¡.

**SoluÃ§Ã£o:** **SEMPRE** configure `delivery.mode: announce` nos crons. Quer saber se rodou.

---

### Armadilha 4: AutomaÃ§Ã£o Sem Escape Hatch

**Erro:** Cron manda email sozinho, sem revisar.

**Problema:** Erro constrangedor enviado pra 500 pessoas.

**SoluÃ§Ã£o:** Pra aÃ§Ãµes crÃ­ticas (emails, posts pÃºblicos), cron **gera draft** â€” humano revisa antes de publicar.

---

## ðŸŽ¯ ConclusÃ£o

**AutomaÃ§Ã£o Ã© uma jornada, nÃ£o um destino.**

- Comece documentando (`SKILL.md`)
- Crie atalhos (`alias`)
- Adicione lembretes (`HEARTBEAT.md`)
- Automatize sÃ³ quando o processo for **estÃ¡vel** e **previsÃ­vel**

**A skill mais importante:** Saber quando **NÃƒO** automatizar.

Nem tudo precisa virar cron. Ã€s vezes, um alias jÃ¡ Ã© suficiente.

---

## ðŸ“š Recursos

- **Skill de exemplo:** `/skills/notion-backup/` (completo, do manual ao cron)
- **Docs de cron:** `/root/.openclaw/workspace-meu-agente/docs/cron-jobs.md`
- **Heartbeat guide:** `/root/.openclaw/workspace-meu-agente/HEARTBEAT.md`

---

**PrÃ³ximos passos:**
1. Assistir a aula
2. Escolher 1 tarefa repetitiva
3. Seguir o ciclo de evoluÃ§Ã£o
4. Mostrar resultado no grupo do curso

**Meta:** Ao final, vocÃª tem **pelo menos 1 automaÃ§Ã£o funcional** rodando sozinha.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
