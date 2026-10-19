---
type: repo
url: https://github.com/HKUDS/Vibe-Trading
host: github.com
owner: hkuds
repo: vibe-trading
commit: 097b29feab9793e3c302e1a7a4f3c0dac6344904
license: MIT
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [trading, financas, agentes, multiagente, mcp, backtest, llm, skills]
---

# HKUDS/Vibe-Trading

> Workspace de pesquisa financeira que transforma perguntas em linguagem natural em análise executável — dados de mercado, geração de estratégias, backtest, relatórios, memória e, opcionalmente, execução limitada por mandato em corretoras autorizadas pelo usuário.

## O que é

Vibe-Trading é descrito como um "open-source research workspace for turning finance questions into runnable analysis". Ele conecta prompts a carregadores de dados, geração de estratégias, engines de backtest, relatórios, exportações e memória persistente de pesquisa. O README separa explicitamente **pesquisa, simulação e backtest** da **execução autônoma**, que só ocorre através de uma corretora que o próprio usuário autoriza — por exemplo, Robinhood Agentic Trading. O projeto "não detém fundos" e diz nunca operar fora dos limites definidos pelo usuário, com parada instantânea.

O público é composto por traders, investidores, pesquisadores e desenvolvedores que querem um agente para conduzir fluxos de análise e pesquisa, com CLI, API, Web UI e servidor MCP. O projeto faz parte do ecossistema [HKUDS](../../../entities/hkuds.md) e é distribuído como pacote PyPI `vibe-trading-ai`.

## Como funciona

O fluxo de pesquisa publicado tem cinco camadas:

| Camada | O que acontece |
| --- | --- |
| **Plan** | Seleciona skills financeiras, ferramentas, fontes de dados e, quando útil, um preset de swarm. |
| **Ground** | Carrega ações A/HK/US/Canadá/UK, cripto, futuros, forex, documentos ou contexto web. |
| **Execute** | Gera código de estratégia testável, executa ferramentas e usa o engine de backtest correspondente. |
| **Validate** | Acrescenta métricas, benchmark, Monte Carlo, Bootstrap, Walk-Forward, run cards e avisos. |
| **Deliver** | Devolve relatórios, artefatos, traces de ferramentas e exportações para TradingView, TDX, MetaTrader 5, clientes MCP ou sessões futuras. |

### Componentes e números declarados

- **90 skills financeiras** em 9 categorias (dados, estratégia, análise, classes de ativo, cripto, fluxo, ferramentas, pesquisa e risco).
- **30 presets de swarm**, como `investment_committee` (debate bull/bear → risco → decisão do PM) e `crypto_trading_desk`.
- **29 fontes de dados**, com seleção automática por mercado e cadeias de fallback ordenadas por risco de bloqueio de IP. Inclui fontes gratuitas (Yahoo, OKX, AKShare, Tencent, B3) e opcionais com chave (Tushare, Longbridge, Polygon, QVeris).
- **19 conectores de corretora**, com perfis de leitura, paper e live limitado por mandato. Paper e live são separados por um guard estrutural do runtime, não por uma flag que o agente possa alternar.
- **Alpha Zoo com 478 alphas** (Qlib, Alpha101, GTJA191, acadêmicos e fundamentais ponto no tempo), com benchmark de IC e categorização alive/reversed/dead.
- **112 ferramentas de agente** e **81 ferramentas MCP** expostas a clientes externos.
- **10 engines de backtest** mais um engine composto cross-market.

### Execução e segurança

O README detalha controles incomuns para um projeto desse tipo:

- **Mandato do usuário** para ordens live: allowlist de símbolos, limites de tamanho/exposição, teto diário de operações e kill switch. Ferramentas de ordem ficam fora do MCP; só o agente e a CLI as acessam.
- **Separação paper/live estrutural** — formato da conta, host separado, flag de demo ou ambiente de trade. Corretoras sem discriminador verificável ficam limitadas a paper + leitura.
- **Modo TAP** opcional para Alpaca: o processo do agente não guarda a chave da corretora; leituras passam pelo proxy e escritas exigem aprovação humana.
- **Código de backtest gerado** roda em subprocesso Python com ambiente estreito: sem chaves de LLM, tokens de API, segredos de corretora ou flags de shell.
- **Shell tools** só são habilitadas na CLI local interativa; API e MCP exigem opt-in explícito.
- O runner live tem orçamento de decisões e tokens por dia e kill switch ao esgotar o orçamento.

## Instalação e uso rápido

Instalação por PyPI:

```bash
pip install vibe-trading-ai
vibe-trading init
vibe-trading run -p "Backtest a BTC-USDT 20/50 moving-average strategy for 2024 and summarize return and drawdown"
```

Comandos publicados:

| Comando | Função |
| --- | --- |
| `vibe-trading` | CLI/TUI interativa. |
| `vibe-trading serve --port 8899` | Servidor FastAPI e Web UI. |
| `vibe-trading-mcp` | Servidor MCP via stdio, SSE ou streamable HTTP. |

Alternativas: Docker (`docker compose up --build`), instalação local com `pip install -e .` ou ClawHub (`npx clawhub@latest install vibe-trading --force`).

Pré-requisitos: Python 3.11+, uma chave de LLM (ou Ollama local), Docker para o caminho mais rápido e credenciais de corretora apenas para execução. O README lista muitos provedores de modelo, incluindo OpenRouter, OpenAI, Anthropic, DeepSeek, Gemini, Groq, Qwen, Kimi, GitHub Copilot, Claude Code CLI e Ollama.

