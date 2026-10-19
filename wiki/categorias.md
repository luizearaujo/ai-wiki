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
- [Fosowl/agenticSeek](repos/github.com/fosowl/agenticseek.md) — assistente local com seleção automática entre agentes de navegação web, código e planejamento, sem depender de nuvem.
- [garrytan/gstack](repos/github.com/garrytan/gstack.md) — 23 especialistas e oito power tools no ciclo Think → Plan → Build → Review → Test → Ship → Reflect.
- [HarnessMD/munder-difflin](repos/github.com/harnessmd/munder-difflin.md) — app desktop que orquestra 12 CLIs em um escritório virtual, com hive de memória e gates humanos.
- [SynkraAI/aiox-core](repos/github.com/synkraai/aiox-core.md) — framework CLI-first com 12 agentes e fluxo PRD → histórias → execução.
- [vastsa/PI-Desktop](repos/github.com/vastsa/pi-desktop.md) — workspace desktop sobre o runtime `pi`, com sessões persistentes, subagentes, Worker Sessions, permissões e plugins `.piplug`.

**Conceitos**
- [Agent harness](concepts/agent-harness.md)
- [Memória de agente](concepts/memoria-de-agente.md)
- [Orquestração multiagente](concepts/orquestracao-multiagente.md)
- [Plugins de agente](concepts/plugins-de-agente.md)

**Entidades**
- [affaan-m](entities/affaan-m.md)
- [ByteDance](entities/bytedance.md)
- [Fosowl](entities/fosowl.md)
- [garrytan](entities/garrytan.md)
- [HarnessMD](entities/harnessmd.md)
- [SynkraAI](entities/synkraai.md)
- [vastsa](entities/vastsa.md)

## Skills, instruções e personalidades de agente

> Formatos que moldam o comportamento do agente — `SKILL.md`, `CLAUDE.md`, personalidades e diretrizes distribuídas como artefatos versionáveis.

