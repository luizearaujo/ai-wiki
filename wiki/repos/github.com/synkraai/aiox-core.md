---
type: repo
url: https://github.com/SynkraAI/aiox-core
host: github.com
owner: synkraai
repo: aiox-core
commit: 4ef6530ff03b83aea953e4a426f95e012b8b70c5
license: MIT
language: TypeScript
status: active
created: 2026-10-18
ingested: 2026-10-18
updated: 2026-10-18
tags: [agentes, orquestracao, cli, desenvolvimento, multi-agente, scrum, ade]
---

# SynkraAI/aiox-core

> Framework CLI-first de orquestração de IA para desenvolvimento full-stack: instala uma equipe de 12 agentes especializados (planejamento, desenvolvimento, QA, DevOps) em qualquer projeto, resolvendo inconsistência de planejamento e perda de contexto entre sessões.

## O que é

AIOX Squad (Artificial Intelligence Orchestration eXperience) é um framework open-source que transforma um projeto de software em um ambiente com equipe ágil de agentes de IA. Cada agente tem papel, responsabilidade e artefatos de entrada/saída bem definidos. A ideia central é uma **abordagem em duas fases**: agentes de planejamento produzem PRDs e documentos de arquitetura detalhados; depois, o Scrum Master transforma esses documentos em histórias hiperdetalhadas que o agente de desenvolvimento abre e executa com contexto completo.

Suporta Claude Code, Gemini CLI, Codex CLI, Cursor e GitHub Copilot, com paridade de hooks variada por plataforma. Extensível via **Squads** para domínios além de software (escrita, negócios, educação, bem-estar).

