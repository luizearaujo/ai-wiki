---
type: entity
kind: org
url: https://github.com/Fincept-Corporation
created: 2026-10-19
updated: 2026-10-19
tags: [organizacao, financas, trading, terminal, india]
---

# Fincept Corporation

> Empresa com sede na Índia que mantém o Fincept Terminal, terminal financeiro desktop nativo, e produtos associados de dados e pesquisa com IA — com edição aberta AGPL e edição Enterprise proprietária.

## O que é

Fincept Corporation é a organização por trás do [FinceptTerminal](../repos/github.com/fincept-corporation/finceptterminal.md). Criada em 2024-08-19, declara 4 repositórios públicos e 423 seguidores; o site é `fincept.in`. A descrição da organização repete a do terminal: "a modern finance application offering advanced market analytics, investment research, and economic data tools".

O modelo é incomum entre os projetos desta wiki: o código aberto é uma edição **reduzida** (AGPL-3.0, uma release por mês), enquanto a equipe desenvolve diariamente a edição **Enterprise** proprietária, vendida por assinatura. O README posiciona o open source como porta de entrada para estudantes, hobistas e acadêmicos, e a Enterprise para firmas e mesas de pesquisa.

## Produtos

- [Fincept Terminal (edição aberta)](../repos/github.com/fincept-corporation/finceptterminal.md) — terminal desktop em C++20/Qt6 com Python 3.11 embutido; 37 agentes, 100+ conectores, paper trading, 16 corretoras, node editor e MCP; AGPL-3.0-or-later.
- **Fincept Terminal Enterprise** — build proprietário com 41 módulos em seis frentes, dados privados point-in-time, pesquisa multiagente, execução live gerenciada, SSO/SAML, auditoria e SLA; US$ 15–45 por usuário/mês.
- **Fincept Data API** — 500+ endpoints REST, 423 mil instrumentos e 2 mil fontes, com tier gratuito para contas.
- **Quantcept** — mesa de pesquisa com dados primários, backtests, portfólios, documentos e monitores 24/7; planos gratuitos e pagos.

## Relevância no ecossistema

A organização ilustra um padrão de **open core invertido**: o repositório público permanece, mas não concentra mais o desenvolvimento principal. Isso afeta como o código aberto deve ser avaliado — recursos anunciados na mesma página podem pertencer apenas à edição paga, e o README mistura material de produto, preços e comparação competitiva.

Também é um dos poucos projetos financeiros da wiki com arquitetura **nativa** (C++/Qt) em vez de web ou Python, o que muda o custo de distribuição e a superfície de integração por agentes.

**A verificar:** a divisão exata entre os dois builds, a governança do repositório público e a consistência dos preços publicados.

## Relações

- **Criou:** [Fincept Terminal](../repos/github.com/fincept-corporation/finceptterminal.md); mantém Data API e Quantcept.
- **Conceitos:** [Análise financeira multiagente](../concepts/analise-financeira-multiagente.md), [Model Context Protocol (MCP)](../concepts/model-context-protocol.md), [Orquestração multiagente](../concepts/orquestracao-multiagente.md).

## Fontes

- https://github.com/Fincept-Corporation — perfil da organização via API do GitHub em 2026-10-19 (descrição, localização, repositórios públicos, seguidores, criação e blog).
- https://github.com/Fincept-Corporation/FinceptTerminal — README no commit `3d8617cae3f13c93874d4bee4fb0f2846e9c83bc`; metadados da API do GitHub observados em 2026-10-19.
