---
type: entity
kind: org
url: https://github.com/trailhq
created: 2026-10-21
updated: 2026-10-21
tags: []
---

# Trail (trailhq)

> Organização que mantém o Trail-Code (antes graft), descrita no próprio GitHub como "Context Graphs for AI Agents".

## O que é

Trail é a organização por trás do Trail-Code, ferramenta que indexa um repositório em um grafo de código via tree-sitter e acrescenta "learnings" — decisões e preferências salvas das conversas com agentes — como memória persistente entre sessões e entre membros de um time. A bio da organização no GitHub resume o foco: "Context Graphs for AI Agents". O site do produto é trailhq.com.

## Repositórios e projetos

- [trailhq/Trail-Code](../repos/github.com/trailhq/trail-code.md) — camada de contexto para agentes de código: graft map (grafo de símbolos) + learnings (memória de decisões), com integração nativa em Claude Code, Cursor, Codex, Gemini CLI e outros, e servidor MCP próprio.

## Relevância no ecossistema

Representa uma categoria específica de ferramenta para agentes de código: combinar um grafo estrutural do repositório (sem modelo, determinístico) com uma camada de memória de equipe versionada em git, em vez de depender só de arquivos de instrução escritos à mão (`CLAUDE.md`/`AGENTS.md`) ou de busca semântica por embeddings.

## Relações

- Colabora com: comunidade de agentes de código (Claude Code, Cursor, Codex, Gemini CLI, Copilot, Windsurf, Kiro, Antigravity e outros, citados como integrações no README do Trail-Code).
- Associado a: pacote anterior `@nanonets/graft`, predecessor do Trail-Code sob outro nome.

## Fontes

- Perfil da organização: https://api.github.com/orgs/trailhq, consultado em 2026-10-21.
- README do Trail-Code: https://raw.githubusercontent.com/trailhq/Trail-Code/b1211efd3eef0efa121b93800e5dd8e547aead77/README.md, consultado em 2026-10-21.
