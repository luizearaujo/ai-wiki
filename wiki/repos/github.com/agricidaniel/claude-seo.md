---
type: repo
url: https://github.com/AgriciDaniel/claude-seo
host: github.com
owner: agricidaniel
repo: claude-seo
commit: 6be93f45064ffbadced572b5d5c95f55fd263af0
license: MIT
language: Python
status: active
created: 2026-10-30
ingested: 2026-10-30
updated: 2026-10-30
tags: [seo, geo, auditoria, agent-skills, claude-code, marketing]
---

# AgriciDaniel/claude-seo

> Plugin gratuito e open source para Claude Code que audita um site completo em 10 a 15 minutos — SEO técnico, Core Web Vitals, E-E-A-T, Schema.org, SEO local, e-commerce e prontidão para busca por IA — e devolve um plano de ação priorizado.

## O que é

Claude SEO é descrito como um substituto de consultoria de SEO dentro do próprio Claude Code: recebe a URL de um site e roda uma auditoria completa cobrindo rastreabilidade e indexação, sitemaps, robots.txt, redirecionamentos, velocidade de página e Core Web Vitals; qualidade de conteúdo (E-E-A-T); dados estruturados (encontra, valida e escreve markup Schema.org); SEO local e de e-commerce; e **GEO** (Generative Engine Optimization) — a chance de páginas serem citadas por AI Overviews do Google, AI Mode, ChatGPT, Perplexity e Gemini.

O projeto é do mesmo autor do [claude-ads](claude-ads.md) e da mesma comunidade (AI Marketing Hub Pro). É construído a partir de **26 sub-skills e 19 agentes especialistas**, com até 17 agentes auditando um site em paralelo. Cada recomendação explica por que importa e como verificar que a correção funcionou.

Público declarado: agências de SEO que querem auditorias semanais por cliente, times in-house de SEO em SaaS/publishers/e-commerce, e consultores freelancers que querem mostrar um diagnóstico real na primeira chamada.

## Como funciona

1. **Detecção de tipo de negócio** — o projeto identifica se o site é SaaS, local, e-commerce, publisher ou agência e ajusta as checagens.
2. **Fan-out de agentes** — até 17 agentes especialistas auditam o site em paralelo (técnico, conteúdo, schema, velocidade, busca por IA e mais).
3. **Plano, não lista de avisos** — achados são pontuados e ordenados em um plano de ação priorizado; cada recomendação diz em que se baseia, de que depende e como confirmar que funcionou.

Relatórios saem em Markdown; `/seo google report` os converte em PDF.

### Os 19 agentes (modelo por agente)

| Agente | Papel | Modelo |
| --- | --- | --- |
| `seo-technical` | Technical SEO Lead | Sonnet |
| `seo-content` | Content Editor | Opus |
| `seo-schema` | Structured Data Engineer | Sonnet |
| `seo-sitemap` | Sitemap Architect | Sonnet |
| `seo-performance` | Performance Engineer | Sonnet |
| `seo-visual` | Visual QA | Sonnet |
| `seo-geo` | AI Search Analyst | Opus |
| `seo-agentic` | Agent Readiness Analyst | Sonnet |
| `seo-local` | Local SEO Specialist | Sonnet |
| `seo-maps` | Maps Analyst | Sonnet |
| `seo-google` | Google Data Analyst | Sonnet |
| `seo-backlinks` | Link Analyst | Sonnet |
| `seo-cluster` | Topic Strategist | Opus |
| `seo-sxo` | Search Experience Designer | Opus |
| `seo-drift` | Change Monitor | Opus |
| `seo-ecommerce` | E-commerce Specialist | Sonnet |
| `seo-flow` | FLOW Strategist | Sonnet |

Cinco agentes (os que exigem mais julgamento) rodam em Opus; o resto em Sonnet — por isso uma auditoria completa consome mais do plano Claude do que a checagem de uma única página. O modelo de cada agente pode ser trocado no respectivo arquivo em `agents/`.

### Comandos (30 no total, em 6 grupos)

