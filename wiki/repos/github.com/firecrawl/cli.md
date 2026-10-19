---
type: repo
url: https://github.com/firecrawl/cli
host: github.com
owner: firecrawl
repo: cli
commit: 84c82119a186bc50a27457f81e1d672ec8f28eaf
license: desconhecida
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [cli, scraping, mcp, agent-skills, navegacao-web, dados]
---

# firecrawl/cli

> Interface de linha de comando do Firecrawl: busca, scrape, crawl, mapeamento, interação com páginas e um comando `agent` de extração autônoma via IA — instalável como provedor web padrão de agentes de código, com famílias de skills e servidor MCP próprios.

## O que é

O Firecrawl CLI expõe, do terminal, toda a superfície de dados web do Firecrawl: raspagem de página única, busca geral e especializada (fontes de pesquisa acadêmica, fontes de desenvolvedor, índice governamental), crawl de site inteiro, mapeamento de URLs, interação com páginas em sessão de browser viva, monitoramento de mudanças e extração autônoma por agente. O mesmo pacote instala skills e um servidor MCP para que agentes de código usem essas capacidades diretamente.

## Como funciona

### Instalação e configuração por agente

```bash
npm install -g firecrawl-cli
# ou, em um comando só: instala, autentica e adiciona skills a todos os editores detectados
npx -y firecrawl-cli@latest init -y --browser
```

A instalação detecta harnesses suportados (Claude Code, Codex, Cursor, Windsurf, OpenCode, OpenClaw, OpenHands, Hermes Agent) e instala skills globalmente em todos por padrão; `--agent <agent>` restringe a um único harness.

### Três famílias de skills

| Família | Comando | Conteúdo |
|---|---|---|
| **Core** (alias `skills`) | `firecrawl setup core` | Primitivas de scrape/search/crawl/interact e skills de índice (pesquisa, desenvolvedor). Instalada por padrão. |
| **Build** | `firecrawl setup build` | Skills de integração da API do Firecrawl em código de aplicação. |
| **Workflows** | `firecrawl setup workflows` | Receitas ponta a ponta (geração de leads, pesquisa profunda, auditoria SEO, QA, base de conhecimento, extração de design system); seleção interativa multi-escolha. |

