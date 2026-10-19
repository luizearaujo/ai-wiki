---
type: repo
url: https://github.com/D4Vinci/Scrapling
host: github.com
owner: d4vinci
repo: scrapling
commit: fd531313a499092d8471bf24a0e08dc5771f2b40
license: BSD-3-Clause
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [scraping, agentes, mcp, agent-skills, navegacao-web, python, crawler]
---

# D4Vinci/Scrapling

> Framework Python de web scraping que une requisições HTTP rápidas, browsers stealth, parsing adaptativo e spiders concorrentes numa única biblioteca, com servidor MCP e Agent Skill para que agentes de IA raspem dados diretamente.

## O que é

Scrapling resolve o ciclo completo de web scraping — de uma requisição isolada a um crawl de site inteiro — numa única ferramenta, usável a partir de Python, do terminal ou de um agente de IA. A tese central é reduzir a fragmentação entre bibliotecas de requisição, browser e parsing que esse domínio normalmente exige.

## Como funciona

- **Fetchers:** `Fetcher` para requisições HTTP rápidas com fingerprint de TLS e headers que imitam browsers; `StealthyFetcher` para automação completa de browser (Playwright/Chromium ou Chrome) com bypass de Cloudflare Turnstile/Interstitial.
- **Sessões:** `FetcherSession` e `StealthySession` mantêm cookies e estado entre requisições; suporte síncrono e assíncrono.
- **Spiders:** API inspirada em Scrapy — `start_urls`, callbacks `parse` assíncronos, `Request`/`Response`, concorrência configurável, múltiplas sessões por spider, pausa/retomada por `crawldir`, modo streaming, AutoThrottle (ajusta o delay por domínio a partir da resposta do site) e templates prontos (`CrawlSpider`, `SitemapSpider`, `ShopifySpider` etc.).
- **Parsing:** seletores CSS, XPath, busca por texto e regex, rastreamento adaptativo de elementos (relocaliza um elemento após a página mudar) e busca de elementos similares.
- **Exportação:** JSON/JSONL/CSV/XML via `result.items.to_json()` e equivalentes.
- **Camada de IA:** um servidor MCP expõe requisições HTTP, ações de browser, screenshots, estado de login salvo e respostas de API capturadas em segundo plano a agentes como Claude ou Cursor; a mesma camada reduz o conteúdo enviado ao modelo e bloqueia anúncios e prompt injection, segundo o README. Uma Agent Skill instalável ensina o agente a usar a API atual da biblioteca. `page.markdown()` converte qualquer página em Markdown limpo para RAG, sem LLM no processo.
- **CLI e shell:** `scrapling shell` abre um shell IPython interativo; `scrapling extract` raspa uma URL para arquivo sem escrever código.

## Instalação e uso rápido

```bash
pip install scrapling
```

A instalação básica traz só o parser; fetchers e spiders exigem dependências extras:

```bash
pip install "scrapling[fetchers]"
scrapling install            # baixa browsers e dependências nativas

pip install "scrapling[ai]"     # servidor MCP
pip install "scrapling[rag]"    # pipeline de RAG
pip install "scrapling[shell]"  # shell e comando extract
pip install "scrapling[all]"    # tudo
```

Imagens Docker com todos os extras: `docker pull pyd4vinci/scrapling` ou `ghcr.io/d4vinci/scrapling:latest`.

## Exemplos de uso

Requisição simples:

```python
from scrapling.fetchers import Fetcher

page = Fetcher.get('https://quotes.toscrape.com/')
quotes = page.css('.quote .text::text').getall()
```

Browser stealth com bypass de Cloudflare:

```python
from scrapling.fetchers import StealthyFetcher

page = StealthyFetcher.fetch('https://nopecha.com/demo/cloudflare', solve_cloudflare=True)
```

Spider completo:

```python
from scrapling.spiders import Spider, Response

class QuotesSpider(Spider):
    name = "quotes"
    start_urls = ["https://quotes.toscrape.com/"]

    async def parse(self, response: Response):
        for quote in response.css('.quote'):
            yield {"text": quote.css('.text::text').get(), "author": quote.css('.author::text').get()}

QuotesSpider().start().items.to_json("quotes.json")
```

CLI sem escrever código:

```bash
scrapling extract get 'https://quotes.toscrape.com/' quotes.md
```

## Quando usar (e quando não usar)

- **Use quando:** o pedido envolve raspar dados estáticos ou dinâmicos, construir um crawler com pausa/retomada e exportação, ou dar a um agente de IA uma ferramenta de scraping via MCP/Agent Skill.
- **Evite quando:** o site tem API oficial ou feed — o próprio ecossistema de navegação agêntica desta wiki recomenda API/feed antes de browser automatizado; ou quando o uso pretendido viola termos de serviço do site-alvo — o README declara a biblioteca "para fins educacionais e de pesquisa" e deixa a conformidade legal a cargo do operador.

## Limitações e cuidados

- **Somente o README foi lido.** Código do parser, dos fetchers, dos spiders, do servidor MCP e da Agent Skill não foi inspecionado.
- O README inclui um aviso de isenção de responsabilidade: uso sujeito a leis locais/internacionais de scraping e privacidade, e aos termos de serviço e `robots.txt` de cada site — decisão do operador, não da ferramenta.
- Anti-bot bypass (Cloudflare Turnstile/Interstitial) é uma corrida contra detecção; durabilidade não verificada por esta wiki.
- O MCP server depende de um browser stealth para lidar com CAPTCHA; isso herda os mesmos riscos de automação de browser documentados em [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md).

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~88,6 mil estrelas, ~9,1 mil forks, 9 issues abertas; criado em 2024-10-13, último push em 2026-10-19.
- **Licença:** BSD-3-Clause.
- **Linguagem principal:** Python; publicado no PyPI como `scrapling`, com imagens Docker oficiais.

## Relações

- **Mantido por:** [D4Vinci](../../../entities/d4vinci.md) (Karim Shoair).
- **Conceitos:** [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — servidor MCP para agentes raspar dados; [Agent skills](../../../concepts/agent-skills.md) — skill instalável que ensina a API atual da biblioteca; [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md) — `StealthyFetcher` como browser real controlado por automação.
- **Relacionado a:** [jo-inc/camofox-browser](../jo-inc/camofox-browser.md) — browser anti-detecção como servidor REST, foco em sessão e snapshot em vez de parsing/crawl.

## Perguntas abertas

- Como o servidor MCP decide o que reduzir do conteúdo enviado ao modelo, e com que perda de informação?
- Qual a taxa real de sucesso do bypass de Cloudflare ao longo do tempo, fora dos benchmarks do próprio projeto?
- A Agent Skill é mantida em sincronia automática com mudanças de API, ou depende de atualização manual?

## Fontes

- README: https://github.com/D4Vinci/Scrapling (commit `fd531313a499092d8471bf24a0e08dc5771f2b40`, consultado em 2026-10-19). Somente o README foi lido; código-fonte, documentação completa em readthedocs e o servidor MCP não foram consultados.
- Metadados do repositório: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas).
- Perfil do mantenedor: API do GitHub (`users/D4Vinci`) em 2026-10-19.
