# Aula: Automações Evolutivas — Do Manual ao Automático

**Objetivo:** Ensinar o aluno a **evoluir uma tarefa manual em automação completa**, seguindo o fluxo natural de maturidade de um processo.

**Duração:** 25-30 minutos

---

## 🎯 Conceito Central

**Automação não começa com código. Começa com repetição.**

O erro clássico: tentar automatizar algo que você fez 1 vez. O jeito certo:

1. **Fazer manual** (1-3x) — aprender o processo
2. **Documentar como skill** — capturar o conhecimento
3. **Criar atalhos** — reduzir fricção
4. **Adicionar checks** — detectar quando fazer
5. **Automatizar completamente** — deixar rodar sozinho

---

## 📚 Estrutura da Aula

### Parte 1: O Ciclo de Evolução (5 min)

**Explicar os 5 estágios:**

#### Estágio 1: Manual Puro
- **Quando:** Tarefa nova, ainda aprendendo
- **Como:** Você faz, descobre os passos, anota mentalmente
- **Exemplo:** "Baixar backup do Notion toda sexta"

#### Estágio 2: Skill Documentada
- **Quando:** Já fez 2-3x, sabe os passos
- **Como:** Cria `SKILL.md` com checklist ou script
- **Exemplo:** Criar `/skills/notion-backup/SKILL.md`

#### Estágio 3: Alias/Atalho
- **Quando:** Faz toda semana, quer economizar tempo
- **Como:** Criar alias bash ou função rápida
- **Exemplo:** `alias backup-notion="./skills/notion-backup/run.sh"`

#### Estágio 4: Heartbeat Check
- **Quando:** Às vezes esquece de fazer
- **Como:** Adicionar check no `HEARTBEAT.md`
- **Exemplo:** "Sexta-feira? Lembrar de fazer backup."

#### Estágio 5: Cron Automático
- **Quando:** Processo 100% previsível
- **Como:** Cron job roda sozinho, só notifica se der erro
- **Exemplo:** Cron roda toda sexta 18h, manda resultado no Telegram

---

### Parte 2: Caso Real — Backup do Notion (10 min)

**Vamos seguir o fluxo completo com exemplo prático.**

#### Passo 1: Manual Puro (Semana 1)

**Contexto:** Você quer fazer backup semanal do Notion.

**Como faz:**
1. Abrir Notion no navegador
2. Settings → Export All Workspace Content
3. Escolher formato (Markdown + CSV)
4. Baixar o ZIP
5. Subir no Google Drive (pasta `/Backups/Notion/`)

**Descobertas:**
- Demora ~2 min pra exportar
- ZIP fica com nome tipo `Export-2026-02-25.zip`
- Precisa lembrar de fazer toda sexta

**⚠️ Ainda não automatiza! Só aprende o processo.**

---

#### Passo 2: Skill Documentada (Semana 2)

**Você fez pela 3ª vez. Hora de documentar.**

Criar: `/root/.openclaw/workspace-meu-agente/skills/notion-backup/SKILL.md`

```markdown
# Notion Backup

**Frequência:** Toda sexta-feira, 18h

## Checklist Manual

1. **Exportar do Notion:**
   - Ir em [Notion Settings](https://www.notion.so/my-settings)
   - Export → Export All Workspace Content
   - Formato: Markdown & CSV
   - Aguardar export (~2 min)
   - Baixar ZIP

2. **Upload no Google Drive:**
   ```bash
   # Assumindo ZIP está em ~/Downloads/Export-YYYY-MM-DD.zip
   gog drive upload ~/Downloads/Export-*.zip \
     --parent 1aB2cD3eF4gH5iJ6kL7mN8oP9qR0  # ID da pasta Backups/Notion
   ```

3. **Limpar Downloads:**
   ```bash
   rm ~/Downloads/Export-*.zip
   ```

## Notas

- Export demora ~2 min (workspace grande)
- Notion limita exports (não fazer mais que 1x/dia)
- Manter últimos 4 backups no Drive (1 mês)
```

**Benefício:** Agora você tem um checklist. Não esquece passos.

---

#### Passo 3: Alias/Atalho (Semana 3)

**Problema:** Toda sexta você lê o checklist e digita os comandos.

**Solução:** Criar script executável.

Criar: `/root/.openclaw/workspace-meu-agente/skills/notion-backup/run.sh`

