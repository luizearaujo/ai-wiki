---
type: repo
url: https://github.com/langflow-ai/langflow
host: github.com
owner: langflow-ai
repo: langflow
commit: 3ec974b7ee82d1c1ca630e68547edbde5c64a8a9
license: MIT
language: Python
status: active
created: 2026-10-22
ingested: 2026-10-22
updated: 2026-10-22
tags: [agentes, workflow, plataforma, mcp]
---

# langflow-ai/langflow

> Plataforma para construir e implantar agentes e workflows de IA visualmente, que expõe cada fluxo como API ou servidor MCP.

## O que é

Langflow dá a desenvolvedores uma experiência de autoria visual (builder de nós) e servidores de API/MCP embutidos, transformando cada workflow construído na interface em uma ferramenta integrável a qualquer framework ou stack. O README o descreve como "powered by batteries included": suporta os principais LLMs, bancos de dados vetoriais e uma biblioteca crescente de ferramentas de IA.

## Como funciona

- **Builder visual**: interface de nós para montar fluxos rapidamente.
- **Acesso ao código-fonte**: qualquer componente pode ser customizado em Python.
- **Playground interativo**: testa e refina fluxos passo a passo.
- **Orquestração multiagente**: gestão de conversa e retrieval entre agentes.
- **Deploy como API** ou exportação em JSON para apps Python.
- **Deploy como servidor MCP**, transformando o fluxo em ferramenta para clientes MCP.
- **Observabilidade** via LangSmith, LangFuse e outras integrações.
- Recursos de segurança e escalabilidade voltados a uso enterprise.

## Instalação e uso rápido

- **Langflow Desktop**: app para Windows/macOS com todas as dependências incluídas, sem gerenciar ambiente Python.
- **Instalação local** (Python 3.10–3.14, `uv` recomendado): `uv pip install langflow -U`, depois `uv run langflow run` — inicia em `http://127.0.0.1:7860`.
- **A partir do código-fonte**: `make run_cli` no diretório clonado.
- **Docker**: definir `LANGFLOW_SUPERUSER_PASSWORD` e rodar `docker run -p 7860:7860 -e LANGFLOW_SUPERUSER_PASSWORD langflowai/langflow:latest`.
- Pacotes oficiais e releases desabilitam login automático por padrão; branches de desenvolvimento mantêm o login automático. Autenticação configurável via variáveis de ambiente.

## Exemplos de uso

- Montar um fluxo de RAG ou multiagente no builder visual e publicá-lo como endpoint de API consumido por uma aplicação Python — exemplo derivado do README.
- Expor o mesmo fluxo como servidor MCP para que um cliente MCP (ex.: um agente de código) o use como ferramenta.

## Quando usar (e quando não usar)

- **Use quando:** quer prototipar e iterar visualmente um pipeline de agente/RAG com múltiplos LLMs e bancos vetoriais, e depois publicá-lo como API ou MCP sem reescrever o fluxo em código.
- **Evite quando:** o fluxo é simples o suficiente para ser escrito direto em código, ou quando autenticação/observabilidade enterprise embutida não é necessária — um script ou framework de agente mais leve pode bastar.

## Limitações e cuidados

- O README não detalha limites de escala, custos de hospedagem própria nem comparação de desempenho entre os LLMs suportados.
- Pacotes de release e tagged source archives exigem senha de superusuário (`LANGFLOW_SUPERUSER_PASSWORD`) antes do login; quem já tinha instalação com login automático precisa seguir instrução de upgrade específica.
- Apenas o README foi lido; `DEVELOPMENT.md` e o código-fonte não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: ver [releases no GitHub](https://github.com/langflow-ai/langflow/releases); última release, `v1.12.7` (2026-10-21).
- Atividade e popularidade observadas em 2026-10-22: 155.908 estrelas, 10.231 forks (GitHub API); push no mesmo dia.
- Licença: MIT.

## Relações

- Mantido por: [Langflow](../../../entities/langflow-ai.md).
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Builder visual de agentes e workflows de IA](../../../concepts/builder-visual-de-agentes.md).
- Alternativas: [langgenius/dify](../langgenius/dify.md) — mesma categoria de plataforma visual para workflows/agentes de IA, com Dify adicionando RAG pipeline, LLMOps e marketplace próprios.

## Perguntas abertas

- Como a observabilidade embutida (LangSmith/LangFuse) se compara, em custo e profundidade, a instrumentar um pipeline de agente feito à mão?
- Que limites de throughput ou concorrência a edição self-hosted suporta antes de precisar da oferta enterprise?

## Fontes

- README: https://raw.githubusercontent.com/langflow-ai/langflow/3ec974b7ee82d1c1ca630e68547edbde5c64a8a9/README.md (commit `3ec974b7ee82d1c1ca630e68547edbde5c64a8a9`, consultado em 2026-10-22). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
