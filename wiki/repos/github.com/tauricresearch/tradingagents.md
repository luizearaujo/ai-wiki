---
type: repo
url: https://github.com/TauricResearch/TradingAgents
host: github.com
owner: tauricresearch
repo: tradingagents
commit: e8f5503e9b86d5c2710b0c76b1f686703968c9df
license: Apache-2.0
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [trading, financas, multiagente, langgraph, llm, pesquisa, agentes]
---

# TauricResearch/TradingAgents

> Framework multiagente em LangGraph que simula a estrutura de uma firma de trading — analistas, pesquisadores, trader, risco e gestor de portfólio — para produzir decisões de investimento com LLMs e dados de mercado.

## O que é

TradingAgents organiza uma análise de mercado como uma **firma de trading**: agentes especializados avaliam condições, debatem teses e submetem uma proposta de operação a uma cadeia de risco e aprovação. O README posiciona o projeto como framework de **pesquisa**, não como produto de investimento: desempenho varia com modelo, temperatura, período, qualidade dos dados e outros fatores não determinísticos, e o resultado não constitui aconselhamento financeiro.

O projeto é mantido pela [Tauric Research](../../../entities/tauricresearch.md) e acompanha o paper *TradingAgents: Multi-Agents LLM Financial Trading Framework* (arXiv 2412.20138, autores Yijia Xiao, Edward Sun, Di Luo e Wei Wang). O README está traduzido em oito idiomas e o projeto tem comunidade em Discord e X.

O público é quem quer estudar ou experimentar análise financeira multiagente: pesquisadores, desenvolvedores e entusiastas que aceitam configurar provedores de modelo, chaves de dados e um ambiente Python.

## Como funciona

O fluxo descrito no README:

1. **Time de analistas.** Quatro papéis — fundamentos, sentimento, notícias e técnico — trabalham **em paralelo**, cada um com suas ferramentas. O analista de sentimento agrega manchetes, StockTwits e Reddit; o técnico usa indicadores como MACD e RSI; o de fundamentos avalia demonstrações e métricas; o de notícias interpreta eventos macro.
2. **Debate de pesquisa.** Quando todos os relatórios chegam, pesquisadores **bullish** e **bearish** confrontam as teses em rodadas estruturadas, equilibrando ganhos e riscos.
3. **Trader.** Compõe os relatórios em uma decisão, com timing e magnitude da operação.
4. **Risco e portfólio.** O time de risco avalia volatilidade, liquidez e outros fatores e envia um parecer ao gestor de portfólio, que aprova ou rejeita a proposta. Se aprovada, a ordem vai para uma exchange simulada.

A orquestração usa **LangGraph**, com estado compartilhado e nós por etapa. O README distingue dois modelos: um **quick** para analistas, pesquisadores, debatedores e trader, e um **deep** para os gestores de pesquisa e de portfólio. Cada camada pode usar um provedor diferente.

### Integridade temporal dos dados

O README dedica espaço incomum ao problema de **look-ahead**. O projeto trata datas de análise como cortes de informação:

- Demonstrações de empresas americanas vêm do **SEC EDGAR**, que registra a data de protocolo de cada figura. Uma análise datada no passado lê os números como estavam naquele dia; uma figura reexpressa depois continua com o valor original. Exemplo do README: o total de ativos da Apple em 2008 foi protocolado como US$ 39,6 bi e reexpresso para US$ 36,2 bi em 2010; uma análise entre as duas datas lê US$ 39,6 bi.
- Demonstrações de outras empresas vêm do Yahoo Finance, que data pelo período coberto, não pela publicação; em análises passadas, o projeto as **retém** em vez de arriscar look-ahead.
- Negociações de insiders são datadas pelo evento, não pelo protocolo, e também são retidas em análises passadas.
- EDGAR exige identificação do chamador; o projeto envia um contato padrão e permite configurar `SEC_EDGAR_USER_AGENT`.
- EDGAR cobre arquivos legíveis por máquina desde 2009; o quarto trimestre é reportado como indisponível em vez de derivado, porque só aparece dentro do número anual.

### Portfólio e memória

- **Portfólio opcional.** Por padrão, os agentes não sabem o que o usuário detém e escrevem para um leitor genérico. Um `PortfolioContext` com caixa, moeda e posições faz trader, risco e gestor trabalharem contra a carteira real. Lista de posições vazia significa carteira zerada; ausência de portfólio não é o mesmo que carteira zerada.
- **Memory log sempre ativo.** Cada execução concluída acrescenta sua decisão a `~/.tradingagents/memory/trading_memory.md`. Em execuções posteriores, enquanto os analistas trabalham, o sistema **liquida** decisões cujo horizonte venceu: busca o retorno realizado, bruto e alfa contra o benchmark regional, e gera uma reflexão de um parágrafo. O gestor de portfólio lê as decisões recentes do mesmo ticker e lições de outros tickers. Se a liquidação falha, a execução continua e o relatório informa.
- **Checkpoint resume opt-in.** Com `--checkpoint`, o LangGraph grava estado após cada nó; uma execução interrompida retoma do último passo. Os checkpoints ficam em SQLite por ticker e são apagados ao concluir com sucesso.

