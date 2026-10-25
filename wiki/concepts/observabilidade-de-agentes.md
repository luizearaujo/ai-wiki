---
type: concept
aliases: [Observabilidade de agentes de código, Agent observability, Agent monitoring, Rastreamento de sessões de agentes]
status: draft
created: 2026-10-25
updated: 2026-10-25
tags: [observabilidade, agentes, dashboard, sessoes, tokens, replay, progresso]
---

# Observabilidade de agentes de código

> Conjunto de técnicas e ferramentas que transformam a atividade interna de agentes de código — tool calls, tokens consumidos, árvores de subagentes, mudanças de arquivo, progresso de tarefas — em dados consultáveis e visualizáveis sem modificar os agentes nem reexecutar suas ações.

## Definição

Agentes de código produzem logs estruturados como subproduto natural de sua execução: arquivos JSONL com turnos, tool calls e metadados de sessão; bancos SQLite com histórico de tarefas; mudanças de arquivo rastreadas por git. Ferramentas de observabilidade lêem esses artefatos e os indexam em um formato queryable.

O princípio central é separar **observação** de **execução**: a ferramenta de observabilidade nunca lança agentes, aprova ações nem altera o comportamento dos agentes. Ela só registra o que já aconteceu.

Isso contrasta com ferramentas de orquestração (que coordenam agentes) e com logs brutos de terminal (que registram, mas não indexam nem visualizam).

## Duas dimensões de análise

A observabilidade de agentes cobre duas dimensões distintas que as ferramentas atuais tratam de formas diferentes:

| Dimensão | Foco | Exemplos de métricas |
|---|---|---|
| **Custo e rastreabilidade** | O que o agente consumiu e executou | Tokens por turno (input/output/cache), custo estimado em USD, tool calls, contexto injetado, árvore de subagentes |
| **Progresso e fluxo** | O que o agente avançou no projeto | Componentes alterados, tarefas abertas/concluídas, contribuições por papel, handoffs entre sessões |

Ferramentas atuais tendem a especializar em uma das dimensões, não nas duas.

## Onde aparece

- [camtrik/agent-trail](../repos/github.com/camtrik/agent-trail.md) — foco em custo e rastreabilidade: token accounting por turno, custo estimado em USD, replay completo com tool calls e árvores de subagentes expostas, skill `local-session-search` para busca em sessões históricas. Suporta Claude Code, OpenClaw, Codex, OpenCode e Qoder.
- [sodiumsun/agenttrail](../repos/github.com/sodiumsun/agenttrail.md) — foco em progresso e fluxo: Map (PLAN.md + mudanças de arquivo + hooks) e Kitchen (visualização 3D com metáfora culinária onde chefs = papéis, tickets = todos, pratos = entregas). Suporta Claude Code, Codex e Cursor. Destaca-se pela distinção entre o que acontece automaticamente e o que requer metadados extras.

## Trade-offs

- **Vantagens:** sem latência de execução — só lê artefatos existentes; dados nunca saem da máquina; não afeta o comportamento dos agentes; pode ser instalado em cima de agentes já rodando.
- **Limitações:** só observa o que os agentes registram; sessões remotas sem logs locais não são descobertas; o formato de log pode mudar entre versões do agente; a correlação entre sessões de agentes diferentes requer convenções (ex.: PLAN.md) ou inferência.
- **Custo escondido:** logs de sessões longas crescem rapidamente; índices locais precisam de manutenção; ferramentas diferentes cobrem diferentes subconjuntos de agentes.

## Relações

- **Relacionado a:** [Agent harness](agent-harness.md) — o harness produz os artefatos que a observabilidade consome; [Orquestração multiagente](orquestracao-multiagente.md) — árvores de subagentes são um caso de uso central para replay.
- **Depende de:** logs estruturados e acessíveis produzidos pelo agente (JSONL, SQLite); convenções de projeto (PLAN.md) para observabilidade de progresso.

## Perguntas abertas

- Qual é o overhead de indexação para sessões muito longas (centenas de turnos, milhares de tool calls)?
- Como correlacionar sessões de agentes diferentes trabalhando no mesmo projeto sem uma convenção explícita de plano?
- É possível observar sessões remotas (cloud) com garantias de privacidade equivalentes às ferramentas locais?
- Quando vale a pena rastrear raciocínio (`reasoning tokens`) além de output tokens?

## Fontes

- [camtrik/agent-trail](../repos/github.com/camtrik/agent-trail.md) — README no commit `6e53f21f292955974ac21a082edb4ac216e2ad92` (consultado em 2026-10-25).
- [sodiumsun/agenttrail](../repos/github.com/sodiumsun/agenttrail.md) — README no commit `e4ba2daa270abd7ecb51565bbfb12386f47ea418` (consultado em 2026-10-25).
