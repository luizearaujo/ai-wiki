---
type: entity
kind: org
url: https://github.com/Graphify-Labs
created: 2026-10-19
updated: 2026-10-19
tags: [grafo-de-conhecimento, code-intelligence, agentes, yc]
---

# Graphify Labs

> Organização criadora do Graphify, skill e CLI que transforma código e documentação em um grafo de conhecimento consultável, e do serviço Graphify Cloud.

## O que é

Graphify Labs é a organização por trás do [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md). O projeto combina análise local de código via tree-sitter com um passo semântico opcional para docs, PDFs, imagens e mídia, e oferece uma camada comercial — **Graphify Cloud** — para grafos sempre ligados, cross-repo, verificação formal e conectores de SDLC.

O README identifica a empresa como **Y Combinator S26** e aponta para site, documentação, Discord, YouTube e LinkedIn. O autor do livro *The Memory Layer* e mantenedor citado é Safi Shamsi, que também aparece no link de GitHub Sponsors.

## Repositórios e projetos

- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — skill `/graphify` + CLI em Python, licença Apache-2.0; ~40 linguagens, grafo com arestas `EXTRACTED`/`INFERRED`, benchmarks próprios.
- **Graphify Cloud** — serviço comercial em [app.graphify.com](https://app.graphify.com), com teste gratuito de 14 dias; a fronteira com o CLI não foi verificada.
- **The Memory Layer** — livro sobre as ideias e a arquitetura do Graphify.

## Relevância no ecossistema

O Graphify representa a tese de **grafo em vez de vector store** para memória e compreensão de código, com forte ênfase em análise local e em explicar a origem de cada aresta. É também um caso de open-source Apache-2.0 com serviço hospedado, padrão que a wiki vem observando em outros projetos.

## Relações

- Colabora com: ecossistema tree-sitter, LangChain e agentes como Claude Code, Codex, Cursor, Gemini CLI e OpenClaw.
- Integra com: [Obsidian](obsidian.md), via o exportador `graphify export obsidian` (documentado em docs.graphify.com, não no README) — ver [Workflow Claude Code + Graphify + Obsidian](../analyses/claude-code-graphify-obsidian.md).
- Associado a: Y Combinator (S26).
- Concorre com: soluções de RAG sobre código, servidores MCP de code intelligence (como o CBM) e plataformas de memória para agentes.

## Fontes

- README de [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md), commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8` (consultado em 2026-10-19).
- Metadados da API do GitHub em 2026-10-19.
