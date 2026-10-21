---
type: concept
aliases: [MCP, Model Context Protocol]
status: stable
created: 2026-10-17
updated: 2026-10-21
tags: [protocolo, agentes, ferramentas]
---

# Model Context Protocol (MCP)

> Protocolo aberto que padroniza como aplicações de LLM descobrem e chamam ferramentas, recursos e prompts expostos por servidores externos.

## Definição

O Model Context Protocol (MCP) é um protocolo cliente-servidor, baseado em JSON-RPC, que separa o **agente/host** das **capacidades** que ele pode usar. Um servidor MCP expõe primitivas como *tools* (ações), *resources* (dados legíveis) e *prompts* (instruções reutilizáveis); um cliente MCP as descobre e as coloca à disposição do modelo.

O transporte pode ser local (stdio, com o servidor rodando como subprocesso do cliente) ou remoto (HTTP). A proposta é evitar integrações bespoke para cada combinação de agente e ferramenta: a mesma ferramenta pode ser usada por Claude Code, Codex, Cursor, Gemini CLI e outros clientes.

## Como funciona

1. O cliente inicia ou conecta a um servidor MCP.
2. O cliente descobre as tools disponíveis, incluindo nomes, descrições e schemas de entrada/saída.
3. O modelo escolhe uma tool e o cliente envia a chamada.
4. O servidor executa a ação — localmente ou em um serviço remoto — e devolve um resultado estruturado.
5. O resultado entra no contexto do modelo; o agente decide o próximo passo.

Duas consequências práticas: (a) o catálogo de tools consome contexto, e catálogos grandes podem custar caro; (b) o servidor executa ações com as permissões do processo, então registro, aprovação e isolamento importam.

## Onde aparece

- [morluto/rea](../repos/github.com/morluto/rea.md) — o REA é um servidor MCP local (`src/main.ts` + `src/server/`) que expõe workflows de engenharia reversa a agentes. A CLI usa a mesma camada de aplicação, e o setup registra o servidor nos clientes com backup e aprovação.
- O projeto depende de `@modelcontextprotocol/client` e `@modelcontextprotocol/server` (`package.json`) e documenta contratos de tools, resultados e sessões em `docs/mcp-contracts.md`.
- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — o Memory Vault expõe opcionalmente `ecc-memory-mcp` com quatro ferramentas (`memory_save`, `memory_search`, `memory_read`, `memory_doctor`), identidade de harness fixa e escopo de usuário protegido por opt-in.
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — `/setup-gbrain` pode registrar o GBrain como servidor MCP (`gbrain serve`) para expor busca, escrita e leitura de conhecimento como tools tipadas.
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — o recurso Capabilities lista MCP servers, skills, plugins e ferramentas que podem ser instalados no harness, com estado de revisão por entrada.
- [upstash/context7](../repos/github.com/upstash/context7.md) — servidor MCP com duas ferramentas (`resolve-library-id`, `query-docs`) para documentação atual por biblioteca e versão, alternativa a uma CLI com skill própria.
- [vercel-labs/agent-browser](../repos/github.com/vercel-labs/agent-browser.md) — servidor MCP (`agent-browser mcp`) com perfis de ferramentas selecionáveis para automação de navegador.
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — o Capability Center cataloga MCP servers e plugins; o README alerta que ser **admin do Gateway equivale a execução de código**, porque servidores MCP stdio rodam comandos no contêiner.
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — instalação opcional do extra `mcp`, ao lado de Neo4j, FalkorDB e Postgres; as tools expostas não são detalhadas no README (**A verificar**).
- [D4Vinci/Scrapling](../repos/github.com/d4vinci/scrapling.md) — servidor MCP (extra `pip install "scrapling[ai]"`) expõe requisições HTTP, ações de browser, screenshots, estado de login salvo e respostas de API capturadas em segundo plano; reduz o conteúdo enviado ao modelo e inclui bloqueio de anúncios e de prompt injection, segundo o README.
- [openbq-org/OpenBB](../repos/github.com/openbq-org/openbb.md) — servidores MCP citados como uma das superfícies de consumo da Open Data Platform para agentes de IA, ao lado de Python, Excel e REST; o README não detalha as tools expostas (**A verificar**).
- [cloudflare/skills](../repos/github.com/cloudflare/skills.md) — empacota o servidor MCP remoto principal da Cloudflare (acesso à API e à documentação via Code Mode MCP) junto com 18 Agent Skills; servidores específicos por produto ficam fora do pacote.
- [firecrawl/cli](../repos/github.com/firecrawl/cli.md) — `firecrawl setup mcp` instala o servidor MCP do Firecrawl em Cursor, Claude Code e VS Code; `firecrawl setup defaults` pode tornar o Firecrawl o provedor web padrão, desativando fetch/search nativo onde suportado.
- [trailhq/Trail-Code](../repos/github.com/trailhq/trail-code.md) — `trail mcp` expõe seis ferramentas (`trail_find_code`, `trail_file_api`, `trail_trace_calls`, `trail_find_all`, `trail_repo_map`, `trail_check_freshness`); os nomes antigos `graft_*` continuam respondendo.
- [bilawalsidhu/gods-eye-view](../repos/github.com/bilawalsidhu/gods-eye-view.md) — o próprio aplicativo (um globo 3D ao vivo, não uma ferramenta de desenvolvimento) se expõe como servidor MCP, para abrir dentro de Claude Desktop, Codex ou ChatGPT desktop.