- **Auditoria e planejamento:** `/seo setup`, `/seo doctor`, `/seo audit <url>`, `/seo page <url>`, `/seo plan <tipo>` (saas, local, ecommerce, publisher, agency).
- **SEO técnico:** `/seo technical`, `/seo sitemap`, `/seo images`, `/seo hreflang`, `/seo programmatic`, `/seo google [comando]` (GSC, PageSpeed, CrUX, Indexing, GA4, relatórios PDF), `/seo drift` (monitoramento de mudanças com snapshots SQLite).
- **Conteúdo e E-E-A-T:** `/seo content`, `/seo content-brief`, `/seo cluster`, `/seo sxo`, `/seo flow`, `/seo competitor-pages`.
- **Schema e busca por IA:** `/seo schema`, `/seo geo`, `/seo agentic` (prontidão para agentes: Lighthouse Agentic Browsing, acesso de agentes de IA, `llms.txt`, Markdown, WebMCP).
- **Local, links, commerce:** `/seo local`, `/seo maps`, `/seo backlinks` (via Moz, Bing, Common Crawl), `/seo ecommerce`.
- **Extensões opcionais:** `/seo image-gen`, `/seo seranking` (share-of-voice em ChatGPT/Gemini/Perplexity/AI Overviews), `/seo profound` (rastreamento de citação por LLM), `/seo bing` (Bing Webmaster + IndexNow), `/seo unlighthouse` (Lighthouse multi-página local).

## Instalação e uso rápido

Requer Claude Code 1.0.33 ou mais recente.

```bash
/plugin marketplace add AgriciDaniel/claude-seo
/plugin install claude-seo@agricidaniel-claude-seo
/seo setup
```

`/seo setup` cria um ambiente Python isolado e um navegador headless próprios, sem alterar o resto do sistema. `/seo doctor` verifica a prontidão do runtime sem mudar nada.

Instalação manual (macOS/Linux):

```bash
git clone --depth 1 https://github.com/AgriciDaniel/claude-seo.git
bash claude-seo/install.sh
```

Instalação manual (Windows, PowerShell):

```powershell
git clone --depth 1 https://github.com/AgriciDaniel/claude-seo.git
powershell -ExecutionPolicy Bypass -File claude-seo\install.ps1
```

O README justifica `git clone` em vez de `irm | iex`: os guardrails de segurança do próprio Claude Code sinalizam baixar e executar código remoto sem verificação como risco de supply chain; `git clone` permite revisar o script antes de rodar.

**Duas versões:** a pública é MIT e gratuita para todos. Membros do AI Marketing Hub Pro (Skool) têm acesso antecipado a uma versão privada via `/plugin marketplace add AI-Marketing-Hub/claude-seo`.

Primeira auditoria:

```bash
/seo audit https://exemplo.com           # auditoria completa com plano priorizado
/seo page https://exemplo.com/precos     # uma página, em profundidade
/seo geo https://exemplo.com             # prontidão para busca por IA
/seo schema https://exemplo.com          # checa e gera Schema.org
/seo local https://exemplo.com           # SEO local e Google Business Profile
```

Pré-requisitos: Claude Code 1.0.33+, Python 3.11 a 3.14. Não exige chave de API para funcionar — chaves gratuitas do Google (PageSpeed Insights, Chrome UX Report, Search Console, GA4) são opcionais via `/seo google setup`, para dados de campo reais em vez de estimativas de laboratório.

Desinstalar: `/plugin uninstall claude-seo@agricidaniel-claude-seo`, ou `bash claude-seo/uninstall.sh` na instalação manual.

## Exemplos de uso

Exemplos derivados do README — não são instruções oficiais além do que ele publica.

- Rodar `/seo audit` em um site novo para obter um plano priorizado de correções antes de uma reunião com cliente.
- Rodar `/seo geo` isoladamente para medir a chance de páginas serem citadas por AI Overviews, ChatGPT, Perplexity e Gemini.
- Rodar `/seo drift baseline` e depois `/seo drift compare` para detectar regressões de SEO entre duas auditorias.
- Conectar `/seo google setup` para substituir estimativas de Core Web Vitals por dados reais do Chrome UX Report e Search Console.

## Quando usar (e quando não usar)

- **Use quando:** quer uma auditoria de SEO completa e repetível, sem custo por site e sem lock-in de dashboard — o resultado fica em arquivos Markdown/PDF/JSON que você guarda.
- **Use quando:** precisa cobrir busca por IA (GEO) além de SEO tradicional, com checklist consistente entre execuções.
- **Use quando:** já está dentro do Claude Code e quer evitar montar infraestrutura própria de SEO (ao contrário do [every-app/open-seo](../every-app/open-seo.md), que exige self-hosting e uma chave DataForSEO paga).
- **Evite quando:** precisa de um crawler mais rápido e profundo, ou de uma base própria de backlinks maior — ferramentas como Screaming Frog ou grandes suítes de SEO cobrem isso; o próprio README diz que "muitas pessoas usam os dois".
- **Evite quando:** o orçamento de uso do plano Claude é apertado — uma auditoria completa usa mais consumo do plano do que uma checagem de página única, por rodar 5 agentes em Opus.

