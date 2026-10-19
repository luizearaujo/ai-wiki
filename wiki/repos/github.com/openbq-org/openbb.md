---
type: repo
url: https://github.com/openbq-org/OpenBB
host: github.com
owner: openbq-org
repo: openbb
commit: 78020ee4b864ab50b8c1f56373877c2b4e7fb623
license: Apache-2.0
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [financas, dados, mcp, agentes, plataforma]
---

# openbq-org/OpenBB

> Open Data Platform que integra fontes de dados financeiros proprietárias, licenciadas e públicas uma única vez e as expõe a Python, Excel, OpenBB Workspace, servidores MCP para agentes de IA e API REST.

## O que é

O OpenBB (Open Data Platform, ODP) ataca o problema de conectar dados financeiros fragmentados — bolsas, corretoras, provedores proprietários, fontes públicas — a múltiplas superfícies de consumo sem reimplementar a integração em cada uma. A proposta é "connect once, consume everywhere": o mesmo backend de dados alimenta ambientes Python para quants, OpenBB Workspace/Excel para analistas, servidores MCP para agentes de IA e APIs REST para outras aplicações.

**Nota de proveniência:** a URL historicamente usada para este projeto, `openbb-finance/openbb`, foi transferida/renomeada; a API do GitHub redireciona para a organização atual, `openbq-org`. Esta página documenta o repositório no destino do redirecionamento.

## Como funciona

- **ODP Python package:** `pip install openbb` expõe `from openbb import obb` com namespaces por domínio (ex.: `obb.equity.price.historical("AAPL")`), convertível para `pandas.DataFrame`.
- **Backend FastAPI:** o comando `openbb-api` sobe um servidor Uvicorn/FastAPI local (`127.0.0.1:6900`) que expõe os mesmos dados via REST.
- **OpenBB Workspace:** UI enterprise separada (`pro.openbb.co`) que consome o backend ODP — conectado via "Connect backend" com nome e URL — e permite anexar agentes de IA próprios através do repositório `agents-for-openbb`.
- **Integrações de dados:** repositórios irmãos citados incluem `backends-for-openbb` (template para trazer dados próprios) e `agents-for-openbb`/`openbb-ai` (SDK para agentes compatíveis com o Workspace).
- **CLI:** `pip install openbb-cli` adiciona uma interface de linha de comando sobre a mesma plataforma de dados.

## Instalação e uso rápido

```bash
pip install openbb
```

```python
from openbb import obb
output = obb.equity.price.historical("AAPL")
df = output.to_dataframe()
```

Conectar ao OpenBB Workspace:

```bash
pip install openbb
openbb-api   # sobe o backend em 127.0.0.1:6900
```

No Workspace: Apps → Connect backend → Nome e URL (`http://127.0.0.1:6900`) → Test → Add.

CLI dedicada: `pip install openbb-cli`.

## Exemplos de uso

Exemplo publicado no README, acessando preço histórico de uma ação:

```python
from openbb import obb
output = obb.equity.price.historical("AAPL")
df = output.to_dataframe()
```

O catálogo completo de integrações de dados está em `docs.openbb.co/python/reference` (não consultado por esta página).

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é centralizar acesso a dados financeiros (equities, crypto, derivativos, economia, renda fixa) a partir de Python, Excel, um agente de IA via MCP ou uma aplicação própria via REST, sem reimplementar cada integração.
- **Evite quando:** a necessidade é só uma fonte de dados isolada e simples — adicionar o ODP inteiro pode ser desproporcional; ou quando decisões de investimento dependem só dos dados do ODP sem validação independente — o README adverte explicitamente que "os dados contidos na Open Data Platform não são necessariamente precisos" e que trading envolve risco de perda total.

## Limitações e cuidados

- **Somente o README foi lido.** Código-fonte, integrações de dados específicas, o SDK de agentes (`openbb-ai`) e o backend FastAPI não foram inspecionados.
- O README é explícito sobre risco financeiro: "trading in financial instruments involves high risks including the risk of losing some, or all, of your investment amount."
- A precisão dos dados não é garantida pelo próprio projeto; cada provedor de dados mantém seus próprios termos.
- A organização e o nome do repositório mudaram (de `openbb-finance` para `openbq-org`); comandos e links publicados em outros lugares da internet podem ainda referenciar o nome antigo.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~74,5 mil estrelas, ~7,7 mil forks, 98 issues abertas; criado em 2020-12-20, último push em 2026-10-18.
- **Licença:** Apache-2.0, segundo o README (a API do GitHub não detectou o arquivo de licença automaticamente).
- **Linguagem principal:** Python; branch padrão `develop`.
- Pacotes publicados no PyPI: `openbb` e `openbb-cli`.

## Relações

- **Mantido por:** [openbq-org](../../../entities/openbq-org.md) (anteriormente organização `openbb-finance`).
- **Conceitos:** [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — servidores MCP citados como uma das superfícies de consumo para agentes de IA.
- **Relacionado a:** outros projetos de análise financeira com agentes documentados nesta wiki, como [TauricResearch/TradingAgents](../tauricresearch/tradingagents.md) e [Fincept-Corporation/FinceptTerminal](../fincept-corporation/finceptterminal.md) — nesses, o agente decide e simula operações; no OpenBB, a plataforma fornece os dados que um agente externo consome.

## Perguntas abertas

- O que motivou a transferência de `openbb-finance` para `openbq-org`, e como isso afeta integrações existentes?
- Quais ferramentas exatas um servidor MCP do ODP expõe a um agente de IA?
- Como a plataforma trata atualização, versionamento e confiabilidade de cada fonte de dados individual?

## Fontes

- README: https://github.com/openbq-org/OpenBB (commit `78020ee4b864ab50b8c1f56373877c2b4e7fb623`, consultado em 2026-10-19). Somente o README foi lido; código-fonte, `backends-for-openbb`, `agents-for-openbb` e a documentação em docs.openbb.co não foram consultados.
- Metadados do repositório: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas); redirecionamento de `openbb-finance/openbb` confirmado via `api.github.com/repos/openbb-finance/openbb` (HTTP 301, `Location` apontando para o id do repositório atual).
- Perfil da organização: API do GitHub (`orgs/openbq-org`) em 2026-10-19.
