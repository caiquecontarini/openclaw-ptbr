# Prompt â€” MÃ³dulo 2: SeguranÃ§a

> Cole este prompt no chat do seu OpenClaw depois de assistir o MÃ³dulo 2.
> Anexe junto o arquivo: `prds/security-hardening.md`

---

Acabei de assistir o MÃ³dulo 2 do curso sobre seguranÃ§a. Leia o PRD de security hardening que estou anexando e me guie passo a passo.

**Importante:**
- Antes de CADA aÃ§Ã£o, me explique O QUE vai fazer e POR QUÃŠ
- Me peÃ§a confirmaÃ§Ã£o antes de executar qualquer mudanÃ§a no servidor
- Se algo jÃ¡ estiver configurado, me avise e pule pro prÃ³ximo passo
- No final, rode um audit de seguranÃ§a e me mostre o resultado

**O que espero que cubra:**
1. Telegram allowlist (dmPolicy) â€” pra ninguÃ©m comandar meu bot
2. Firewall UFW â€” bloquear portas desnecessÃ¡rias
3. Fail2ban â€” proteger contra brute force SSH
4. Credenciais â€” guardar API keys com `openclaw secrets` (nÃ£o em .env ou hardcodado). Use `openclaw secrets audit` pra verificar se hÃ¡ credenciais expostas e `openclaw secrets apply` pra migrar. Se usar 1Password, configure via `op` CLI.
5. Portas de aplicaÃ§Ã£o â€” nÃ£o expor nada em 0.0.0.0

Vamos blindar meu servidor?


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
