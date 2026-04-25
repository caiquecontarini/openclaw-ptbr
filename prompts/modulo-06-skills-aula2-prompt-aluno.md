# Prompt do Aluno â€” M06 Aula 2: Skills â€” O sistema de superpoderes

> Use este prompt no seu agente depois de assistir a aula.

---

## ðŸ“¦ Dica â€” O skill-creator jÃ¡ vem instalado no seu OpenClaw

O skill-creator jÃ¡ faz parte das skills oficiais do OpenClaw. Para verificar se estÃ¡ ativo:

```bash
openclaw skills list | grep skill-creator
```

Se nÃ£o aparecer, instale:
```bash
clawhub install skill-creator
```

O comando `/criar-skill` vai estar disponÃ­vel automaticamente no seu agente.

---

## ðŸŽ¯ O que vocÃª vai praticar

Criar sua primeira skill do zero, organizar a pasta corretamente e testar se o agente consegue executar o processo de forma consistente.

---

## Prompt para usar no seu agente

```
Quero criar minha primeira skill seguindo a estrutura correta do OpenClaw.

O processo que quero documentar Ã©: [descreva aqui o processo que vocÃª repete com frequÃªncia â€” ex: "gerar relatÃ³rio semanal de mÃ©tricas", "criar carrossel de LinkedIn", "responder emails de suporte"]

Me ajuda a:
1. Definir o nome correto da skill em kebab-case
2. Escolher a categoria certa (content, analytics, operations, research, ou criar uma nova)
3. Criar o SKILL.md com: name, description (com triggers), metadata e o passo a passo de execuÃ§Ã£o
4. Criar a estrutura de pasta em skills/{categoria}/{nome-da-skill}/

Depois de criar, quero testar se vocÃª consegue executar o processo sÃ³ lendo o SKILL.md â€” sem eu precisar explicar nada.
```

---

## VariaÃ§Ãµes por nÃ­vel

**ðŸŸ¢ Iniciante â€” copiar uma skill existente:**
```
Me mostra o SKILL.md de uma skill simples que vocÃª jÃ¡ tem, e me explica cada campo. 
Quero entender a estrutura antes de criar a minha.
```

**ðŸŸ¡ IntermediÃ¡rio â€” criar skill de analytics:**
```
Cria uma skill chamada "relatorio-semanal" em skills/analytics/.
Ela deve: puxar as mÃ©tricas mais importantes da semana (vocÃª define quais fazem sentido pro meu negÃ³cio), 
formatar num texto limpo com os principais nÃºmeros, e me enviar toda segunda-feira de manhÃ£.
Inclui os triggers certos no description pra eu acionar facilmente.
```

**ðŸ”´ AvanÃ§ado â€” criar skill com script:**
```
Quero uma skill que automatize [processo que usa API ou linha de comando].
Cria o SKILL.md + um script em scripts/ que execute a parte tÃ©cnica.
A skill deve buscar as credenciais pelo 1Password â€” nunca hardcodado.
```

---

## Checklist pÃ³s-criaÃ§Ã£o

Antes de considerar a skill pronta, confirme:

- [ ] Pasta criada em `skills/{categoria}/{nome}/`
- [ ] SKILL.md tem: name, description com triggers, metadata, e passo a passo claro
- [ ] Testei chamando o agente sÃ³ com o trigger â€” sem dar contexto extra
- [ ] O agente executou corretamente lendo sÃ³ o SKILL.md
- [ ] Skill estÃ¡ no Git (backup feito)

---

## Pergunta de reflexÃ£o

> "Qual processo vocÃª faz mais de 2 vezes por semana que ainda nÃ£o virou skill?"

Esse Ã© seu prÃ³ximo candidato.


---
*Créditos originais da metodologia: [Bruno Okamoto](https://github.com/okjpg)*