## Trade-offs

- **Vantagens:** integração padronizada entre agentes e ferramentas; reuso do mesmo servidor por vários clientes; execução local com controle de permissões; ecossistema crescente de servidores.
- **Limitações:** custo de contexto do catálogo e dos schemas; variação de suporte entre clientes; necessidade de registro e reinício; riscos de segurança quando o servidor executa ações locais; evolução rápida do protocolo e dos SDKs.
- **Custo concreto observado:** no estudo de caso do REA, uma estimativa `cl100k_base` sobre uma passada do catálogo JSON bruto, argumentos e respostas chegou a ~846 mil tokens — cerca de ~802 mil só do catálogo. O próprio documento ressalva que isso é **serialização de transporte**, não contexto renderizado nem uso real de tokens.

## Relações

- **Relacionado a:** function calling, agent skills, plugins de agentes.
- **Contrasta com:** integrações proprietárias por agente; RAG (MCP expõe ferramentas e dados, não é uma técnica de recuperação).
- **Pré-requisito para:** usar o REA a partir de um agente.

## Perguntas abertas

- Como medir o custo real de contexto de um catálogo MCP em um cliente concreto, e não apenas o tamanho da serialização?
- Quais padrões de autorização, isolamento e auditoria estão emergindo para servidores MCP locais?
- Como evitar divergência entre a versão do servidor, os schemas anunciados e as instruções da skill do agente?

## Fontes

- [morluto/rea](../repos/github.com/morluto/rea.md) — `README.md`, `package.json`, `src/main.ts`, `src/server/`, `docs/mcp-contracts.md`, `docs/installation.md` e `.agents/skills/rea-analysis-optimization/references/kuna-case-study.md` (commit `09de00b4108a5d738ebe56903e0110ef63820aca`, consultado em 2026-10-17).
- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — README no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34` (consultado em 2026-10-19).
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037` (consultado em 2026-10-19).
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — README no commit `436d65a74a69d347c57641fbace4eb822bf98600` (consultado em 2026-10-19).
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — README no commit `fee0cd0c180874325305e995197db99f03fa6a6f` (consultado em 2026-10-19).
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — README no commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8` (consultado em 2026-10-19).
- [D4Vinci/Scrapling](../repos/github.com/d4vinci/scrapling.md) — README no commit `fd531313a499092d8471bf24a0e08dc5771f2b40` (consultado em 2026-10-19).
- [openbq-org/OpenBB](../repos/github.com/openbq-org/openbb.md) — README no commit `78020ee4b864ab50b8c1f56373877c2b4e7fb623` (consultado em 2026-10-19).
- [cloudflare/skills](../repos/github.com/cloudflare/skills.md) — README no commit `86505e44f87d801aa1864a3c4109e9a8ae5c409f` (consultado em 2026-10-19).
- [firecrawl/cli](../repos/github.com/firecrawl/cli.md) — README no commit `84c82119a186bc50a27457f81e1d672ec8f28eaf` (consultado em 2026-10-19).
- [trailhq/Trail-Code](../repos/github.com/trailhq/trail-code.md) — README no commit `b1211efd3eef0efa121b93800e5dd8e547aead77` (consultado em 2026-10-21).
- [bilawalsidhu/gods-eye-view](../repos/github.com/bilawalsidhu/gods-eye-view.md) — README no commit `5a1598fd9e5ff707ba73bcb30ba1ae6071a8df68` (consultado em 2026-10-21).
