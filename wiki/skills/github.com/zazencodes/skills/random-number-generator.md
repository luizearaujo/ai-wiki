---
type: skill
name: Random Number Generator
slug: random-number-generator
url: https://github.com/zazencodes/skills/tree/main/skills/random-number-generator
source_url: https://github.com/zazencodes/skills
source_path: skills/random-number-generator
author: zazencodes
version: desconhecida
license: MIT
status: active
created: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, aleatoriedade, python, cli]
---

# Random Number Generator

> Gera inteiros, floats, escolhas (ponderadas ou não), embaralhamentos, amostras sem reposição e tokens/inteiros criptograficamente seguros, só com a biblioteca padrão do Python (`random` e `secrets`), com saída em JSON.

## O que é

Skill do catálogo [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md) para qualquer pedido de número aleatório, RNG, inteiro ou float aleatório, lançamento de dado, escolha (ponderada ou não), embaralhamento de lista, amostra sem reposição, inteiro seguro, aleatoriedade criptográfica, token seguro, candidato a senha, entropia de senha ou token hex — resolvendo tudo com um único script Python, sem dependência externa.

## Como funciona

- Executa um script empacotado (`scripts/random_number.py`), que só usa os módulos padrão `random` e `secrets` — nenhuma dependência de terceiros.
- **Regra de execução**: rodar a partir da pasta da própria skill, para que o script resolva caminhos relativos a este `SKILL.md`; se o shell não estiver nessa pasta, entrar nela primeiro.
- Ordem de preferência de interpretador: `python3`, depois `py -3` no Windows, depois `python` só depois de confirmar que é Python 3. Se Python 3 não estiver disponível, a instrução é dizer isso ao usuário — nunca simular um resultado aleatório falso.
- Saída em JSON por padrão, para fácil parsing por outro programa ou pelo próprio agente.

### Comandos

| Comando | O que gera |
|---|---|
| `random-int --low L --high H [--size N]` | Inteiro(s) aleatório(s) entre `L` e `H` |
| `random-float --low L --high H [--size N]` | Float(s) aleatório(s) entre `L` e `H` |
| `random-choices --population-json '[...]' --k N` | `N` escolhas com reposição |
| `random-choices --population-json '[...]' --weights-json '[...]' --k N` | `N` escolhas ponderadas, com reposição |
| `random-shuffle --items-json '[...]'` | A lista embaralhada |
| `random-sample --population-json '[...]' --k N` | `N` itens sem reposição |
| `secure-token-hex --nbytes B [--size N]` | Token(s) hexadecimal(is) seguro(s), via `secrets` |
| `secure-random-int --upper-bound U [--size N]` | Inteiro(s) seguro(s) de `0` até `U` (exclusivo), via `secrets` |

## Instalação e uso

```bash
# Plugin do Claude Code
claude plugin marketplace add zazencodes/skills
claude plugin install zazencodes-skills@zazencodes

# skills.sh, só esta skill
npx skills@latest add zazencodes/skills --skill random-number-generator
```

```bash
python3 scripts/random_number.py random-int --low 1 --high 100
# Windows PowerShell:
py -3 scripts/random_number.py random-int --low 1 --high 100
# lote:
python3 scripts/random_number.py random-int --low 1 --high 100 --size 5
```

## Exemplos de uso

> Exemplos derivados da descrição publicada — não são instruções oficiais da skill.

- "Role um dado" → `random-int --low 1 --high 6`.
- "Gere um token seguro de 16 bytes" → `secure-token-hex --nbytes 16`.
- "Embaralhe esta lista de times" → `random-shuffle --items-json '[...]'`.

## Saídas esperadas

JSON impresso no stdout com o(s) valor(es) gerado(s) para o comando pedido; falha explícita (sem resultado inventado) se Python 3 não estiver disponível.

## Quando usar (e quando não usar)

- **Use quando:** precisa de um número, escolha, embaralhamento ou token aleatório reprodutível por script, sem depender de o próprio modelo "inventar" um número (LLMs não são boas fontes de aleatoriedade).
- **Evite quando:** a aleatoriedade precisa de uma fonte auditável por um terceiro externo (ex.: sorteio público verificável) — o script roda localmente, sem prova de entropia externa.

## Limitações e cuidados

- Depende de Python 3 estar instalado e acessível; a skill não traz um caminho alternativo sem Python.
- A distinção entre `random` (não segura) e `secrets` (segura) é feita pelo comando escolhido (`secure-*` vs os demais) — usar o comando errado para um caso sensível (senha, token de sessão) quebra a garantia de segurança.
- Script completo não foi lido linha a linha nesta ingestão; os comandos acima vêm do `SKILL.md`.
- Esta skill está listada no catálogo instalável (`package.json`), mas, até esta ingestão, não tem entrada própria em `CHANGELOG.md` — ver nota em [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md#perguntas-abertas).

## Estado e adoção

- Versão: desconhecida — presente no catálogo atual (`v0.1.1`), mas sem changeset próprio identificado no `CHANGELOG.md` consultado.
- Preço/licença: MIT (declarada no próprio frontmatter do `SKILL.md`).

## Relações

- Autor: [zazencodes (Alexander Galea)](../../../../entities/zazencodes.md)
- Repositório-fonte: [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md)
- Conceitos: [Agent skills](../../../../concepts/agent-skills.md)

## Perguntas abertas

- Por que esta skill não aparece no `CHANGELOG.md`, diferente das outras quatro?

## Fontes

- `SKILL.md`: https://raw.githubusercontent.com/zazencodes/skills/9f2d7c8f0e112e03d0e440676afd49fde3c9dff2/skills/random-number-generator/SKILL.md (commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2`, lido via clone local autorizado, consultado em 2026-10-21).