### Backtesting e reprodutibilidade

`run_backtest` executa o mesmo pipeline sobre uma grade de tickers e datas, grava em um memory log próprio e pontua as decisões cujo horizonte já negociou. Cada célula é avaliada por **alfa realizado** contra o benchmark regional e agrupada por rating. A entrada ocorre no primeiro fechamento após a data da decisão, porque a execução lê notícias publicadas depois do fechamento daquele dia. Reexecutar a mesma grade com o mesmo `run_id` pula células já feitas.

O README é explícito sobre variação entre execuções: amostragem de LLM não é determinística, modelos de raciocínio variam mais, e fontes ao vivo (notícias, StockTwits, Reddit) mudam com o tempo mesmo para uma data histórica fixa. Reduzir temperatura ajuda apenas em modelos que a respeitam. O que o projeto tornou determinístico: a identidade da empresa é resolvida antes de qualquer agente, e o analista de mercado ancora preços e indicadores em um snapshot verificado. Resultados de backtest **não** são garantidos contra nenhuma cifra publicada.

## Instalação e uso rápido

Pré-requisito: Python 3.11 ou superior. O README sugere conda ou uv:

```bash
git clone https://github.com/TauricResearch/TradingAgents.git
cd TradingAgents
conda create -n tradingagents python=3.13
conda activate tradingagents
pip install .
```

Alternativa com Docker:

```bash
cp .env.example .env   # preencher chaves
docker compose run --rm tradingagents
```

O Docker mantém resultados, relatórios, memory log e cache no volume `tradingagents_data`; `TRADINGAGENTS_DATA_DIR` aponta para uma pasta do host.

Chaves são necessárias para o provedor de modelo escolhido (OpenAI, Google, Anthropic, xAI, DeepSeek, Qwen, GLM, MiniMax, OpenRouter, Mistral, Kimi, Groq, NVIDIA etc.), além de fontes opcionais como FRED, Alpha Vantage e TypeSafe. Também há suporte a Azure OpenAI, Bedrock, Ollama local, qualquer endpoint compatível com OpenAI e login na assinatura ChatGPT Plus/Pro.

```bash
tradingagents   # CLI interativo
python -m cli.main
```

Modo não interativo:

```bash
export TRADINGAGENTS_LLM_PROVIDER=openai TRADINGAGENTS_QUICK_THINK_LLM=gpt-6-luna TRADINGAGENTS_DEEP_THINK_LLM=gpt-6-sol
tradingagents --ticker NVDA --date 2026-09-23 --analysts market,news,fundamentals --save --no-show
```

O CLI aceita tickers de qualquer mercado coberto pelo Yahoo Finance, com sufixo de exchange: `AAPL`/`SPY` (EUA), `0700.HK`, `7203.T`, `AZN.L`, `RELIANCE.NS`, `.TO`, `.AX`, `600519.SS` (A-shares), `BTC-USD` (cripto).

## Exemplos de uso

Exemplos derivados do README — não são instruções oficiais além do que ele publica.

Uso como biblioteca:

```python
from tradingagents.graph.trading_graph import TradingAgentsGraph
from tradingagents.default_config import DEFAULT_CONFIG

ta = TradingAgentsGraph(debug=True, config=DEFAULT_CONFIG.copy())

state, decision = ta.propagate("NVDA", "2026-09-01")
print(decision)

ta.save_reports(state, "NVDA")
```

Configuração de modelos e rodadas:

```python
config = DEFAULT_CONFIG.copy()
config["llm_provider"] = "openai"
config["deep_think_llm"] = "gpt-6-sol"
config["quick_think_llm"] = "gpt-6-luna"
config["max_debate_rounds"] = 2

ta = TradingAgentsGraph(debug=True, config=config)
_, decision = ta.propagate("NVDA", "2026-09-01")
```

Com carteira real:

```python
from tradingagents.portfolio import PortfolioContext

portfolio = PortfolioContext.model_validate({
    "cash": 25000.0,
    "currency": "USD",
    "positions": [{"ticker": "NVDA", "quantity": 120, "average_price": 150.0}],
})
_, decision = ta.propagate("NVDA", "2026-09-01", portfolio=portfolio)
```

Backtest:

```bash
tradingagents backtest NVDA,AAPL --start 2026-06-01 --end 2026-08-01 --every 7
```