```bash
#!/bin/bash
set -e

echo "🔄 Iniciando backup do Notion..."

# Variáveis
BACKUP_DIR="$HOME/Downloads"
DRIVE_FOLDER_ID="1aB2cD3eF4gH5iJ6kL7mN8oP9qR0"  # Pasta Backups/Notion
DATE=$(date +%Y-%m-%d)

# Passo 1: Avisar pra fazer export manual
echo "📋 Passo 1: Exportar do Notion"
echo "   1. Abra: https://www.notion.so/my-settings"
echo "   2. Export → Export All Workspace Content"
echo "   3. Formato: Markdown & CSV"
echo "   4. Aguarde o download (~2 min)"
echo ""
read -p "✅ Export concluído? (pressione Enter quando baixar o ZIP)"

# Passo 2: Encontrar o ZIP mais recente
LATEST_ZIP=$(ls -t $BACKUP_DIR/Export-*.zip 2>/dev/null | head -1)

if [ -z "$LATEST_ZIP" ]; then
  echo "❌ Erro: Nenhum Export-*.zip encontrado em $BACKUP_DIR"
  exit 1
fi

echo "📦 Arquivo encontrado: $(basename $LATEST_ZIP)"

# Passo 3: Upload pro Drive
echo "☁️  Fazendo upload pro Google Drive..."
export GOG_KEYRING_PASSWORD=$(op item get "GOG Keyring" --vault "Meu Vault" --field password --reveal)
gog drive upload "$LATEST_ZIP" --parent "$DRIVE_FOLDER_ID" --account seu-email@exemplo.com

# Passo 4: Limpar Downloads
echo "🗑️  Limpando Downloads..."
rm "$LATEST_ZIP"

echo "✅ Backup concluído!"
echo "📅 Próximo backup: sexta-feira, $(date -d 'next friday' +%Y-%m-%d)"
```

Tornar executável:
```bash
chmod +x /root/.openclaw/workspace-meu-agente/skills/notion-backup/run.sh
```

Criar alias no `.bashrc`:
```bash
alias backup-notion="/root/.openclaw/workspace-meu-agente/skills/notion-backup/run.sh"
```

**Benefício:** Agora você só roda `backup-notion` — o script guia você.

---

#### Passo 4: Heartbeat Check (Semana 4)

**Problema:** Às vezes esquece de rodar na sexta.

**Solução:** Adicionar check no `HEARTBEAT.md`.

Editar: `/root/.openclaw/workspace-meu-agente/HEARTBEAT.md`

```markdown
## Checks Semanais

### Sexta-feira (18h-20h)

- [ ] **Backup do Notion** — Se não fez hoje, avisar
  - Comando: `backup-notion`
  - Verificar: Último backup no Drive (`gog drive search "name contains 'Export-'" --max 1`)
  - Se último backup > 7 dias → avisar
```

No heartbeat (cron que roda a cada 30 min), a Amora vai:
1. Verificar se é sexta-feira entre 18h-20h
2. Checar último backup no Drive
3. Se faz > 7 dias → **te avisar**: "Hey, faz tempo que não faz backup do Notion. Quer rodar agora?"

**Benefício:** Você não esquece. A Amora te cutuca.

---

#### Passo 5: Cron Automático (Semana 6)

**Problema:** Mesmo com lembrete, você tem que fazer manualmente.

**Solução:** Automatizar o export usando browser automation.

Criar: `/root/.openclaw/workspace-meu-agente/skills/notion-backup/auto-export.sh`

```bash
#!/bin/bash
set -e

# Variáveis
WORKSPACE_DIR="/root/.openclaw/workspace-meu-agente"
BACKUP_DIR="$HOME/Downloads"
DRIVE_FOLDER_ID="1aB2cD3eF4gH5iJ6kL7mN8oP9qR0"
DATE=$(date +%Y-%m-%d)

echo "🤖 Backup automático do Notion — $DATE"

# Passo 1: Usar browser automation pra exportar
cd $WORKSPACE_DIR
cat > /tmp/notion-export.js <<'EOF'
// Script de automação (roda no browser via Playwright/Puppeteer)
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
echo "⏳ Aguardando export..."
sleep 30

# Passo 3: Upload pro Drive
LATEST_ZIP=$(ls -t $BACKUP_DIR/Export-*.zip 2>/dev/null | head -1)
if [ -z "$LATEST_ZIP" ]; then
  echo "❌ Erro: Export falhou"
  exit 1
fi

echo "☁️  Upload: $(basename $LATEST_ZIP)"
export GOG_KEYRING_PASSWORD=$(op item get "GOG Keyring" --vault "Meu Vault" --field password --reveal)
gog drive upload "$LATEST_ZIP" --parent "$DRIVE_FOLDER_ID" --account seu-email@exemplo.com

# Passo 4: Limpar
rm "$LATEST_ZIP"
rm /tmp/notion-export.js

echo "✅ Backup automático concluído!"
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
        message: "Rodar backup automático do Notion: /root/.openclaw/workspace-meu-agente/skills/notion-backup/auto-export.sh"
      sessionTarget: isolated
      delivery:
        mode: announce
        channel: telegram
        to: "1983085858"  # Seu chat privado
```

