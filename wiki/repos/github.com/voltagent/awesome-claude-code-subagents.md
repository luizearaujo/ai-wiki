---
type: repo
url: https://github.com/VoltAgent/awesome-claude-code-subagents
host: github.com
owner: voltagent
repo: awesome-claude-code-subagents
commit: 408d3c9eee2d0c75c12a3abb5de29e53c2ca6b9e
license: MIT
language: Shell
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [agent-skills, subagentes, claude-code, plugins, catalogo]
---

# VoltAgent/awesome-claude-code-subagents

> Coleção curada de 161+ subagentes para Claude Code organizados em 10 categorias, instaláveis individualmente, por categoria (como plugin) ou via instalador interativo.

## O que é

O repositório se declara "a coleção definitiva de subagentes do Claude Code": definições prontas de assistentes de IA especializados para tarefas de desenvolvimento específicas — do design de API ao orquestrador meta que instala outros subagentes. O README deixa explícito que PRs cujo propósito principal é promover um produto, empresa ou projeto pessoal não são aceitos; subagentes precisam ser genuinamente úteis e vendor-neutral, e a via suportada para divulgar um produto é patrocinar o repositório.

## Como funciona

Os subagentes são organizados em 10 categorias, cada uma com um plugin próprio instalável via marketplace do Claude Code:

| # | Categoria | Plugin |
|---|---|---|
| 01 | Core Development | `voltagent-core-dev` |
| 02 | Language Specialists | `voltagent-lang` |
| 03 | Infrastructure | — |
| 04 | Quality & Security | — |
| 05 | Data & AI | — |
| 06 | Developer Experience | — |
| 07 | Specialized Domains | — |
| 08 | Business & Product | — |
| 09 | Meta & Orchestration | `voltagent-meta` |
| 10 | Research & Analysis | — |

A categoria "01. Core Development" por si só inclui treze subagentes (de `api-designer` a `websocket-engineer`); o total declarado no README é 161+ subagentes. Um `subagent-catalog` (em `tools/`) expõe comandos `/subagent-catalog:fetch`, `/subagent-catalog:list` e `/subagent-catalog:invalidate` para buscar, listar e atualizar definições sem precisar clonar o repositório inteiro.

O README observa que os agentes de orquestração em `voltagent-meta` funcionam melhor quando outras categorias já estão instaladas — ou seja, o catálogo foi desenhado para composição entre categorias, não apenas para agentes isolados.

## Instalação e uso rápido

```bash
# Como plugin do Claude Code (recomendado)
claude plugin marketplace add VoltAgent/awesome-claude-code-subagents
claude plugin install voltagent-lang    # especialistas de linguagem
claude plugin install voltagent-infra   # infraestrutura e DevOps
```

```bash
# Instalador interativo (com clone)
git clone https://github.com/VoltAgent/awesome-claude-code-subagents.git
cd awesome-claude-code-subagents
./install-agents.sh
```

```bash
# Instalador autônomo, sem clonar
curl -sO https://raw.githubusercontent.com/VoltAgent/awesome-claude-code-subagents/main/install-agents.sh
chmod +x install-agents.sh
./install-agents.sh
```

Manualmente, os arquivos de agente também podem ser copiados para `~/.claude/agents/` (acesso global) ou `.claude/agents/` (específico do projeto).

## Exemplos de uso

Exemplo derivado do README para instalar e usar o instalador de agentes dentro do próprio Claude Code:

```bash
curl -s https://raw.githubusercontent.com/VoltAgent/awesome-claude-code-subagents/main/categories/09-meta-orchestration/agent-installer.md \
  -o ~/.claude/agents/agent-installer.md
```

```text
Use the agent-installer to show me available categories
Find PHP agents and install php-pro globally
```

## Quando usar (e quando não usar)

- **Use quando:** você quer um especialista pronto para uma tarefa recorrente (API, testes, linguagem específica, segurança) sem escrever a definição do subagente, ou quer compor várias categorias com os agentes de meta-orquestração.
- **Evite quando:** você precisa de um subagente auditado para um contexto de alto risco — o próprio README declara que não há garantia de segurança ou correção sobre os subagentes listados.

## Limitações e cuidados

- **Sem auditoria declarada.** O README afirma que os subagentes são fornecidos "as is", sem garantia, e que os mantenedores não auditam nem garantem segurança ou correção de nenhum subagente listado — revisão antes do uso é responsabilidade de quem instala.
- **Contribuições vendor-neutral.** A política de contribuição rejeita PRs com propósito primário de promoção; isso reduz (mas não elimina) viés comercial no conteúdo dos subagentes.
- Apenas o README foi lido: as definições individuais dos 161+ subagentes e o código do `install-agents.sh` não foram consultados.

## Estado e adoção

- Observado em 2026-10-23: 25.972 estrelas, 2.987 forks, 3 issues abertas; criado em 2025-07-30; último push em 2026-10-11.
- Licença: MIT.
- Linguagem principal na API: Shell (scripts de instalação); o conteúdo em si é majoritariamente Markdown.
- O README cita uma coleção irmã para Codex (`VoltAgent/awesome-codex-subagents`), não ingerida nesta wiki.

## Relações

- Mantido por: [VoltAgent](../../../entities/voltagent.md)
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [Plugins de agente](../../../concepts/plugins-de-agente.md)
- Comparável a: [msitarzewski/agency-agents](../msitarzewski/agency-agents.md) (150+ personalidades em Markdown), [ComposioHQ/awesome-claude-skills](../composiohq/awesome-claude-skills.md) (catálogo de skills e plugins).

## Perguntas abertas

- Qual é a taxa de manutenção real dos 161+ subagentes conforme o Claude Code evolui (ferramentas, modelos, formato de agente)?
- Como o `subagent-catalog` resolve conflitos de nome entre subagentes de categorias diferentes?

## Fontes

- README: https://raw.githubusercontent.com/VoltAgent/awesome-claude-code-subagents/408d3c9eee2d0c75c12a3abb5de29e53c2ca6b9e/README.md (commit `408d3c9eee2d0c75c12a3abb5de29e53c2ca6b9e`, consultado em 2026-10-23). Somente o README foi lido; as definições individuais de subagentes não foram consultadas.
- Metadados: API do GitHub (`/repos/VoltAgent/awesome-claude-code-subagents`) em 2026-10-23.
