---
type: repo
url: https://github.com/unclecode/crawl4ai
host: github.com
owner: unclecode
repo: crawl4ai
commit: 30165f1ee1fb61f6cce1477feed2acc5e2181e25
license: Apache-2.0
language: Python
status: active
created: 2026-10-22
ingested: 2026-10-22
updated: 2026-10-22
tags: [scraping, rag, mcp, automacao-web]
---

# unclecode/crawl4ai

> Crawler/scraper web open source que transforma qualquer site em Markdown limpo e pronto para LLM, com opção de biblioteca Python local, servidor Docker próprio ou serviço em nuvem por créditos.

## O que é

Crawl4AI resolve o problema de converter páginas web em texto estruturado adequado a RAG, agentes e pipelines de dados — "o crawler web open source para LLMs e agentes de IA", segundo o próprio título do README. Ele se posiciona como o crawler mais estrelado do GitHub (badge Trendshift) e tem uma oferta paga (Crawl4AI Cloud) ao lado da biblioteca gratuita.

## Como funciona

Duas formas de uso, segundo o README:

- **Biblioteca open source**: `pip install -U crawl4ai` + `crawl4ai-setup` instala o browser; `AsyncWebCrawler().arun(url=...)` retorna `result.markdown`. Também disponível como servidor Docker (`unclecode/crawl4ai:latest`) com REST API (`/md`, `/html`, `/crawl`, `/screenshot`, `/pdf`, `/execute_js`), MCP, dashboard e playground; e como CLI (`crwl`).
- **Crawl4AI Cloud**: sem browsers/proxies próprios — endpoints `/scrape` (Markdown), `/extract` (JSON), `/search`, `/serp` (resultado de busca do Google como dado, beta), `/answer` (resposta direta, experimental); 1.000 créditos grátis por mês, planos pagos a partir de $10/mês.

Capacidades da biblioteca: geração de Markdown com filtros de conteúdo (`PruningContentFilterLXML`, `BM25ContentFilter`, `LLMContentFilter`) e citações; extração estruturada via CSS/XPath/Regex sem LLM, ou via LLM para schemas tipados; controle de browser (perfis persistentes, CDP remoto, sessões, stealth, proxies, Chromium/Firefox/WebKit); crawling profundo (BFS/DFS/best-first com `resume_state`), crawler adaptativo que para quando aprendeu o suficiente, descoberta de URL via sitemaps/Common Crawl; screenshots, PDFs e múltiplas URLs em paralelo via `arun_many`.

## Instalação e uso rápido

- **pip**: `pip install -U crawl4ai && crawl4ai-setup && crawl4ai-doctor`; fallback manual `playwright install --with-deps chromium`.
- **Docker server**: exige `CRAWL4AI_API_TOKEN`; `docker run -d -p 11235:11235 ... unclecode/crawl4ai:latest`; dashboard em `/dashboard`, playground em `/playground`.
- **CLI `crwl`**: ex. `crwl https://exemplo.com -o markdown`, `crwl ... --deep-crawl bfs --max-pages 10`.
- **MCP**: `claude mcp add --transport http crawl4ai https://api.crawl4ai.com/mcp --header "Authorization: Bearer $CRAWL4AI_KEY"` (variante cloud); self-hosted expõe o próprio endpoint MCP.

## Exemplos de uso

- Converter uma página de notícias em Markdown limpo com filtro de poda de conteúdo, exemplo do próprio README.
- Extrair preços de modelos de uma página de pricing via LLM com schema Pydantic tipado — exemplo do README.
- Conectar o servidor Docker self-hosted a Claude Code via MCP para extração sob demanda.

## Quando usar (e quando não usar)

- **Use quando:** precisa de Markdown ou dados estruturados prontos para LLM/RAG a partir de páginas web, com controle de código sobre browser, sessão e filtros, e quer rodar localmente ou em Docker próprio.
- **Evite quando:** um bypass totalmente gerenciado de bot walls é obrigatório sem rodar infraestrutura própria — aí a opção é a Crawl4AI Cloud paga.

## Limitações e cuidados

- Atribuição é exigida pela licença: README pede badge ou linha de texto citando o projeto em qualquer uso.
- A seção "My Personal Story" e os números de popularidade (estrelas, Trendshift) são afirmações promocionais do próprio projeto, não verificadas de forma independente.
- SOC 2 Type I está concluído e Type II em andamento, segundo o README — não verificado por auditoria externa citada.
- Apenas o README foi lido; `docs/examples`, `ROADMAP.md` e código-fonte não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: `v0.9.5` (2026-10-14, citada no próprio título do README).
- Atividade e popularidade observadas em 2026-10-22: 86.018 estrelas, 8.940 forks (GitHub API); push em 2026-10-21.
- Licença: Apache-2.0, com requisito de atribuição (badge ou texto) recomendado pelo README.

## Relações

- Mantido por: [UncleCode](../../../entities/unclecode.md).
- Conceitos: [Raspagem web para agentes e LLMs](../../../concepts/raspagem-web-para-agentes.md), [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md).
- Alternativas: [D4Vinci/Scrapling](../d4vinci/scrapling.md) — já documentado na wiki, foco em fetchers stealth e parsing adaptativo sem geração de Markdown como produto central.

## Perguntas abertas

- Qual a cobertura real de bypass de bot walls fora da oferta Cloud (que promete tratamento automático)?
- Como o crawler adaptativo decide, na prática, que "aprendeu o suficiente" para parar?

## Fontes

- README: https://raw.githubusercontent.com/unclecode/crawl4ai/30165f1ee1fb61f6cce1477feed2acc5e2181e25/README.md (commit `30165f1ee1fb61f6cce1477feed2acc5e2181e25`, consultado em 2026-10-22). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
