---
type: repo
url: https://github.com/browser-use/browser-use
host: github.com
owner: browser-use
repo: browser-use
commit: aa093a843da5edbf323c0b4145c9b6a0db3ecde8
license: MIT
language: Python
status: active
created: 2026-10-22
ingested: 2026-10-22
updated: 2026-10-22
tags: [agentes, navegador, automacao-web]
---

# browser-use/browser-use

> Biblioteca Python (e CLI) open source que dá a um agente LLM controle de um navegador real, local ou em nuvem, para navegar na web como um humano faria.

## O que é

Browser Use resolve o problema de automatizar tarefas que só existem na interface web — agendar um compromisso, resolver um CAPTCHA, preencher um formulário — guiando um browser real por um agente que decide a cada passo. O README oferece três caminhos de uso: API totalmente hospedada (Browser Use Cloud), CLI que dá a um agente existente (Claude Code, Codex, Cursor etc.) acesso ao navegador, e biblioteca Python para rodar o agente no próprio código.

## Como funciona

A classe central é `Agent(task=..., llm=..., tools=...)`, que recebe uma tarefa em linguagem natural e um LLM (qualquer provedor, com preferência declarada pelo modelo próprio `BU2`, otimizado para automação de navegador). O agente abre um navegador — local ou, com `Browser(use_cloud=True)`, um navegador hospedado na nuvem com stealth, proxies residenciais e resolução de CAPTCHA — e executa o loop de navegação até concluir a tarefa, retornando o resultado via `history.final_result()`.

Browser Use também expõe um toolset para o SDK da Anthropic: implementa as 31 ações de navegador do "browser tool" do Claude e inclui uma ferramenta Bash, usados através de `client.beta.messages.tool_runner`.

## Instalação e uso rápido

- **Biblioteca Python** (requer Python ≥3.11): `uv add browser-use`, chave de LLM em `.env` (ex. `OPENAI_API_KEY`), script com `Agent(task=..., llm=...)` e `uv run agent.py`.
- **CLI**: instruir um agente existente (Claude Code, Codex, Hermes, OpenClaw) a instalar e rodar `browser-use skill install`.
- **Cloud**: obter uma API key em `cloud.browser-use.com` (créditos gratuitos no cadastro) e chamar a API hospedada diretamente.

## Exemplos de uso

- Encontrar um horário disponível, escolher data e resolver CAPTCHA para agendar uma prova de direção — demo citada no README.
- Registrar uma ferramenta customizada (`@tools.action`) para o agente consultar, por exemplo, a hora atual em UTC — exemplo do README.
- Usar `ChatBrowserUse(model='anthropic/claude-sonnet-4-6')` ou `'google/gemini-3-pro'` para rodar outros provedores através do gateway da Browser Use.

## Quando usar (e quando não usar)

- **Use quando:** a tarefa só existe na UI web (sem API), exige decisão passo a passo (preencher formulário, navegar por menus) ou precisa rodar em CI/serverless sem instalar Chrome (via navegador em nuvem).
- **Evite quando:** existe API oficial ou feed estático para o mesmo dado — o README recomenda a biblioteca como "última milha", não primeiro recurso (mesmo critério já registrado no conceito [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md)).

## Limitações e cuidados

- Resolução de CAPTCHA e redução de detecção de bots dependem do site e do desafio; o README não garante sucesso em todos os casos.
- Sincronização de perfil (cookies) para navegador em nuvem não transfere local storage, IndexedDB nem extensões — alguns sites exigem novo login.
- O toolset para Claude exige uma versão do SDK Anthropic com `anthropic.tools.browser` e host Linux/macOS (ou WSL) para a ferramenta Bash.
- Apenas o README foi lido; repositórios relacionados (Browser Harness, Cloud SDK, Benchmark) não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: biblioteca Python no PyPI; última release no GitHub, `0.13.13` (2026-10-15).
- Atividade e popularidade observadas em 2026-10-22: 118.843 estrelas, 13.196 forks (GitHub API); push em 2026-10-20.
- Licença: MIT (biblioteca Python); serviços de modelo e navegador em nuvem são pagos separadamente.

## Relações

- Mantido por: [Browser Use](../../../entities/browser-use.md).
- Conceitos: [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md).
- Alternativas: [jo-inc/camofox-browser](../jo-inc/camofox-browser.md), [vercel-labs/agent-browser](../vercel-labs/agent-browser.md) — mesma classe de problema (browser real controlado por agente), com ênfases diferentes: Browser Use foca no agente de alto nível (`Agent`, modelo BU2, benchmark próprio); os outros dois são CLIs/servidores mais próximos de uma camada de automação pura.

## Perguntas abertas

- Como o modelo proprietário BU2 se compara a modelos genéricos (GPT, Claude, Gemini) em tarefas de navegação fora do benchmark próprio da empresa?
- Qual é a cobertura real de stealth/anti-detecção do navegador em nuvem fora dos casos de demonstração?

## Fontes

- README: https://raw.githubusercontent.com/browser-use/browser-use/aa093a843da5edbf323c0b4145c9b6a0db3ecde8/README.md (commit `aa093a843da5edbf323c0b4145c9b6a0db3ecde8`, consultado em 2026-10-22). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
