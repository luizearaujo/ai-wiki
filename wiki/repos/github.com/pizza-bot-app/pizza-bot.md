---
type: repo
url: https://github.com/pizza-bot-app/pizza-bot
host: github.com
owner: pizza-bot-app
repo: pizza-bot
commit: bb9ce39a23718e7c9e515b4b52d04f0d03bada93
license: Apache-2.0
language: TypeScript
status: active
created: 2026-10-24
ingested: 2026-10-24
updated: 2026-10-24
tags: [email-para-agentes, agent-skills, mcp, orquestracao-multiagente]
---

# pizza-bot-app/pizza-bot

> Inbox local-first para trabalho de IA de longa duração: inicie ou agende uma tarefa, afaste-se, e volte a um "Unread" com trabalho concluído e a um "Action" com decisões pendentes.

## O que é

Pizza Bot foi desenvolvido na Amazon e tenta resolver o problema de acompanhar agentes que trabalham em segundo plano por tempo indeterminado. Em vez de uma janela de chat síncrona, organiza o trabalho em filas: conversas concluídas caem em **Unread**, aprovações duráveis (human-in-the-loop) caem em **Action**, e o usuário pode trocar de conversa sem interromper execuções em curso.

## Como funciona

Um runtime stateful sobre **DeepAgents/LangGraph** serve a mesma experiência React tanto no app desktop (Electron) quanto no browser; desktop, app web e CLI de terminal falam com um `api-server` via HTTP/SSE, e só esse processo precisa ficar de pé para o agente continuar trabalhando. Execuções fazem checkpoint e sobrevivem à desconexão do cliente; gatilhos de cron ou webhook podem iniciar trabalho sem uma conversa aberta. Skills tornam-se subagentes com escopo de ferramentas, com progresso visível no painel de Activity; uma skill customizada pode substituir uma Built-in ou de Plugin com o mesmo id sem alterar o original.

Provedores de modelo suportados: Amazon Bedrock (perfil AWS, chaves de acesso ou Bedrock API key), Anthropic, Google Gemini, OpenAI, OpenRouter, Requesty e Ollama — selecionáveis via `PIZZA_MODEL=<provider>:<id>`.

## Instalação e uso rápido

Requer Node.js 24+:

```bash
npm install
npm run build
npm run dev
```

`npm run dev` inicia o frontend Vite e o shell Electron, que por sua vez sobe e supervisiona seu próprio `api-server`. Também há instaladores empacotados por release (`.dmg`/`.zip` para macOS assinados e notarizados, `-setup.exe` para Windows, `.deb`/`.rpm` para Linux não assinados) e um modo de backend standalone (Docker/Compose/Kubernetes) para Electron remoto, browsers ou containers.

## Exemplos de uso

- Adicionar servidores MCP pela UI ou em `<PIZZA_DATA_ROOT>/.mcp.json`.
- Adicionar Agent Skills em `<PIZZA_DATA_ROOT>/skills`, ou instalar plugins que empacotam MCP + skills juntos.
- A skill Built-in "Pizza Bot Guide" explica recursos, sugere workflows e aponta para a documentação do projeto.

## Quando usar (e quando não usar)

- **Use quando:** quiser um inbox local-first e assíncrono para trabalho de agente de longa duração, com aprovações humanas, múltiplos provedores de modelo e extensão por skills/MCP.
- **Evite quando:** precisar de uma solução multiusuário/multi-tenant hospedada — o design é local-first por padrão, com o `api-server` ligado em `127.0.0.1` e autenticação exigida apenas para bind não-loopback.

## Limitações e cuidados

- Acesso a pastas locais exige concessão explícita em **Settings > Files**; por padrão, o Pizza Bot não tem acesso ao diretório home.
- Servidores MCP e plugins são tratados como confiáveis: seus comandos podem executar com as permissões do usuário — o README recomenda instalar só fontes confiáveis.
- Estado da aplicação (threads, checkpoints, memórias, anexos, logs) fica local em `<PIZZA_DATA_ROOT>` (`~/.pizza-bot-oss` por padrão); requisições de modelo/ferramenta vão para os provedores configurados.
- **A verificar:** o README não detalha o modelo de dados do checkpoint nem a política de retenção de logs além do que está em `docs/LOGGING.md` (não lido nesta ingestão).

## Estado e adoção

- Observado em 2026-10-24: 521 stars, 55 forks, 26 issues abertas, push mais recente em 2026-10-21.
- Contribuidores citados no README (Executive/Sous Chefs) e mais de 2.000 usuários internos da Amazon que testaram versões anteriores, segundo o próprio README.
- Licença: Apache-2.0.

## Relações

- Mantido por: [pizza-bot-app](../../../entities/pizza-bot-app.md).
- Conceitos: [Email para agentes](../../../concepts/email-para-agentes.md) — mesmo padrão de "inbox como interface de agente", mas local-first/Electron em vez de cloud/Workers, e sem foco específico em e-mail; [Agent skills](../../../concepts/agent-skills.md); [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md); [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — skills como subagentes com escopo de ferramentas.
- Alternativas: [cloudflare/agentic-inbox](../cloudflare/agentic-inbox.md) — inbox de e-mail self-hosted em Cloudflare Workers, cloud-first, com isolamento por mailbox em vez de local-first por desktop.

## Perguntas abertas

- Como o checkpoint do LangGraph se comporta em runs muito longos (horas/dias) em termos de custo de armazenamento?
- Qual é o modelo de autorização quando o `api-server` roda remotamente (Electron remoto, browsers, containers) além do que `docs/STANDALONE_BACKEND.md` descreve?
- Há algum limite declarado de skills/subagentes simultâneos por run?

## Fontes

- README: https://raw.githubusercontent.com/pizza-bot-app/pizza-bot/bb9ce39a23718e7c9e515b4b52d04f0d03bada93/README.md (commit `bb9ce39a23718e7c9e515b4b52d04f0d03bada93`, consultado em 2026-10-24). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados da API do GitHub, consultados em 2026-10-24.
