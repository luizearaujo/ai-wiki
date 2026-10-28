---
type: category
created: 2026-10-19
updated: 2026-10-25
tags: [navegacao, categorias, indice-tematico]
---

# Categorias

> Catálogo temático da wiki: agrupa repositórios, skills, conceitos e entidades por área, complementando o catálogo por tipo em [`index.md`](index.md).

## Sumário

- [Como ler](#como-ler)
- [Harnesses e orquestração de agentes](#harnesses-e-orquestração-de-agentes)
- [Plataformas self-hosted de aplicações e interfaces de IA](#plataformas-self-hosted-de-aplicações-e-interfaces-de-ia)
- [Skills, instruções e personalidades de agente](#skills-instruções-e-personalidades-de-agente)
- [Guias, cursos e listas curadas sobre Claude Code](#guias-cursos-e-listas-curadas-sobre-claude-code)
- [Grafos de conhecimento e contexto de código](#grafos-de-conhecimento-e-contexto-de-código)
- [Engenharia reversa e análise de sistemas](#engenharia-reversa-e-análise-de-sistemas)
- [Cibersegurança e operações de segurança](#cibersegurança-e-operações-de-segurança)
- [Geração de mídia e artefatos HTML](#geração-de-mídia-e-artefatos-html)
- [Geração de imagem e vídeo com modelos de difusão](#geração-de-imagem-e-vídeo-com-modelos-de-difusão)
- [Síntese, clonagem e transcrição de voz](#síntese-clonagem-e-transcrição-de-voz)
- [Design de interface e direção de arte](#design-de-interface-e-direção-de-arte)
- [Comunicação e caixas de entrada agênticas](#comunicação-e-caixas-de-entrada-agênticas)
- [Trabalho, projetos e colaboração humano-agente](#trabalho-projetos-e-colaboração-humano-agente)
- [Análise financeira e trading](#análise-financeira-e-trading)
- [Marketing, mídia paga e conteúdo](#marketing-mídia-paga-e-conteúdo)
- [Inferência local e runtime de modelos](#inferência-local-e-runtime-de-modelos)
- [Modelos abertos e treinamento de LLMs](#modelos-abertos-e-treinamento-de-llms)
- [Engenharia e interfaces agent-first](#engenharia-e-interfaces-agent-first)
- [Protocolos, integrações e confiabilidade](#protocolos-integrações-e-confiabilidade)
- [Avaliação de UX e pesquisa](#avaliação-de-ux-e-pesquisa)
- [Escrita e comunicação](#escrita-e-comunicação)
- [Conhecimento pessoal e curadoria](#conhecimento-pessoal-e-curadoria)
- [Pesquisa e notas pessoais com IA](#pesquisa-e-notas-pessoais-com-ia)
- [Pesquisa social e monitoramento de tendências](#pesquisa-social-e-monitoramento-de-tendências)
- [OSINT geoespacial e agentes de voz](#osint-geoespacial-e-agentes-de-voz)
- [Navegação e meta](#navegação-e-meta)
- [Manutenção](#manutenção)
- [Fontes](#fontes)

## Como ler

- A mesma página pode aparecer em mais de uma categoria quando cobre mais de uma área.
- [`index.md`](index.md) continua sendo a lista canônica e sem duplicatas de todas as páginas.
- Categorias são de navegação, não de escopo fechado: uma página pode mudar de categoria conforme a wiki cresce.

## Harnesses e orquestração de agentes

> Camadas que instalam processo, especialistas, memória e supervisão sobre CLIs existentes, ou que coordenam vários agentes em torno de um objetivo.

**Repositórios**
- [affaan-m/ECC](repos/github.com/affaan-m/ecc.md) — processo, 71 agentes, 311 skills e memória portátil sobre Claude Code, Codex e outros clientes.
- [bytedance/deer-flow](repos/github.com/bytedance/deer-flow.md) — super agent harness em Python/LangGraph com agente líder, subagentes, sandbox e memória DeerMem.
- [camtrik/agent-trail](repos/github.com/camtrik/agent-trail.md) — dashboard local de observabilidade que agrega token usage, custo, tool calls e replay de sessões de Claude Code, Codex, OpenCode, OpenClaw e Qoder.
- [Fosowl/agenticSeek](repos/github.com/fosowl/agenticseek.md) — assistente local com seleção automática entre agentes de navegação web, código e planejamento, sem depender de nuvem.
- [garrytan/gstack](repos/github.com/garrytan/gstack.md) — 23 especialistas e oito power tools no ciclo Think → Plan → Build → Review → Test → Ship → Reflect.
- [google-research/harness2](repos/github.com/google-research/harness2.md) — framework de pesquisa que otimiza automaticamente o harness de um agente por recursão Propose–Probe–Compose, com paper (arXiv:2610.14224) e três benchmarks profissionais.
- [HarnessMD/munder-difflin](repos/github.com/harnessmd/munder-difflin.md) — app desktop que orquestra 12 CLIs em um escritório virtual, com hive de memória e gates humanos.
- [hellosverre/claude-skins](repos/github.com/hellosverre/claude-skins.md) — mod `/skin`: redesenha tool calls, diffs, tabelas e Mermaid do Claude Code em dezesseis temas, repintáveis ou desenhados pelo próprio Claude.
- [JohnnyVizz/claude-kit](repos/github.com/johnnyvizz/claude-kit.md) — skill `savvy-flow` (planeja, delega a subagentes, revisa) e dois mods de interface (`savvy-progress`, `session-band`) para o Claude Code.
- [obra/superpowers](repos/github.com/obra/superpowers.md) — metodologia design → plano → TDD por subagentes → revisão, imposta como skills que disparam automaticamente em mais de uma dezena de harnesses.
- [open-gsd/gsd-core](repos/github.com/open-gsd/gsd-core.md) — loop de cinco fases (Discuss, Plan, Execute, Verify, Ship) com subagentes de contexto limpo e estado persistente em `STATE.md`/`CONTEXT.md`, sobre Claude Code e outros runtimes.
- [openai/codex-plugin-cc](repos/github.com/openai/codex-plugin-cc.md) — plugin oficial da OpenAI que traz review e delegação de tarefas ao Codex como slash commands dentro do Claude Code.
- [OpenHands/OpenHands](repos/github.com/openhands/openhands.md) — Agent Canvas, control center self-hosted que conecta e automatiza múltiplos backends de agente (OpenHands, Claude Code, Codex, Gemini, Pi, OpenCode) via ACP.
- [sodiumsun/agenttrail](repos/github.com/sodiumsun/agenttrail.md) — observabilidade local com vista Map (PLAN.md + mudanças de arquivo) e Kitchen (3D com chefs, tickets e pratos como metáfora de progresso do projeto).
- [SynkraAI/aiox-core](repos/github.com/synkraai/aiox-core.md) — framework CLI-first com 12 agentes e fluxo PRD → histórias → execução.
- [thedotmack/claude-mem](repos/github.com/thedotmack/claude-mem.md) — memória persistente para Claude Code: hooks de ciclo de vida, worker local e busca híbrida SQLite/Chroma em 3 camadas.
- [trailhq/Trail-Code](repos/github.com/trailhq/trail-code.md) — também nesta categoria pelos "learnings": decisões e preferências salvas das conversas, versionadas em git em três escopos (pessoal, repositório, equipe).
- [vastsa/PI-Desktop](repos/github.com/vastsa/pi-desktop.md) — workspace desktop sobre o runtime `pi`, com sessões persistentes, subagentes, Worker Sessions, permissões e plugins `.piplug`.
- [volcengine/OpenViking](repos/github.com/volcengine/openviking.md) — também nesta categoria pelo VikingBot, framework de agente embutido no banco de contexto; detalhe em [Memória de agente](concepts/memoria-de-agente.md).
- [zazencodes/zazencodes-season-3](repos/github.com/zazencodes/zazencodes-season-3.md) — duas pastas com padrões distintos: fábrica de software com a skill [Factory](skills/github.com/zazencodes/zazencodes-season-3/factory.md), sete subagentes e revisão em paralelo (`software-factory-claude-code`), e hub-and-spoke com sub-agentes `pi` isolados por pasta (`pi-agent-fleet`), além de harnesses sempre ativos sobre Pi/Neon e eve.

**Skills**
- [Gemini Web Research](skills/github.com/zazencodes/skills/gemini-web-research.md) — orquestrador/trabalhador em que cada trabalhador é uma sessão `agy` em seu próprio painel de tmux.
- [reflect-mod](skills/github.com/bayramannakov/claude-reflect/reflect-mod.md) — mod que revisa cada prompt curto no momento da correção e oferece salvar a regra aprendida direto no `CLAUDE.md`, numa faixa acima do prompt.

**Conceitos**
- [Agent harness](concepts/agent-harness.md)
- [Memória de agente](concepts/memoria-de-agente.md)
- [Observabilidade de agentes de código](concepts/observabilidade-de-agentes.md)
- [Orquestração multiagente](concepts/orquestracao-multiagente.md)
- [Plugins de agente](concepts/plugins-de-agente.md)
- [TDD para agentes](concepts/tdd-para-agentes.md)

**Entidades**
- [affaan-m](entities/affaan-m.md)
- [Alex Newman (thedotmack)](entities/thedotmack.md)
- [Alexander Galea (zazencodes)](entities/zazencodes.md)
- [Bayram Annakov (BayramAnnakov)](entities/bayramannakov.md)
- [ByteDance](entities/bytedance.md)
- [camtrik](entities/camtrik.md)
- [Fosowl](entities/fosowl.md)
- [garrytan](entities/garrytan.md)
- [Google Research (google-research)](entities/google-research.md)
- [HarnessMD](entities/harnessmd.md)
- [hellosverre](entities/hellosverre.md)
- [Jesse Vincent (obra)](entities/obra.md)
- [Johnny (JohnnyVizz)](entities/johnnyvizz.md)
- [Open GSD (open-gsd)](entities/open-gsd.md)
- [OpenAI (openai)](entities/openai.md)
- [OpenHands](entities/openhands.md)
- [sodiumsun](entities/sodiumsun.md)
- [SynkraAI](entities/synkraai.md)
- [Trail (trailhq)](entities/trailhq.md)
- [vastsa](entities/vastsa.md)
- [Volcengine](entities/volcengine.md)

## Plataformas self-hosted de aplicações e interfaces de IA

> Produtos completos e self-hosted que dão a qualquer LLM uma interface de uso, um workflow visual de construção de agentes/RAG, ou ambos — com gestão de provedores de modelo e extensão via ferramentas e MCP.

**Repositórios**
- [langflow-ai/langflow](repos/github.com/langflow-ai/langflow.md) — builder visual de agentes/workflows de IA, com acesso ao código de cada componente e deploy como API ou servidor MCP.
- [langgenius/dify](repos/github.com/langgenius/dify.md) — plataforma de apps LLM com workflow, pipeline de RAG, agentes autônomos com sandbox, LLMOps e marketplace de ferramentas.
- [LibreChat-AI/LibreChat](repos/github.com/librechat-ai/librechat.md) — interface self-hosted que unifica todos os grandes provedores de LLM, com Agentes, Skills, MCP, Code Interpreter e Artifacts; antes `danny-avila/LibreChat`.
- [open-webui/open-webui](repos/github.com/open-webui/open-webui.md) — interface self-hosted e offline-capaz para qualquer modelo (Ollama ou API compatível com OpenAI), com RAG local, plugins, MCP e um ecossistema de apps companheiros.

**Conceitos**
- [Agent skills](concepts/agent-skills.md)
- [Builder visual de agentes e workflows de IA](concepts/builder-visual-de-agentes.md)
- [Model Context Protocol (MCP)](concepts/model-context-protocol.md)

**Entidades**
- [Langflow](entities/langflow-ai.md)
- [LangGenius](entities/langgenius.md)
- [LibreChat AI (LibreChat-AI)](entities/librechat-ai.md)
- [Open WebUI](entities/open-webui.md)

## Skills, instruções e personalidades de agente

> Formatos que moldam o comportamento do agente — `SKILL.md`, `CLAUDE.md`, personalidades e diretrizes distribuídas como artefatos versionáveis.

**Repositórios**
- [addyosmani/agent-skills](repos/github.com/addyosmani/agent-skills.md) — Pacote de 25 skills de engenharia de produção que codifica spec, plano, build, teste, revisão e lançamento como workflows com gates de verificação para agentes.
- [affaan-m/ECC](repos/github.com/affaan-m/ecc.md) — também nesta categoria pelo catálogo de 311 skills e pela migração de comandos para skills.
- [anthropics/skills](repos/github.com/anthropics/skills.md) — Implementação de referência da Anthropic: exemplos criativos/técnicos/enterprise, especificação do formato e skills de documento source-available.
- [ayghri/i-have-adhd](repos/github.com/ayghri/i-have-adhd.md) — skill de dez regras de estilo de saída direto, sem rodeios, para agentes de código.
- [cloudflare/skills](repos/github.com/cloudflare/skills.md) — 18 Agent Skills oficiais para Workers, Agents SDK, Durable Objects e Sandbox, com o servidor MCP principal da Cloudflare incluído.
- [ComposioHQ/awesome-claude-skills](repos/github.com/composiohq/awesome-claude-skills.md) — Lista curada de mais de mil skills e plugins para Claude e agentes de código, com integração própria via MCP Gateway e 78 automações SaaS.
- [davila7/claude-code-templates](repos/github.com/davila7/claude-code-templates.md) — CLI e catálogo web de mais de 100 agentes, comandos, MCPs, settings, hooks e skills reempacotados de dezenas de fontes, com analytics, monitor de conversas e dashboard de plugins próprios.
- [dietrichgebert/ponytail](repos/github.com/dietrichgebert/ponytail.md) — Skill e plugin que faz o agente escrever só o código necessário — escada YAGNI em sete degraus, revisão e auditoria de risco, testes preservados e painel de custo e tokens no Claude Code.
- [Egonex-AI/Understand-Anything](repos/github.com/egonex-ai/understand-anything.md) — Plugin e skill que transformam código, domínios de negócio ou wikis em grafo de conhecimento interativo com pipeline híbrido tree-sitter/LLM, dashboard, busca, tours e análise de impacto.
- [firecrawl/cli](repos/github.com/firecrawl/cli.md) — três famílias de skills (core, build, workflows) para busca, scrape e extração web, distribuídas por catálogo próprio e instaladas em todos os harnesses detectados.
- [github/awesome-copilot](repos/github.com/github/awesome-copilot.md) — Catálogo comunitário de agentes, instructions, skills e plugins para o GitHub Copilot, com site de busca e `llms.txt` para agentes.
- [JuliusBrussee/caveman](repos/github.com/juliusbrussee/caveman.md) — Skill e proxy que reduzem tokens de entrada e saída comprimindo a linguagem e o contexto, com roteamento de modelo, blocks reutilizáveis e compressão de logs, JSON e páginas.
- [Leonxlnx/taste-skill](repos/github.com/leonxlnx/taste-skill.md) — Família de Agent Skills anti-slop que sorteia direção de arte, usa imagens reais creditadas e inspeciona a página em navegador; a skill padrão também cobre dashboards e telas de app.
- [MadsLorentzen/ai-job-search](repos/github.com/madslorentzen/ai-job-search.md) — skills de portal de vaga com contrato padronizado e auto-descoberta, dentro de um framework de candidatura sobre Claude Code.
- [mattpocock/skills](repos/github.com/mattpocock/skills.md) — Coleção de skills pequenas e compostas para engenharia com agentes — grilling, domínio compartilhado, TDD, design de módulos e produtividade — instaláveis em Claude Code, Codex, Copilot, Gemini CLI e outros.
- [msitarzewski/agency-agents](repos/github.com/msitarzewski/agency-agents.md) — 150+ personalidades em Markdown, organizadas em 16 divisões.
- [mukul975/Anthropic-Cybersecurity-Skills](repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — também nesta categoria pela biblioteca de 818 skills de domínio.
- [multica-ai/andrej-karpathy-skills](repos/github.com/multica-ai/andrej-karpathy-skills.md) — quatro princípios de comportamento em um único `CLAUDE.md`.
- [nextlevelbuilder/ui-ux-pro-max-skill](repos/github.com/nextlevelbuilder/ui-ux-pro-max-skill.md) — Skill, motor de busca em Python e CLI que geram design systems para UI/UX a partir de catálogos de estilos, paletas, tipografia, UX e 22 stacks, com persistência em MASTER.md.
- [obra/superpowers](repos/github.com/obra/superpowers.md) — framework de skills compostas com instruções iniciais que as disparam sem comandos especiais, cobrindo design, plano, TDD e revisão.
- [OpenBMB/MiniCPM](repos/github.com/openbmb/minicpm.md) — também nesta categoria pelos cookbooks de deploy e fine-tune distribuídos como Agent Skills roteadoras.
- [pbakaus/impeccable](repos/github.com/pbakaus/impeccable.md) — skill de design com comandos e detector de regras.
- [remotion-dev/skills](repos/github.com/remotion-dev/skills.md) — doze skills oficiais do Remotion para criação, markup, render, mapas animados e legendas em projetos de vídeo programático.
- [SnailSploit/Claude-Red](repos/github.com/snailsploit/claude-red.md) — biblioteca de 78 skills de segurança ofensiva, organizada em 23 categorias e carregada por gatilho conversacional.
- [t3dotgg/tstack](repos/github.com/t3dotgg/tstack.md) — nove skills de fluxo de pull request (review multi-modelo, merge autônomo, takeover, rebase) para Claude Code e Codex.
- [tt-a1i/archify](repos/github.com/tt-a1i/archify.md) — skill de diagramas interativos em HTML.
- [usestrix/strix](repos/github.com/usestrix/strix.md) — também nesta categoria pelas nove skills (`npx skills add usestrix/strix`) que dão a qualquer agente a capacidade de rodar pentests e configurar scanning em CI.
- [vercel-labs/agent-skills](repos/github.com/vercel-labs/agent-skills.md) — oito skills oficiais da Vercel: auditoria de projeto, boas práticas React/Next.js/React Native, guidelines de design e escrita, e deploy "claimable".
- [virgiliojr94/book-to-skill](repos/github.com/virgiliojr94/book-to-skill.md) — converte um livro ou pasta de documentos em uma skill unificada com capítulos carregados sob demanda.
- [VoltAgent/awesome-claude-code-subagents](repos/github.com/voltagent/awesome-claude-code-subagents.md) — coleção curada de 161+ subagentes para Claude Code em 10 categorias, instaláveis individualmente ou como plugin por categoria.
- [zazencodes/skills](repos/github.com/zazencodes/skills.md) — catálogo versionado (MIT, changesets) de cinco skills de uso diário: geração de imagem via Codex, pesquisa web via Gemini/tmux, convenções de commit, `AGENTS.md` enxuto e números aleatórios.
- [zazencodes/zazencodes-season-3](repos/github.com/zazencodes/zazencodes-season-3.md) — a skill [Factory](skills/github.com/zazencodes/zazencodes-season-3/factory.md) orquestra sete subagentes; `cross-platform-agent-skills` é uma referência de onde cada agente procura skills; `claude-code-devtool-kanban-board` usa um hook para manter a skill do projeto sincronizada com a skill global do usuário.

**Skills**
- [Codex Image Gen](skills/github.com/zazencodes/skills/codex-image-gen.md) — gera e edita imagens via a ferramenta embutida na CLI `codex`, usando o login do ChatGPT em vez de chave de API.
- [Factory](skills/github.com/zazencodes/zazencodes-season-3/factory.md) — orquestra sete subagentes do Claude Code em um loop spec → build → revisão em quatro frentes → aprovação, com cada job em seu próprio git worktree.
- [Git Commit Conventions](skills/github.com/zazencodes/skills/git-commit-conventions.md) — um commit por lote de intenção, sem atribuição de IA, com um método de reconstrução para dividir um working tree misturado.
- [Init AGENTS.md](skills/github.com/zazencodes/skills/init-agents-md.md) — escreve um `AGENTS.md` curto e específico do repositório e sincroniza `CLAUDE.md` com ele via symlink.
- [Random Number Generator](skills/github.com/zazencodes/skills/random-number-generator.md) — inteiros, floats, escolhas ponderadas, embaralhamentos e tokens/inteiros seguros via a biblioteca padrão do Python.
- [Skill Creator](skills/github.com/anthropics/skills/skill-creator.md) — cria, testa e otimiza skills com evals, benchmark e ajuste de descrição por pontuação hold-out.

**Conceitos**
- [Agent skills](concepts/agent-skills.md)
- [CLAUDE.md](concepts/claude-md.md)
- [YAGNI para agentes](concepts/yagni-para-agentes.md)

**Entidades**
- [Addy Osmani (addyosmani)](entities/addyosmani.md)
- [affaan-m](entities/affaan-m.md)
- [Alexander Galea (zazencodes)](entities/zazencodes.md)
- [Anthropic (anthropics)](entities/anthropics.md)
- [Ayoub Ghriss (ayghri)](entities/ayghri.md)
- [Cloudflare](entities/cloudflare.md)
- [Composio (ComposioHQ)](entities/composiohq.md)
- [Daniel Avila (davila7)](entities/davila7.md)
- [DietrichGebert](entities/dietrichgebert.md)
- [Firecrawl](entities/firecrawl.md)
- [GitHub](entities/github.md)
- [Jesse Vincent (obra)](entities/obra.md)
- [Julius Brussee (juliusbrussee)](entities/juliusbrussee.md)
- [Mads Lorentzen (MadsLorentzen)](entities/madslorentzen.md)
- [Matt Pocock (mattpocock)](entities/mattpocock.md)
- [msitarzewski](entities/msitarzewski.md)
- [multica-ai](entities/multica-ai.md)
- [Remotion (remotion-dev)](entities/remotion-dev.md)
- [SnailSploit (Kai Aizen)](entities/snailsploit.md)
- [Strix (usestrix)](entities/usestrix.md)
- [Theo Browne (t3dotgg)](entities/t3dotgg.md)
- [Vercel Labs (vercel-labs)](entities/vercel-labs.md)
- [Virgilio Junior (virgiliojr94)](entities/virgiliojr94.md)
- [VoltAgent](entities/voltagent.md)

**Skills documentadas em outras categorias**
- [Agent DX CLI Scale](skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md), [Ink](skills/github.com/google-labs-code/design.md/ink.md), [TDD Red-Green-Refactor](skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md) e [Typed Service Contracts](skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — em [Engenharia e interfaces agent-first](#engenharia-e-interfaces-agent-first).
- [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) e [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — em [Geração de mídia e artefatos HTML](#geração-de-mídia-e-artefatos-html).
- [Understand](skills/github.com/egonex-ai/understand-anything/understand.md) — em [Grafos de conhecimento e contexto de código](#grafos-de-conhecimento-e-contexto-de-código).
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — em [Avaliação de UX e pesquisa](#avaliação-de-ux-e-pesquisa).
- [Gemini Web Research](skills/github.com/zazencodes/skills/gemini-web-research.md) — em [Harnesses e orquestração de agentes](#harnesses-e-orquestração-de-agentes).

## Guias, cursos e listas curadas sobre Claude Code

> Recursos que explicam, ensinam ou catalogam o ecossistema do Claude Code — guias de referência, cursos de harness engineering e listas "awesome" — em contraste com ferramentas instaláveis para uso direto do agente.

**Repositórios**
- [FlorianBruniaux/claude-code-ultimate-guide](repos/github.com/florianbruniaux/claude-code-ultimate-guide.md) — guia de referência extenso sobre arquitetura, harness, contexto, segurança e operação do Claude Code, publicado como site e servidor MCP próprio.
- [hesreallyhim/awesome-claude-code](repos/github.com/hesreallyhim/awesome-claude-code.md) — lista "awesome" canônica do ecossistema, com mais de 270 recursos anotados em 24 categorias.
- [shareAI-lab/learn-claude-code](repos/github.com/shareai-lab/learn-claude-code.md) — curso de 17 lições que reconstrói mecanismos de agent harness do zero, usando o Claude Code como estudo de caso.

**Conceitos**
- [Agent harness](concepts/agent-harness.md)
- [Model Context Protocol (MCP)](concepts/model-context-protocol.md)

**Entidades**
- [Florian Bruniaux (FlorianBruniaux)](entities/florianbruniaux.md)
- [hesreallyhim](entities/hesreallyhim.md)
- [shareAI (shareAI-lab)](entities/shareai-lab.md)

## Grafos de conhecimento e contexto de código

> Representações persistentes de código e documentos como grafos consultáveis, para responder perguntas estruturais com menos tokens do que reler arquivos.

**Repositórios**
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — servidor MCP local em C puro; 162 linguagens, Hybrid LSP e 17 ferramentas.
- [Egonex-AI/Understand-Anything](repos/github.com/egonex-ai/understand-anything.md) — Plugin e skill que transformam código, domínios de negócio ou wikis em grafo de conhecimento interativo com pipeline híbrido tree-sitter/LLM, dashboard, busca, tours e análise de impacto.
- [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) — skill e CLI que gera grafo com arestas `EXTRACTED`/`INFERRED`, sem vector store.
- [trailhq/Trail-Code](repos/github.com/trailhq/trail-code.md) — grafo de código via tree-sitter (o "graft map"), sem modelo, com camada opcional de resumos por LLM.
- [tt-a1i/archify](repos/github.com/tt-a1i/archify.md) — Skill e CLI zero-dependency que converte ideia, plano ou repositório em diagrama interativo autocontido em HTML, com dez tipos, JSON IR tipado e validação antes da entrega.

**Skills**
- [Understand](skills/github.com/egonex-ai/understand-anything/understand.md) — método em sete fases para gerar e validar um grafo de código com dashboard.

**Análises**
- [Workflow Claude Code + Graphify + Obsidian](analyses/claude-code-graphify-obsidian.md) — separa o que é verificável no exportador Graphify→Obsidian do que é alegação de terceiro sem fonte rastreável.

**Conceitos**
- [Grafo de conhecimento de código](concepts/grafo-de-conhecimento-de-codigo.md)

**Entidades**
- [DeusData](entities/deusdata.md)
- [Egonex-AI](entities/egonex-ai.md)
- [Graphify Labs](entities/graphify-labs.md)
- [Obsidian](entities/obsidian.md)
- [Trail (trailhq)](entities/trailhq.md)

## Engenharia reversa e análise de sistemas

> Investigação de binários, aplicações e tráfego para reconstruir comportamento sem código-fonte, com evidência explícita e limitações declaradas.

**Repositórios**
- [Egonex-AI/Understand-Anything](repos/github.com/egonex-ai/understand-anything.md) — Plugin e skill que transformam código, domínios de negócio ou wikis em grafo de conhecimento interativo com pipeline híbrido tree-sitter/LLM, dashboard, busca, tours e análise de impacto.
- [kalil0321/reverse-api-engineer](repos/github.com/kalil0321/reverse-api-engineer.md) — captura tráfego HTTP de qualquer site em HAR (manual ou agente autônomo) e gera clientes tipados em 10 linguagens; modos manual, agent, engineer e collector.
- [littledivy/mimic](repos/github.com/littledivy/mimic.md) — captura tráfego iOS/web e usa Claude para gerar um cliente Python a partir de sessões autenticadas.
- [morluto/rea](repos/github.com/morluto/rea.md) — CLI e servidor MCP local para análise estática e em runtime de binários, apps e firmware.

**Conceitos**
- [Engenharia reversa agêntica](concepts/engenharia-reversa-agentica.md)
- [Evidência e proveniência](concepts/evidencia-e-proveniencia.md)

**Entidades**
- [kalil0321](entities/kalil0321.md)
- [littledivy](entities/littledivy.md)
- [morluto](entities/morluto.md)

## Cibersegurança e operações de segurança

> Conhecimento e ferramentas para agentes atuarem em defesa, resposta a incidentes, threat hunting e testes ofensivos autorizados.

**Repositórios**
- [mukul975/Anthropic-Cybersecurity-Skills](repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — 818 skills em 34 domínios, mapeadas a MITRE ATT&CK, NIST CSF 2.0, ATLAS, D3FEND, AI RMF e F3.
- [SnailSploit/Claude-Red](repos/github.com/snailsploit/claude-red.md) — 78 skills exclusivamente ofensivas em 23 categorias, de SQLi a evasão de EDR, carregadas sob demanda.
- [usestrix/strix](repos/github.com/usestrix/strix.md) — agentes autônomos de pentest que exploram o alvo dinamicamente e validam achados com provas de conceito reais, com orquestração multiagente ("Graph of Agents") e nove skills instaláveis em qualquer agente.

**Conceitos**
- [Cibersegurança com agentes](concepts/ciberseguranca-com-agentes.md)

**Entidades**
- [mukul975](entities/mukul975.md)
- [SnailSploit (Kai Aizen)](entities/snailsploit.md)
- [Strix (usestrix)](entities/usestrix.md)

## Geração de mídia e artefatos HTML

> Produção de vídeo, voz, apresentações e diagramas como artefatos reproduzíveis, com pipelines declarados ou arquivos HTML autocontidos.

**Repositórios**
- [Anil-matcha/Open-Generative-AI](repos/github.com/anil-matcha/open-generative-ai.md) — estúdio self-hosted de geração de imagem/vídeo sobre 600+ modelos (Flux, Midjourney, Kling, Sora, Veo) via MuAPI, com app desktop e dois motores de inferência local.
- [calesthio/OpenMontage](repos/github.com/calesthio/openmontage.md) — produção de vídeo agêntica com pipelines YAML, skills de direção e validação sobre Remotion, HyperFrames e FFmpeg.
- [heygen-com/hyperframes](repos/github.com/heygen-com/hyperframes.md) — composição em HTML puro com timing por atributos, animação seekable e render determinístico em Chrome headless + FFmpeg; 21 skills para agentes.
- [myshell-ai/OpenVoice](repos/github.com/myshell-ai/openvoice.md) — modelo de clonagem instantânea de voz, zero-shot e cross-lingual, com controle de estilo.
- [oso95/scroll-world](repos/github.com/oso95/scroll-world.md) — landing page de voo contínuo gerada por IA (imagem + vídeo), conduzida por scroll, com motor de scrub em JS puro e HTML autocontido; fork registrado em ChecheChat/scroll-world.
- [remotion-dev/skills](repos/github.com/remotion-dev/skills.md) — skills oficiais do Remotion, framework de vídeo programático em React usado como provedor de renderização pelo OpenMontage.
- [tt-a1i/archify](repos/github.com/tt-a1i/archify.md) — Skill e CLI zero-dependency que converte ideia, plano ou repositório em diagrama interativo autocontido em HTML, com dez tipos, JSON IR tipado e validação antes da entrega.

**Skills**
- [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — sistema de design para diagramas editoriais em HTML/SVG, com gate de style guide.
- [Excalidraw Diagram](skills/github.com/coleam00/excalidraw-diagram-skill/excalidraw-diagram.md) — diagramas Excalidraw a partir de linguagem natural, com validação visual via Playwright.
- [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — apresentações HTML autocontidas em palco 16:9, com descoberta de estilo e edição inline.

**Conceitos**
- [Artefatos HTML autocontidos](concepts/artefatos-html-autocontidos.md)
- [Clonagem de voz](concepts/clonagem-de-voz.md)
- [Produção de vídeo agêntica](concepts/producao-de-video-agentica.md)

**Entidades**
- [Anil Chandra Naidu Matcha (Anil-matcha)](entities/anil-matcha.md)
- [calesthio](entities/calesthio.md)
- [cathrynlavery](entities/cathrynlavery.md)
- [Cole Medin (coleam00)](entities/coleam00.md)
- [HeyGen](entities/heygen.md)
- [MyShell (myshell-ai)](entities/myshell-ai.md)
- [oso95](entities/oso95.md)
- [Remotion (remotion-dev)](entities/remotion-dev.md)
- [tt-a1i](entities/tt-a1i.md)
- [zarazhangrui](entities/zarazhangrui.md)

## Geração de imagem e vídeo com modelos de difusão

> Modelos de base e motores de execução para gerar e editar imagem, vídeo e humanos digitais a partir de texto, imagem ou voz, localmente ou via nó visual.

**Repositórios**
- [Comfy-Org/ComfyUI](repos/github.com/comfy-org/comfyui.md) — GUI, API e backend modular de nós para modelos de difusão de imagem, vídeo, 3D e áudio, com weight streaming assíncrono para hardware de consumo.
- [duixcom/Duix-Avatar](repos/github.com/duixcom/duix-avatar.md) — ferramenta offline que combina clonagem de voz e de aparência para gerar vídeos de avatar digital com lip-sync.
- [Wan-Video/Wan2.1](repos/github.com/wan-video/wan2.1.md) — suíte aberta de modelos de geração de vídeo e imagem (texto-para-vídeo, imagem-para-vídeo, edição), Apache-2.0.

**Conceitos**
- [Geração de imagem e vídeo com modelos de difusão](concepts/geracao-de-imagem-e-video-com-difusao.md)

**Entidades**
- [Comfy Org](entities/comfy-org.md)
- [Duix](entities/duixcom.md)
- [Wan (Wan-Video)](entities/wan-video.md)

## Síntese, clonagem e transcrição de voz

> Ferramentas que sintetizam, clonam ou transcrevem voz — da clonagem zero-shot à dublagem, dictation e transcrição offline.

**Repositórios**
- [cjpais/Handy](repos/github.com/cjpais/handy.md) — app de desktop multiplataforma de transcrição de fala totalmente offline, via Whisper ou Parakeet.
- [debpalash/VoiceStudio](repos/github.com/debpalash/voicestudio.md) — alternativa open source e local ao ElevenLabs: clonagem/design de voz, dublagem de vídeo, dictation, transcrição e audiobook em 646 idiomas, com API/MCP local.
- [Open-LLM-VTuber/Open-LLM-VTuber](repos/github.com/open-llm-vtuber/open-llm-vtuber.md) — também nesta categoria por ASR/TTS extensivos (inclui GPT-SoVITS); vai além da voz com percepção visual e avatar Live2D interativo em tempo real.

**Conceitos**
- [Clonagem de voz](concepts/clonagem-de-voz.md)

**Entidades**
- [CJ Pais (cjpais)](entities/cjpais.md)
- [Open-LLM-VTuber](entities/open-llm-vtuber.md)
- [Palash Debnath (debpalash)](entities/debpalash.md)

**Repositórios documentados em outras categorias**
- [myshell-ai/OpenVoice](repos/github.com/myshell-ai/openvoice.md) — em [Geração de mídia e artefatos HTML](#geração-de-mídia-e-artefatos-html).

## Design de interface e direção de arte

> Skills que dão a agentes critério visual — regras anti-slop, direção de arte, redesign, geração de referências visuais e design systems persistentes.

**Repositórios**
- [Leonxlnx/taste-skill](repos/github.com/leonxlnx/taste-skill.md) — Família de Agent Skills anti-slop que sorteia direção de arte, usa imagens reais creditadas e inspeciona a página em navegador; a skill padrão também cobre dashboards e telas de app.
- [nextlevelbuilder/ui-ux-pro-max-skill](repos/github.com/nextlevelbuilder/ui-ux-pro-max-skill.md) — Skill, motor de busca em Python e CLI que geram design systems para UI/UX a partir de catálogos de estilos, paletas, tipografia, UX e 22 stacks, com persistência em MASTER.md.
- [pbakaus/impeccable](repos/github.com/pbakaus/impeccable.md) — Linguagem de design para agentes de código com skill de 24 comandos, iteração visual no navegador e detector determinístico de 61 regras contra vícios do frontend gerado por IA.

**Skills**
- [Brandkit](skills/github.com/leonxlnx/taste-skill/brandkit.md) — boards de identidade de marca em uma imagem, com estratégia, logo, paleta e aplicações.
- [Design Taste Frontend](skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) — run anti-slop com direção sorteada, ideia do assunto e inspeção por screenshots.
- [Design Taste Frontend v1](skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v1.md) — regras fixas da primeira geração, preservadas por compatibilidade.
- [Design Taste Frontend v2 Experimental](skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v2-experimental.md) — arquivo único com design read, dials e protocolo de redesign.
- [GPT Taste](skills/github.com/leonxlnx/taste-skill/gpt-taste.md) — sorteio determinístico, AIDA, hero de duas linhas e GSAP para GPT/Codex.
- [High-End Visual Design](skills/github.com/leonxlnx/taste-skill/high-end-visual-design.md) — estética de agência premium com variância de arquétipos e movimento elaborado.
- [Image Taste Frontend](skills/github.com/leonxlnx/taste-skill/image-taste-frontend.md) — image-to-code para Codex: gerar, analisar e implementar.
- [Image to Code](skills/github.com/leonxlnx/taste-skill/image-to-code.md) — entrada movida para `imagegen-skills`, sem conteúdo publicado na origem.
- [Imagegen Frontend Mobile](skills/github.com/leonxlnx/taste-skill/imagegen-frontend-mobile.md) — variante mobile de referências visuais, movida para `imagegen-skills`.
- [Imagegen Frontend Web](skills/github.com/leonxlnx/taste-skill/imagegen-frontend-web.md) — uma imagem horizontal por seção, com consistência de marca.
- [Impeccable](skills/github.com/pbakaus/impeccable/impeccable.md) — quatro modos de superfície, 24 comandos e verificação no navegador.
- [Industrial Brutalist UI](skills/github.com/leonxlnx/taste-skill/industrial-brutalist-ui.md) — brutalismo industrial com Swiss print ou telemetria CRT.
- [Minimalist UI](skills/github.com/leonxlnx/taste-skill/minimalist-ui.md) — minimalismo utilitário editorial com monofonia quente e pastéis.
- [Redesign Existing Projects](skills/github.com/leonxlnx/taste-skill/redesign-existing-projects.md) — auditoria e upgrades pontuais sem trocar de stack.
- [Stitch Design Taste](skills/github.com/leonxlnx/taste-skill/stitch-design-taste.md) — `DESIGN.md` semântico e anti-slop para o Google Stitch.
- [Taste Skill (alias de design-taste-frontend-v1)](skills/github.com/leonxlnx/taste-skill/taste-skill.md) — entrada de catálogo com slug próprio e conteúdo da v1.
- [UI/UX Pro Max](skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md) — base pesquisável de estilos, paletas, tipografia, UX e 22 stacks.
- [Frontend Design](skills/github.com/anthropics/skills/frontend-design.md) — direção visual deliberada em duas passagens, com plano de tokens e lista de clichês de design por IA a evitar.

**Conceitos**
- [Design system com agentes](concepts/design-system-com-agentes.md)
- [Design taste para agentes](concepts/design-taste-para-agentes.md)
- [Image-to-code](concepts/image-to-code.md)

**Entidades**
- [Anthropic (anthropics)](entities/anthropics.md)
- [Leon Lin (leonxlnx)](entities/leonxlnx.md)
- [Next Level Builder](entities/nextlevelbuilder.md)
- [Paul Bakaus (pbakaus)](entities/pbakaus.md)
- [tt-a1i](entities/tt-a1i.md)

**Skills documentadas em outras categorias**
- [Full-Output Enforcement](skills/github.com/leonxlnx/taste-skill/full-output-enforcement.md) — em [Engenharia e interfaces agent-first](#engenharia-e-interfaces-agent-first).

## Comunicação e caixas de entrada agênticas

> Ferramentas em que o agente lê, organiza e redige comunicação em nome do usuário, com isolamento de dados, confirmação de envio e fronteiras de autorização explícitas.

**Repositórios**
- [cloudflare/agentic-inbox](repos/github.com/cloudflare/agentic-inbox.md) — cliente de e-mail self-hosted em Workers, com nove ferramentas de e-mail, isolamento por mailbox e servidor MCP.
- [pizza-bot-app/pizza-bot](repos/github.com/pizza-bot-app/pizza-bot.md) — inbox local-first para trabalho de agentes de longa duração sobre DeepAgents/LangGraph, com filas Unread/Action, checkpoint e aprovações humanas.

**Conceitos**
- [Email para agentes](concepts/email-para-agentes.md)

**Entidades**
- [Cloudflare](entities/cloudflare.md)
- [Pizza Bot (pizza-bot-app)](entities/pizza-bot-app.md)

## Trabalho, projetos e colaboração humano-agente

> Ferramentas em que pessoas e agentes compartilham o mesmo fluxo de trabalho, board ou unidade de tarefa.

**Repositórios**
- [croffasia/itsaplan](repos/github.com/croffasia/itsaplan.md) — issue tracker self-hosted em que agentes de IA são membros de projeto com permissões e issues no mesmo board.
- [twentyhq/twenty](repos/github.com/twentyhq/twenty.md) — CRM open source "desenhado para IA" com objetos, views e workflows definidos como código e skills oficiais para agentes.

**Conceitos**
- [Agent skills](concepts/agent-skills.md)
- [Orquestração multiagente](concepts/orquestracao-multiagente.md)

**Entidades**
- [croffasia](entities/croffasia.md)
- [twentyhq](entities/twentyhq.md)

## Análise financeira e trading

> Decisão de investimento decomposta em papéis de analista, debate, execução e risco, com integridade temporal dos dados e memória de decisões passadas.

**Repositórios**
- [Fincept-Corporation/FinceptTerminal](repos/github.com/fincept-corporation/finceptterminal.md) — terminal desktop nativo com 37 agentes, 100+ conectores, analytics institucional, paper trading e 16 corretoras; edição aberta AGPL e Enterprise proprietária.
- [himself65/trade-skills](repos/github.com/himself65/trade-skills.md) — skill de trading de opções multi-leg com base de conhecimento OKF de 37 armadilhas e estudos de caso reais; instalação por `npx`.
- [HKUDS/Vibe-Trading](repos/github.com/hkuds/vibe-trading.md) — workspace de pesquisa financeira com 90 skills, 30 presets de swarm, backtest cross-market e execução live limitada por mandato.
- [Jakeschincariol/trader-skill](repos/github.com/jakeschincariol/trader-skill.md) — 11 skills encadeadas (SEC EDGAR 13F, rastreamento de mandatos do Congresso, dimensionamento, corretora Alpaca, risco, imposto) com confirmação explícita antes de qualquer ordem; Python stdlib, paper trading por padrão.
- [openbq-org/OpenBB](repos/github.com/openbq-org/openbb.md) — Open Data Platform que conecta fontes financeiras a Python, Excel, MCP e REST para analistas, quants e agentes de IA.
- [TauricResearch/TradingAgents](repos/github.com/tauricresearch/tradingagents.md) — firma de trading simulada em LangGraph, com quatro analistas, debate bullish/bearish, risco, gestor de portfólio, memory log e backtest.
- [The-Swarm-Corporation/AutoHedge](repos/github.com/the-swarm-corporation/autohedge.md) — pipeline Director → Quant → Risk → Execution com execução autônoma em Solana; README curto, sem backtest publicado.

**Conceitos**
- [Análise financeira multiagente](concepts/analise-financeira-multiagente.md)

**Entidades**
- [Fincept Corporation](entities/fincept-corporation.md)
- [himself65](entities/himself65.md)
- [HKUDS](entities/hkuds.md)
- [jakeschincariol](entities/jakeschincariol.md)
- [openbq-org](entities/openbq-org.md)
- [Tauric Research](entities/tauricresearch.md)
- [The Swarm Corporation](entities/the-swarm-corporation.md)

## Marketing, mídia paga e conteúdo

> Skills que operam domínios de marketing com controles explícitos: auditoria de contas de anúncios, evidência por achado e escrita gated por capacidade.

**Repositórios**
- [AgriciDaniel/claude-ads](repos/github.com/agricidaniel/claude-ads.md) — auditoria de mídia paga em 12 plataformas, com conductor + workers, quatro estados de controle, cobertura de evidência e escrita read-only por padrão.
- [every-app/open-seo](repos/github.com/every-app/open-seo.md) — stack de SEO self-hosted com servidor MCP e Agent Skills para pesquisa de palavra-chave, rastreamento de posição, backlinks e auditoria de site.

**Conceitos**
- [Auditoria de mídia paga](concepts/auditoria-de-midia-paga.md)

**Entidades**
- [Agrici Daniel (AgriciDaniel)](entities/agricidaniel.md)
- [Every App (every-app)](entities/every-app.md)

## Inferência local e runtime de modelos

> Execução de modelos de linguagem em hardware próprio, com decisões explícitas sobre onde os pesos residem e como o runtime troca capacidade por latência.

**Repositórios**
- [Anil-matcha/Open-Generative-AI](repos/github.com/anil-matcha/open-generative-ai.md) — também nesta categoria pelos dois motores de inferência local do app desktop (sd.cpp bundled; Wan2GP via instalação própria ou servidor MCP remoto) para modelos de imagem/vídeo, em vez de LLMs.
- [Comfy-Org/ComfyUI](repos/github.com/comfy-org/comfyui.md) — também nesta categoria pelo weight streaming assíncrono que roda modelos de difusão grandes com apenas 4GB de VRAM, mesmo princípio de troca memória↔latência do colibri aplicado a imagem/vídeo em vez de MoE de texto.
- [Drumih/turbo-fieldfare](repos/github.com/drumih/turbo-fieldfare.md) — runtime Swift + Metal model-specific para Gemma 4 26B-A4B no Apple Silicon: ~2 GB de RAM, core denso residente, cache LFU de 16 slots por camada e experts roteados lidos do SSD; 5–6 tok/s em 8 GB M2.
- [JustAResearcher/gpu-unlock-ada](repos/github.com/justaresearcher/gpu-unlock-ada.md) — fork do gpu-unlock que estende o desbloqueio de tensor cores a RTX 4090 e GPUs Ada Lovelace experimentais (AD102–AD107, incluindo variantes de notebook), com opt-in por chip.
- [JustVugg/colibri](repos/github.com/justvugg/colibri.md) — motor em C puro para MoE com experts transmitidos do disco, tiers opcionais de Vulkan/CUDA/Metal, servidor compatível com OpenAI/Anthropic e modo de decisão System One.
- [OpenBMB/MiniCPM](repos/github.com/openbmb/minicpm.md) — família de LLMs compactos para dispositivos, com MiniCPM5 denso, SALA híbrido para 1M+ tokens, MiniCPM4/4.1 com atenção esparsa treinável e cookbooks de deploy/fine-tune.
- [PrismML-Eng/Bonsai-demo](repos/github.com/prismml-eng/bonsai-demo.md) — demo para rodar localmente a família Bonsai 2 (2B–27B), com pesos ternários (~1,75 bit/peso), visão, tool calling e cliente MCP.
- [unslothai/unsloth](repos/github.com/unslothai/unsloth.md) — app desktop, UI web e biblioteca para treinar e rodar LLMs, diffusion, embedding e áudio localmente, com fine-tuning 2× mais rápido e 70% menos VRAM alegados pelo projeto.
- [Zagitta/gpu-unlock](repos/github.com/zagitta/gpu-unlock.md) — módulo de kernel Linux que remove o cap de metade da taxa de tensor cores em GeForce RTX 20/30/40 para FP16/BF16/TF32, elevando prefill, fine-tuning e geração de imagem/vídeo locais.

**Conceitos**
- [Atenção esparsa para contexto longo](concepts/atencao-esparsa-para-contexto-longo.md)
- [LLMs compactos on-device](concepts/llms-compactos-on-device.md)
- [Streaming de experts em MoE](concepts/streaming-de-experts-em-moe.md)

**Entidades**
- [Comfy Org](entities/comfy-org.md)
- [Drumih (Andrey Mikhaylov)](entities/drumih.md)
- [JustAResearcher (Tim)](entities/justaresearcher.md)
- [OpenBMB](entities/openbmb.md)
- [PrismML](entities/prismml.md)
- [Unsloth AI (unslothai)](entities/unslothai.md)
- [Vincenzo Fornaro (JustVugg)](entities/vincenzo-fornaro.md)
- [Zagitta (Simon)](entities/zagitta.md)
- [Z.ai (zai-org / Zhipu AI)](entities/zai-org.md) — também nesta categoria por contraste: GLM-5.3-FlashX é servido só via API (cloud), não localmente, mas aparece como modelo suportado pelo Unsloth e é citado para contexto de nomenclatura/preço.

## Modelos abertos e treinamento de LLMs

> Treinamento de modelos do zero, corpus, tokenizador, dinâmica de treino e avaliação — com reprodutibilidade e proveniência como critério de publicação.

**Repositórios**
- [Instituto-IA-LNCC/manaca-1b-base](repos/github.com/instituto-ia-lncc/manaca-1b-base.md) — modelo base de ~1,72B treinado do zero para português do Brasil, com corpus de ~20,1B tokens, tokenizador próprio, pré-treino em Megatron-LM, conversão para HuggingFace e avaliação pareada em quatro benchmarks.
- [NVIDIA-NeMo/Nemotron](repos/github.com/nvidia-nemo/nemotron.md) — hub de receitas de treinamento (pré-treino → SFT → RL) e cookbooks de uso para a família Nemotron, incluindo o Nemotron 3 Ultra (550B/55B, híbrido Mamba-Attention MoE, contexto de 1M).

**Entidades**
- [Instituto de IA do LNCC (Instituto-IA-LNCC)](entities/instituto-ia-lncc.md)
- [NVIDIA](entities/nvidia.md)

## Engenharia e interfaces agent-first

> Desenho de CLIs, contratos de serviço, ciclos de verificação e superfícies de terminal pensados para que agentes operem ferramentas com previsibilidade e segurança.

**Repositórios**
- [addyosmani/agent-skills](repos/github.com/addyosmani/agent-skills.md) — Pacote de 25 skills de engenharia de produção que codifica spec, plano, build, teste, revisão e lançamento como workflows com gates de verificação para agentes.
- [dietrichgebert/ponytail](repos/github.com/dietrichgebert/ponytail.md) — Skill e plugin que faz o agente escrever só o código necessário — escada YAGNI em sete degraus, revisão e auditoria de risco, testes preservados e painel de custo e tokens no Claude Code.
- [jo-inc/camofox-browser](repos/github.com/jo-inc/camofox-browser.md) — servidor REST de browser com snapshots de acessibilidade, refs estáveis, sessões isoladas e importação de cookies; anti-detecção declarada.
- [vercel-labs/agent-browser](repos/github.com/vercel-labs/agent-browser.md) — CLI Rust nativa que controla o Chrome via CDP sem Node.js/Playwright, com snapshots de acessibilidade estáveis e servidor MCP.
- [browser-use/browser-use](repos/github.com/browser-use/browser-use.md) — biblioteca/CLI/API open source com a classe `Agent`, modelo próprio BU2 para automação de navegador, navegador em nuvem com stealth e toolset oficial de 31 ações para o SDK da Anthropic.
- [google/artemis](repos/github.com/google/artemis.md) — automação Android via linguagem natural, com servidor MCP nativo, perfis Flash (reativo) e Pro (planejamento multiagente com verificação) e 99%+ no benchmark AndroidWorld.
- [JuliusBrussee/caveman](repos/github.com/juliusbrussee/caveman.md) — Skill e proxy que reduzem tokens de entrada e saída comprimindo a linguagem e o contexto, com roteamento de modelo, blocks reutilizáveis e compressão de logs, JSON e páginas.
- [mattpocock/skills](repos/github.com/mattpocock/skills.md) — Coleção de skills pequenas e compostas para engenharia com agentes — grilling, domínio compartilhado, TDD, design de módulos e produtividade — instaláveis em Claude Code, Codex, Copilot, Gemini CLI e outros.
- [pbakaus/impeccable](repos/github.com/pbakaus/impeccable.md) — Linguagem de design para agentes de código com skill de 24 comandos, iteração visual no navegador e detector determinístico de 61 regras contra vícios do frontend gerado por IA.
- [virgiliojr94/book-to-skill](repos/github.com/virgiliojr94/book-to-skill.md) — também nesta categoria pela economia de tokens: capítulos carregados sob demanda, 24×–51× menos tokens que despejar o livro no contexto.
- [zenbu-labs/terminal-browser](repos/github.com/zenbu-labs/terminal-browser.md) — Chromium real renderizado dentro do terminal via protocolo gráfico kitty, com CLI compatível com `agent-browser` para interação do agente.
- [zazencodes/zazencodes-season-3](repos/github.com/zazencodes/zazencodes-season-3.md) — também nesta categoria pelo demo do Jev (TypeSafe AI): decisão tipada e calibrada em uma única passada, sem geração, para roteamento e guardrails.

**Skills**
- [Agent DX CLI Scale](skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md) — escala de sete eixos para avaliar CLIs; nota de 0–21 e bônus multi-superfície.
- [Full-Output Enforcement](skills/github.com/leonxlnx/taste-skill/full-output-enforcement.md) — entrega integral, sem placeholders, com pausa explícita no limite de tokens.
- [Ink](skills/github.com/google-labs-code/design.md/ink.md) — UI de terminal a partir de specs JSON, com catálogo tipado, eventos e streaming.
- [TDD Red-Green-Refactor](skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md) — ciclo de um teste por vez como contrapressão ao código gerado.
- [Typed Service Contracts](skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — spec/handler com Zod e Result Pattern, sem exceções na fronteira.

**Conceitos**
- [CLI agent-first](concepts/cli-agent-first.md)
- [Contratos tipados de serviço](concepts/contratos-tipados-de-servico.md)
- [Decisão não generativa para agentes (System 1)](concepts/decisao-nao-generativa-para-agentes.md)
- [Economia de tokens em agentes](concepts/economia-de-tokens-em-agentes.md)
- [Navegação web agêntica](concepts/navegacao-web-agentica.md)
- [Saída completa de agente](concepts/saida-completa-de-agente.md)
- [TDD para agentes](concepts/tdd-para-agentes.md)
- [YAGNI para agentes](concepts/yagni-para-agentes.md)

**Entidades**
- [Alexander Galea (zazencodes)](entities/zazencodes.md)
- [Browser Use](entities/browser-use.md)
- [DietrichGebert](entities/dietrichgebert.md)
- [Google](entities/google.md)
- [Google Labs Code](entities/google-labs-code.md)
- [jo-inc](entities/jo-inc.md)
- [Julius Brussee (juliusbrussee)](entities/juliusbrussee.md)
- [Matt Pocock (mattpocock)](entities/mattpocock.md)
- [Vercel Labs (vercel-labs)](entities/vercel-labs.md)
- [Virgilio Junior (virgiliojr94)](entities/virgiliojr94.md)
- [zenbu-labs](entities/zenbu-labs.md)

## Protocolos, integrações e confiabilidade

> Camada que conecta agentes a ferramentas e dados, e critérios para que resultados de agentes sejam auditáveis.

**Conceitos**
- [Evidência e proveniência](concepts/evidencia-e-proveniencia.md)
- [Model Context Protocol (MCP)](concepts/model-context-protocol.md)
- [Raspagem web para agentes e LLMs](concepts/raspagem-web-para-agentes.md)

**Implementações e integrações documentadas**
- [bilawalsidhu/gods-eye-view](repos/github.com/bilawalsidhu/gods-eye-view.md) — o próprio globo ao vivo se expõe como servidor MCP, para abrir dentro de Claude Desktop, Codex ou ChatGPT desktop.
- [cloudflare/agentic-inbox](repos/github.com/cloudflare/agentic-inbox.md) — servidor MCP em `/mcp` com ferramentas de e-mail.
- [cloudflare/skills](repos/github.com/cloudflare/skills.md) — servidor MCP remoto principal da Cloudflare, empacotado com 18 Agent Skills.
- [croffasia/itsaplan](repos/github.com/croffasia/itsaplan.md) — REST API, MCP e webhooks.
- [D4Vinci/Scrapling](repos/github.com/d4vinci/scrapling.md) — servidor MCP que expõe requisições HTTP, ações de browser, screenshots e respostas de API capturadas em segundo plano.
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — servidor MCP de grafo de código.
- [every-app/open-seo](repos/github.com/every-app/open-seo.md) — servidor MCP que expõe dados de SEO como ferramentas para agentes.
- [Fincept-Corporation/FinceptTerminal](repos/github.com/fincept-corporation/finceptterminal.md) — ferramentas MCP dentro da automação do terminal.
- [firecrawl/cli](repos/github.com/firecrawl/cli.md) — servidor MCP próprio e opção de se tornar o provedor web padrão de agentes suportados.
- [google/artemis](repos/github.com/google/artemis.md) — servidor MCP nativo que conecta Antigravity, Claude Code, Codex e Windsurf a dispositivos Android reais para teste e reprodução de bugs.
- [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) — extra opcional `mcp`, além de Neo4j, FalkorDB e Postgres.
- [HKUDS/Vibe-Trading](repos/github.com/hkuds/vibe-trading.md) — 82 tools MCP expostas sem ferramentas de ordem.
- [JustVugg/colibri](repos/github.com/justvugg/colibri.md) — servidor MCP (`coli mcp`) para detectar hardware, recomendar, instalar, iniciar, parar e checar o modelo.
- [lfnovo/open-notebook](repos/github.com/lfnovo/open-notebook.md) — integração MCP do lado cliente, conectando Claude Desktop, VS Code e outros clientes MCP ao Open Notebook.
- [MODSetter/SurfSense](repos/github.com/modsetter/surfsense.md) — registro de plugins de terceiros via servidor MCP (DeepWiki, Notion, ou qualquer um por URL).
- [morluto/rea](repos/github.com/morluto/rea.md) — CLI e servidor MCP local de engenharia reversa.
- [openbq-org/OpenBB](repos/github.com/openbq-org/openbb.md) — servidores MCP citados como uma das superfícies de consumo da Open Data Platform para agentes de IA.
- [trailhq/Trail-Code](repos/github.com/trailhq/trail-code.md) — servidor MCP (`trail mcp`) com seis ferramentas de busca e navegação de código, mais os nomes antigos `graft_*`.
- [unclecode/crawl4ai](repos/github.com/unclecode/crawl4ai.md) — servidor Docker próprio com endpoint MCP, além de MCP hospedado na Crawl4AI Cloud; converte sites em Markdown pronto para LLM/RAG.
- [upstash/context7](repos/github.com/upstash/context7.md) — servidor MCP e CLI (`ctx7`) com duas ferramentas (`resolve-library-id`, `query-docs`) para documentação atual por biblioteca e versão.
- [usestrix/strix](repos/github.com/usestrix/strix.md) — conecta-se a servidores MCP próprios do usuário durante um scan, e também aceita conexões MCP de entrada.
- [vercel-labs/agent-browser](repos/github.com/vercel-labs/agent-browser.md) — servidor MCP (`agent-browser mcp`) com perfis de ferramentas selecionáveis para automação de navegador.
- [zazencodes/zazencodes-season-3](repos/github.com/zazencodes/zazencodes-season-3.md) — três servidores/apps MCP distintos: `skybridge-dataset-visualizer` (MCP app com UI), `agent-identity-introduction` (MCP + identidade delegada via Descope) e `literature-review-consensus-mcp` (skill sobre o Consensus MCP).

**Entidades**
- [Alexander Galea (zazencodes)](entities/zazencodes.md)
- [Bilawal Sidhu (bilawalsidhu)](entities/bilawalsidhu.md)
- [Cloudflare](entities/cloudflare.md)
- [croffasia](entities/croffasia.md)
- [D4Vinci](entities/d4vinci.md)
- [DeusData](entities/deusdata.md)
- [Every App (every-app)](entities/every-app.md)
- [Fincept Corporation](entities/fincept-corporation.md)
- [Firecrawl](entities/firecrawl.md)
- [Google](entities/google.md)
- [Graphify Labs](entities/graphify-labs.md)
- [HKUDS](entities/hkuds.md)
- [Luis Novo (lfnovo)](entities/lfnovo.md)
- [morluto](entities/morluto.md)
- [openbq-org](entities/openbq-org.md)
- [Rohan Verma (MODSetter)](entities/modsetter.md)
- [Strix (usestrix)](entities/usestrix.md)
- [There's An AI For That (theresanaiforthat)](entities/theresanaiforthat.md)
- [Trail (trailhq)](entities/trailhq.md)
- [UncleCode](entities/unclecode.md)
- [Upstash (upstash)](entities/upstash.md)
- [Vercel Labs (vercel-labs)](entities/vercel-labs.md)

## Avaliação de UX e pesquisa

> Avaliação estruturada de produtos contra frameworks explícitos, operacionalizada como skill reutilizável.

**Repositórios**
- [pbakaus/impeccable](repos/github.com/pbakaus/impeccable.md) — Linguagem de design para agentes de código com skill de 24 comandos, iteração visual no navegador e detector determinístico de 61 regras contra vícios do frontend gerado por IA.

**Skills**
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — auditoria ampla de UX com os frameworks de Morville, ISO e interaction design.

**Conceitos**
- [Auditoria de UX](concepts/auditoria-de-ux.md)

**Entidades**
- [mastepanoski](entities/mastepanoski.md)

## Escrita e comunicação

> Edição de prosa assistida por agentes: remover maneirismos de escrita gerada por IA, preservar a voz do autor e revisar texto factual sem alterar afirmações.

**Repositórios**
- [petergyang/no-ai-slop](repos/github.com/petergyang/no-ai-slop.md) — mais de 20 padrões de slop, com comando de edição, comando de detecção (só cita, sem veredito de autoria) e modo satírico.

**Skills**
- [Humanizer](skills/github.com/blader/humanizer/humanizer.md) — catálogo de 26 padrões de escrita por IA em seis famílias, com fluxo de quatro etapas e três modos de saída.
- [Stop Slop](skills/github.com/hardikpandya/stop-slop/stop-slop.md) — oito regras centrais, lista de checagens e nota de 1–10 em cinco dimensões.

**Conceitos**
- [Humanização de texto gerado por IA](concepts/humanizacao-de-texto-por-ia.md)

**Entidades**
- [blader](entities/blader.md)
- [hardikpandya](entities/hardikpandya.md)
- [Peter Yang (petergyang)](entities/petergyang.md)

## Conhecimento pessoal e curadoria

> Padrões para acumular fontes e sínteses de forma persistente — wikis mantidas por LLM, indexação, proveniência e manutenção — em contraste com a recuperação de trechos a cada consulta.

**Análises**
- [Workflow Claude Code + Graphify + Obsidian](analyses/claude-code-graphify-obsidian.md) — grafo de conhecimento exportado para um vault pessoal, com arquitetura de três camadas (fontes, conhecimento gerado, conhecimento curado).

**Conceitos**
- [Wiki pessoal com LLMs](concepts/wiki-pessoal-com-llms.md)

**Entidades**
- [Andrej Karpathy (karpathy)](entities/andrej-karpathy.md)
- [Obsidian](entities/obsidian.md)

## Pesquisa e notas pessoais com IA

> Alternativas self-hosted ou air-gapped ao Notebook LM: organizam documentos do próprio usuário, respondem com citação de fonte e, em alguns casos, editam os arquivos originais — com o índice e os dados sob controle do usuário, não de um provedor fechado.

**Repositórios**
- [lfnovo/open-notebook](repos/github.com/lfnovo/open-notebook.md) — self-hosted via Docker, com mais de 20 provedores de modelo, busca full-text/vetorial e geração de podcast multi-falante.
- [MODSetter/SurfSense](repos/github.com/modsetter/surfsense.md) — app desktop air-gapped que não só pesquisa, mas edita os documentos do usuário (PDF, Word, Excel, PowerPoint), sempre em uma cópia nova.

**Entidades**
- [Luis Novo (lfnovo)](entities/lfnovo.md)
- [Rohan Verma (MODSetter)](entities/modsetter.md)

## Pesquisa social e monitoramento de tendências

> Agentes que buscam em paralelo múltiplas plataformas sociais e de dados (Reddit, X, YouTube, TikTok, Polymarket, GitHub...) e sintetizam um brief ranqueado por engajamento real das pessoas, não por SEO ou curadoria editorial.

**Repositórios**
- [mvanhorn/last30days-skill](repos/github.com/mvanhorn/last30days-skill.md) — skill `/last30days`: ~28 fontes buscadas em paralelo, clusterizadas e sintetizadas em um brief citado por fonte; modo de descoberta sem tópico; MIT.

**Entidades**
- [Matt Van Horn (mvanhorn)](entities/mvanhorn.md)

## OSINT geoespacial e agentes de voz

> Aplicações que agregam sinais públicos (voo, navios, satélites, câmeras, clima) em uma visualização única, operadas por um agente de voz em tempo real como interface principal.

**Repositórios**
- [bilawalsidhu/gods-eye-view](repos/github.com/bilawalsidhu/gods-eye-view.md) — globo 3D ao vivo com 20 camadas de dados públicos e agente de voz em tempo real (OpenAI Realtime API) com 30 ferramentas de câmera, anotação, consulta e operação do console.

**Entidades**
- [Bilawal Sidhu (bilawalsidhu)](entities/bilawalsidhu.md)

## Navegação e meta

- [index.md](index.md) — catálogo canônico por tipo de página.
- [overview.md](overview.md) — síntese em evolução do ecossistema.
- [log.md](log.md) — histórico append-only de operações.

## Manutenção

- Ao criar, renomear ou atualizar uma página, inclua-a na categoria adequada ou ajuste a entrada existente.
- Páginas transversais podem ser listadas em mais de uma categoria; não crie páginas duplicadas para isso.
- Se nenhuma categoria servir, crie uma nova com título claro e uma frase de escopo, e registre a mudança em [`log.md`](log.md).
- Remova a entrada quando a página for removida ou renomeada.
- **Passo obrigatório:** toda vez que este arquivo sofrer qualquer alteração — categoria criada, renomeada, removida ou reordenada — atualize o [Sumário](#sumário) no topo da página no mesmo commit, para que ele continue listando exatamente os títulos de primeiro nível (`##`) da página, na mesma ordem em que aparecem.

## Fontes

- Páginas da própria wiki: [index.md](index.md), [overview.md](overview.md) e [log.md](log.md), consultadas em 2026-10-19.
