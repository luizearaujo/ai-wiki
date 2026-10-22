---
type: concept
aliases: [Raspagem web para agentes, Web scraping para LLMs, Data extraction for agents, Crawling agêntico]
status: draft
created: 2026-10-22
updated: 2026-10-22
tags: [scraping, crawling, mcp, rag, ferramentas]
---

# Raspagem web para agentes e LLMs

> Ferramentas que convertem sites em dados estruturados ou Markdown limpo, pensados para alimentar LLMs, RAG e agentes de IA — em contraste com scraping clássico voltado a planilhas ou bancos de dados.

## Definição

Esta camada resolve um problema específico: um LLM lê melhor Markdown ou JSON estruturado do que HTML bruto com menus, rodapés e boilerplate. Os projetos da wiki que ocupam esse espaço — [unclecode/crawl4ai](../repos/github.com/unclecode/crawl4ai.md) e [D4Vinci/Scrapling](../repos/github.com/d4vinci/scrapling.md) — convergem em alguns pontos: geração de Markdown "fit" para LLM, extração estruturada com ou sem LLM, servidor MCP para expor a extração a agentes, e controle de browser real (stealth, proxies) para lidar com bot walls.

A diferença em relação a scraping tradicional está no **destino do dado**: não é uma tabela para análise humana, é contexto para um modelo — o que muda a prioridade de design para "menos ruído, mais sinal por token" em vez de "cobertura de campos".

## Como funciona

| Componente | Papel | Exemplo |
|---|---|---|
| **Fetcher/browser** | Busca a página, real ou headless, com ou sem stealth | `AsyncWebCrawler` (crawl4ai), `StealthyFetcher` (Scrapling) |
| **Geração de Markdown** | Filtra boilerplate e formata para leitura por LLM | `PruningContentFilterLXML`, `BM25ContentFilter` (crawl4ai), `page.markdown()` (Scrapling) |
| **Extração estruturada** | Produz JSON/schema, com ou sem LLM | CSS/XPath/Regex (sem LLM) ou schema tipado via LLM (crawl4ai) |
| **Crawling profundo** | Segue links, BFS/DFS/best-first, com estado de retomada | `resume_state` (crawl4ai) |
| **Exposição a agentes** | Servidor MCP ou API que um agente chama como ferramenta | MCP do crawl4ai, MCP do Scrapling |
| **Camada paga opcional** | Infra gerenciada (browsers, proxies, bypass de bot wall) por créditos | Crawl4AI Cloud |

A escolha estrutural central é **onde o LLM entra**: extração sem LLM (CSS/XPath/Regex) é rápida e barata, mas frágil a mudanças de layout; extração com LLM é mais robusta a variação, mas custa tokens e latência por página. Projetos maduros oferecem as duas, deixando a escolha ao usuário por tarefa.

## Onde aparece

- [unclecode/crawl4ai](../repos/github.com/unclecode/crawl4ai.md) — biblioteca/servidor/CLI que gera Markdown "fit" para LLM com filtros de conteúdo, extração CSS/XPath/Regex/LLM, crawling profundo e adaptativo, e oferta paga em nuvem por créditos.
- [D4Vinci/Scrapling](../repos/github.com/d4vinci/scrapling.md) — fetchers HTTP e browser stealth, spiders concorrentes, parsing adaptativo e `page.markdown()` para conteúdo pronto para RAG sem LLM no processo; já documentado na wiki antes deste lote.

## Trade-offs

- **Vantagens:** reduz o custo de contexto por página (Markdown limpo em vez de HTML); dá a agentes acesso programático a sites sem API; crawling profundo cobre casos que uma extração pontual não resolve.
- **Limitações:** bot walls, CAPTCHAs e mudanças de layout seguem sendo barreira; extração com LLM custa tokens e introduz variação; serviços em nuvem por crédito criam dependência de um provedor terceiro para a parte mais difícil (contornar detecção).
- **Critério prático:** prefira extração sem LLM quando o layout é estável e conhecido; reserve LLM para páginas variáveis ou sem schema fixo; avalie self-host vs. cloud pelo volume de bot walls que a tarefa realmente enfrenta.

## Relações

- **Relacionado a:** [Navegação web agêntica](navegacao-web-agentica.md) — mesma dependência de browser real e anti-detecção, mas voltada a um loop de decisão passo a passo em vez de extração em lote; [Model Context Protocol (MCP)](model-context-protocol.md) — camada de exposição comum a todos os projetos citados; [Economia de tokens em agentes](economia-de-tokens-em-agentes.md) — Markdown "fit" é, na prática, uma técnica de economia de contexto.
- **Contrasta com:** scraping clássico para planilha/BI, sem preocupação com formato de leitura por modelo.
- **Depende de:** browser real ou headless, filtros de conteúdo, e (opcionalmente) um LLM para extração robusta a variação de layout.

## Perguntas abertas

- Como medir, de forma comparável entre projetos, a taxa de sucesso contra bot walls modernos (Cloudflare, Akamai etc.)?
- Qual é o custo real por página da extração via LLM em escala, comparado ao custo de manter seletores CSS/XPath atualizados manualmente?

## Fontes

- [unclecode/crawl4ai](../repos/github.com/unclecode/crawl4ai.md) — README no commit `30165f1ee1fb61f6cce1477feed2acc5e2181e25` (consultado em 2026-10-22).
- [D4Vinci/Scrapling](../repos/github.com/d4vinci/scrapling.md) — página existente da wiki, usada como comparação.
