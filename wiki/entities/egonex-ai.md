---
type: entity
kind: org
url: https://github.com/Egonex-AI
created: 2026-10-19
updated: 2026-10-19
tags: [grafo-de-conhecimento, codebase, agent-skills]
---

# Egonex-AI

> Organização que mantém o Understand Anything, plugin de skills que gera um grafo de conhecimento interativo de uma base de código.

## O que é

Egonex-AI é a organização por trás do repositório `Egonex-AI/Understand-Anything` (grafado em minúsculas nas URLs de instalação). O produto é um plugin de skills para agentes de código: a skill principal, [understand](../skills/github.com/egonex-ai/understand-anything/understand.md), analisa um projeto e produz `knowledge-graph.json` para um dashboard de arquitetura.

A árvore do repositório, consultada via API, lista outras skills do plugin: `understand-chat`, `understand-dashboard`, `understand-diff`, `understand-domain`, `understand-explain`, `understand-figma`, `understand-knowledge` e `understand-onboard`. O README descreve o produto como grafos que ensinam — de código, negócio e relações — compatíveis com Claude Code, Codex, Cursor, Copilot, Gemini CLI e outros.

## Repositórios e projetos

- [Egonex-AI/Understand-Anything](https://github.com/Egonex-AI/Understand-Anything) — plugin de skills e CLI; MIT; ~86,9 mil stars em 2026-10-19.
- [Skill understand](../skills/github.com/egonex-ai/understand-anything/understand.md) — análise em sete fases, grafo persistente, dashboard e atualização incremental.
- Site: [understand-anything.com](https://understand-anything.com/).

## Relevância no ecossistema

O projeto ocupa o mesmo espaço que o Graphify e o CBM: dar ao agente um mapa estrutural consultável em vez de leitura arquivo por arquivo. A diferença é o empacotamento como **plugin de skills com subagentes e dashboard**, com forte ênfase em explicar o processo em fases e em validar o grafo antes de publicá-lo.

## Relações

- Colabora com: ecossistema de agent skills e catálogos como o skills.sh.
- Associado a: Claude Code, Codex, Cursor, Copilot e Gemini CLI.
- Concorre com: [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) e [DeusData/codebase-memory-mcp](../repos/github.com/deusdata/codebase-memory-mcp.md).

## Fontes

- Página do repositório `Egonex-AI/Understand-Anything` e metadados da API do GitHub em 2026-10-19; commit `f2d0164f72fe678805c34245a6df36acededfebd`.
- Página da skill: https://www.skills.sh/egonex-ai/understand-anything/understand (consultada em 2026-10-19).
