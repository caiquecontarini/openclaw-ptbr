# Prompt do Aluno â€” Aula N-2: Bot sem acesso ao shell

**Como usar:** Cole o prompt abaixo diretamente no chat do seu agente OpenClaw.  
O agente vai diagnosticar a prÃ³pria configuraÃ§Ã£o e guiar vocÃª atÃ© a soluÃ§Ã£o.

---

## PROMPT PARA COLAR NO CHAT

```
Vou fazer um diagnÃ³stico do seu acesso ao shell. Por favor, execute cada etapa na ordem.

## ETAPA 0 â€” Verificar tools.profile (primeiro check SEMPRE)

Antes de qualquer coisa, verifique se o perfil de ferramentas estÃ¡ correto:

1. Execute: `openclaw config get tools.profile`
2. Se o resultado NÃƒO for "full", execute: `openclaw config set tools.profile full`
3. Reinicie o gateway: `openclaw gateway restart`
4. Teste: `echo "TOOLS_PROFILE_CHECK_OK"`

> Este Ã© o problema mais comum: o agente nÃ£o executa nada porque o tools.profile estÃ¡ em "minimal" (padrÃ£o apÃ³s instalaÃ§Ã£o). Sem `tools.profile full`, o agente sÃ³ responde mensagens.

Se o teste acima funcionou â†’ problema resolvido! ðŸŽ‰
Se ainda falha â†’ continue para a Etapa 1.

---

## ETAPA 1 â€” Teste bÃ¡sico de acesso

Tente executar este comando e me diga exatamente o que aconteceu:
execute: echo "SHELL_TEST_OK"

Se funcionou â†’ me confirme "OK" e vÃ¡ para a Etapa 3.
Se falhou ou vocÃª recebeu erro â†’ descreva o erro e continue na Etapa 2.

---

## ETAPA 2 â€” DiagnÃ³stico de configuraÃ§Ã£o

Agora verifique sua configuraÃ§Ã£o atual:

1. Leia o arquivo de configuraÃ§Ã£o principal:
   - Tente: `cat ~/.openclaw/config.json`
   - Ou: `cat openclaw.json` (se estiver num workspace)

2. Me mostre o conteÃºdo completo do arquivo. Procuro especificamente por:
   - Chave "tools" ou "allowlist" (para verificar se "exec" estÃ¡ na lista)
   - Chave "sandbox" (valores possÃ­veis: "off", "non-main", "all")
   - Chave "security" (valores possÃ­veis: "deny", "allowlist", "full")
   - Chave "shell" (path do shell, ex: "/bin/bash")

3. TambÃ©m verifique os logs do gateway:
   `openclaw gateway logs --tail 30`

---

## ETAPA 3 â€” Identificar a causa

Com base no que vocÃª encontrou, me diga qual dessas situaÃ§Ãµes se aplica:

**A) Causa 1 â€” exec nÃ£o estÃ¡ no allowlist**
Sintoma: config tem "allowlist" mas "exec" nÃ£o estÃ¡ na lista
â†’ SoluÃ§Ã£o: adicionar "exec" ao allowlist de tools

**B) Causa 2 â€” Sandbox bloqueando**
Sintoma: config tem "sandbox": "all" ou sandbox configurado de forma restritiva
â†’ SoluÃ§Ã£o: mudar para "sandbox": "off" (agente principal) ou "non-main"

**C) Causa 3 â€” Security mode "deny"**
Sintoma: config tem "security": "deny"
â†’ SoluÃ§Ã£o: mudar para "security": "allowlist"

**D) Causa 4 â€” Shell nÃ£o encontrado**
Sintoma: erro de path ou shell nÃ£o localizado nos logs
â†’ SoluÃ§Ã£o: configurar "shell": "/bin/bash" (ou o path correto)

**E) NÃ£o encontrei nada suspeito na config**
â†’ Me descreva o erro exato que vocÃª vÃª e os logs do gateway

---

## ETAPA 4 â€” Aplicar a correÃ§Ã£o

Baseado na causa identificada, edite o arquivo de configuraÃ§Ã£o com a correÃ§Ã£o correta.

**Para Causa 1 (exec nÃ£o no allowlist):**
```json
{
  "agents": {
    "main": {
      "tools": {
        "allowlist": ["exec", "read", "write", "edit", "web_search", "web_fetch"]
      }
    }
  }
}
```

**Para Causa 2 (sandbox bloqueando):**
```json
{
  "agents": {
    "main": {
      "sandbox": "off"
    }
  }
}
```

**Para Causa 3 (security deny):**
```json
{
  "agents": {
    "main": {
      "security": "allowlist"
    }
  }
}
```

**Para Causa 4 (shell nÃ£o encontrado):**
```json
{
  "agents": {
    "main": {
      "shell": "/bin/bash"
    }
  }
}
```

ApÃ³s editar, execute:
`openclaw gateway restart`

---

## ETAPA 5 â€” VerificaÃ§Ã£o final

ApÃ³s reiniciar, verifique se estÃ¡ funcionando:

1. `echo "VERIFICACAO_FINAL_OK"` â†’ deve retornar o texto
2. `touch /tmp/teste-openclaw && echo "arquivo criado"` â†’ deve funcionar
3. `openclaw gateway status` â†’ deve mostrar status "running"

Se tudo passou: **problema resolvido!** ðŸŽ‰
Se ainda falha: copie o erro exato e os logs do gateway para analisar.
```

---

## NOTAS PARA O ALUNO

### Quando usar este prompt
- Seu agente responde perguntas mas nÃ£o executa comandos
- VocÃª vÃª erros como "exec not available", "permission denied" ou "sandbox restriction"
- O agente diz "nÃ£o consigo executar tarefas no sistema"

### O que o prompt faz
0. **Verifica o tools.profile** â€” causa #1 mais frequente, resolve 70% dos casos
1. Testa o acesso ao shell com um comando simples
2. LÃª sua configuraÃ§Ã£o atual
3. Identifica qual das 4 causas se aplica ao seu caso
4. Guia vocÃª na correÃ§Ã£o especÃ­fica
5. Verifica que a correÃ§Ã£o funcionou

### Causa mais comum (verifique primeiro!)
Na maioria dos casos, o problema Ã© simplesmente o `tools.profile` nÃ£o estar em `full`. Execute no terminal do servidor:
```bash
openclaw config set tools.profile full
openclaw gateway restart
```

### Dica importante
Se o agente nÃ£o conseguir nem ler o arquivo de configuraÃ§Ã£o, vocÃª precisarÃ¡ fazer isso **manualmente no terminal** (nÃ£o pelo agente). Nesse caso, abra um terminal no servidor onde o OpenClaw estÃ¡ rodando e edite o `config.json` diretamente.

---

*Prompt para Aula N-2 Â· Curso OpenClaw Â· Pixel EducaÃ§Ã£o*


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
