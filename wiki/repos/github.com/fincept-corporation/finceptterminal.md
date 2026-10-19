---
type: repo
url: https://github.com/Fincept-Corporation/FinceptTerminal
host: github.com
owner: fincept-corporation
repo: finceptterminal
commit: 3d8617cae3f13c93874d4bee4fb0f2846e9c83bc
license: AGPL-3.0-or-later
language: C++
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [trading, financas, agentes, desktop, qt, cpp, python, mcp, dados]
---

# Fincept-Corporation/FinceptTerminal

> Terminal financeiro desktop nativo em C++20/Qt6 com Python embutido, que reúne analytics institucional, 37 agentes de IA, 100+ conectores de dados, node editor e paper/live trading em um único binário.

## O que é

Fincept Terminal é descrito como uma "state-of-the-art financial intelligence platform" com analytics financeiro de nível institucional, automação por IA e conectividade de dados. A implementação é nativa — C++20, Qt6 e Python 3.11 embutido — em um único binário, sem Electron, Node.js ou runtime de navegador.

O repositório distribui a **edição aberta AGPL-3.0**, voltada a aprendizado, uso pessoal e pesquisa acadêmica, com uma release por mês. A edição **Enterprise** é proprietária, desenvolvida diariamente pela equipe, e atende fundos, family offices e mesas de pesquisa. A comparação do README é explícita: a edição aberta usa fontes públicas e a chave de LLM do próprio usuário, enquanto a Enterprise inclui datasets privados, pesquisa multiagente, roteamento gerenciado de ordens, SSO/SAML, logs de auditoria e SLA.

O projeto se posiciona como alternativa de custo a terminais proprietários: o README compara US$ 180–540 por usuário/ano da Enterprise com cerca de US$ 27 mil por assento de Bloomberg.

## Como funciona

O README descreve duas edições sobre um mesmo núcleo de dados, sem detalhar a arquitetura interna. Os módulos publicados da edição aberta são:

| Área | O que inclui |
| --- | --- |
| **Analytics** | DCF, otimização de portfólio, VaR/Sharpe, precificação de derivativos, renda fixa, alternativos e uma suíte QuantLib de 18 módulos. |
| **IA** | 37 agentes de trader/investidor, economia e geopolítica, com chave própria de OpenAI, Anthropic, Gemini, Groq, DeepSeek, OpenRouter ou Ollama. |
| **Dados** | 100+ conectores, incluindo FRED, IMF, World Bank, DBnomics, AkShare, Polygon, Kraken, Yahoo Finance e APIs governamentais. |
| **Trading** | Feeds de cripto e ações, engine de paper trading e 16 integrações de corretora. |
| **Automação** | Node editor visual, ferramentas MCP e AI Quant Lab com machine learning, descoberta de fatores e reinforcement learning. |
| **Inteligência global** | Rastreamento marítimo, análise geopolítica e mapeamento de relações. |

A edição Enterprise acrescenta 41 módulos em seis frentes (pesquisa agêntica, quant lab e backtesting, pesquisa fundamentalista, mercados e execução, macro e inteligência global, workspace próprio), documentados em um manual de 700 páginas.

## Instalação e uso rápido

A instalação recomendada é por binário da release **v4.5.1**:

| Plataforma | Formato |
| --- | --- |
| Windows x64 | instalador `.exe` |
| Linux x64 | AppImage/instalador `.run`, `.deb` (Debian/Ubuntu) ou `.rpm` (Fedora/RHEL) |
| macOS Apple Silicon | `.dmg` |

Build a partir do código-fonte em Linux/macOS:

```bash
git clone https://github.com/Fincept-Corporation/FinceptTerminal
cd FinceptTerminal
./setup.sh
```

O README fixa a toolchain: CMake 3.27.7, Ninja 1.11.1, Qt 6.8.3 e Python 3.11.9. Versões diferentes são declaradas sem suporte. Instruções de Windows, build manual e troubleshooting ficam em `docs/GETTING_STARTED.md` — arquivo **não lido** nesta ingestão.

## Exemplos de uso

O README não publica comandos de uso do terminal. Os fluxos que ele sugere são de interface: análise fundamentalista (Equity Research), acompanhamento de portfólio, leitura de notícias, construção de automações no node editor e pesquisa com agentes. Qualquer exemplo de linha de comando seria inventado — não há CLI documentada no README.

## Quando usar (e quando não usar)