**Benefício:** Roda sozinho toda sexta 18h. Você só recebe notificação de sucesso (ou erro).

---

### Parte 3: Quando Parar em Cada Estágio (5 min)

**Nem tudo precisa virar automação completa.** Aqui vai o bom senso:

#### Fique no Estágio 1 (Manual) quando:
- ✅ Tarefa rara (< 1x/mês)
- ✅ Processo ainda mudando
- ✅ Precisa de decisão humana a cada vez
- **Exemplo:** Renovar domínio (1x/ano)

#### Fique no Estágio 2 (Skill) quando:
- ✅ Tarefa mensal, mas complexa
- ✅ Passos mudam de vez em quando
- ✅ Quer documentação, não velocidade
- **Exemplo:** Deploy de app (mensal, mas cada vez é diferente)

#### Fique no Estágio 3 (Alias) quando:
- ✅ Tarefa semanal, sempre igual
- ✅ Quer rapidez, mas precisa decidir QUANDO fazer
- ✅ Contexto importa (ex: só faz se bateu meta da semana)
- **Exemplo:** Relatório semanal de vendas

#### Use Estágio 4 (Heartbeat) quando:
- ✅ Tarefa semanal, às vezes esquece
- ✅ Timing flexível (entre 18h-20h, por ex.)
- ✅ Quer lembrete, não automação forçada
- **Exemplo:** Revisar emails importantes da semana

#### Use Estágio 5 (Cron) quando:
- ✅ Tarefa semanal/diária, 100% previsível
- ✅ Timing fixo (toda sexta 18h, todo dia 9h)
- ✅ Zero decisão humana necessária
- ✅ Quer esquecer que existe
- **Exemplo:** Backup de banco de dados, scraping diário

---

### Parte 4: Outros Exemplos de Evolução (5 min)

#### Exemplo 1: Post Semanal no LinkedIn

**Evolução:**
1. **Manual:** Escreve post no Notion, copia pro LinkedIn (semana 1-2)
2. **Skill:** Checklist de "como escrever post" (`skills/linkedin-post/SKILL.md`)
3. **Alias:** Script que lê Notion, formata, e **abre draft** no LinkedIn
4. **Heartbeat:** Segunda-feira 10h, Amora pergunta: "Já escreveu o post da semana?"
5. **Cron:** Segunda 10h, Amora sugere tópicos baseado em analytics + publica draft

#### Exemplo 2: Relatório de Vendas

**Evolução:**
1. **Manual:** Baixa CSV do Stripe, faz pivot no Excel (semana 1-3)
2. **Skill:** Script Python que baixa CSV, gera gráficos (`skills/sales-report/run.py`)
3. **Alias:** `alias vendas="python skills/sales-report/run.py"`
4. **Heartbeat:** Sexta 17h, Amora pergunta: "Quer o relatório de vendas?"
5. **Cron:** Sexta 17h, gera relatório, manda PDF no Telegram automaticamente

#### Exemplo 3: Limpeza de Email

**Evolução:**
1. **Manual:** Marca como lido, arquiva, deleta spam (diário)
2. **Skill:** Regras de filtro documentadas (`skills/email-cleanup/SKILL.md`)
3. **Alias:** Script que roda filtros (`cleanup-email`)
4. **Heartbeat:** Todo dia 8h, Amora mostra: "23 emails não lidos. Rodar cleanup?"
5. **Cron:** Todo dia 8h, roda filtros, arquiva newsletters, só alerta se tiver > 5 importantes

---

### Parte 5: Como Decidir Se Deve Automatizar (5 min)

**Use a regra dos 5 minutos:**

