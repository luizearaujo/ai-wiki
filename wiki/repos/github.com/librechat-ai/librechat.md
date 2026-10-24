---
type: repo
url: https://github.com/LibreChat-AI/LibreChat
host: github.com
owner: librechat-ai
repo: librechat
commit: a378657583567310c841d652b0f6b00c83e2bd6b
license: MIT
language: TypeScript
status: active
created: 2026-10-24
ingested: 2026-10-24
updated: 2026-10-24
tags: [mcp, agent-skills, orquestracao-multiagente]
---

# LibreChat-AI/LibreChat

> Plataforma self-hosted de chat com IA que unifica todos os grandes provedores numa única interface, com Agentes, MCP, Code Interpreter, Artifacts e autenticação multiusuário de nível enterprise.

## O que é

LibreChat resolve o problema de depender de um único provedor de chat de IA: unifica Anthropic, AWS Bedrock, OpenAI, Azure, Google/Vertex AI, OpenAI Responses API e qualquer endpoint compatível com OpenAI (Ollama, Mistral, DeepSeek, Qwen, OpenRouter e outros) em uma única interface self-hosted, inspirada no ChatGPT. Além do chat, publica Agentes de IA, suporte a Model Context Protocol (MCP), Code Interpreter sandboxado, Artifacts (código gerado renderizado no chat) e autenticação multiusuário pronta para empresa (OAuth2, LDAP, e-mail).

**O repositório foi transferido**: a URL original era `danny-avila/LibreChat` (nome do mantenedor original), hoje redireciona para `LibreChat-AI/LibreChat`. Mais um caso do padrão de transferência silenciosa de organização já registrado em [`overview.md`](../../../overview.md) para OpenHands e ComfyUI — links antigos continuam funcionando via redirecionamento do GitHub, mas é preciso resolver o nome canônico antes de registrar a página.

## Como funciona

- **Agentes LibreChat:** assistentes sem código, com marketplace para descobrir/publicar agentes da comunidade, compartilhamento colaborativo por usuário/grupo, MCP servers, file search e execução de código. Skills ([`SKILL.md`](https://www.librechat.ai/docs/features/skills)) empacotam instruções reutilizáveis para workflows manuais, automáticos ou sempre ativos; Agent Plugins empacotam skills + servidores MCP carregados na inicialização (experimental); Subagents delegam trabalho a execuções filhas isoladas com contexto próprio.
- **Code Interpreter:** execução sandboxada em Python, Node.js, Go, C/C++, Java, PHP, Rust e Fortran, via [ClickHouse/code-interpreter](https://github.com/ClickHouse/code-interpreter) open-source.
- **Novidades da v0.8.8:** Agent Management API (beta, com OpenAPI/Swagger) para criar, descobrir, atualizar e remover agentes e skills via cliente autenticado por OIDC; "Attached workspaces" (altamente experimental) deixa agentes inspecionarem árvores de arquivo, ler, buscar, editar e rodar Bash com timeout limitado; controles de aprovação de código (Ask/Allow/Deny/Full access); compactação manual de contexto; inspetor de uso de contexto; anexos unificados; observabilidade via Trace Viewer, OpenTelemetry e Langfuse.
- **Web search, geração de imagem** (GPT-Image-1, Stable Diffusion local, Flux ou qualquer servidor MCP) e **streams retomáveis** (reconexão automática entre abas/dispositivos, inclusive em deploy horizontal com Redis).

## Instalação e uso rápido

Docker é o caminho recomendado pela documentação oficial (fora do README, não verificado nesta ingestão): clonar o repositório, copiar `.env.example` para `.env` e `docker compose up -d`. Deploy com um clique também via Railway, Zeabur e Sealos (links no README). Desenvolvimento local requer Node.js e um banco (MongoDB).

## Exemplos de uso

Exemplos derivados do README — não são instruções oficiais além do que ele publica.

- Importar conversas de LibreChat, ChatGPT ou Chatbot UI; exportar como screenshot, Markdown, texto ou JSON.
- Criar um Agente sem código, anexar Skills e servidores MCP, e compartilhá-lo com um grupo específico de usuários.
- Configurar [S3 com CloudFront](https://www.librechat.ai/docs/configuration/cdn/cloudfront) para links de mídia estáveis em produção.

## Quando usar (e quando não usar)

- **Use quando:** quiser uma interface única e self-hosted para vários provedores de LLM, com agentes, MCP, skills e controle de acesso multiusuário — sem depender de um único vendor.
- **Evite quando:** quiser evitar operar infraestrutura própria (banco de dados, Redis para escala horizontal, sandbox de code interpreter) — nesse caso, um app de chat hospedado por um único provedor é mais simples.
- **Evite quando:** depender de "Attached workspaces" para produção — o próprio README marca o recurso como altamente experimental.

## Limitações e cuidados

- README pede consulta ao changelog antes de atualizar por possíveis breaking changes — não há garantia de compatibilidade entre versões menores.
- "Attached workspaces" e a Agent Management API estão em beta/experimental; podem mudar de comportamento sem aviso na mesma intensidade que recursos estáveis.
- **A verificar:** passos de instalação detalhados (Docker, variáveis de ambiente, pré-requisitos de banco) estão apenas no site de documentação oficial, não no README — não foram lidos nesta ingestão.
- Métricas de estrelas/forks variam bastante entre fontes de terceiros por causa da transferência de organização recente; a API do GitHub é a fonte usada aqui.

## Estado e adoção

- Observado em 2026-10-24: 46.251 stars, 9.507 forks, 977 issues abertas, push mais recente em 2026-10-24.
- Nome atual: `LibreChat-AI/LibreChat` (antes `danny-avila/LibreChat`).
- Licença: MIT.
- Versão citada no README: v0.8.8.

## Relações

- Mantido por: organização `LibreChat-AI` (antes mantido na conta pessoal de Danny Avila, `danny-avila`).
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md); [Agent skills](../../../concepts/agent-skills.md) — Skills em formato `SKILL.md`; [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — Subagents com contexto isolado.
- Alternativas/comparáveis: [open-webui/open-webui](../open-webui/open-webui.md) — mesmo padrão de interface self-hosted unificando múltiplos modelos com RAG/MCP/plugins, mais próximo do LibreChat do que do builder visual de nós do Langflow/Dify; [langflow-ai/langflow](../langflow-ai/langflow.md) e [langgenius/dify](../langgenius/dify.md) — builders de workflow, não apenas interface de chat.

## Perguntas abertas

- Quais os passos exatos de instalação e configuração (fora do README, no site de documentação)?
- Como a Agent Management API em beta se relaciona com o controle de acesso por papel/grupo já existente?
- O "Attached workspaces" chega a ficar estável, ou permanece como recurso experimental de nicho?

## Fontes

- README: https://raw.githubusercontent.com/LibreChat-AI/LibreChat/a378657583567310c841d652b0f6b00c83e2bd6b/README.md (commit `a378657583567310c841d652b0f6b00c83e2bd6b`, consultado em 2026-10-24; URL original fornecida, `danny-avila/LibreChat`, redireciona para este nome canônico). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados da API do GitHub, consultados em 2026-10-24.
