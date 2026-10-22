---
type: repo
url: https://github.com/open-webui/open-webui
host: github.com
owner: open-webui
repo: open-webui
commit: 91ea4e3421d1d8069f13d4a463fcb5986d94ea60
license: Open WebUI License (código-fonte disponível, ver nota)
language: Python
status: active
created: 2026-10-22
ingested: 2026-10-22
updated: 2026-10-22
tags: [plataforma, interface, mcp, rag]
---

# open-webui/open-webui

> Plataforma de IA self-hosted e extensível — "um lar para IA" — que dá uma interface única, offline-capaz, a qualquer modelo via Ollama ou API compatível com OpenAI.

## O que é

Open WebUI resolve o problema de ter uma interface consistente para usar modelos locais (Ollama) e remotos (qualquer API compatível com OpenAI, como LMStudio, GroqCloud, Mistral, OpenRouter, vLLM) sem depender de um provedor fechado. O README a descreve como "extensível, rica em recursos, amigável e pensada para rodar inteiramente offline".

## Como funciona

A lista de recursos do README é extensa; os pontos centrais:

- **RBAC granular** por usuário/grupo.
- **Extensão via plugins** (Filters, Actions, Pipes, Tools, Skills) e via protocolos externos (MCP, MCPO, servidores de ferramentas OpenAPI).
- **Agentes**: qualquer modelo base pode ser envolvido com instruções, ferramentas e conhecimento customizados.
- **Execução agêntica** via Open Terminal (terminal e filesystem dentro do chat) ou Terminals (Enterprise, containers isolados por usuário).
- **RAG local** com 9 bancos vetoriais (ChromaDB, PGVector, Qdrant, Milvus, Elasticsearch, OpenSearch, Pinecone, S3Vector, Oracle 23ai), busca híbrida BM25+vetorial e reranking.
- **Busca web** via dezenas de provedores (SearXNG, Google PSE, Brave, Tavily, Perplexity, Firecrawl, Bing, Exa etc.), injetada direto na conversa.
- Notas, canais colaborativos, memória persistente entre conversas, agendamento de prompts, geração/edição de imagem, conversas multi-modelo, analytics de uso, autenticação enterprise (LDAP/SSO/SCIM) e observabilidade via OpenTelemetry.

O ecossistema ao redor do core inclui Open WebUI Computer (agente de código mobile-first), Open Terminal/Terminals, `oikb` (ingestão de bases de conhecimento de 45+ fontes como GitHub, Confluence, Slack) e um app desktop nativo com inferência local via `llama.cpp`.

## Instalação e uso rápido

- **pip** (Python 3.11): `pip install open-webui` seguido de `open-webui serve`, acessível em `http://localhost:8080`.
- **Docker** (requer `-v open-webui:/app/backend/data` para persistir dados): variantes para Ollama local, Ollama remoto, GPU Nvidia, somente API OpenAI, ou imagem bundlada com Ollama (`:ollama`, com ou sem GPU).
- **Branch `:dev`** para recursos de ponta, instável por definição.
- **Modo offline**: `export HF_HUB_OFFLINE=1` evita downloads de modelo da internet.

## Exemplos de uso

- Conectar um modelo local via Ollama e um modelo remoto via API OpenAI na mesma conversa, comparando respostas lado a lado — exemplo derivado do README.
- Alimentar o RAG com uma base de conhecimento sincronizada via `oikb` a partir do Confluence ou Notion da equipe.

## Quando usar (e quando não usar)

- **Use quando:** quer uma interface única, self-hosted e extensível para múltiplos modelos e provedores, com RAG, busca web e automações sem depender de um provedor fechado.
- **Evite quando:** o objetivo é construir e publicar workflows/agentes como API ou MCP — [langgenius/dify](../langgenius/dify.md) ou [langflow-ai/langflow](../langflow-ai/langflow.md) são mais diretos para isso; Open WebUI é, primariamente, interface de uso, não builder de workflow.

## Limitações e cuidados

- A licença não é um SPDX padrão: o README afirma que o código atual usa a "Open WebUI License", com exigência adicional de preservar a marca "Open WebUI", além de contribuições anteriores sob suas licenças originais — ver `LICENSE` e `LICENSE_HISTORY` no repositório. **A verificar**: o texto completo e as implicações práticas de uso comercial.
- A API do GitHub retorna `NOASSERTION` para a licença, consistente com uma licença customizada.
- O README não detalha limites de escala para deployments enterprise nem o escopo exato do plano Enterprise, remetendo à documentação própria.
- Apenas o README foi lido; `docs/`, código-fonte e os repositórios do ecossistema (`computer`, `open-terminal`, `oikb`, `desktop`) não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: ver badges de última release; release no GitHub, `v0.12.3` (2026-10-16).
- Atividade e popularidade observadas em 2026-10-22: 156.432 estrelas, 22.768 forks (GitHub API); push em 2026-10-22.
- Licença: "Open WebUI License" (código-fonte disponível, com cláusula de marca) — não é SPDX padrão; **a verificar**.

## Relações

- Mantido por: [Open WebUI](../../../entities/open-webui.md); criado por Timothy Jaeryang Baek.
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md).
- Alternativas: [langgenius/dify](../langgenius/dify.md), [langflow-ai/langflow](../langflow-ai/langflow.md) — plataformas vizinhas para construir workflows/agentes, em vez de uma interface de uso sobre modelos existentes.

## Perguntas abertas

- Quais usos comerciais a "Open WebUI License" restringe em relação a uma licença OSI padrão?
- Como o desempenho e a cobertura de RAG local (9 bancos vetoriais suportados) se comparam entre si na prática?

## Fontes

- README: https://raw.githubusercontent.com/open-webui/open-webui/91ea4e3421d1d8069f13d4a463fcb5986d94ea60/README.md (commit `91ea4e3421d1d8069f13d4a463fcb5986d94ea60`, consultado em 2026-10-22). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
