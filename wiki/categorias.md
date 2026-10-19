---
type: category
created: 2026-10-19
updated: 2026-10-19
tags: [navegacao, categorias, indice-tematico]
---

# Categorias

> Catálogo temático da wiki: agrupa repositórios, skills, conceitos e entidades por área, complementando o catálogo por tipo em [`index.md`](index.md).

## Como ler

- A mesma página pode aparecer em mais de uma categoria quando cobre mais de uma área.
- [`index.md`](index.md) continua sendo a lista canônica e sem duplicatas de todas as páginas.
- Categorias são de navegação, não de escopo fechado: uma página pode mudar de categoria conforme a wiki cresce.

## Harnesses e orquestração de agentes

> Camadas que instalam processo, especialistas, memória e supervisão sobre CLIs existentes, ou que coordenam vários agentes em torno de um objetivo.

**Repositórios**
- [affaan-m/ECC](repos/github.com/affaan-m/ecc.md) — processo, 71 agentes, 311 skills e memória portátil sobre Claude Code, Codex e outros clientes.
- [bytedance/deer-flow](repos/github.com/bytedance/deer-flow.md) — super agent harness em Python/LangGraph com agente líder, subagentes, sandbox e memória DeerMem.
- [garrytan/gstack](repos/github.com/garrytan/gstack.md) — 23 especialistas e oito power tools no ciclo Think → Plan → Build → Review → Test → Ship → Reflect.
- [HarnessMD/munder-difflin](repos/github.com/harnessmd/munder-difflin.md) — app desktop que orquestra 12 CLIs em um escritório virtual, com hive de memória e gates humanos.
- [SynkraAI/aiox-core](repos/github.com/synkraai/aiox-core.md) — framework CLI-first com 12 agentes e fluxo PRD → histórias → execução.

**Conceitos**
- [Agent harness](concepts/agent-harness.md)
- [Memória de agente](concepts/memoria-de-agente.md)
- [Orquestração multiagente](concepts/orquestracao-multiagente.md)

**Entidades**
- [affaan-m](entities/affaan-m.md)
- [ByteDance](entities/bytedance.md)
- [garrytan](entities/garrytan.md)
- [HarnessMD](entities/harnessmd.md)
- [SynkraAI](entities/synkraai.md)

## Skills, instruções e personalidades de agente

> Formatos que moldam o comportamento do agente — `SKILL.md`, `CLAUDE.md`, personalidades e diretrizes distribuídas como artefatos versionáveis.

**Repositórios**
- [affaan-m/ECC](repos/github.com/affaan-m/ecc.md) — também nesta categoria pelo catálogo de 311 skills e pela migração de comandos para skills.
- [msitarzewski/agency-agents](repos/github.com/msitarzewski/agency-agents.md) — 150+ personalidades em Markdown, organizadas em 16 divisões.
- [multica-ai/andrej-karpathy-skills](repos/github.com/multica-ai/andrej-karpathy-skills.md) — quatro princípios de comportamento em um único `CLAUDE.md`.

**Conceitos**
- [Agent skills](concepts/agent-skills.md)
- [CLAUDE.md](concepts/claude-md.md)

**Entidades**
- [affaan-m](entities/affaan-m.md)
- [msitarzewski](entities/msitarzewski.md)
- [multica-ai](entities/multica-ai.md)

