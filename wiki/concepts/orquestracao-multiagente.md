---
type: concept
aliases: [Orquestração multiagente, Multi-agent orchestration, Orquestração de agentes]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [agentes, orquestracao, multi-agente, harness]
---

# Orquestração multiagente

> Coordenação de vários agentes de IA com papéis, estado compartilhado, regras de handoff e supervisão, de modo que o trabalho paralelo não vire uma coleção de sessões independentes e conflitantes.

## Definição

Orquestração multiagente é a camada que decide **quem faz o quê, com qual contexto, em que ordem e como os resultados se encontram**. Ela aparece quando uma tarefa é decomposta entre agentes especializados — planejador, implementador, revisor, QA, designer, segurança — ou quando várias instâncias do mesmo agente trabalham em paralelo.

Não é o mesmo que ter vários prompts em abas diferentes. A orquestração exige algum mecanismo de:

- **papéis e escopo** — cada agente tem responsabilidade e permissões delimitadas;
- **estado compartilhado** — planos, specs, filas, mailboxes, blackboards ou um repositório de artefatos;
- **roteamento e handoff** — quem recebe o quê e em que formato;
- **isolamento** — worktrees, PTYs, sandboxes ou contextos separados para evitar colisões;
- **supervisão** — um orquestrador, um humano ou ambos decidem exceções e aprovações;
- **observabilidade** — logs, ledger de tarefas, custo e evidência de execução.

## Como funciona

Os padrões observados na wiki:

| Padrão | Como coordena | Exemplo |
|---|---|---|
| **Pipeline por artefatos** | Cada etapa lê o documento produzido pela anterior | gstack: design doc → plano → review → QA → ship |
| **Supervisor/orquestrador** | Um agente recebe o pedido, distribui e escala exceções | Munder Difflin: Michael, o agente "GOD" |
| **Papéis ágeis** | Agentes especializados com passagem por PRD/histórias | AIOX: analyst, pm, architect, dev, QA, devops |
| **Revisão em contexto novo** | O autor não revisa o próprio trabalho; um agente separado lê o diff | ECC: `/code-review`, agentes revisores por linguagem |
| **Paralelismo isolado** | Sessões independentes em worktrees/branches separados | gstack com Conductor; ECC com worktrees |
| **Coordenação visual** | Agentes viram avatares com mesa, mailbox e board | Munder Difflin |
| **Board compartilhado** | Agentes são assignees no mesmo issue tracker que humanos | [croffasia/itsaplan](../repos/github.com/croffasia/itsaplan.md) |

O ponto comum é a **externalização do contexto**: em vez de depender do histórico de uma sessão, a coordenação passa por artefatos que outros agentes conseguem ler. Isso reduz perda de contexto, mas cria trabalho de bookkeeping e exige que os artefatos sejam mantidos corretos.

## Onde aparece

- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — 71 subagentes especializados, revisão em contexto novo, família de orquestradores `orch-*`, worktrees e Memory Vault para handoffs.
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — especialistas por etapa do sprint, `/autoplan`, `/pair-agent` para compartilhar navegador entre agentes de fornecedores diferentes e 10–15 sprints paralelos via Conductor.
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — orquestrador Michael, hive com memória/mailbox/blackboard/log, committer único para git, PTY por agente e escritório visual.
- [SynkraAI/aiox-core](../repos/github.com/synkraai/aiox-core.md) — equipe de 12 agentes com roles ágeis e PRD/histórias como unidade de contexto.
- [croffasia/itsaplan](../repos/github.com/croffasia/itsaplan.md) — agentes como membros de projeto com assignee, permissões e issues no mesmo Kanban.

## Trade-offs

- **Vantagens:** paralelismo real; especialização e contexto menor por agente; revisão independente; capacidade de rodar tarefas longas sem monopolizar uma sessão; trilha de artefatos auditável.
- **Limitações:** custo multiplicado de tokens e chamadas; overhead de coordenação; erros podem se propagar entre agentes; risco de contexto duplicado ou divergente; necessidade de isolamento (git, filesystem, credenciais); observabilidade e aprovação humana ficam mais complexas; latência de handoff pode anular o ganho em tarefas pequenas.
- **Quando não usar:** tarefas sequenciais curtas, onde um único agente com bom contexto é mais barato e mais previsível.

## Relações

- **Relacionado a:** [Agent harness](agent-harness.md) — o harness fornece o runtime onde a orquestração acontece; [Agent skills](agent-skills.md) — encapsulam os workflows que cada papel executa; [CLAUDE.md](claude-md.md) — instruções persistentes que alinham vários agentes; [Model Context Protocol](model-context-protocol.md) — ferramentas compartilhadas entre agentes.
- **Contrasta com:** um único agente generalista com prompt longo; várias abas independentes sem handoff.
- **Pré-requisito para:** automação de ponta a ponta com revisão independente e QA, em vez de geração de código em uma só passada.

## Perguntas abertas

- Como medir se a orquestração compensa em custo e qualidade, e não apenas em paralelismo?
- Qual é o mecanismo mais confiável de estado compartilhado: arquivos, mailbox, board, banco ou memória vetorial?
- Como evitar que um agente-orquestrador se torne gargalo ou ponto único de falha?
- Como isolar credenciais, filesystem e git entre agentes sem impedir a colaboração?
- Como auditar decisões e ações quando vários agentes agem ao mesmo tempo?
- Que padrões de handoff e de resolução de conflito estão emergindo entre fornecedores?

## Fontes

- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — README no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34` (consultado em 2026-10-19).
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037` (consultado em 2026-10-19).
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — README no commit `436d65a74a69d347c57641fbace4eb822bf98600` (consultado em 2026-10-19).
- [SynkraAI/aiox-core](../repos/github.com/synkraai/aiox-core.md) e [croffasia/itsaplan](../repos/github.com/croffasia/itsaplan.md) — páginas existentes da wiki, usadas como comparação.
