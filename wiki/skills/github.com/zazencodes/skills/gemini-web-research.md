---
type: skill
name: Gemini Web Research
slug: gemini-web-research
url: https://github.com/zazencodes/skills/tree/main/skills/gemini-web-research
source_url: https://github.com/zazencodes/skills
source_path: skills/gemini-web-research
author: zazencodes
version: 0.1.1
license: desconhecida
status: active
created: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, pesquisa-web, gemini, antigravity, tmux, orquestracao-multiagente]
---

# Gemini Web Research

> Delega pesquisa web substancial a sessões interativas do `agy` (Google Antigravity) em painéis separados do tmux, enquanto o agente principal só lê os relatórios, decide o que falta e sintetiza — sem rodar busca ou fetch por conta própria.

## O que é

Skill do catálogo [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md) para pesquisa web delegada: em vez de o próprio agente gastar contexto abrindo páginas, ele orquestra sessões `agy` (Google Antigravity) como trabalhadores, cada um em seu próprio painel de tmux, visível ao usuário. Dispara só quando o usuário pede explicitamente para delegar a pesquisa ao Gemini/`agy` — o `SKILL.md` é explícito: não disparar "apenas porque a pesquisa é extensa".

## Como funciona

- **Papéis**: o agente principal é o orquestrador; as sessões `agy` são as trabalhadoras que fazem o trabalho caro (buscar, abrir páginas, checar links, condensar). O orquestrador decide o que perguntar, lê os relatórios, aponta lacunas e contradições, e envia a próxima pergunta — seu contexto é para pensar e sintetizar, não para páginas cruas.
- **Workflow**: (1) dividir a pergunta em áreas independentes e lançar uma sessão por área, em paralelo, com um primeiro prompt leve e estreito; (2) ler cada relatório ao chegar, procurando o que falta, não foi verificado, está raso ou em conflito com outro relatório; (3) fazer follow-up na mesma sessão para aprofundar uma área já coberta — a sessão mantém contexto, então o follow-up pode ser curto; (4) abrir novas sessões para áreas não relacionadas, ou quando uma sessão se perde/confunde; (5) iterar até as descobertas responderem a pergunta, então sintetizar.
- **Lançar uma sessão**: `scripts/agy-research.sh <scratch>/<area>-1.md 'Research <tópico>. ...'` — o launcher divide o painel atual, inicia `agy -i` com Gemini 3.8 Flash em esforço alto, imprime `started in tmux pane %<id>` em stderr, espera o relatório existir, depois o imprime. Cada launcher deve rodar como comando em segundo plano, sem redirecionar stderr, para notificar separadamente quando terminar, mantendo o ID do painel no output.
- **Follow-up**: `scripts/agy-followup.sh %<id> <scratch>/<area>-2.md '<pergunta pontual>'` — digita o prompt no painel via `tmux send-keys`, espera o novo relatório, imprime-o. O prompt precisa ser uma única linha; cada follow-up precisa de um caminho de relatório novo; só enviar follow-up a uma sessão que já terminou o último relatório.
- Painéis ficam abertos depois do turno; o usuário os fecha. Se um painel fechar antes de escrever seu relatório, o script falha com erro — a instrução é relatar isso, não trocar silenciosamente de serviço.

## Instalação e uso

```bash
# Plugin do Claude Code
claude plugin marketplace add zazencodes/skills
claude plugin install zazencodes-skills@zazencodes

# skills.sh, só esta skill
npx skills@latest add zazencodes/skills --skill gemini-web-research
```

Requer a CLI [`agy`](https://antigravity.google) (Google Antigravity) e tmux; o usuário precisa já estar trabalhando dentro do tmux, já que cada sessão abre em um painel novo.

## Exemplos de uso

> Exemplos derivados da descrição publicada — não são instruções oficiais da skill.

- "Delegue ao Gemini uma pesquisa sobre X, Y e Z" — divide em três sessões paralelas, uma por área.
- Depois de ler um relatório raso sobre um sub-tópico, mandar um follow-up pontual só para aquele painel, sem reabrir pesquisa nova.

## Saídas esperadas

Um arquivo de relatório Markdown por área (e por follow-up), escrito pela sessão `agy` correspondente em uma única gravação completa; o agente principal sintetiza os relatórios lidos, sem produzir pesquisa própria.

## Quando usar (e quando não usar)

- **Use quando:** o usuário pede explicitamente para delegar pesquisa ao Gemini/`agy`, especialmente em paralelo, com várias áreas independentes a cobrir.
- **Evite quando:** é uma pergunta de pesquisa comum ou uma busca rápida — o `SKILL.md` instrui a não escolher esta skill só porque a pesquisa é "extensa"; nesse caso, pesquisar diretamente é mais simples.

## Limitações e cuidados

- Dependência rígida de tmux: sem um painel ativo, o launcher não tem onde abrir a sessão.
- Se o modelo padrão (Gemini 3.8 Flash) ficar indisponível, a correção descrita é manual: checar `agy models`, escolher o Gemini Flash atual e atualizar os dois scripts (`agy-research.sh`, `agy-followup.sh`) — não há fallback automático.
- Scripts completos (`scripts/agy-research.sh`, `scripts/agy-followup.sh`) não foram lidos linha a linha nesta ingestão; o comportamento descrito vem do `SKILL.md`.
- Licença não declarada no frontmatter deste `SKILL.md` especificamente (diferente de `codex-image-gen` e `random-number-generator`, que declaram `license: MIT` no próprio arquivo); a licença geral do repositório (MIT) provavelmente se aplica, mas isso não foi confirmado além da inferência pela licença do repositório.

## Estado e adoção

- Versão: parte do catálogo [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md) desde o release `v0.1.0`, segundo o `CHANGELOG.md`.
- Preço/licença: desconhecida no próprio arquivo da skill (ver Limitações); licença do repositório como um todo é MIT.

## Relações

- Autor: [zazencodes (Alexander Galea)](../../../../entities/zazencodes.md)
- Repositório-fonte: [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md)
- Conceitos: [Agent skills](../../../../concepts/agent-skills.md), [Orquestração multiagente](../../../../concepts/orquestracao-multiagente.md) — padrão orquestrador/trabalhador com isolamento por painel de terminal, em vez de subagente nativo do host.

## Perguntas abertas

- "Google Antigravity" (`agy`) ainda não tem página própria nesta wiki — candidato a entidade/conceito, se o usuário pedir uma ingestão dedicada.
- O que acontece se duas sessões diferentes tentam escrever no mesmo caminho de relatório simultaneamente? Não documentado no `SKILL.md`.

## Fontes

- `SKILL.md`: https://raw.githubusercontent.com/zazencodes/skills/9f2d7c8f0e112e03d0e440676afd49fde3c9dff2/skills/gemini-web-research/SKILL.md (commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2`, lido via clone local autorizado, consultado em 2026-10-21).
