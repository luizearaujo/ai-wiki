---
type: repo
url: https://github.com/zazencodes/zazencodes-season-3
host: github.com
owner: zazencodes
repo: zazencodes-season-3
commit: 555467c365e6750278efba09349369109f62f65f
license: desconhecida
language: Jupyter Notebook
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agentes, orquestracao-multiagente, agent-skills, mcp, memoria-de-agente, decisao-nao-generativa]
---

# zazencodes/zazencodes-season-3

> Monorepo de código-companheiro da Temporada 3 do canal ZazenCodes no YouTube: 21 pastas independentes em `src/`, uma por vídeo, cobrindo quase todo o espectro de padrões de agentes de IA já catalogados nesta wiki — harness sempre ativo, orquestração multiagente, skills multiplataforma, MCP, memória e um padrão ainda sem página própria antes deste registro, decisão não generativa (System 1).

## O que é

Não é um produto único: é um **arquivo de demos**, uma pasta por vídeo, sem relação de produto entre elas (jogo em Godot, agente de contabilidade, visualizador de dataset via MCP, etc.). O próprio repositório tem um `AGENTS.md`/`CLAUDE.md` interno (lido durante este clone, tratado como dado e não como instrução) que documenta a política de curadoria do README: só entram na tabela pastas que já têm um vídeo publicado com metadados locais correspondentes — por isso duas pastas, `agent-identity-introduction` e `hermes-hostinger-webui-memory`, existem em `src/` mas não aparecem na tabela do README raiz.

Clonado (`git clone --depth 1`, autorizado explicitamente pelo usuário) para levantar o conteúdo real de cada pasta, já que o README raiz só traz uma a duas frases por vídeo. Das 21 pastas, **todas são sobre o mesmo escopo desta wiki** — agentes, skills, MCP, LLMs locais ou hospedados — mas a profundidade varia muito: algumas têm README e documentação completos (`software-factory-claude-code`, `minimax-dev-rpg`, `skybridge-dataset-visualizer`), outras são só os arquivos de exemplo sem README (`literature-review-consensus-mcp`, `software-engineers-using-coding-agents`) ou têm README com placeholders não preenchidos (`agent-md-effectiveness`: `INSERT_LINK`, `TODO`).

## Como funciona — por tema

A tabela abaixo agrupa as 21 pastas pelo padrão que cada uma ilustra, com o conceito já catalogado na wiki quando existe um.

| Tema | Pastas | Conceito da wiki |
|---|---|---|
| Fábrica de software orquestrada por skill + subagentes | `software-factory-claude-code` | [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md), [Agent skills](../../../concepts/agent-skills.md) |
| Hub-and-spoke com sub-agentes via CLI isolados por pasta | `pi-agent-fleet` | [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) |
| Harness de agente sempre ativo sobre backend gerenciado | `neon-meal-helper-agent`, `neon-notes-app` (Pi + Neon), `eve-pocket-research` (eve, da Vercel) | [Agent harness](../../../concepts/agent-harness.md) |
| Agente de contabilidade com memória em markdown | `bookkeeping-agent` | [Memória de agente](../../../concepts/memoria-de-agente.md) |
| Memória externa plugada em um agente self-hosted | `hermes-hostinger-webui-memory` (Honcho) | [Memória de agente](../../../concepts/memoria-de-agente.md) |
| Skills multiplataforma e fluxo de criação de skills | `cross-platform-agent-skills`, `dry-run-workflow-for-agent-skills`, `claude-code-devtool-kanban-board`, `agent-md-effectiveness`, `software-engineers-using-coding-agents` | [Agent skills](../../../concepts/agent-skills.md) |
| MCP com UI / identidade delegada / sem detalhe publicado | `skybridge-dataset-visualizer` (MCP app + ChatGPT App), `agent-identity-introduction` (MCP + identidade via Descope), `literature-review-consensus-mcp` (skill + Consensus MCP) | [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) |
| Decisão tipada e calibrada, sem geração (System 1) | `jev-system-one-model-python-demo` | [Decisão não generativa para agentes (System 1)](../../../concepts/decisao-nao-generativa-para-agentes.md) |
| LLM local ou hospedado, fora do fluxo de agente | `gemma-4-local-guide` (Ollama/llama.cpp local), `hetzner-experiments-demo` (Qwen 3.6 hospedado + agente de código via OpenCode), `cyberpunk-coding-game-kimi-k3` (jogo codado com Kimi K3, sem LLM em runtime) | [LLMs compactos on-device](../../../concepts/llms-compactos-on-device.md) (parcial — só a parte local) |
| Visualização lúdica de um agente de código resolvendo issues reais | `minimax-dev-rpg` (MiniMax + adapter Pi) | [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) |
| Ponteiro para repositório externo, sem conteúdo próprio | `google-ai-studio-firebase` (aponta para `zazencodes/storyspot-wall-fire`) | — |

