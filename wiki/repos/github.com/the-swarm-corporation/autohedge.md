---
type: repo
url: https://github.com/The-Swarm-Corporation/AutoHedge
host: github.com
owner: the-swarm-corporation
repo: autohedge
commit: c549c7950da112286e76725d49f6a25de8fa99bd
license: MIT
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [trading, financas, multiagente, solana, agentes, swarms, execucao]
---

# The-Swarm-Corporation/AutoHedge

> Sistema autônomo de hedge fund que encadeia agentes especializados — direção, quant, risco e execução — para analisar o mercado e operar em Solana com mínima intervenção humana.

## O que é

AutoHedge se apresenta como um "autonomous agent hedge fund" de nível empresarial, construído para "rodar análise contínua, gerar e validar teses de trading, dimensionar risco e executar ordens". O README descreve quatro agentes em um pipeline fixo e declara suporte atual a **trading autônomo completo em Solana**, com Coinbase e outras exchanges no roadmap.

O público declarado são instituições e desenvolvedores que querem um framework extensível de agentes financeiros, com saídas estruturadas, logging detalhado e arquitetura "risk-first". O projeto é mantido pela [The Swarm Corporation](../../../entities/the-swarm-corporation.md) e usa o framework de agentes Swarms.

## Como funciona

O pipeline publicado no README:

```text
Director Agent -> Quant Agent -> Risk Manager -> Execution Agent -> Trade Output
```

| Agente | Responsabilidade declarada |
| --- | --- |
| **Director** | Gerar estratégia e tese de trading. |
| **Quant** | Análise técnica e estatística. |
| **Risk Management** | Dimensionamento de posição e avaliação de risco. |
| **Execution** | Gerar e executar ordens. |

O README também cita análise de mercado em tempo real, saídas em JSON para sistemas a jusante, logging configurável para auditoria e depuração, e design modular para novas estratégias e venues. Não há detalhamento de como o estado passa entre os agentes, como o risco veta uma ordem ou como falhas de execução são tratadas.

## Instalação e uso rápido

```bash
pip install -U autohedge
```

Variáveis de ambiente listadas no README:

| Variável | Uso declarado |
| --- | --- |
| `JUPITER_API_KEY` | Preços e busca de tokens via Jupiter. |
| `OPENAI_API_KEY` / `ANTHROPIC_API_KEY` | Agentes experimentais. |
| `WORKSPACE_DIR` | Diretório de trabalho (`agent_workspace` por padrão). |
| `WALLET_PRIVATE_KEY` | Chave privada da carteira usada para operar. |

O uso básico publicado é apenas:

```bash
autohedge
```

O README não documenta flags, arquivos de configuração, formato da tese ou como selecionar estratégias.

## Exemplos de uso

Exemplos derivados do README — não são instruções oficiais além do que ele publica.

- Rodar o pipeline com as variáveis configuradas: `autohedge`.
- Estender o framework com novas estratégias ou venues, aproveitando o design modular citado.

Não há exemplo de definição de estratégia, backtest ou simulação.

## Quando usar (e quando não usar)

- **Use quando:** você quer estudar ou prototipar um pipeline autônomo de trading multiagente em Solana, com separação explícita entre tese, quant, risco e execução.
- **Use quando:** precisa de um ponto de partida em Python sobre o framework Swarms para agentes financeiros.
- **Evite quando:** o objetivo é operar capital real. O README não publica backtest, métricas de desempenho, política de risco verificável nem mecanismos de parada; a afirmação de "enterprise-grade" é do próprio projeto.
- **Evite quando:** você precisa de mercados tradicionais ou de múltiplas venues — apenas Solana é suportado hoje.
- **Evite quando:** não há como proteger uma chave privada de carteira. O README instrui a colocá-la em variável de ambiente, sem detalhar custódia, limites ou isolamento.

## Limitações e cuidados

- **Somente o README foi lido.** Código, configuração, testes, estratégias e documentação interna não foram consultados. A implementação real do pipeline e dos controles de risco é **A verificar**.
- **README curto e promocional.** São 123 linhas, sem arquitetura detalhada, sem resultados de backtest e sem evidência de desempenho.
- **Execução autônoma em blockchain.** Ordens são irreversíveis; erros de dimensionamento, slippage ou chave comprometida têm consequência financeira direta.
- **Chave privada em ambiente.** `WALLET_PRIVATE_KEY` em variável de ambiente é um modelo de custódia frágil; não há menção a hardware wallet, multisig, limites por operação ou kill switch.
- **Escopo restrito.** Solana é a única venue suportada; Coinbase e outras exchanges aparecem apenas como "coming soon" e "roadmap".
- **Sem sinal de paper trading.** O README descreve execução, não simulação; testar sem risco não está documentado.
- **Atividade.** O último push observado é de 2026-05-11; a página registra o estado nessa data, não uma garantia de manutenção contínua.

## Estado e adoção

- **Versão/releases citadas no README:** nenhuma. Não há seção de releases nem changelog.
- **Atividade e popularidade observadas em 2026-10-19:** ~6,4 mil estrelas, ~925 forks, 26 issues abertas; criado em 2024-12-10; último push em 2026-05-11.
- **Licença:** MIT.
- **Linguagem principal:** Python.
- **Commit de referência:** `c549c7950da112286e76725d49f6a25de8fa99bd`.

## Relações

- **Mantido por:** [The Swarm Corporation](../../../entities/the-swarm-corporation.md).
- **Conceitos:** [Análise financeira multiagente](../../../concepts/analise-financeira-multiagente.md) — variante orientada a execução; [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — pipeline com papéis fixos.
- **Alternativas:** [TauricResearch/TradingAgents](../../github.com/tauricresearch/tradingagents.md) — foco em pesquisa e decisão simulada; [HKUDS/Vibe-Trading](../../github.com/hkuds/vibe-trading.md) — workspace de pesquisa com execução limitada por mandato; [Fincept-Corporation/FinceptTerminal](../../github.com/fincept-corporation/finceptterminal.md) — terminal desktop com agentes e trading paper/live.
- **Tecnologias:** Python, framework Swarms, Jupiter, Solana.

## Perguntas abertas

- Como o Risk Manager veta ou redimensiona uma ordem gerada pelo Quant, e quais limites são configuráveis?
- O pipeline usa dados históricos para backtest ou apenas dados ao vivo?
- Existe modo paper/simulação antes da execução em Solana?
- Como a chave privada é isolada do processo do agente, e há suporte a multisig ou limites por transação?
- Qual é o comportamento em falha parcial de execução, slippage extremo ou indisponibilidade da RPC?
- O que "estruturado para instituições" significa em termos de auditoria, permissões e compliance?

## Fontes

- README: https://github.com/The-Swarm-Corporation/AutoHedge/blob/main/README.md (commit `c549c7950da112286e76725d49f6a25de8fa99bd`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório e do perfil da organização: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, datas e descrição).
