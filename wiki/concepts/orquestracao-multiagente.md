---
type: concept
aliases: [Orquestração multiagente, Multi-agent orchestration, Orquestração de agentes]
status: draft
created: 2026-10-19
updated: 2026-10-23
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
| **Drafter-reviewer** | Um agente redige, um segundo agente com contexto novo pesquisa e critica, o primeiro revisa | MadsLorentzen/ai-job-search: `/apply` redige CV/carta, um revisor pesquisa a empresa e critica antes da versão final |
| **Graph of Agents especializados por fase ofensiva** | Agentes de recon, exploração e pós-exploração compartilham descobertas e encadeiam vulnerabilidades em paralelo, contra vários alvos | usestrix/strix |
| **Paralelismo isolado** | Sessões independentes em worktrees/branches separados | gstack com Conductor; ECC com worktrees |
| **Coordenação visual** | Agentes viram avatares com mesa, mailbox e board | Munder Difflin |
| **Board compartilhado** | Agentes são assignees no mesmo issue tracker que humanos | [croffasia/itsaplan](../repos/github.com/croffasia/itsaplan.md) |
| **Subagente com contexto isolado** | O líder despacha subtarefas com contexto isolado ou um snapshot do histórico e sintetiza os resultados | DeerFlow: agente líder + `task`, com memória DeerMem compartilhada |
| **Pipeline declarado com gates** | Etapas em manifesto, skills de direção por etapa e checkpoints resumíveis | OpenMontage: proposta → roteiro → ativos → edição → validação |
| **Papéis de firma com debate e aprovação** | Analistas em paralelo, debate entre teses opostas, trader e cadeia de risco que aprova ou rejeita | TradingAgents: analistas → pesquisadores bullish/bearish → trader → risco → gestor de portfólio |
| **Pipeline com revisão paralela e aprovador** | Builder sobre branch própria, quatro revisores em paralelo ("WAIT FOR ALL"), aprovador que mergeia ou escala | skill [Factory](../skills/github.com/zazencodes/zazencodes-season-3/factory.md), em zazencodes/zazencodes-season-3: spec-writer → builder → [security, ux, ui, code] → approver |
| **Hub-and-spoke por CLI isolado em pasta** | Um agente qualquer na raiz é o hub e delega para sub-agentes rodando um runtime próprio em subpastas, cada um com seu próprio "cérebro" em markdown | zazencodes/zazencodes-season-3 (`pi-agent-fleet`): hub lê `AGENTS.md`, sub-agentes `pi` em `agents/<nome>/` com `brain.md` |
| **Orquestrador/trabalhador por painel de terminal** | O agente principal só pensa e sintetiza; cada trabalhador roda em uma sessão de CLI isolada em seu próprio painel de tmux, visível ao usuário | skill [Gemini Web Research](../skills/github.com/zazencodes/skills/gemini-web-research.md): sessões `agy` (Google Antigravity) por área de pesquisa, com follow-up na mesma sessão |

O ponto comum é a **externalização do contexto**: em vez de depender do histórico de uma sessão, a coordenação passa por artefatos que outros agentes conseguem ler. Isso reduz perda de contexto, mas cria trabalho de bookkeeping e exige que os artefatos sejam mantidos corretos.

## Onde aparece

- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — 71 subagentes especializados, revisão em contexto novo, família de orquestradores `orch-*`, worktrees e Memory Vault para handoffs.
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — agente líder que decompõe a tarefa e despacha subagentes com contexto isolado ou snapshot; checkpoints, compactação e memória DeerMem para retomar tarefas longas.
- [OpenMontage](../repos/github.com/calesthio/openmontage.md) — o assistente de código é o orquestrador de um pipeline de produção de vídeo declarado em YAML, com skills de direção por etapa, gates de revisão e checkpoints com custo e decisões.
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — especialistas por etapa do sprint, `/autoplan`, `/pair-agent` para compartilhar navegador entre agentes de fornecedores diferentes e 10–15 sprints paralelos via Conductor.
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — orquestrador Michael, hive com memória/mailbox/blackboard/log, committer único para git, PTY por agente e escritório visual.
- [vastsa/PI-Desktop](../repos/github.com/vastsa/pi-desktop.md) — subagentes em background com contexto próprio e Session Orchestrator com Worker Sessions completas, inspecionáveis e reutilizáveis; o usuário define a autonomia por sessão.
- [SynkraAI/aiox-core](../repos/github.com/synkraai/aiox-core.md) — equipe de 12 agentes com roles ágeis e PRD/histórias como unidade de contexto.
- [croffasia/itsaplan](../repos/github.com/croffasia/itsaplan.md) — agentes como membros de projeto com assignee, permissões e issues no mesmo Kanban.
- [TauricResearch/TradingAgents](../repos/github.com/tauricresearch/tradingagents.md) — quatro analistas em paralelo, debate estruturado entre pesquisadores bullish e bearish, trader, time de risco e gestor de portfólio; LangGraph com estado compartilhado, checkpoints opcionais e memory log.
- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) — duas pastas com padrões distintos: a skill [Factory](../skills/github.com/zazencodes/zazencodes-season-3/factory.md) (sete subagentes do Claude Code, revisão em quatro frentes em paralelo e aprovador, cada job em seu próprio git worktree) e `pi-agent-fleet` (hub-and-spoke: um agente qualquer na raiz delega para sub-agentes `pi` isolados por pasta, cada um com seu `brain.md`); também `minimax-dev-rpg`, que visualiza como jogo um agente MiniMax resolvendo issues reais do GitHub.
- [Gemini Web Research](../skills/github.com/zazencodes/skills/gemini-web-research.md) — padrão orquestrador/trabalhador em que cada trabalhador é uma sessão `agy` (Google Antigravity) em seu próprio painel de tmux; o orquestrador só lê relatórios, decide o que falta e sintetiza.
- [MadsLorentzen/ai-job-search](../repos/github.com/madslorentzen/ai-job-search.md) — drafter-reviewer em `/apply`: um agente redige CV e carta, um segundo agente com contexto novo pesquisa a empresa e critica os rascunhos, o primeiro revisa antes da compilação final.
- [usestrix/strix](../repos/github.com/usestrix/strix.md) — "Graph of Agents": times especializados em recon, exploração e pós-exploração compartilham descobertas, encadeiam vulnerabilidades e rodam em paralelo contra vários alvos.
- [google-research/harness2](../repos/github.com/google-research/harness2.md) — subagentes como um dos oito componentes editáveis do harness, orquestrando trabalho delegado dentro de um loop que o próprio framework otimiza automaticamente por contraste comportamental (ver [Agent harness](agent-harness.md)).
- [open-gsd/gsd-core](../repos/github.com/open-gsd/gsd-core.md) — fase Execute do loop de cinco fases: planos rodam em ondas paralelas, cada executor com um contexto novo de 200 mil tokens, antes de a fase Verify consolidar o resultado.

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
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — README no commit `fee0cd0c180874325305e995197db99f03fa6a6f` (consultado em 2026-10-19).
- [OpenMontage](../repos/github.com/calesthio/openmontage.md) — README no commit `c8066452325cb57c8fc1ba8c2a71b6e8842e6b65` (consultado em 2026-10-19).
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037` (consultado em 2026-10-19).
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — README no commit `436d65a74a69d347c57641fbace4eb822bf98600` (consultado em 2026-10-19).
- [vastsa/PI-Desktop](../repos/github.com/vastsa/pi-desktop.md) — README no commit `87a48b953e8bada43a7a63f8922846198b9efb61` (consultado em 2026-10-19).
- [SynkraAI/aiox-core](../repos/github.com/synkraai/aiox-core.md) e [croffasia/itsaplan](../repos/github.com/croffasia/itsaplan.md) — páginas existentes da wiki, usadas como comparação.
- [TauricResearch/TradingAgents](../repos/github.com/tauricresearch/tradingagents.md) — README no commit `e8f5503e9b86d5c2710b0c76b1f686703968c9df` (consultado em 2026-10-19).
- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) — clone local no commit `555467c365e6750278efba09349369109f62f65f`, READMEs de `software-factory-claude-code`, `pi-agent-fleet` e `minimax-dev-rpg` (consultado em 2026-10-21).
- [Gemini Web Research](../skills/github.com/zazencodes/skills/gemini-web-research.md) — `SKILL.md` de `zazencodes/skills` no commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2` (clone local, consultado em 2026-10-21).
- [MadsLorentzen/ai-job-search](../repos/github.com/madslorentzen/ai-job-search.md) — README no commit `e16acee3abdaae57f8026789338a3c6eebf4608b` (consultado em 2026-10-21).
- [usestrix/strix](../repos/github.com/usestrix/strix.md) — README no commit `fde37a149fc942dd107666441a1989f187d30c3b` (consultado em 2026-10-21).
- [google-research/harness2](../repos/github.com/google-research/harness2.md) — README no commit `1cfe254e8d25b15f37048c3730134686abe60335` (consultado em 2026-10-21).
- [open-gsd/gsd-core](../repos/github.com/open-gsd/gsd-core.md) — README no commit `6ddd0cef9cb26673bd8321c5480c0814a92d54cb` (consultado em 2026-10-23).
