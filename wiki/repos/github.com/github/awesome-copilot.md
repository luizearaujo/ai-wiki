---
type: repo
url: https://github.com/github/awesome-copilot
host: github.com
owner: github
repo: awesome-copilot
commit: cb64ad12e32737ae764becd6885462e9b4c7cb00
license: MIT
language: JavaScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agent-skills, github-copilot, catalogo, instrucoes, plugins]
---

# github/awesome-copilot

> Catálogo comunitário — hospedado na organização do GitHub, mas alimentado por desenvolvedores terceiros — de agentes, instructions, skills, hooks, workflows e plugins para o GitHub Copilot, com site de busca próprio e um `llms.txt` para consumo por agentes.

## O que é

O repositório reúne customizações do GitHub Copilot em cinco categorias — agentes, instructions, skills, plugins e cookbook — contribuídas pela comunidade. O README é explícito: "the customizations here are sourced from third-party developers. Please inspect any agent and its documentation before installing" — ou seja, é um catálogo de descoberta, não um conjunto curado e auditado pelo GitHub.

## Como funciona

| Recurso | Papel | Documentação |
|---|---|---|
| **Agentes** | Agentes especializados do Copilot que integram com servidores MCP. | `docs/README.agents.md` |
| **Instructions** | Padrões de código aplicados automaticamente por padrão de arquivo. | `docs/README.instructions.md` |
| **Skills** | Pastas autocontidas com instruções e recursos empacotados. | `docs/README.skills.md` |
| **Plugins** | Pacotes curados de agentes e skills para workflows específicos. | `docs/README.plugins.md` |
| **Cookbook** | Receitas prontas para copiar e colar ao trabalhar com as APIs do Copilot. | `cookbook/README.md` |

O site **awesome-copilot.github.com** oferece busca e filtro em texto completo sobre todo o catálogo, além de um **Learning Hub** com artigos e tutoriais sobre agentes, skills, instructions, hooks, workflows agênticos, servidores MCP e o Copilot coding agent. Um arquivo `llms.txt` machine-readable lista agentes, instructions e skills de forma estruturada, pensado para ser consumido por agentes de IA, não só por humanos.

## Instalação e uso rápido

Instalar um plugin diretamente (marketplace já registrado na maioria dos setups):

```bash
copilot plugin install <plugin-name>@awesome-copilot
```

Se a marketplace não for reconhecida (versão antiga do Copilot CLI ou setup customizado):

```bash
copilot plugin marketplace add github/awesome-copilot
copilot plugin install <plugin-name>@awesome-copilot
```

## Exemplos de uso

O README não publica exemplos de prompt — é um catálogo de navegação. O uso típico é: buscar no site ou nos índices (`docs/README.*.md`) um agente, instruction, skill ou plugin para a tarefa, e instalar com o comando acima.

## Quando usar (e quando não usar)

- **Use quando:** você usa GitHub Copilot (CLI ou VS Code) e quer descobrir customizações já publicadas pela comunidade, com busca e filtro dedicados.
- **Use quando:** quer integrar o catálogo via `llms.txt` em um fluxo automatizado que descobre recursos para agentes.
- **Evite quando:** precisa de uma lista curada e auditada — o próprio README recomenda inspecionar cada agente antes de instalar, porque o conteúdo vem de terceiros.
- **Alternativas:** catálogos equivalentes para outros clientes, como [ComposioHQ/awesome-claude-skills](../composiohq/awesome-claude-skills.md) para Claude.

## Limitações e cuidados

- **Somente o README foi lido.** `docs/README.agents.md`, `docs/README.instructions.md`, `docs/README.skills.md`, `docs/README.plugins.md`, `cookbook/README.md`, `AGENTS.md` e `SECURITY.md` não foram consultados.
- O catálogo é explicitamente de terceiros: nenhuma garantia de qualidade, segurança ou manutenção é declarada pelo GitHub além da recomendação de inspecionar antes de instalar.
- É um repositório de nome "awesome-*" hospedado na organização oficial `github`, o que pode sugerir curadoria oficial — o README esclarece que o conteúdo é comunitário.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~40,2 mil estrelas, ~5,2 mil forks, 101 issues abertas; criado em 2025-06-11, último push em 2026-10-16.
- **Licença:** MIT.
- **Linguagem principal:** JavaScript.
- Marcas registradas da Microsoft citadas no README quanto a uso de logos/trademarks em versões modificadas do projeto.

## Relações

- **Mantido por:** [GitHub](../../../entities/github.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — uma das cinco categorias do catálogo, ao lado de agentes, instructions, hooks e plugins; [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — os agentes do catálogo integram com servidores MCP.
- **Relacionado a:** [ComposioHQ/awesome-claude-skills](../composiohq/awesome-claude-skills.md) — catálogo equivalente para Claude; [anthropics/skills](../anthropics/skills.md), [vercel-labs/agent-skills](../vercel-labs/agent-skills.md), [cloudflare/skills](../cloudflare/skills.md) e [remotion-dev/skills](../remotion-dev/skills.md) — coleções oficiais de fornecedores que poderiam, em princípio, ser descobertas por um catálogo como este.

## Perguntas abertas

- Qual é o processo de revisão (se algum) para aceitar uma contribuição no catálogo?
- O `llms.txt` é mantido em sincronia automática com o conteúdo do repositório, ou gerado manualmente?
- Como o catálogo lida com entradas desatualizadas ou abandonadas pelos autores originais?

## Fontes

- README: https://github.com/github/awesome-copilot (commit `cb64ad12e32737ae764becd6885462e9b4c7cb00`, consultado em 2026-10-19). Somente o README foi lido; os índices em `docs/`, o `cookbook/` e os arquivos de governança não foram consultados.
- Metadados do repositório e do perfil `github` via API do GitHub (consultados em 2026-10-19).