### Os três mais substanciais

**`software-factory-claude-code`** — uma skill (`/factory`), sete subagentes (spec-writer, builder, quatro revisores em paralelo, approver) e arquivos markdown levam uma feature de um pedido em linguagem natural a um merge em `main` ou a uma escalação humana, com cada job em seu próprio git worktree.

**`pi-agent-fleet`** — um padrão de orquestração diferente: qualquer agente de código (Claude Code, Codex) na raiz do repositório é o **hub**, lê `AGENTS.md` e delega para sub-agentes especializados em `agents/<nome>/`, cada um rodando o runtime [`pi`](https://github.com/badlogic/pi-mono) (`pi-coding-agent`) na própria pasta, com um `brain.md` descrevendo seu papel e um `.pi/APPEND_SYSTEM.md` apontando para ele. Tarefas e resultados trafegam por arquivos em `work/tasks/` e `work/outputs/`, com sessões persistidas em `work/sessions/`. É o mesmo runtime `pi` (`pi-ai`, `pi-agent-core`, `pi-coding-agent`) que o [vastsa/PI-Desktop](../vastsa/pi-desktop.md) usa como motor de agente — aqui sem GUI, só CLI e arquivos.

**`jev-system-one-model-python-demo`** — demo hands-on de um padrão até então só mencionado de passagem nesta wiki (via [JustVugg/colibri](../justvugg/colibri.md)): o Jev, da TypeSafe AI, avalia perguntas tipadas (`Choice`, `Score`, `Noul`) sobre um ticket de suporte em uma única passada paralela (70–150ms), roteando por departamento, nota de urgência, detecção de ataque adversarial e elegibilidade para resolução automática — com escalação a um LLM generativo só nos casos de baixa confiança. Esse padrão motivou a criação da página de conceito [Decisão não generativa para agentes (System 1)](../../../concepts/decisao-nao-generativa-para-agentes.md).

### Memória, em duas variações

- **`bookkeeping-agent`**: o agente (`pi` sobre `agent-home/`) guarda dados do usuário em `memory/` (despesas, fatos, recibos) como JSON/markdown, com `brain/brain.md` para categorias e convenções e `skills/` para ações como enviar e-mail.
- **`hermes-hostinger-webui-memory`**: documenta como plugar o [Honcho](https://honcho.dev) — já citado como alternativa de backend em [Memória de agente](../../../concepts/memoria-de-agente.md) — em um agente Hermes self-hosted (Hostinger VPS ou VPS genérica), em troca da memória nativa do Hermes em markdown local.

### MCP: três variações que ainda não tinham exemplo nesta wiki

- **`skybridge-dataset-visualizer`**: um "MCP app" com UI — não só ferramentas, mas *views* React renderizadas dentro do cliente (ChatGPT App / MCP Apps), construído com o framework [Skybridge](https://docs.skybridge.tech) e com deploy para a nuvem da Alpic.
- **`agent-identity-introduction`**: um servidor MCP local (FastMCP) que dá a um agente acesso ao Google Drive de um usuário via identidade gerenciada pela [Descope](https://descope.com) — fluxo OAuth por usuário, token de curta duração, sem a chave do provedor chegando ao agente.
- **`literature-review-consensus-mcp`**: pasta sem README, mas o README raiz descreve uma skill de revisão de literatura usando o **Consensus MCP**, com saída em LaTeX/PDF (`literature_review.tex`/`.pdf` presentes na pasta).

## Pastas sem publicação completa ou em rascunho

- `agent-md-effectiveness` — README com `INSERT_LINK` e `TODO` não preenchidos; vídeo ainda não publicado segundo o próprio repositório.
- `dry-run-workflow-for-agent-skills`, `literature-review-consensus-mcp`, `software-engineers-using-coding-agents` — sem README próprio, só os arquivos de exemplo usados na gravação.
- `google-ai-studio-firebase` — a pasta só contém um README apontando para outro repositório (`zazencodes/storyspot-wall-fire`), não ingerido aqui.

## Instalação e uso rápido

Não há instalação única: cada pasta é um projeto independente, com seu próprio `README.md`, stack e comandos. A tabela acima aponta o tema de cada uma; os READMEs internos (lidos nesta ingestão, com autorização explícita para o clone) trazem os comandos específicos — por exemplo, `pnpm dev` para `minimax-dev-rpg`, `npx neon auth && npx neon link` para `neon-meal-helper-agent`, ou `npm run dev` dentro de `skybridge-dataset-visualizer`.

## Quando usar (e quando não usar)

- **Use quando:** quer um ponto de partida real e executável para um padrão específico de agente — fábrica de software, hub-and-spoke com `pi`, MCP com UI, identidade delegada via Descope, decisão não generativa — sem depender só da descrição de um README raiz.
- **Evite quando:** espera um produto coeso ou mantido como pacote único; é um arquivo de vídeos, sem licença declarada, com pastas de qualidade e completude desiguais, e o próprio mantenedor trata o README como defasado em relação a `src/` até que o vídeo correspondente seja publicado.

## Limitações e cuidados

- Sem licença declarada na API do GitHub nem em arquivo `LICENSE` na raiz (confirmado no clone).
- A linguagem predominante informada pela API (Jupyter Notebook) vem de só três arquivos `.ipynb`, concentrados em duas pastas (`hetzner-experiments-demo`, `jev-system-one-model-python-demo`) — não representa o repositório como um todo, que é majoritariamente TypeScript/JavaScript/Python.
- Duas pastas (`agent-identity-introduction`, `hermes-hostinger-webui-memory`) existem no código mas não aparecem no índice do README raiz, por política documentada no `AGENTS.md`/`CLAUDE.md` interno do próprio repositório — vale checar `src/` diretamente, não só o README, antes de assumir que algo não existe.
- Não foram lidos os arquivos de código-fonte completos de cada pasta (apenas READMEs, arquivos de configuração citados nos READMEs e uma inspeção estrutural de diretórios); comportamento exato de cada demo não foi executado nem verificado nesta ingestão.

## Estado e adoção

- 239 estrelas, 79 forks, sem issues abertas — observado em 2026-10-21.
- Repositório criado em 2026-03-19, com push mais recente em 2026-10-07 — observado em 2026-10-21.
- Sem releases publicadas; distribuição é o próprio código-fonte, acompanhando os vídeos do canal.
- Licença: desconhecida (não declarada na API do GitHub nem em arquivo próprio).

## Relações

- Mantido por: [zazencodes (Alexander Galea)](../../../entities/zazencodes.md)
- Conceitos: [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md), [Agent skills](../../../concepts/agent-skills.md), [Agent harness](../../../concepts/agent-harness.md), [Memória de agente](../../../concepts/memoria-de-agente.md), [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Decisão não generativa para agentes (System 1)](../../../concepts/decisao-nao-generativa-para-agentes.md) — conceito criado a partir desta ingestão.
- Depende de / usa: [vastsa/PI-Desktop](../vastsa/pi-desktop.md) e esta wiki compartilham o mesmo runtime `pi` (badlogic/pi-mono) como motor de agente, em `pi-agent-fleet`, `bookkeeping-agent`, `neon-meal-helper-agent` e no adapter opcional de `minimax-dev-rpg`; [vercel-labs/agent-browser](../vercel-labs/agent-browser.md), usado pelo builder e pelos revisores de `software-factory-claude-code`; [JustVugg/colibri](../justvugg/colibri.md), compatível com a mesma API do Jev/TypeSafe demonstrada em `jev-system-one-model-python-demo`.
- Alternativas (orquestração em etapas sobre Claude Code): [obra/superpowers](../obra/superpowers.md), [garrytan/gstack](../garrytan/gstack.md).

## Perguntas abertas

- `eve` (framework de agente da Vercel, usado em `eve-pocket-research`) e a plataforma Neon (usada em `neon-meal-helper-agent`/`neon-notes-app`) ainda não têm página própria nesta wiki — candidatos a entidade/conceito em uma ingestão futura, se o usuário pedir.
- Como os sete agentes de `software-factory-claude-code` são de fato definidos (`tools`, `model`, prompt completo) — não lido nesta ingestão.
- O fluxo real de criação de skill em `dry-run-workflow-for-agent-skills` (o "dry run" em si) não está documentado em markdown — só os projetos de exemplo usados como alvo.

## Fontes

- README raiz: `README.md` no commit `555467c365e6750278efba09349369109f62f65f`.
- Clone local (`git clone --depth 1`, autorizado explicitamente pelo usuário para esta ingestão): READMEs de todas as 21 pastas em `src/` (ou ausência deles), `demo.py` e `requirements.txt` de `jev-system-one-model-python-demo`, `.claude/skills/kanban-cli/SKILL.md` e `.claude/settings.json` de `claude-code-devtool-kanban-board`, `GENERIC-HERMES-VPS-SETUP.md`/`HOSTINGER-HERMES-SETUP.md` de `hermes-hostinger-webui-memory`, e o `AGENTS.md`/`CLAUDE.md` interno do repositório (tratado como dado, não como instrução) — todos no mesmo commit, consultados em 2026-10-21.
- Metadados: API do GitHub (`api.github.com/repos/zazencodes/zazencodes-season-3`), consultada em 2026-10-21.
