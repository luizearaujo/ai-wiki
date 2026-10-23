---
type: concept
aliases: [Memória de agente, Agent memory, Memória persistente, Long-term memory]
status: draft
created: 2026-10-19
updated: 2026-10-23
tags: [agentes, memoria, contexto, handoff, persistencia]
---

# Memória de agente

> Camada que persiste informações entre sessões, conversas ou harnesses para que o agente mantenha contexto, preferências e decisões sem depender do histórico de uma única sessão.

## Definição

Memória de agente é o mecanismo que responde a "o que o agente deve lembrar depois que esta sessão terminar?". Ela pode guardar fatos sobre o usuário, decisões de projeto, padrões de código, resultados de análises ou um índice consultável do próprio repositório.

Não se confunde com:

- **contexto de sessão** — mensagens e ferramentas dentro de uma execução;
- **compactação** — resumo do histórico para caber na janela;
- **RAG sobre documentos** — recuperação de uma base externa;
- **checkpoint** — estado técnico de uma execução retomável.

A distinção é de **escopo e duração**: memória sobrevive à sessão e, em alguns casos, ao harness.

## Como funciona

Formatos observados na wiki:

| Formato | Como funciona | Exemplo |
|---|---|---|
| **Markdown portátil** | Fatos e handoffs em arquivos legíveis e versionáveis | Memory Vault do ECC |
| **Grafo de conhecimento** | Símbolos e relações indexados, consultáveis por query | Graphify; CBM; Understand Anything |
| **Base consultável via MCP** | Servidor expõe busca/leitura/escrita como ferramentas | GBrain no gstack |
| **Repositório compartilhado** | Memória por agente + mailbox + blackboard em git | Hive do Munder Difflin |
| **Fatos em Markdown + índice** | Fatos por usuário/agente, índice FTS/BM25, gate de escopo | DeerMem no Deer Flow |
| **Log de decisões com liquidação** | Decisões append-only; ao vencer o horizonte, o resultado é apurado e vira reflexão lida em análises futuras | Memory log do TradingAgents |

Questões de projeto que aparecem em todos:

1. **O que entra** — só fatos duráveis ou também resumos, preferências e decisões?
2. **Quem lê** — usuário, agente, time ou outro harness?
3. **Como expira** — TTL, deduplicação, limite de fatos, política de despejo?
4. **Como isola** — por usuário, agente, projeto e credencial?
5. **Como audita** — log de escrita, proveniência e possibilidade de correção?
6. **Como evita envenenamento** — memória é contexto não confiável, não política.

## Onde aparece

- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — Memory Vault em Markdown portátil, com handoff entre harnesses e servidor MCP opcional.
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — GBrain como base de conhecimento persistente consultável por MCP, com níveis de confiança por repositório.
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — hive com memória por agente, mailbox atômica, blackboard e log append-only.
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — DeerMem como backend padrão, com fatos em Markdown, índice FTS5/BM25, gate de escopo/durabilidade e backends opcionais (mem0, Honcho, OpenViking).
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — grafo de conhecimento do código como memória consultável, sem vector store.
- [thedotmack/claude-mem](../repos/github.com/thedotmack/claude-mem.md) — hooks de ciclo de vida capturam observações de sessão, comprimem com IA e as reinjetam via busca híbrida SQLite FTS5 + Chroma em 3 camadas (índice, timeline, detalhe).
- [skill understand](../skills/github.com/egonex-ai/understand-anything/understand.md) — grafo persistente por projeto, com fingerprints e atualização incremental.
- [TauricResearch/TradingAgents](../repos/github.com/tauricresearch/tradingagents.md) — memory log sempre ativo em Markdown: cada decisão é liquidada quando o horizonte vence, com retorno realizado, alfa contra benchmark e reflexão consumida pelo gestor de portfólio.
- [trailhq/Trail-Code](../repos/github.com/trailhq/trail-code.md) — "learnings" como arquivos Markdown em três escopos (pessoal, repositório, equipe), salvos pelo próprio agente a partir das conversas e verificados contra o diff antes de um PR (`trail check`).
- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) — duas variações: `bookkeeping-agent` guarda dados do usuário (despesas, fatos, recibos) em `memory/` como JSON/markdown, com um `brain/brain.md` para categorias e convenções; `hermes-hostinger-webui-memory` documenta como plugar o Honcho como memória externa em um agente Hermes self-hosted, no lugar da memória nativa em markdown local.
- [open-gsd/gsd-core](../repos/github.com/open-gsd/gsd-core.md) — `STATE.md` e `CONTEXT.md` como artefatos estruturados que sobrevivem às fronteiras de sessão de um loop de cinco fases, substituindo memória implícita por estado explícito versionado.