**Repositórios**
- [addyosmani/agent-skills](repos/github.com/addyosmani/agent-skills.md) — Pacote de 25 skills de engenharia de produção que codifica spec, plano, build, teste, revisão e lançamento como workflows com gates de verificação para agentes.
- [affaan-m/ECC](repos/github.com/affaan-m/ecc.md) — também nesta categoria pelo catálogo de 311 skills e pela migração de comandos para skills.
- [anthropics/skills](repos/github.com/anthropics/skills.md) — Implementação de referência da Anthropic: exemplos criativos/técnicos/enterprise, especificação do formato e skills de documento source-available.
- [cloudflare/skills](repos/github.com/cloudflare/skills.md) — 18 Agent Skills oficiais para Workers, Agents SDK, Durable Objects e Sandbox, com o servidor MCP principal da Cloudflare incluído.
- [ComposioHQ/awesome-claude-skills](repos/github.com/composiohq/awesome-claude-skills.md) — Lista curada de mais de mil skills e plugins para Claude e agentes de código, com integração própria via MCP Gateway e 78 automações SaaS.
- [dietrichgebert/ponytail](repos/github.com/dietrichgebert/ponytail.md) — Skill e plugin que faz o agente escrever só o código necessário — escada YAGNI em sete degraus, revisão e auditoria de risco, testes preservados e painel de custo e tokens no Claude Code.
- [Egonex-AI/Understand-Anything](repos/github.com/egonex-ai/understand-anything.md) — Plugin e skill que transformam código, domínios de negócio ou wikis em grafo de conhecimento interativo com pipeline híbrido tree-sitter/LLM, dashboard, busca, tours e análise de impacto.
- [firecrawl/cli](repos/github.com/firecrawl/cli.md) — três famílias de skills (core, build, workflows) para busca, scrape e extração web, distribuídas por catálogo próprio e instaladas em todos os harnesses detectados.
- [github/awesome-copilot](repos/github.com/github/awesome-copilot.md) — Catálogo comunitário de agentes, instructions, skills e plugins para o GitHub Copilot, com site de busca e `llms.txt` para agentes.
- [JuliusBrussee/caveman](repos/github.com/juliusbrussee/caveman.md) — Skill e proxy que reduzem tokens de entrada e saída comprimindo a linguagem e o contexto, com roteamento de modelo, blocks reutilizáveis e compressão de logs, JSON e páginas.
- [Leonxlnx/taste-skill](repos/github.com/leonxlnx/taste-skill.md) — Família de Agent Skills anti-slop que sorteia direção de arte, usa imagens reais creditadas e inspeciona a página em navegador; a skill padrão também cobre dashboards e telas de app.
- [mattpocock/skills](repos/github.com/mattpocock/skills.md) — Coleção de skills pequenas e compostas para engenharia com agentes — grilling, domínio compartilhado, TDD, design de módulos e produtividade — instaláveis em Claude Code, Codex, Copilot, Gemini CLI e outros.
- [msitarzewski/agency-agents](repos/github.com/msitarzewski/agency-agents.md) — 150+ personalidades em Markdown, organizadas em 16 divisões.
- [mukul975/Anthropic-Cybersecurity-Skills](repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — também nesta categoria pela biblioteca de 818 skills de domínio.
- [multica-ai/andrej-karpathy-skills](repos/github.com/multica-ai/andrej-karpathy-skills.md) — quatro princípios de comportamento em um único `CLAUDE.md`.
- [nextlevelbuilder/ui-ux-pro-max-skill](repos/github.com/nextlevelbuilder/ui-ux-pro-max-skill.md) — Skill, motor de busca em Python e CLI que geram design systems para UI/UX a partir de catálogos de estilos, paletas, tipografia, UX e 22 stacks, com persistência em MASTER.md.
- [OpenBMB/MiniCPM](repos/github.com/openbmb/minicpm.md) — também nesta categoria pelos cookbooks de deploy e fine-tune distribuídos como Agent Skills roteadoras.
- [pbakaus/impeccable](repos/github.com/pbakaus/impeccable.md) — skill de design com comandos e detector de regras.
- [remotion-dev/skills](repos/github.com/remotion-dev/skills.md) — doze skills oficiais do Remotion para criação, markup, render, mapas animados e legendas em projetos de vídeo programático.
- [tt-a1i/archify](repos/github.com/tt-a1i/archify.md) — skill de diagramas interativos em HTML.
- [vercel-labs/agent-skills](repos/github.com/vercel-labs/agent-skills.md) — oito skills oficiais da Vercel: auditoria de projeto, boas práticas React/Next.js/React Native, guidelines de design e escrita, e deploy "claimable".

**Conceitos**
- [Agent skills](concepts/agent-skills.md)
- [CLAUDE.md](concepts/claude-md.md)
- [YAGNI para agentes](concepts/yagni-para-agentes.md)

**Entidades**
- [Addy Osmani (addyosmani)](entities/addyosmani.md)
- [affaan-m](entities/affaan-m.md)
- [Anthropic (anthropics)](entities/anthropics.md)
- [Cloudflare](entities/cloudflare.md)
- [Composio (ComposioHQ)](entities/composiohq.md)
- [DietrichGebert](entities/dietrichgebert.md)
- [Firecrawl](entities/firecrawl.md)
- [GitHub](entities/github.md)
- [Julius Brussee (juliusbrussee)](entities/juliusbrussee.md)
- [Matt Pocock (mattpocock)](entities/mattpocock.md)
- [msitarzewski](entities/msitarzewski.md)
- [multica-ai](entities/multica-ai.md)
- [Remotion (remotion-dev)](entities/remotion-dev.md)
- [Vercel Labs (vercel-labs)](entities/vercel-labs.md)

**Skills documentadas em outras categorias**
- [Agent DX CLI Scale](skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md), [Ink](skills/github.com/google-labs-code/design.md/ink.md), [TDD Red-Green-Refactor](skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md) e [Typed Service Contracts](skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — em [Engenharia e interfaces agent-first](#engenharia-e-interfaces-agent-first).
- [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) e [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — em [Geração de mídia e artefatos HTML](#geração-de-mídia-e-artefatos-html).
- [Understand](skills/github.com/egonex-ai/understand-anything/understand.md) — em [Grafos de conhecimento e contexto de código](#grafos-de-conhecimento-e-contexto-de-código).
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — em [Avaliação de UX e pesquisa](#avaliação-de-ux-e-pesquisa).

## Grafos de conhecimento e contexto de código

> Representações persistentes de código e documentos como grafos consultáveis, para responder perguntas estruturais com menos tokens do que reler arquivos.

**Repositórios**
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — servidor MCP local em C puro; 162 linguagens, Hybrid LSP e 17 ferramentas.
- [Egonex-AI/Understand-Anything](repos/github.com/egonex-ai/understand-anything.md) — Plugin e skill que transformam código, domínios de negócio ou wikis em grafo de conhecimento interativo com pipeline híbrido tree-sitter/LLM, dashboard, busca, tours e análise de impacto.
- [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) — skill e CLI que gera grafo com arestas `EXTRACTED`/`INFERRED`, sem vector store.
- [tt-a1i/archify](repos/github.com/tt-a1i/archify.md) — Skill e CLI zero-dependency que converte ideia, plano ou repositório em diagrama interativo autocontido em HTML, com dez tipos, JSON IR tipado e validação antes da entrega.

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
- [Egonex-AI/Understand-Anything](repos/github.com/egonex-ai/understand-anything.md) — Plugin e skill que transformam código, domínios de negócio ou wikis em grafo de conhecimento interativo com pipeline híbrido tree-sitter/LLM, dashboard, busca, tours e análise de impacto.
- [littledivy/mimic](repos/github.com/littledivy/mimic.md) — captura tráfego iOS/web e usa Claude para gerar um cliente Python a partir de sessões autenticadas.
- [morluto/rea](repos/github.com/morluto/rea.md) — CLI e servidor MCP local para análise estática e em runtime de binários, apps e firmware.

**Conceitos**
- [Engenharia reversa agêntica](concepts/engenharia-reversa-agentica.md)
- [Evidência e proveniência](concepts/evidencia-e-proveniencia.md)

**Entidades**
- [littledivy](entities/littledivy.md)
- [morluto](entities/morluto.md)

## Cibersegurança e operações de segurança

> Conhecimento e ferramentas para agentes atuarem em defesa, resposta a incidentes, threat hunting e testes ofensivos autorizados.

**Repositórios**
- [mukul975/Anthropic-Cybersecurity-Skills](repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — 818 skills em 34 domínios, mapeadas a MITRE ATT&CK, NIST CSF 2.0, ATLAS, D3FEND, AI RMF e F3.

**Conceitos**
- [Cibersegurança com agentes](concepts/ciberseguranca-com-agentes.md)

**Entidades**
- [mukul975](entities/mukul975.md)

## Geração de mídia e artefatos HTML

> Produção de vídeo, voz, apresentações e diagramas como artefatos reproduzíveis, com pipelines declarados ou arquivos HTML autocontidos.

**Repositórios**
- [calesthio/OpenMontage](repos/github.com/calesthio/openmontage.md) — produção de vídeo agêntica com pipelines YAML, skills de direção e validação sobre Remotion, HyperFrames e FFmpeg.
- [heygen-com/hyperframes](repos/github.com/heygen-com/hyperframes.md) — composição em HTML puro com timing por atributos, animação seekable e render determinístico em Chrome headless + FFmpeg; 21 skills para agentes.
- [myshell-ai/OpenVoice](repos/github.com/myshell-ai/openvoice.md) — modelo de clonagem instantânea de voz, zero-shot e cross-lingual, com controle de estilo.
- [remotion-dev/skills](repos/github.com/remotion-dev/skills.md) — skills oficiais do Remotion, framework de vídeo programático em React usado como provedor de renderização pelo OpenMontage.
- [tt-a1i/archify](repos/github.com/tt-a1i/archify.md) — Skill e CLI zero-dependency que converte ideia, plano ou repositório em diagrama interativo autocontido em HTML, com dez tipos, JSON IR tipado e validação antes da entrega.

**Skills**
- [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — sistema de design para diagramas editoriais em HTML/SVG, com gate de style guide.
- [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — apresentações HTML autocontidas em palco 16:9, com descoberta de estilo e edição inline.

**Conceitos**
- [Artefatos HTML autocontidos](concepts/artefatos-html-autocontidos.md)
- [Clonagem de voz](concepts/clonagem-de-voz.md)
- [Produção de vídeo agêntica](concepts/producao-de-video-agentica.md)

**Entidades**
- [calesthio](entities/calesthio.md)
- [cathrynlavery](entities/cathrynlavery.md)
- [HeyGen](entities/heygen.md)
- [MyShell (myshell-ai)](entities/myshell-ai.md)
- [Remotion (remotion-dev)](entities/remotion-dev.md)
- [tt-a1i](entities/tt-a1i.md)
- [zarazhangrui](entities/zarazhangrui.md)

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

**Conceitos**
- [Design system com agentes](concepts/design-system-com-agentes.md)
- [Design taste para agentes](concepts/design-taste-para-agentes.md)
- [Image-to-code](concepts/image-to-code.md)

**Entidades**
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

**Conceitos**
- [Email para agentes](concepts/email-para-agentes.md)

**Entidades**
- [Cloudflare](entities/cloudflare.md)

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
- [HKUDS/Vibe-Trading](repos/github.com/hkuds/vibe-trading.md) — workspace de pesquisa financeira com 90 skills, 30 presets de swarm, backtest cross-market e execução live limitada por mandato.
- [openbq-org/OpenBB](repos/github.com/openbq-org/openbb.md) — Open Data Platform que conecta fontes financeiras a Python, Excel, MCP e REST para analistas, quants e agentes de IA.
- [TauricResearch/TradingAgents](repos/github.com/tauricresearch/tradingagents.md) — firma de trading simulada em LangGraph, com quatro analistas, debate bullish/bearish, risco, gestor de portfólio, memory log e backtest.
- [The-Swarm-Corporation/AutoHedge](repos/github.com/the-swarm-corporation/autohedge.md) — pipeline Director → Quant → Risk → Execution com execução autônoma em Solana; README curto, sem backtest publicado.

**Conceitos**
- [Análise financeira multiagente](concepts/analise-financeira-multiagente.md)

**Entidades**
- [Fincept Corporation](entities/fincept-corporation.md)
- [HKUDS](entities/hkuds.md)
- [openbq-org](entities/openbq-org.md)
- [Tauric Research](entities/tauricresearch.md)
- [The Swarm Corporation](entities/the-swarm-corporation.md)

## Marketing, mídia paga e conteúdo

> Skills que operam domínios de marketing com controles explícitos: auditoria de contas de anúncios, evidência por achado e escrita gated por capacidade.

**Repositórios**
- [AgriciDaniel/claude-ads](repos/github.com/agricidaniel/claude-ads.md) — auditoria de mídia paga em 12 plataformas, com conductor + workers, quatro estados de controle, cobertura de evidência e escrita read-only por padrão.

**Conceitos**
- [Auditoria de mídia paga](concepts/auditoria-de-midia-paga.md)

**Entidades**
- [Agrici Daniel (AgriciDaniel)](entities/agricidaniel.md)

## Inferência local e runtime de modelos

> Execução de modelos de linguagem em hardware próprio, com decisões explícitas sobre onde os pesos residem e como o runtime troca capacidade por latência.

**Repositórios**
- [JustVugg/colibri](repos/github.com/justvugg/colibri.md) — motor em C puro para MoE com experts transmitidos do disco, tiers opcionais de Vulkan/CUDA/Metal, servidor compatível com OpenAI/Anthropic e modo de decisão System One.
- [OpenBMB/MiniCPM](repos/github.com/openbmb/minicpm.md) — família de LLMs compactos para dispositivos, com MiniCPM5 denso, SALA híbrido para 1M+ tokens, MiniCPM4/4.1 com atenção esparsa treinável e cookbooks de deploy/fine-tune.

**Conceitos**
- [Atenção esparsa para contexto longo](concepts/atencao-esparsa-para-contexto-longo.md)
- [LLMs compactos on-device](concepts/llms-compactos-on-device.md)
- [Streaming de experts em MoE](concepts/streaming-de-experts-em-moe.md)

**Entidades**
- [OpenBMB](entities/openbmb.md)
- [Vincenzo Fornaro (JustVugg)](entities/vincenzo-fornaro.md)

## Modelos abertos e treinamento de LLMs

> Treinamento de modelos do zero, corpus, tokenizador, dinâmica de treino e avaliação — com reprodutibilidade e proveniência como critério de publicação.

**Repositórios**
- [Instituto-IA-LNCC/manaca-1b-base](repos/github.com/instituto-ia-lncc/manaca-1b-base.md) — modelo base de ~1,72B treinado do zero para português do Brasil, com corpus de ~20,1B tokens, tokenizador próprio, pré-treino em Megatron-LM, conversão para HuggingFace e avaliação pareada em quatro benchmarks.

**Entidades**
- [Instituto de IA do LNCC (Instituto-IA-LNCC)](entities/instituto-ia-lncc.md)

## Engenharia e interfaces agent-first

> Desenho de CLIs, contratos de serviço, ciclos de verificação e superfícies de terminal pensados para que agentes operem ferramentas com previsibilidade e segurança.

**Repositórios**
- [addyosmani/agent-skills](repos/github.com/addyosmani/agent-skills.md) — Pacote de 25 skills de engenharia de produção que codifica spec, plano, build, teste, revisão e lançamento como workflows com gates de verificação para agentes.
- [dietrichgebert/ponytail](repos/github.com/dietrichgebert/ponytail.md) — Skill e plugin que faz o agente escrever só o código necessário — escada YAGNI em sete degraus, revisão e auditoria de risco, testes preservados e painel de custo e tokens no Claude Code.
- [jo-inc/camofox-browser](repos/github.com/jo-inc/camofox-browser.md) — servidor REST de browser com snapshots de acessibilidade, refs estáveis, sessões isoladas e importação de cookies; anti-detecção declarada.
- [JuliusBrussee/caveman](repos/github.com/juliusbrussee/caveman.md) — Skill e proxy que reduzem tokens de entrada e saída comprimindo a linguagem e o contexto, com roteamento de modelo, blocks reutilizáveis e compressão de logs, JSON e páginas.
- [mattpocock/skills](repos/github.com/mattpocock/skills.md) — Coleção de skills pequenas e compostas para engenharia com agentes — grilling, domínio compartilhado, TDD, design de módulos e produtividade — instaláveis em Claude Code, Codex, Copilot, Gemini CLI e outros.
- [pbakaus/impeccable](repos/github.com/pbakaus/impeccable.md) — Linguagem de design para agentes de código com skill de 24 comandos, iteração visual no navegador e detector determinístico de 61 regras contra vícios do frontend gerado por IA.

**Skills**
- [Agent DX CLI Scale](skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md) — escala de sete eixos para avaliar CLIs; nota de 0–21 e bônus multi-superfície.
- [Full-Output Enforcement](skills/github.com/leonxlnx/taste-skill/full-output-enforcement.md) — entrega integral, sem placeholders, com pausa explícita no limite de tokens.
- [Ink](skills/github.com/google-labs-code/design.md/ink.md) — UI de terminal a partir de specs JSON, com catálogo tipado, eventos e streaming.
- [TDD Red-Green-Refactor](skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md) — ciclo de um teste por vez como contrapressão ao código gerado.
- [Typed Service Contracts](skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — spec/handler com Zod e Result Pattern, sem exceções na fronteira.

**Conceitos**
- [CLI agent-first](concepts/cli-agent-first.md)
- [Contratos tipados de serviço](concepts/contratos-tipados-de-servico.md)
- [Economia de tokens em agentes](concepts/economia-de-tokens-em-agentes.md)
- [Navegação web agêntica](concepts/navegacao-web-agentica.md)
- [Saída completa de agente](concepts/saida-completa-de-agente.md)
- [TDD para agentes](concepts/tdd-para-agentes.md)
- [YAGNI para agentes](concepts/yagni-para-agentes.md)

**Entidades**
- [DietrichGebert](entities/dietrichgebert.md)
- [Google Labs Code](entities/google-labs-code.md)
- [jo-inc](entities/jo-inc.md)
- [Julius Brussee (juliusbrussee)](entities/juliusbrussee.md)
- [Matt Pocock (mattpocock)](entities/mattpocock.md)

## Protocolos, integrações e confiabilidade

> Camada que conecta agentes a ferramentas e dados, e critérios para que resultados de agentes sejam auditáveis.

**Conceitos**
- [Evidência e proveniência](concepts/evidencia-e-proveniencia.md)
- [Model Context Protocol (MCP)](concepts/model-context-protocol.md)

**Implementações e integrações documentadas**
- [cloudflare/agentic-inbox](repos/github.com/cloudflare/agentic-inbox.md) — servidor MCP em `/mcp` com ferramentas de e-mail.
- [cloudflare/skills](repos/github.com/cloudflare/skills.md) — servidor MCP remoto principal da Cloudflare, empacotado com 18 Agent Skills.
- [croffasia/itsaplan](repos/github.com/croffasia/itsaplan.md) — REST API, MCP e webhooks.
- [D4Vinci/Scrapling](repos/github.com/d4vinci/scrapling.md) — servidor MCP que expõe requisições HTTP, ações de browser, screenshots e respostas de API capturadas em segundo plano.
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — servidor MCP de grafo de código.
- [Fincept-Corporation/FinceptTerminal](repos/github.com/fincept-corporation/finceptterminal.md) — ferramentas MCP dentro da automação do terminal.
- [firecrawl/cli](repos/github.com/firecrawl/cli.md) — servidor MCP próprio e opção de se tornar o provedor web padrão de agentes suportados.
- [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) — extra opcional `mcp`, além de Neo4j, FalkorDB e Postgres.
- [HKUDS/Vibe-Trading](repos/github.com/hkuds/vibe-trading.md) — 81 tools MCP expostas sem ferramentas de ordem.
- [JustVugg/colibri](repos/github.com/justvugg/colibri.md) — servidor MCP (`coli mcp`) para detectar hardware, recomendar, instalar, iniciar, parar e checar o modelo.
- [morluto/rea](repos/github.com/morluto/rea.md) — CLI e servidor MCP local de engenharia reversa.
- [openbq-org/OpenBB](repos/github.com/openbq-org/openbb.md) — servidores MCP citados como uma das superfícies de consumo da Open Data Platform para agentes de IA.

**Entidades**
- [Cloudflare](entities/cloudflare.md)
- [croffasia](entities/croffasia.md)
- [D4Vinci](entities/d4vinci.md)
- [DeusData](entities/deusdata.md)
- [Fincept Corporation](entities/fincept-corporation.md)
- [Firecrawl](entities/firecrawl.md)
- [Graphify Labs](entities/graphify-labs.md)
- [HKUDS](entities/hkuds.md)
- [morluto](entities/morluto.md)
- [openbq-org](entities/openbq-org.md)

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

**Skills**
- [Humanizer](skills/github.com/blader/humanizer/humanizer.md) — catálogo de 26 padrões de escrita por IA em seis famílias, com fluxo de quatro etapas e três modos de saída.
- [Stop Slop](skills/github.com/hardikpandya/stop-slop/stop-slop.md) — oito regras centrais, lista de checagens e nota de 1–10 em cinco dimensões.

**Conceitos**
- [Humanização de texto gerado por IA](concepts/humanizacao-de-texto-por-ia.md)

**Entidades**
- [blader](entities/blader.md)
- [hardikpandya](entities/hardikpandya.md)

## Conhecimento pessoal e curadoria

> Padrões para acumular fontes e sínteses de forma persistente — wikis mantidas por LLM, indexação, proveniência e manutenção — em contraste com a recuperação de trechos a cada consulta.

**Conceitos**
- [Wiki pessoal com LLMs](concepts/wiki-pessoal-com-llms.md)

**Entidades**
- [Andrej Karpathy (karpathy)](entities/andrej-karpathy.md)

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