## Limitações e cuidados

- **Somente o README foi lido.** Código, os 26 sub-skills, os 19 agentes, `docs/ARCHITECTURE.md`, `skills/seo/references/thinking-framework.md` e os testes (o README cita 1.077 passando) não foram verificados nesta ingestão.
- **Sem chave de API, dados são estimativa.** Core Web Vitals ficam como estimativa de laboratório e a indexação é inferida da própria página, não confirmada via Search Console.
- **Sites com conteúdo carregado só após scroll/clique podem gerar resultado ruidoso**, segundo o próprio README.
- **Dados trafegam para a Anthropic como qualquer uso do Claude Code** — o README é explícito que páginas e dados analisados são enviados ao modelo da mesma forma que qualquer outro conteúdo trabalhado na ferramenta. Além do site auditado, algumas checagens leem fontes públicas (Wikipedia, Reddit, Common Crawl); ver `PRIVACY.md` para a lista completa — não consultado nesta ingestão.
- **Extensões pagas opcionais** (SE Ranking, Profound, Banana) usam contas próprias do usuário e não são necessárias para o funcionamento básico.
- **Resultados "reais" citados são do próprio site do projeto** (claude-seo.md: 10,8 mil cliques e 99 de PageSpeed), não uma avaliação independente.
- **Tabela de preço comparativa** (grátis vs. agência US$2k–15k vs. software US$99–999/mês) é marcada no próprio README como "preços de mercado ilustrativos", não uma pesquisa própria.

## Estado e adoção

- **Versão citada:** sem número de versão fixo no README; releases ficam em `github.com/AgriciDaniel/claude-seo/releases`. Testes: 1.077 passando (badge do README).
- **Atividade e popularidade observadas em 2026-10-30:** 24.270 estrelas, 3.247 forks, 75 issues abertas; criado em 2026-02-07, último push em 2026-10-22.
- **Licença:** MIT.
- **Linguagem principal:** Python.
- **Destaque:** GitHub Trending #12 Repository of the Day (badge Trendshift), observado no README.

## Relações

- **Mantido por:** [Agrici Daniel (AgriciDaniel)](../../../entities/agricidaniel.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — 26 sub-skills e 19 agentes especialistas; [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — não expõe servidor MCP próprio, mas audita prontidão de agentes via `/seo agentic` (WebMCP, llms.txt).
- **Alternativas:** [every-app/open-seo](../every-app/open-seo.md) — mesma área (pesquisa de palavra-chave, auditoria de site, backlinks), mas exige self-hosting (Docker/Cloudflare) e uma chave DataForSEO paga por uso; claude-seo roda só dentro do Claude Code, sem infraestrutura própria, e é gratuito mesmo no uso contínuo (fora o consumo normal do plano Claude).
- **Mesma família do autor:** [AgriciDaniel/claude-ads](../claude-ads.md) — mídia paga, em vez de SEO orgânico; `AgriciDaniel/claude-blog` e `AgriciDaniel/chatgpt-seo`, citados no README como projetos relacionados, sem página própria nesta wiki.

## Perguntas abertas

- O manifesto de capacidades e os gates de escrita (schema gerado, sitemaps) seguem o mesmo modelo de aprovação explícita do claude-ads, ou a escrita de arquivos é direta?
- Como os 19 agentes compartilham contexto entre si durante o fan-out paralelo, e o que acontece se um agente obrigatório falhar?
- O backlink profile (`/seo backlinks`) usa só fontes gratuitas (Moz, Bing, Common Crawl) ou também aceita uma chave paga equivalente à DataForSEO do open-seo?
- Que fração dos "26 sub-skills" é exclusiva da versão pública MIT versus reservada à versão privada do AI Marketing Hub Pro?

## Fontes

- README: https://raw.githubusercontent.com/AgriciDaniel/claude-seo/6be93f45064ffbadced572b5d5c95f55fd263af0/README.md (commit `6be93f45064ffbadced572b5d5c95f55fd263af0`, consultado em 2026-10-30). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/AgriciDaniel/claude-seo`), consultada em 2026-10-30.