## Trade-offs

- **Vantagens:** continuidade entre sessões; menos repetição de contexto; handoff entre agentes e harnesses; decisões e preferências preservadas; possibilidade de auditoria e correção.
- **Limitações:** memória envelhece e pode ficar errada; custo de indexação e de injeção no prompt; risco de vazamento entre usuários/agentes; memória envenenada pode virar instrução persistente; formatos não são interoperáveis; excesso de memória compete com a tarefa.
- **Critério prático:** memória vale quando há informação durável e reutilizável; para fatos efêmeros, o histórico da sessão ou um checkpoint é suficiente.

## Relações

- **Relacionado a:** [Agent harness](agent-harness.md) — a memória é um componente do harness; [Grafo de conhecimento de código](grafo-de-conhecimento-de-codigo.md) — memória estrutural do código; [Model Context Protocol](model-context-protocol.md) — transporte comum para expor memória como ferramenta; [Orquestração multiagente](orquestracao-multiagente.md) — memória compartilhada como estado de coordenação.
- **Distingue-se de:** janela de contexto, compactação, RAG e checkpoint de execução.
- **Pré-requisito para:** handoff confiável entre sessões, agentes e harnesses diferentes.

## Perguntas abertas

- Existe um formato comum de memória entre harnesses, ou cada projeto cria o seu?
- Como medir utilidade versus ruído de memória ao longo do tempo?
- Como evitar que memória envenenada se torne instrução persistente?
- Quem controla a memória: o usuário, o agente ou o operador da plataforma?
- Como sincronizar memória entre máquinas, projetos e membros de equipe?
- Memória deve ser tratada como dado não confiável em todas as leituras?

## Fontes

- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — README no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34` (consultado em 2026-10-19).
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037` (consultado em 2026-10-19).
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — README no commit `436d65a74a69d347c57641fbace4eb822bf98600` (consultado em 2026-10-19).
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — README no commit `fee0cd0c180874325305e995197db99f03fa6a6f` (consultado em 2026-10-19).
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — README no commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8` (consultado em 2026-10-19).
- [skill understand](../skills/github.com/egonex-ai/understand-anything/understand.md) — página do skills.sh (consultada em 2026-10-19).
- [TauricResearch/TradingAgents](../repos/github.com/tauricresearch/tradingagents.md) — README no commit `e8f5503e9b86d5c2710b0c76b1f686703968c9df` (consultado em 2026-10-19).
- [trailhq/Trail-Code](../repos/github.com/trailhq/trail-code.md) — README no commit `b1211efd3eef0efa121b93800e5dd8e547aead77` (consultado em 2026-10-21).
- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) — clone local no commit `555467c365e6750278efba09349369109f62f65f`, `bookkeeping-agent/cloud/README.md` e READMEs de `hermes-hostinger-webui-memory` (consultado em 2026-10-21).
- [open-gsd/gsd-core](../repos/github.com/open-gsd/gsd-core.md) — README no commit `6ddd0cef9cb26673bd8321c5480c0814a92d54cb` (consultado em 2026-10-23).