**Skills documentadas em outras categorias**
- [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) e [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — em [Geração de mídia e artefatos HTML](#geração-de-mídia-e-artefatos-html).
- [Understand](skills/github.com/egonex-ai/understand-anything/understand.md) — em [Grafos de conhecimento e contexto de código](#grafos-de-conhecimento-e-contexto-de-código).
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — em [Avaliação de UX e pesquisa](#avaliação-de-ux-e-pesquisa).

## Grafos de conhecimento e contexto de código

> Representações persistentes de código e documentos como grafos consultáveis, para responder perguntas estruturais com menos tokens do que reler arquivos.

**Repositórios**
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — servidor MCP local em C puro; 162 linguagens, Hybrid LSP e 17 ferramentas.
- [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) — skill e CLI que gera grafo com arestas `EXTRACTED`/`INFERRED`, sem vector store.

**Skills**
- [Understand](skills/github.com/egonex-ai/understand-anything/understand.md) — método em sete fases para gerar e validar um grafo de código com dashboard.

**Conceitos**
- [Grafo de conhecimento de código](concepts/grafo-de-conhecimento-de-codigo.md)

**Entidades**
- [DeusData](entities/deusdata.md)
- [Egonex-AI](entities/egonex-ai.md)
- [Graphify Labs](entities/graphify-labs.md)

## Engenharia reversa e análise de sistemas

> Investigação de binários, aplicações e tráfego para reconstruir comportamento sem código-fonte, com evidência explícita e limitações declaradas.

**Repositórios**
- [littledivy/mimic](repos/github.com/littledivy/mimic.md) — captura tráfego iOS/web e usa Claude para gerar um cliente Python a partir de sessões autenticadas.
- [morluto/rea](repos/github.com/morluto/rea.md) — CLI e servidor MCP local para análise estática e em runtime de binários, apps e firmware.

**Conceitos**
- [Engenharia reversa agêntica](concepts/engenharia-reversa-agentica.md)
- [Evidência e proveniência](concepts/evidencia-e-proveniencia.md)

**Entidades**
- [littledivy](entities/littledivy.md)
- [morluto](entities/morluto.md)

## Geração de mídia e artefatos HTML

> Produção de vídeo, apresentações e diagramas como artefatos reproduzíveis, com pipelines declarados ou arquivos HTML autocontidos.

**Repositórios**
- [calesthio/OpenMontage](repos/github.com/calesthio/openmontage.md) — produção de vídeo agêntica com pipelines YAML, skills de direção e validação sobre Remotion, HyperFrames e FFmpeg.

**Skills**
- [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — sistema de design para diagramas editoriais em HTML/SVG, com gate de style guide.
- [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — apresentações HTML autocontidas em palco 16:9, com descoberta de estilo e edição inline.

**Conceitos**
- [Artefatos HTML autocontidos](concepts/artefatos-html-autocontidos.md)
- [Produção de vídeo agêntica](concepts/producao-de-video-agentica.md)

**Entidades**
- [calesthio](entities/calesthio.md)
- [cathrynlavery](entities/cathrynlavery.md)
- [zarazhangrui](entities/zarazhangrui.md)

## Trabalho, projetos e colaboração humano-agente

> Ferramentas em que pessoas e agentes compartilham o mesmo fluxo de trabalho, board ou unidade de tarefa.

**Repositórios**
- [croffasia/itsaplan](repos/github.com/croffasia/itsaplan.md) — issue tracker self-hosted em que agentes de IA são membros de projeto com permissões e issues no mesmo board.

**Conceitos**
- [Orquestração multiagente](concepts/orquestracao-multiagente.md)

**Entidades**
- [croffasia](entities/croffasia.md)

## Protocolos, integrações e confiabilidade

> Camada que conecta agentes a ferramentas e dados, e critérios para que resultados de agentes sejam auditáveis.

**Conceitos**
- [Evidência e proveniência](concepts/evidencia-e-proveniencia.md)
- [Model Context Protocol (MCP)](concepts/model-context-protocol.md)

**Implementações e integrações documentadas**
- [croffasia/itsaplan](repos/github.com/croffasia/itsaplan.md) — REST API, MCP e webhooks.
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — servidor MCP de grafo de código.
- [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) — extra opcional `mcp`, além de Neo4j, FalkorDB e Postgres.
- [morluto/rea](repos/github.com/morluto/rea.md) — CLI e servidor MCP local de engenharia reversa.

**Entidades**
- [croffasia](entities/croffasia.md)
- [DeusData](entities/deusdata.md)
- [Graphify Labs](entities/graphify-labs.md)
- [morluto](entities/morluto.md)

## Avaliação de UX e pesquisa

> Avaliação estruturada de produtos contra frameworks explícitos, operacionalizada como skill reutilizável.

**Skills**
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — auditoria ampla de UX com os frameworks de Morville, ISO e interaction design.

**Conceitos**
- [Auditoria de UX](concepts/auditoria-de-ux.md)

**Entidades**
- [mastepanoski](entities/mastepanoski.md)

## Navegação e meta

- [index.md](index.md) — catálogo canônico por tipo de página.
- [overview.md](overview.md) — síntese em evolução do ecossistema.
- [log.md](log.md) — histórico append-only de operações.

## Manutenção

- Ao criar, renomear ou atualizar uma página, inclua-a na categoria adequada ou ajuste a entrada existente.
- Páginas transversais podem ser listadas em mais de uma categoria; não crie páginas duplicadas para isso.
- Se nenhuma categoria servir, crie uma nova com título claro e uma frase de escopo, e registre a mudança em [`log.md`](log.md).
- Remova a entrada quando a página for removida ou renomeada.

## Fontes

- Páginas da própria wiki: [index.md](index.md), [overview.md](overview.md) e [log.md](log.md), consultadas em 2026-10-19.
