---
type: concept
aliases: [Elephant-Goldfish Model, EGM, revisão por perspectiva fresca]
status: stable
created: 2026-11-10
updated: 2026-11-10
tags: [design, spec, revisao, subagentes, orquestracao]
---

> Padrão de design de software com dois perfis de agente: um com contexto profundo (Elephant) que rascunha a especificação, e um com contexto limpo (Goldfish) que a revisa expondo suposições ocultas.

## O padrão

O Elephant-Goldfish Model separa a **criação** da **revisão** em dois perfis de agente com assimetria intencional de contexto:

- **Elephant** acumula contexto: projeto, requisitos anteriores, decisões já tomadas, histórico da sessão. É quem entende o problema em profundidade e redige a spec.
- **Goldfish** começa do zero: recebe apenas o documento e o código referenciado, sem conversa prévia. É quem lê o design como um estranho e encontra o que o Elephant não consegue mais ver.

A assimetria é uma garantia de qualidade, não um defeito. Revisores com contexto compartilhado tendem a aceitar as mesmas premissas que o autor — o "goldfish" lê o que está escrito, não o que o autor quis dizer.

## Por que o contexto limpo importa

O Goldfish precisa de um **subagente com contexto genuinamente limpo** — não uma instrução de "ignore o contexto anterior". Se o agente não consegue criar subagentes independentes, a revisão não é executada. Essa decisão de design é explícita no EGM: prefere falhar visivelmente a dar uma falsa sensação de revisão.

## Estrutura típica

1. **Brainstorm** — explorar a ideia com o Elephant e salvar um breve conceitual.
2. **Draft** — converter o breve em documento de design.
3. **Review** — um ou mais Goldfishes leem o documento e levantam achados.
4. **Resolve** — o usuário decide trade-offs e o Elephant incorpora as resoluções.

Variantes incluem "review loop" (múltiplos Goldfishes configurados) e "drift report" (comparar uma spec existente com o código atual).

## Implementações

- [google/elephant-goldfish-model](../repos/github.com/google/elephant-goldfish-model.md) — plugin open-source para Claude Code, Codex, Antigravity e ChatGPT Desktop com sete skills; publicado pela Google como projeto não-oficial.

## Relação com outros padrões

O EGM é um caso específico de [orquestração multiagente](orquestracao-multiagente.md) em que a divisão de papéis é definida pelo **histórico de contexto** e não por especialização funcional. Difere de pipelines debate-bullish/bearish (como no [TradingAgents](../repos/github.com/tauricresearch/tradingagents.md)) porque o Goldfish não argumenta contra o Elephant — ele simplesmente não conhece o contexto, e isso é suficiente para revelar lacunas.

## Fontes

- README.md de [google/elephant-goldfish-model](../repos/github.com/google/elephant-goldfish-model.md), commit `bdcfe8cdaee99699c4b2cb7ad4e3b2c1a6b56a31`, lido em 2026-11-10.
