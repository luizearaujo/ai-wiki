---
type: repo
url: https://github.com/t3dotgg/tstack
host: github.com
owner: t3dotgg
repo: tstack
commit: 1085050f3baed1ac724caa4a8166145fb2ac88af
license: MIT
language: Python
status: active
created: 2026-10-28
ingested: 2026-10-28
updated: 2026-10-28
tags: [agent-skills, claude-code, codex, pull-request, revisao-de-codigo, github-cli]
---

# t3dotgg/tstack

> Nove skills de fluxo de pull request — review, merge, takeover, rebase e formatação de comentários — que o autor usa todo dia, limpas para uso em Claude Code e Codex.

## O que é

`tstack` empacota as Agent Skills que Theo Browne usa no próprio fluxo de desenvolvimento, "limpas para qualquer pessoa usar". Cobrem o ciclo de um PR de ponta a ponta: provar e revisar uma mudança, escrever a descrição do PR, acompanhar CI e bots de review, resolver findings, decidir se um PR antigo ainda deve existir, e assumir um PR/branch/thread de agente deixado por outra pessoa. Funcionam em Claude Code e Codex; algumas usam recursos do `T3 Code` (`pingdotgg/t3code`) quando disponíveis e caem para ferramentas nativas quando não.

## Como funciona

Nove skills, compostas entre si (uma skill chama outra como dependência):

| Skill | Gatilho por fala | O que faz |
|---|---|---|
| `full-send` | "full send" | Pega uma mudança até um PR mergeado sem ninguém observando: prova, revisa, arquiva, acompanha e faz merge. |
| `full-stop` | "full stop" | Igual a `full-send`, mas para quando o PR está pronto para o usuário mergear. |
| `council` | "council" | Pede review de três modelos de provedores diferentes e repete até concordarem. |
| `sol-loop` | "sol loop" | Revisa uma mudança com "GPT Sol" em loop até os dois agentes concordarem. |
| `file-pr` | "file a PR" | Arquiva um PR curto que lidera com o problema, não um inventário de mudanças. |
| `takeover` | "take over" | Termina o PR, branch ou thread de agente de outra pessoa, mantendo o crédito dela. |
| `babysit-pr` | "babysit" | Acompanha um PR por CI e bots de review, corrigindo os findings reais. |
| `modernize` | "modernize" | Faz rebase de um PR antigo e decide se ele ainda deve existir. |
| `leaving-pr-comments` | (automático) | Formata comentários que um agente posta em nome do usuário. |

Dependências declaradas entre skills: `full-send` usa `sol-loop`, `file-pr` e `babysit-pr`; `full-stop` usa `full-send`; `takeover` usa `modernize`, `file-pr`, `babysit-pr` e `leaving-pr-comments`; `file-pr`, `babysit-pr` e `modernize` usam `leaving-pr-comments`.

`council` e `sol-loop` dependem de subagentes em modelos de outros provedores — o README cita o `delegate_task` do T3 Code como o mecanismo usado pelo autor, e deixa explícito que, sem ele, é preciso um harness próprio capaz de rodar esses modelos.

## Instalação e uso rápido

```bash
git clone https://github.com/t3dotgg/tstack
cp -R tstack/skills/* ~/.claude/skills/   # Claude Code
cp -R tstack/skills/* ~/.codex/skills/    # Codex
```

Pré-requisitos declarados: GitHub CLI (`gh`) autenticado; `python3` para o script `pr-wait` usado por `babysit-pr`; para `council` e `sol-loop`, um harness com subagentes em modelos de outros provedores.

## Exemplos de uso

- Abrir, revisar e mergear uma mudança pequena sem supervisão humana no meio do caminho, usando `full-send`.
- Assumir um PR de agente abandonado por outra pessoa, preservando a autoria original, com `takeover`.
- Forçar concordância entre revisores de provedores diferentes antes de aceitar uma mudança sensível, com `council`.

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** o fluxo de trabalho já passa por PRs no GitHub via `gh`, e o objetivo é reduzir a supervisão humana no ciclo de revisão/merge ou organizar como um agente retoma trabalho de outro.
- **Evite quando:** não há `gh` autenticado ou o repositório não usa pull requests do GitHub; para `council`/`sol-loop`, evite sem um harness que rode subagentes em modelos de provedores diferentes do principal.

## Limitações e cuidados

- O README recomenda editar as skills e mover preferências pessoais (ex.: quais modelos compõem o "council") para `CLAUDE.md`/`AGENTS.md`, para não perdê-las em atualizações — ou seja, são ponto de partida, não configuração final.
- Duas skills (`council`, `sol-loop`) dependem de capacidade de multi-provider subagent que o `T3 Code` supre; sem ele, a skill exige um harness equivalente, não documentado em detalhe pelo README.
- Nenhum conteúdo interno de `skills/*/SKILL.md` foi lido nesta ingestão — apenas a tabela e as instruções do `README.md` na raiz. Prompts exatos, formato de saída e lógica detalhada de cada skill ficam como **a verificar**.
- Repositório criado em 2026-10-24 (4 dias antes desta ingestão); crescimento rápido (2.042 estrelas, 121 forks observados em 2026-10-28) registrado apenas como observação datada.

## Estado e adoção

- Sem releases/versão citadas no README.
- Atividade observada em 2026-10-28: 2.042 estrelas, 121 forks, 10 issues abertas; push mais recente em 2026-10-28.
- Licença: MIT (`LICENSE`, confirmada pela API do GitHub).

## Relações

- Mantido por: [Theo Browne (t3dotgg)](../../../entities/t3dotgg.md).
- Conceitos: nenhum conceito dedicado nesta wiki cobre "revisão multi-modelo" ou "takeover de PR de agente"; a página fica listada na categoria [Skills, instruções e personalidades de agente](../../../categorias.md#skills-instruções-e-personalidades-de-agente).
- Dependência opcional citada no README: `pingdotgg/t3code` (não ingerido nesta wiki).

## Perguntas abertas

- O que cada `SKILL.md` individual especifica (prompts, formato de saída, critérios de "findings reais" em `babysit-pr`), já que apenas a tabela do README foi lida?
- Como `council`/`sol-loop` se comportam sem o `T3 Code`, num harness genérico com subagentes?

## Fontes

- README: https://raw.githubusercontent.com/t3dotgg/tstack/1085050f3baed1ac724caa4a8166145fb2ac88af/README.md (commit `1085050f3baed1ac724caa4a8166145fb2ac88af`, consultado em 2026-10-28). Somente o README foi lido; os arquivos em `skills/` não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/t3dotgg/tstack`, `api.github.com/users/t3dotgg`), consultada em 2026-10-28.