## Quando usar (e quando não usar)

- **Use quando:** você quer estudar análise financeira multiagente, comparar modelos ou testar a arquitetura de debate e risco em cenários históricos.
- **Use quando:** precisa de um pipeline que respeite datas de publicação de dados e permita backtest com grade de datas.
- **Use quando:** quer um exemplo de orquestração LangGraph com papéis, estado compartilhado, memória e checkpoints.
- **Evite quando:** você espera uma estratégia de investimento pronta ou retorno reproduzível. O próprio README diz que resultados de backtest não são garantidos e que o framework é um scaffold de pesquisa.
- **Evite quando:** você não pode configurar chaves de provedores, credenciais de dados ou revisar o custo de várias chamadas de LLM por análise.
- **Evite quando:** o uso pretendido é operar capital real sem supervisão; o projeto envia ordens a uma exchange **simulada** e não é aconselhamento financeiro.

## Limitações e cuidados

- **Somente o README foi lido.** Código, `CHANGELOG.md`, `tradingagents/default_config.py`, docs e testes não foram consultados. Comportamento interno, cobertura de testes e qualidade das decisões são **a verificar**.
- **Firma simulada.** A exchange é simulada; o projeto não se conecta a corretoras reais pelo que o README descreve.
- **Custo e latência.** Cada análise dispara múltiplas chamadas a modelos, em vários papéis e rodadas de debate; o custo cresce com profundidade de pesquisa, número de analistas e rodadas.
- **Dados de terceiros.** Yahoo Finance, SEC EDGAR, StockTwits, Reddit, FRED, Alpha Vantage e outros provedores têm termos, limites e lacunas próprios. O README trata retenção de dados indisponíveis, mas não garante cobertura universal.
- **Não determinismo.** Mesmo com temperatura baixa, modelos de raciocínio variam; o README recomenda tratar a variação como esperada, não como defeito.
- **Assinatura ChatGPT.** Usar o plano Plus/Pro conta contra os limites de uso e não aceita `temperature` ou `max_tokens`.
- **Update check e telemetria.** O CLI interativo verifica no máximo uma vez por dia se há versão nova e envia "nada sobre suas execuções", segundo o README; `TRADINGAGENTS_NO_UPDATE_CHECK=1` desliga. Execuções sem terminal não verificam.
- **Licença Apache-2.0** permite uso comercial, mas não remove a responsabilidade por compliance de dados e por decisões tomadas com a saída.

## Estado e adoção

- **Versão citada:** v0.7.0 (outubro de 2026), com backtest pontuado a partir do primeiro fechamento após cada decisão, aviso de nova release e wheel por release. O README lista releases desde v0.2.0 e o paper de 2024.
- **Atividade e popularidade observadas em 2026-10-19:** ~112 mil estrelas e ~21,6 mil forks na API do GitHub; criado em 2024-12-28; último push em 2026-10-16.
- **Licença:** Apache-2.0.
- **Linguagem principal:** Python.
- **Commit de referência:** `e8f5503e9b86d5c2710b0c76b1f686703968c9df`.

## Relações

- **Mantido por:** [Tauric Research](../../../entities/tauricresearch.md).
- **Conceitos:** [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — papéis, debate e supervisão; [Memória de agente](../../../concepts/memoria-de-agente.md) — memory log com liquidação e reflexão; [Análise financeira multiagente](../../../concepts/analise-financeira-multiagente.md) — conceito que o projeto operacionaliza.
- **Alternativas:** plataformas de backtesting determinístico (por exemplo, vectorbt, Backtrader, Zipline) para estratégias com regras fixas; agentes de análise financeira single-agent não documentados nesta wiki.
- **Tecnologias:** LangGraph, SEC EDGAR, Yahoo Finance, Docker.

## Perguntas abertas

- Como o debate bullish/bearish termina — por rodadas fixas, consenso ou decisão de um manager?
- Qual é o custo médio e a latência de uma análise com os modelos e a profundidade padrão?
- Como o memory log evita contaminar análises futuras com reflexões geradas pelo próprio modelo?
- A liquidação de decisões usa que horizonte de holding, e ele é configurável?
- Quão estável é o alfa realizado em backtests fora do período e dos tickers usados no paper?
- O projeto tem testes de integridade temporal que cubram todos os provedores, ou apenas EDGAR?
- Qual é a fronteira entre o framework open-source e eventuais serviços da Tauric Research?

## Fontes

- README: https://github.com/TauricResearch/TradingAgents/blob/main/README.md (commit `e8f5503e9b86d5c2710b0c76b1f686703968c9df`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, datas).
- Paper citado pelo README: https://arxiv.org/abs/2412.20138 (não consultado diretamente nesta ingestão).
