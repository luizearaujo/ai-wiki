# Índice da Wiki

> Catálogo de todas as páginas da wiki. Atualize a cada ingestão, consulta arquivada ou remoção.
> Última atualização: 2026-10-19 (ingestão de OpenMontage, DeerFlow, Graphify e três skills do skills.sh)

## Repositórios

- [affaan-m/ECC](repos/github.com/affaan-m/ecc.md) — harness de agente com 71 agentes, 311 skills, memória portátil e AgentShield; processo de engenharia sobre Claude Code, Codex e outros clientes.
- [bytedance/deer-flow](repos/github.com/bytedance/deer-flow.md) — super agent harness em Python/LangGraph com agente líder, subagentes, skills de carregamento progressivo, sandbox, memória DeerMem e browser agêntico.
- [calesthio/OpenMontage](repos/github.com/calesthio/openmontage.md) — produção de vídeo agêntica em que o assistente de código orquestra pipelines YAML, skills de direção e validação sobre Remotion, HyperFrames e FFmpeg.
- [croffasia/itsaplan](repos/github.com/croffasia/itsaplan.md) — alternativa self-hosted ao Linear/Jira onde agentes de IA são membros de projeto com permissões e issues no mesmo board que as pessoas.
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — servidor MCP local em C puro que indexa bases de código em grafo de conhecimento persistente; 162 linguagens, Hybrid LSP, 17 ferramentas, ~120× menos tokens.
- [garrytan/gstack](repos/github.com/garrytan/gstack.md) — configuração de Claude Code com 23 especialistas e oito power tools que organizam o trabalho em um sprint de produto, de `/office-hours` a `/ship`.
- [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) — skill e CLI que transforma código e documentação em grafo de conhecimento com arestas extraídas/inferidas, sem vector store, e oferece um serviço Cloud.
- [HarnessMD/munder-difflin](repos/github.com/harnessmd/munder-difflin.md) — app desktop que transforma CLIs de agentes em um escritório virtual, com orquestrador Michael, hive de memória/mailbox e edição Pro.
- [littledivy/mimic](repos/github.com/littledivy/mimic.md) — captura tráfego de app iOS/web via mitmproxy, extrai auth e usa Claude para gerar um cliente Python chamável como biblioteca.
- [morluto/rea](repos/github.com/morluto/rea.md) — CLI e servidor MCP local para engenharia reversa de binários, aplicações e comportamento em execução com agentes.
- [msitarzewski/agency-agents](repos/github.com/msitarzewski/agency-agents.md) — mais de 150 personalidades de agente de IA em Markdown, organizadas em divisões especializadas e instaláveis em Claude Code, Cursor, Codex e outros.
- [multica-ai/andrej-karpathy-skills](repos/github.com/multica-ai/andrej-karpathy-skills.md) — diretrizes de comportamento para agentes em um único `CLAUDE.md`, derivadas das observações de Andrej Karpathy.
- [SynkraAI/aiox-core](repos/github.com/synkraai/aiox-core.md) — framework CLI-first de orquestração de IA com 12 agentes especializados (planejamento, dev, QA, DevOps) e ADE para desenvolvimento autônomo.

## Skills

