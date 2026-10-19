---
type: entity
kind: org
url: https://github.com/google-labs-code
created: 2026-10-19
updated: 2026-10-19
tags: [google, design-systems, agent-skills, cli, jules]
---

# Google Labs Code

> Organização no GitHub que publica o formato DESIGN.md, skills para agentes e ferramentas do ecossistema Jules e Stitch; é a origem das quatro skills documentadas a partir de `design.md`.

## O que é

Google Labs Code (`google-labs-code`) é uma organização no GitHub criada em 2024-02-26, com nove repositórios públicos observados em 2026-10-19. O nome, o escopo dos projetos e o pacote npm `@google/design.md` apontam para uma iniciativa do Google Labs voltada a ferramentas de código e agentes, mas a API do GitHub marca a organização como **não verificada** (`is_verified: false`) e não publica descrição, site ou localização; o vínculo corporativo oficial não foi confirmado por uma fonte independente nesta ingestão.

A produção observada combina três linhas:

- **Design para agentes:** o repositório `design.md` define um formato que une tokens de design legíveis por máquina a uma justificativa em prosa, para que agentes mantenham uma identidade visual consistente.
- **Skills para agentes:** `stitch-skills` distribui skills para o servidor MCP do Stitch, no padrão Agent Skills, compatível com Antigravity, Gemini CLI, Claude Code e Cursor; `jules-skills` faz o equivalente para o Jules.
- **SDKs e ações:** `stitch-sdk` gera telas a partir de texto e extrai HTML e screenshots; `jules-sdk`, `jules-action` e `action-setup` apoiam automação com o agente Jules em fluxos de código.

## Repositórios e projetos

- [google-labs-code/design.md](https://github.com/google-labs-code/design.md) — especificação DESIGN.md, CLI `@google/design.md` de lint/diff/export e as quatro skills documentadas nesta wiki: [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md), [TDD Red-Green-Refactor](../skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md), [Ink](../skills/github.com/google-labs-code/design.md/ink.md) e [Agent DX CLI Scale](../skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md). Apache-2.0, TypeScript, ~28,4 mil estrelas em 2026-10-19.
- [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills) — biblioteca de skills para o servidor MCP do Stitch, seguindo o padrão Agent Skills; ~8,5 mil estrelas observadas em 2026-10-19.
- [google-labs-code/stitch-sdk](https://github.com/google-labs-code/stitch-sdk) — geração programática de telas de UI a partir de prompts, com extração de HTML e screenshots; ~1,8 mil estrelas.
- [google-labs-code/jules-awesome-list](https://github.com/google-labs-code/jules-awesome-list) — coleção de prompts para o agente Jules; ~3,2 mil estrelas.
- [google-labs-code/jules-skills](https://github.com/google-labs-code/jules-skills), [jules-sdk](https://github.com/google-labs-code/jules-sdk), [jules-action](https://github.com/google-labs-code/jules-action), [stax](https://github.com/google-labs-code/stax) e [action-setup](https://github.com/google-labs-code/action-setup) — ferramentas menores de automação e integração contínua.

## Relevância no ecossistema

- **Formato para design systems:** o DESIGN.md propõe que a identidade visual seja um artefato versionado com tokens e justificativa, em vez de um conjunto de decisões implícitas no prompt. Isso dialoga com a tese de [Agent skills](../concepts/agent-skills.md): conhecimento durável empacotado para ser lido sob demanda.
- **Skills como produto:** as quatro skills de `design.md` cobrem engenharia de software — contratos tipados, TDD, UI de terminal e avaliação de CLI —, não o formato em si. É um caso de repositório que distribui método de engenharia junto do produto principal.
- **Padrão Agent Skills:** a organização mantém bibliotecas de skills para Stitch e Jules no mesmo padrão aberto usado por Claude Code, Cursor e outros clientes, ampliando a interoperabilidade entre hosts.
- **Ecossistema Google para agentes:** a organização se soma a Jules (agente de código) e Stitch (geração de UI) como as iniciativas observáveis, sem publicar uma tese única ou um harness próprio.

## Relações

- **Associado a:** Google Labs e ao pacote npm `@google/design.md`; vínculo corporativo oficial não verificado nesta wiki.
- **Publica:** as quatro skills de `design.md` documentadas em [Skills, instruções e personalidades de agente](../categorias.md#skills-instruções-e-personalidades-de-agente) e na categoria [Engenharia e interfaces agent-first](../categorias.md#engenharia-e-interfaces-agent-first).
- **Conceitos relacionados:** [CLI agent-first](../concepts/cli-agent-first.md), [Contratos tipados de serviço](../concepts/contratos-tipados-de-servico.md) e [TDD para agentes](../concepts/tdd-para-agentes.md).
- **Ecossistema semelhante:** [Egonex-AI](egonex-ai.md) e [Graphify Labs](graphify-labs.md) também publicam skills e ferramentas de contexto para agentes.

## Fontes

- https://github.com/google-labs-code — metadados da organização via API do GitHub em 2026-10-19 (criada em 2024-02-26, nove repositórios públicos, ~3,2 mil seguidores, `is_verified: false`).
- https://api.github.com/orgs/google-labs-code/repos — lista de repositórios e estrelas observadas em 2026-10-19.
- https://github.com/google-labs-code/design.md — README no commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15` e metadados da API do GitHub em 2026-10-19 (Apache-2.0, TypeScript).
- https://www.skills.sh/google-labs-code/design.md — página do catálogo consultada em 2026-10-19 (quatro skills e 1,7 mil instalações totais).