- **Use quando:** você quer um terminal financeiro desktop nativo, com analytics, dados e agentes no mesmo aplicativo, e aceita trazer sua chave de LLM.
- **Use quando:** o objetivo é aprendizado, uso pessoal ou pesquisa acadêmica sob AGPL-3.0.
- **Use quando:** precisa de paper trading e de conectar uma corretora sem depender de uma plataforma web.
- **Evite quando:** sua organização não pode assumir obrigações de copyleft forte. AGPL-3.0 exige publicar alterações ao distribuir o binário ou ao operá-lo como serviço acessível por terceiros.
- **Evite quando:** você precisa de datasets privados, point-in-time, auditoria, SSO ou SLA — a própria comparação do README empurra esses casos para a Enterprise.
- **Evite quando:** o custo de dados e de tokens de LLM precisa ser previsível. A edição aberta cobra por token, sem teto, e os conectores têm termos próprios.

## Limitações e cuidados

- **Somente o README foi lido.** Código C++/Python, `docs/`, manifestos, testes e a implementação dos agentes, conectores e do engine de paper trading não foram consultados. As capacidades são afirmações do projeto.
- **Divergência de licença entre API e README.** O README declara AGPL-3.0-or-later; a API do GitHub retorna `NOASSERTION`. A página adota o README e registra a divergência.
- **Freemium com edição aberta reduzida.** O README afirma que a edição aberta recebe uma release por mês porque o desenvolvimento diário ocorre na Enterprise. Recursos citados no material promocional (pesquisa multiagente, execução live gerenciada, dados point-in-time) não fazem parte da edição aberta.
- **Preços e planos inconsistentes no próprio README.** O bloco superior do Quantcept anuncia Alpha a US$ 3 e Apex a US$ 8 por 30 dias; a seção "Also from Fincept" repete os valores como US$ 14 e US$ 24. O mesmo ocorre com a descrição de créditos da Enterprise. Trate números comerciais como afirmações datadas e conflitantes.
- **Custo variável.** A edição aberta usa a chave de LLM do usuário, cobrada por token sem teto, além das cotas e termos de cada fonte de dados.
- **Superfície de execução.** Há paper trading e 16 integrações de corretora; o README não detalha limites, kill switch, separação paper/live ou custódia de credenciais. **A verificar** no código e nos docs.
- **Marca registrada.** "Fincept", "Fincept Terminal" e o logo exigem permissão escrita para uso em forks, derivados, rebranding ou produto comercial, mesmo sob AGPL.
- **Sem CLI pública documentada.** O produto é uma aplicação desktop; automação por script não está descrita no README.

## Estado e adoção

- **Versão citada:** v4.5.1, referenciada na tabela de downloads.
- **Atividade e popularidade observadas em 2026-10-19:** ~32,7 mil estrelas, ~4,7 mil forks, 9 issues abertas; criado em 2024-08-29 e último push em 2026-10-13.
- **Licença:** AGPL-3.0-or-later no README; `NOASSERTION` na API do GitHub.
- **Linguagem principal:** C++ (Qt6 + Python embutido).
- **Commit de referência:** `3d8617cae3f13c93874d4bee4fb0f2846e9c83bc`.

## Relações

- **Mantido por:** [Fincept Corporation](../../../entities/fincept-corporation.md).
- **Conceitos:** [Análise financeira multiagente](../../../concepts/analise-financeira-multiagente.md) — 37 agentes, incluindo times de pesquisa na Enterprise; [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — ferramentas MCP na automação; [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md).
- **Alternativas:** [TauricResearch/TradingAgents](../../github.com/tauricresearch/tradingagents.md) — framework de pesquisa em vez de terminal; [HKUDS/Vibe-Trading](../../github.com/hkuds/vibe-trading.md) — workspace CLI/Web/MCP; [The-Swarm-Corporation/AutoHedge](../../github.com/the-swarm-corporation/autohedge.md) — execução autônoma em Solana.
- **Produtos relacionados:** Fincept Data API (500+ endpoints REST, 423 mil instrumentos, 2 mil fontes) e Quantcept (mesa de pesquisa com dados primários, backtests e monitores).

## Perguntas abertas

- A edição aberta realmente contém os 37 agentes e os 100+ conectores, ou parte deles é exclusiva da Enterprise?
- Como paper e live trading são separados, e quais limites de risco existem no código aberto?
- A licença efetiva é AGPL-3.0-or-later, como diz o README, ou há restrição adicional não capturada pela API?
- Qual é o custo real de uma sessão de pesquisa com 37 agentes em modelos de fronteira?
- Como o Python embutido é isolado do processo C++ e das credenciais de corretora?
- Quais conectores funcionam sem chave paga e com que cobertura histórica?
- Qual é a fronteira entre o terminal open-source, a Enterprise, a Data API e o Quantcept?

## Fontes

- README: https://github.com/Fincept-Corporation/FinceptTerminal/blob/main/README.md (commit `3d8617cae3f13c93874d4bee4fb0f2846e9c83bc`, consultado em 2026-10-19). Somente o README foi lido; `docs/` e os demais arquivos do repositório não foram consultados.
- Metadados do repositório e da organização: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas e tópicos).