```
Tempo economizado = (minutos por tarefa) × (vezes por mês) × 12 meses
Tempo pra automatizar = X horas

Se (tempo economizado em 1 ano) > (tempo pra automatizar × 3)
  → Vale a pena
```

**Exemplo:**
- Backup do Notion: 5 min/semana = 4h/ano
- Automatizar: 2h (script + browser automation)
- 4h > (2h × 3)? **NÃO** — melhor ficar no alias/heartbeat

**Mas considere:**
- **Erro humano:** Se você sempre esquece → automação vale
- **Custo de falha:** Backup crítico? Automação vale (paz de espírito)
- **Aprendizado:** Quer aprender browser automation? Vale mesmo que não economize tempo

---

## 🎓 Exercício Prático

**Tarefa pro aluno:**

1. **Escolher 1 tarefa repetitiva** que você faz toda semana
2. **Documentar como skill** (`skills/nome-tarefa/SKILL.md`)
3. **Criar alias** ou script simples
4. **Adicionar check no HEARTBEAT.md**
5. **(Opcional)** Criar cron se for 100% automátivel

**Entregáveis:**
- Arquivo `SKILL.md` da tarefa escolhida
- Script executável (`.sh` ou `.py`)
- Trecho do `HEARTBEAT.md` com o check
- Screenshot do resultado (se tiver cron, mostrar log)

---

## 📋 Checklist de Automação

**Antes de automatizar, responda:**

- [ ] **Já fiz isso manualmente 3+ vezes?** (senão, volte pro Estágio 1)
- [ ] **Os passos são sempre os mesmos?** (senão, fique no Estágio 2)
- [ ] **Demora > 5 min toda vez?** (senão, alias já resolve)
- [ ] **Esqueço de fazer com frequência?** (heartbeat resolve)
- [ ] **Timing é fixo (ex: toda sexta 18h)?** (só aqui vale cron)
- [ ] **Zero decisão humana necessária?** (se precisar escolher algo, não automatize completamente)

Se marcou TUDO → automação completa faz sentido.
Se marcou 3-4 → heartbeat + alias já resolve.
Se marcou < 3 → fique na skill documentada.

---

## 🚨 Armadilhas Comuns

### Armadilha 1: Automatizar Cedo Demais

**Erro:** Criar cron na primeira vez que faz a tarefa.

**Problema:** Processo muda, automação quebra, você perde tempo corrigindo.

**Solução:** Faça manual 3x. Documente. Aí automatize.

---

### Armadilha 2: Over-Engineering

**Erro:** Criar sistema complexo com retry, logs, dashboards pra tarefa de 2 min.

**Problema:** Gastou 10h pra economizar 1h/ano.

**Solução:** Use a regra dos 5 minutos. Se não valer, fique no alias.

---

### Armadilha 3: Esquecer de Monitorar

**Erro:** Cron roda, falha silenciosamente, você não percebe.

**Problema:** Acha que tá funcionando, mas não tá.

**Solução:** **SEMPRE** configure `delivery.mode: announce` nos crons. Quer saber se rodou.

---

### Armadilha 4: Automação Sem Escape Hatch

**Erro:** Cron manda email sozinho, sem revisar.

**Problema:** Erro constrangedor enviado pra 500 pessoas.

**Solução:** Pra ações críticas (emails, posts públicos), cron **gera draft** — humano revisa antes de publicar.

---

## 🎯 Conclusão

**Automação é uma jornada, não um destino.**

- Comece documentando (`SKILL.md`)
- Crie atalhos (`alias`)
- Adicione lembretes (`HEARTBEAT.md`)
- Automatize só quando o processo for **estável** e **previsível**

**A skill mais importante:** Saber quando **NÃO** automatizar.

Nem tudo precisa virar cron. Às vezes, um alias já é suficiente.

---

## 📚 Recursos

- **Skill de exemplo:** `/skills/notion-backup/` (completo, do manual ao cron)
- **Docs de cron:** `/root/.openclaw/workspace-meu-agente/docs/cron-jobs.md`
- **Heartbeat guide:** `/root/.openclaw/workspace-meu-agente/HEARTBEAT.md`

---

**Próximos passos:**
1. Assistir a aula
2. Escolher 1 tarefa repetitiva
3. Seguir o ciclo de evolução
4. Mostrar resultado no grupo do curso

**Meta:** Ao final, você tem **pelo menos 1 automação funcional** rodando sozinha.