O pacote npm é `@aiox-squads/core` (sucessor de `aiox-core` sem scope; comandos de CLI preservados durante a transição). O site é [aioxsquad.ai](https://aioxsquad.ai).

> **A verificar:** a API do GitHub reportou licença como `"other/NOASSERTION"`, mas o README e o badge indicam MIT. O arquivo `docs/legal/license-clarification.md` (não lido) pode esclarecer a distinção entre core (MIT) e Pro (comercial).

## Como funciona

### Premissa arquitetural: CLI First

```
CLI First → Observability Second → UI Third
```

A CLI é a fonte da verdade. Toda execução, decisões e automação acontecem nela. Dashboards apenas observam o que o CLI está fazendo; a UI nunca é requisito para operar o sistema.

### As duas inovações-chave

**1. Planejamento agêntico:** agentes dedicados (`analyst`, `pm`, `architect`) colaboram com o usuário via human-in-the-loop para criar PRDs e documentos de arquitetura detalhados, muito além da geração genérica de tarefas. Resolve **inconsistência de planejamento**.

**2. Histórias hiperdetalhadas:** o agente `sm` (Scrum Master) transforma esses planos em arquivos de história com contexto completo, detalhes de implementação e orientação arquitetural embutidos. O `dev` abre o arquivo e já sabe o que construir, como e por quê. Resolve **perda de contexto entre sessões**.

### Fluxo principal

```
Planejamento (Web UI):
  @analyst → @pm → @architect → documentos PRD + Arquitetura

Desenvolvimento (IDE):
  @pm *write-spec → @architect *create-plan → @dev *execute-subtask → @qa *review-build
```

### 12 agentes especializados

| Grupo | Agentes | Ambiente |
|-------|---------|----------|
| **Meta** | aiox-master, aiox-orchestrator | qualquer |
| **Planejamento** | analyst, pm, architect, ux-expert | interface web |
| **Desenvolvimento** | sm, dev, qa, po, data-engineer, devops | IDE |

`devops` é a **autoridade exclusiva de push** — nenhum outro agente faz push diretamente.

### ADE — Autonomous Development Engine

O ADE é o motor de desenvolvimento autônomo, composto por 7 epics:

| Epic | Nome | Descrição |
|------|------|-----------|
| 1 | Worktree Manager | Isolamento de branches via Git worktrees |
| 2 | Migration V2→V3 | Migração para formato autoClaude V3 |
| 3 | Spec Pipeline | Transforma requisitos em specs executáveis |
| 4 | Execution Engine | Executa specs com 13 steps + self-critique |
| 5 | Recovery System | Recuperação automática de falhas |
| 6 | QA Evolution | Review estruturado em 10 fases |
| 7 | Memory Layer | Memória persistente de padrões e insights |

### Compatibilidade de hooks por IDE

| IDE/CLI | Paridade vs Claude Code | Impacto prático |
|---------|------------------------|-----------------|
| Claude Code | Completa (referência) | Automação máxima |
| Gemini CLI | Alta (eventos nativos) | Cobertura forte |
| Codex CLI | Parcial/limitada | Parte das automações depende de `AGENTS.md` e MCP |
| Cursor | Sem lifecycle hooks | Foco em regras e MCP |
| GitHub Copilot | Sem lifecycle hooks | Instruções de repositório + MCP no VS Code |
| AntiGravity | Workflow-based | Integração por workflows, não por hooks |

## Instalação e uso rápido

```bash
# Novo projeto (assistente interativo)
npx aiox-core init meu-projeto

# Projeto existente
cd seu-projeto
npx aiox-core install

# Atualizar instalação existente
npx aiox-core@latest install

# Diagnóstico
npx aiox-core doctor
```

O instalador interativo (inspirado em Vite/Next.js) usa `@clack/prompts`, detecta instalação existente, cria arquivos de backup `.bak` para customizações e configura o IDE automaticamente (Claude Code, Codex CLI ou Cursor).

**Para Claude Code:** o arquivo `.claude/CLAUDE.md` é carregado automaticamente após a instalação.

## Squads

Squads são equipes modulares de agentes para qualquer domínio. Estrutura básica:

```
squads/meu-squad/
├── config.yaml
├── agents/
├── tasks/
├── templates/
└── README.md
```

Squads externos disponíveis (repositórios separados): `hybrid-ops` (operações híbridas humano-agente).

## AIOX Pro

Módulo premium exclusivo para membros do **AIOX Cohort Advanced**. Features adicionais: squads avançados, Memory Layer entre sessões, métricas e analytics, integrações Enterprise (Jira, Linear, Notion), configuração em camadas L1–L4 e licenciamento por chave.

```bash
npx -y -p @aiox-squads/core@latest aiox pro setup
```

**A verificar:** modelo de licença e diferença entre uso core (MIT) e Pro (comercial) — ver `docs/legal/license-clarification.md`.

## Quando usar (e quando não usar)

- **Use quando:** quiser uma equipe ágil de agentes de IA com roles bem definidos, artefatos de planejamento explícitos e histórias como unidade de contexto; quando Claude Code for o IDE principal (paridade de hooks completa); quando precisar de agentes em múltiplos domínios via Squads.
- **Evite quando:** o projeto precisar de um agente simples sem cerimônia de planejamento; quando Cursor/Copilot forem os IDEs únicos e os lifecycle hooks forem essenciais para o workflow; quando o modelo de licença Pro conflitar com o uso pretendido.

## Limitações e cuidados

- Paridade de hooks incompleta em Cursor, Copilot e AntiGravity — funcionalidades avançadas dependem de hooks de ciclo de vida que essas plataformas não têm.
- O pacote `aiox-core` (sem scope) está sendo migrado para `@aiox-squads/core`; comandos de CLI preservados, mas verificar conflitos em instalações mistas.
- AIOX Pro exige acesso ao Cohort Advanced; não é open-source.
- Não lidos: `docs/`, código-fonte, `CONTRIBUTING.md`, manifestos de agente individuais, `docs/legal/license-clarification.md`.

## Estado e adoção

- Versão observada nos exemplos do README: v4.2.11.
- Último push: 2026-10-18.
- Observado em 2026-10-18: ~3.131 stars, ~962 forks, ~45 issues abertas.
- Licença: MIT declarada no README e no badge (API do GitHub retornou `other/NOASSERTION` — divergência a verificar).

## Relações

- Mantido por: [SynkraAI](../../../entities/synkraai.md)
- Conceitos: [CLAUDE.md](../../../concepts/claude-md.md), [Agent skills](../../../concepts/agent-skills.md)
- Relacionado: [msitarzewski/agency-agents](../msitarzewski/agency-agents.md) — personalidades de agente instaláveis que podem ser combinadas com o sistema de agentes do AIOX.
- Relacionado: [croffasia/itsaplan](../croffasia/itsaplan.md) — issue tracker que também usa agentes como membros de equipe, abordagem diferente para integração humano-agente.

## Perguntas abertas

- Qual é a distinção exata de licença entre o core (MIT) e o Pro? O arquivo `docs/legal/license-clarification.md` não foi lido.
- Os arquivos de agente (`.aiox-core/agents/`) são semelhantes em formato aos da Agency Agents (`.md` com personalidade e regras)? Relação com o formato `SKILL.md`?
- A Memory Layer do ADE (Epic 7) é a mesma do AIOX Pro ou uma versão open-source mais limitada?
- Como o ADE interage com o servidor MCP do Claude Code para `@dev *execute-subtask`?

## Fontes

- README: https://raw.githubusercontent.com/SynkraAI/aiox-core/4ef6530ff03b83aea953e4a426f95e012b8b70c5/README.md (commit `4ef6530ff03b83aea953e4a426f95e012b8b70c5`, consultado em 2026-10-18). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub em 2026-10-18.