## Exemplos de uso

Exemplos derivados do README — não são instruções oficiais além do que ele publica.

```bash
# Pesquisa em linguagem natural
vibe-trading run -p "Backtest a BTC-USDT 20/50 moving-average strategy for 2024, summarize return and drawdown, then export the report"

# Benchmark de alphas
vibe-trading alpha bench --zoo gtja191 --universe csi300 --period 2018-2025 --top 20

# Análise do próprio histórico de trades
vibe-trading --upload trades_export.csv
vibe-trading run -p "Analyze my trading behavior, extract my shadow strategy, and compare it with my actual trades"
```

## Quando usar (e quando não usar)

- **Use quando:** você quer um workspace integrado para pesquisa financeira com agente, cobrindo dados, estratégia, backtest, validação e relatórios.
- **Use quando:** precisa comparar mercados e fontes, ou avaliar alphas em lote, sem montar toda a infraestrutura manualmente.
- **Use quando:** quer expor ferramentas financeiras a outro agente via MCP.
- **Use quando:** deseja executar ordens somente dentro de limites explícitos e com separação paper/live — mas trate a integração como experimental.
- **Evite quando:** você espera retorno garantido ou estratégia pronta. O README declara que o projeto é software de pesquisa e não aconselhamento financeiro.
- **Evite quando:** não pode revisar custo de LLM, credenciais de corretora e termos das fontes de dados.
- **Evite quando:** precisa de garantia de produção verificada por terceiros. O próprio README diz que a capacidade de trading via corretora é experimental e não foi verificada contra uma conta real.

## Limitações e cuidados

- **Somente o README foi lido.** Código, testes, engines, conectores, docs internas e resultados de backtest não foram consultados. A implementação real dos guards, do mandato e da execução é **A verificar**.
- **README muito extenso.** São cerca de 2.500 linhas; números e capacidades são afirmações do projeto, não especificação estável.
- **Integração com corretoras declarada como experimental.** O disclaimer diz que a execução via corretora "não é verificada por nós contra uma conta real".
- **Custo de modelo.** Runs de pesquisa, swarms e loops live consomem chamadas de LLM; o runner live tem orçamento, mas chamadas de modelo são cobradas mesmo sem ordens.
- **Dados de terceiros.** 29 fontes têm termos, limites, throttling e lacunas próprias; o fallback reduz o risco de indisponibilidade, não o de qualidade.
- **Superfície de execução.** Apesar dos guards documentados, habilitar live trading exige revisão própria de permissões, limites e kill switch.
- **MCP não é write-capable por padrão.** Ferramentas de ordem ficam fora do MCP, mas catálogos grandes de 81 tools consomem contexto.
- **Licença MIT** não remove responsabilidade por perdas, compliance de dados ou uso de APIs de terceiros.

## Estado e adoção

- **Versão citada:** v0.1.16, publicada em 2026-09-29.
- **Atividade e popularidade observadas em 2026-10-19:** ~35,9 mil estrelas, ~5,8 mil forks, 22 issues abertas; criado em 2026-04-01; último push em 2026-10-19.
- **Licença:** MIT.
- **Linguagem principal:** Python; frontend em React 19.
- **Commit de referência:** `097b29feab9793e3c302e1a7a4f3c0dac6344904`.

## Relações

- **Mantido por:** [HKUDS](../../../entities/hkuds.md) — Data Intelligence Lab @ HKU.
- **Conceitos:** [Análise financeira multiagente](../../../concepts/analise-financeira-multiagente.md) — pesquisa e times de analistas; [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — 30 presets de swarm; [Memória de agente](../../../concepts/memoria-de-agente.md) — memória cross-session e search index; [Agent skills](../../../concepts/agent-skills.md) — 90 skills financeiras; [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — 81 tools expostas.
- **Alternativas:** [TauricResearch/TradingAgents](../../github.com/tauricresearch/tradingagents.md) — foco em firma simulada e integridade temporal; [The-Swarm-Corporation/AutoHedge](../../github.com/the-swarm-corporation/autohedge.md) — execução autônoma em Solana; [Fincept-Corporation/FinceptTerminal](../../github.com/fincept-corporation/finceptterminal.md) — terminal desktop nativo.
- **Tecnologias:** Python, FastAPI, React 19, Docker, MCP, LangChain.

## Perguntas abertas

- Os guards paper/live e o mandato são aplicados no código ou apenas declarados no README?
- Qual é o custo médio de uma pesquisa completa com swarm e backtest, em modelos “sweet spot” e “best”?
- Como o Shadow Account separa comportamento do usuário de ruído estatístico?
- Que nível de verificação existe para cada um dos 19 conectores de corretora?
- Como o sistema evita look-ahead nos dados de fontes com datas de publicação ambíguas?
- O servidor MCP exposto em rede mantém a separação de credenciais e a ausência de ferramentas de ordem?
- Qual é a fronteira entre o projeto open-source e os serviços QVeris/OpenSpace promovidos no README?

## Fontes

- README: https://github.com/HKUDS/Vibe-Trading/blob/main/README.md (commit `097b29feab9793e3c302e1a7a4f3c0dac6344904`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório e do perfil da organização: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, datas, release e tópicos).