Todas as famílias vivem no catálogo [`firecrawl/skills`](https://github.com/firecrawl/skills) — read-only; contribuições vão para o repositório de origem de cada família (este CLI, o monorepo `firecrawl/firecrawl` para skills de build/SDK, ou `firecrawl/firecrawl-workflows` para workflows).

### MCP e "Firecrawl como provedor padrão"

```bash
firecrawl setup mcp        # instala o servidor MCP do Firecrawl em Cursor, Claude Code, VS Code etc.
firecrawl setup defaults   # torna o Firecrawl o provedor web padrão, desativando fetch/search nativo onde suportado
```

`setup defaults` pergunta harness por harness (Claude Code, Codex) qual trocar, e pode ser desfeito com `firecrawl setup defaults --undo`.

### Comandos principais

| Comando | Função |
|---|---|
| `scrape` | Extrai conteúdo de uma ou mais URLs concorrentemente; salva cada resultado em `.firecrawl/`. |
| `search` | Busca na web geral. |
| `developer` | Busca em fontes de desenvolvedor. |
| `gov` | Busca no índice governamental do Firecrawl. |
| `research` | Busca em papers de pesquisa, com subcomandos dedicados. |
| `map` | Descobre todas as URLs de um site. |
| `crawl` | Rastreia um site inteiro. |
| `interact` | Faz scrape de uma página e interage com ela em sessão de browser viva, por linguagem natural ou código. |
| `monitor` | Observa páginas por mudanças. |
| `agent` | Extração de dados web autônoma por IA, com prompt em linguagem natural; tarefas levam de 2 a 5 minutos. |
| `download` (experimental, `firecrawl x`) | Combina `map` + `scrape` para salvar um site inteiro como arquivos locais. |
| `config` / `view-config` / `login` / `logout` | Configuração e autenticação. |

### Comando `agent` e provedores Alexandria

O comando `agent` aceita `--schema`/`--schema-file` para saída estruturada, `--effort` (low/medium/high), `--max-credits`, `--webhook`, `--thread` para continuar uma conversa, e `--mode extract|chat`. Com `--toolkits`, o agente pode chamar até 5 **provedores Alexandria** (ex.: Apollo, Crunchbase, Benzinga) por turno, com `--max-calls` limitando chamadas e `--require-approval` exigindo aprovação explícita antes de qualquer chamada paga.

Quando um provedor exige aceite de termos de dados (`THIRD_PARTY_DATA_TERMS_REQUIRED`), só um admin da organização pode aceitar pelo painel do Firecrawl — a CLI não aceita termos por conta própria, e o README instrui o agente a devolver o link ao usuário e não repetir a chamada até o aceite.

Cada execução Alexandria devolve um **receipt**: `creditsUsed` (uso real reportado), `requestId` (idempotência) e `operationId`/`operationType`. Reusar o mesmo `requestId` recupera uma execução pendente ou incerta sem recobrar; uma nova execução deliberada precisa de um `requestId` novo.

### Telemetria

A CLI coleta dados anônimos de uso na autenticação — versão da CLI, SO, versão do Node.js e detecção de ferramentas de desenvolvimento (Cursor, VS Code, Claude Code). O README declara explicitamente que **nenhum dado de comando, URL ou conteúdo de arquivo é coletado**. Desativável com `FIRECRAWL_NO_TELEMETRY=1`.

## Instalação e uso rápido

```bash
npm install -g firecrawl-cli
firecrawl https://example.com
```

Autenticação (login por browser, API key direta ou variável de ambiente):

```bash
firecrawl login
firecrawl login --api-key fc-your-api-key
export FIRECRAWL_API_KEY=fc-your-api-key
```

Self-hosted/local:

```bash
firecrawl --api-url http://localhost:3002 scrape https://example.com
```

## Exemplos de uso

Exemplos derivados do README:

```bash
firecrawl agent "Find the top 5 competitors of Notion and their pricing" --wait --timeout 300
firecrawl agent "Get all blog post titles and dates" --urls https://blog.example.com --max-credits 100 --wait
firecrawl scrape benzinga/news/search --options '{"pageSize":10}'   # atalho Alexandria, sem URL
firecrawl x download https://docs.firecrawl.dev --screenshot --limit 20 -y
```

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é dar a um agente de código acesso padronizado a busca, scrape, crawl e extração autônoma da web, com skills e MCP já empacotados.
- **Use quando:** a tarefa precisa de fontes especializadas (papers de pesquisa, índice governamental, fontes de desenvolvedor) ou de provedores de dados de terceiros via Alexandria.
- **Evite quando:** o uso pretendido não aceita depender de uma API comercial com créditos e termos de terceiros por provedor — cada chamada Alexandria tem custo e pode exigir aceite de termos por um admin.
- **Evite quando:** o requisito é só scraping/parsing local sem camada de agente — nesse caso, uma biblioteca como [D4Vinci/Scrapling](../d4vinci/scrapling.md) cobre o mesmo núcleo sem depender de um serviço hospedado.

## Limitações e cuidados

- **Somente o README foi lido.** Código-fonte do CLI, do servidor MCP e das skills (hospedadas em `firecrawl/skills`, repositório separado) não foram inspecionados.
- `setup defaults` desativa fetch/search nativo de agentes suportados para rotear tudo pelo Firecrawl — é uma mudança de comportamento global do agente, não apenas uma ferramenta adicional; o README oferece `--undo`, mas a reversão também é por harness.
- Tarefas de `agent` custam créditos e levam de 2 a 5 minutos (ou mais); o próprio README recomenda uso comedido e `--max-credits`.
- Provedores Alexandria são serviços de terceiros com termos próprios; a CLI não aceita esses termos automaticamente, e cada chamada tem custo de crédito real.
- O comando `download` está em `firecrawl experimental` (`firecrawl x`) — API sujeita a mudança.
- A API do GitHub não detectou licença para o repositório.

## Estado e adoção

- **Atividade observada em 2026-10-19:** 656 estrelas, 117 forks, 85 issues abertas; criado em 2026-01-07, último push em 2026-10-19.
- **Licença:** desconhecida (não detectada pela API do GitHub).
- **Linguagem principal:** TypeScript.

## Relações

- **Mantido por:** [Firecrawl](../../../entities/firecrawl.md).
- **Conceitos:** [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — `firecrawl setup mcp` instala o servidor MCP do Firecrawl; [Agent skills](../../../concepts/agent-skills.md) — três famílias de skills (core/build/workflows) distribuídas via catálogo próprio; [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md) — o comando `interact` abre sessão de browser viva controlada por linguagem natural ou código.
- **Relacionado a:** [D4Vinci/Scrapling](../d4vinci/scrapling.md) — outra ferramenta de scraping com camada de agente (MCP + Agent Skill), mas como biblioteca open source autoexecutável, em vez de CLI sobre um serviço comercial hospedado.

## Perguntas abertas

- Como o comando `agent` lida com falhas parciais em tarefas de extração complexas além do que os exemplos mostram?
- Qual é o modelo de custo real de créditos para uso intensivo de `agent` e dos provedores Alexandria?
- `setup defaults` é reversível de forma completa, sem resíduo de configuração, em todos os harnesses suportados?

## Fontes

- README: https://github.com/firecrawl/cli (commit `84c82119a186bc50a27457f81e1d672ec8f28eaf`, consultado em 2026-10-19). Somente o README foi lido; código-fonte, o catálogo `firecrawl/skills` e a documentação em docs.firecrawl.dev não foram consultados.
- Metadados do repositório e do perfil `firecrawl` via API do GitHub (consultados em 2026-10-19).