- [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — sistema de design para diagramas editoriais em HTML/SVG, com gate de style guide e contrato de acessibilidade.
- [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — apresentações HTML autocontidas em palco 16:9, com descoberta de estilo, prévias, edição inline e exportação.
- [Understand](skills/github.com/egonex-ai/understand-anything/understand.md) — método em sete fases para gerar e validar um grafo de conhecimento de código com dashboard interativo.
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — auditoria ampla de UX com os frameworks de Morville, ISO e interaction design.

## Conceitos

- [Agent harness](concepts/agent-harness.md) — camada que define contexto, ferramentas, permissões, memória e supervisão de um agente já existente.
- [Agent skills](concepts/agent-skills.md) — instruções empacotadas em `SKILL.md`, distribuídas e instaladas como artefatos versionáveis.
- [Artefatos HTML autocontidos](concepts/artefatos-html-autocontidos.md) — apresentações e diagramas gerados como um único arquivo HTML com CSS, JS e SVG inline.
- [Auditoria de UX](concepts/auditoria-de-ux.md) — avaliação estruturada de um produto contra frameworks explícitos, com lacunas e recomendações.
- [CLAUDE.md](concepts/claude-md.md) — arquivo de instruções persistentes que fixa convenções e comportamento do agente no projeto.
- [Engenharia reversa agêntica](concepts/engenharia-reversa-agentica.md) — agentes com ferramentas que investigam e reconstroem software sem código-fonte.
- [Evidência e proveniência](concepts/evidencia-e-proveniencia.md) — resultados de análise como registros canônicos com cobertura, limitações e incertezas.
- [Grafo de conhecimento de código](concepts/grafo-de-conhecimento-de-codigo.md) — representação de código como grafo de nós e arestas tipadas, consultável por agentes sem leitura de arquivos.
- [Memória de agente](concepts/memoria-de-agente.md) — formatos e mecanismos para persistir decisões e handoffs entre sessões, harnesses e agentes.
- [Model Context Protocol (MCP)](concepts/model-context-protocol.md) — protocolo que conecta agentes a ferramentas e fontes externas.
- [Orquestração multiagente](concepts/orquestracao-multiagente.md) — coordenação de vários agentes com papéis, estado compartilhado, handoffs e supervisão.
- [Produção de vídeo agêntica](concepts/producao-de-video-agentica.md) — pipelines declarados e skills de direção que levam um agente de pesquisa e roteiro à renderização e validação de vídeo.

## Entidades

- [affaan-m](entities/affaan-m.md) — Affaan Mustafa, autor do ECC, harness de agente com foco em processo, memória e segurança.
- [ByteDance](entities/bytedance.md) — organização mantenedora do DeerFlow, super agent harness open-source com serviços comerciais de modelos e busca.
- [calesthio](entities/calesthio.md) — autor do OpenMontage, sistema de produção de vídeo agêntica baseado em pipelines e skills.
- [cathrynlavery](entities/cathrynlavery.md) — autora da skill Diagram Design, que gera diagramas editoriais em HTML/SVG com sistema de design consistente.
- [croffasia](entities/croffasia.md) — Andrii Poluosmak, autor do It's a Plan, issue tracker self-hosted com agentes de IA como membros de equipe.
- [DeusData](entities/deusdata.md) — organização criadora do codebase-memory-mcp, servidor MCP local de análise e grafo de conhecimento de código.
- [Egonex-AI](entities/egonex-ai.md) — organização que mantém o Understand Anything, plugin de skills que gera grafos de conhecimento de código com dashboard.
- [garrytan](entities/garrytan.md) — Garry Tan, presidente e CEO da Y Combinator, autor do gstack e do GBrain.
- [Graphify Labs](entities/graphify-labs.md) — organização Y Combinator S26 criadora do Graphify e do serviço Graphify Cloud.
- [HarnessMD](entities/harnessmd.md) — organização que mantém o Munder Difflin e o catálogo awesome-agent-capabilities.
- [littledivy](entities/littledivy.md) — autor do mimic, ferramenta de captura de tráfego e geração de cliente Python via Claude.
- [mastepanoski](entities/mastepanoski.md) — autor da coleção `claude-skills`, incluindo a skill de auditoria de UX.
- [morluto](entities/morluto.md) — criador do REA e mantenedor de ferramentas de engenharia reversa para agentes.
- [msitarzewski](entities/msitarzewski.md) — criador do Agency Agents, coleção de personalidades de agente organizadas em divisões especializadas.
- [multica-ai](entities/multica-ai.md) — organização por trás do Multica e do repositório de diretrizes `andrej-karpathy-skills`.
- [SynkraAI](entities/synkraai.md) — organização criadora do AIOX Squad, framework open-source CLI-first de orquestração de IA para equipes ágeis.
- [zarazhangrui](entities/zarazhangrui.md) — autor da skill Frontend Slides, que ensina agentes a criar apresentações HTML autocontidas.

## Análises

_Nenhuma análise arquivada ainda._
