---
type: repo
url: https://github.com/langgenius/dify
host: github.com
owner: langgenius
repo: dify
commit: 0d06488de5dfc0ae49b28be5ffb19c8b819ef364
license: Apache-2.0 com condições adicionais (ver nota)
language: Python
status: active
created: 2026-10-22
ingested: 2026-10-22
updated: 2026-10-22
tags: [agentes, workflow, rag, plataforma, mcp]
---

# langgenius/dify

> Plataforma open source de desenvolvimento de aplicações LLM que combina workflow, pipeline de RAG, agentes autônomos, gestão de modelos e observabilidade em uma única interface.

## O que é

Dify resolve o problema de ir do prototype à produção com uma aplicação baseada em LLM sem integrar manualmente cada peça (orquestração de prompt, RAG, agente, logging, métricas). O README descreve sete recursos centrais: workflow visual, suporte a centenas de modelos proprietários/open-source, um IDE de prompt, pipeline de RAG com extração de texto de PDFs/PPTs e outros formatos, agentes autônomos com sandbox próprio, LLMOps (monitoramento e análise contínua) e exposição de tudo via API (backend-as-a-service).

## Como funciona

O recurso "Agent" descrito no README dá a agentes autônomos um sandbox próprio: eles rodam comandos, instalam software e manipulam arquivos para completar tarefas abertas. O usuário descreve o agente desejado e ele se constrói; skills, servidores MCP do Dify Marketplace ou APIs próprias podem ser conectados, e o agente roda como app de chat ou como etapa de um workflow maior. Integrações de observabilidade citadas: Opik, Langfuse e Arize Phoenix.

## Instalação e uso rápido

- **Pré-requisitos**: CPU ≥2 núcleos, RAM ≥4 GiB; Docker e Docker Compose v2.24.0+.
- **Quick start**:
  ```bash
  cd dify/docker
  cp .env.example .env
  docker compose up -d
  ```
  Acesso ao dashboard em `http://localhost/install` para iniciar o processo de inicialização.
- Alternativas: Dify Cloud (hospedado, planos pagos) ou Dify Enterprise (self-hosting com SSO, RBAC e suporte SLA, mediante formulário).

## Exemplos de uso

- Construir um workflow visual que combina RAG sobre documentos próprios com um agente que chama ferramentas do Marketplace — exemplo derivado do README.
- Expor um app de chat construído no Dify como API para integrar à lógica de negócio de outra aplicação.

## Quando usar (e quando não usar)

- **Use quando:** quer uma plataforma completa (workflow + RAG + agente + observabilidade) para ir do protótipo à produção sem integrar cada peça manualmente, com opção de self-host ou cloud.
- **Evite quando:** precisa apenas de um builder de fluxos simples sem RAG/LLMOps embutidos — [langgenius/dify](dify.md) é mais pesado que [langflow-ai/langflow](../langflow-ai/langflow.md) para esse caso.

## Limitações e cuidados

- A licença não é Apache-2.0 pura: o README aponta a licença como "Dify Open Source License", baseada em Apache 2.0 **com condições adicionais** (ver arquivo `LICENSE` do repositório) — **a verificar**: quais são exatamente essas condições, já que não foram lidas fora do README.
- A API do GitHub retorna `NOASSERTION` para a licença, o que é consistente com uma licença customizada não reconhecida como SPDX padrão.
- O README não detalha limites de recursos, custos do Dify Cloud além de referenciar a página de pricing, nem benchmarks de desempenho.
- Apenas o README foi lido; `docs/ADVANCED_SETUP.md`, código-fonte e manifestos não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: ver [releases no GitHub](https://github.com/langgenius/dify/releases); última release, `1.17.1` (2026-09-10).
- Atividade e popularidade observadas em 2026-10-22: 159.240 estrelas, 25.159 forks (GitHub API); push no mesmo dia.
- Licença: "Dify Open Source License" (Apache-2.0 com condições adicionais) — não é SPDX puro; **a verificar** o texto completo das condições.

## Relações

- Mantido por: [LangGenius](../../../entities/langgenius.md).
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Builder visual de agentes e workflows de IA](../../../concepts/builder-visual-de-agentes.md).
- Alternativas: [langflow-ai/langflow](../langflow-ai/langflow.md) — builder visual mais enxuto, sem LLMOps/marketplace próprios; [open-webui/open-webui](../open-webui/open-webui.md) — foco em interface de chat sobre modelos existentes, não em construção de workflow/agente.

## Perguntas abertas

- Quais são, no texto completo da "Dify Open Source License", as condições adicionais em relação ao Apache 2.0 puro?
- Como o sandbox dos agentes autônomos isola comandos e acesso a arquivos na edição self-hosted Community?

## Fontes

- README: https://raw.githubusercontent.com/langgenius/dify/0d06488de5dfc0ae49b28be5ffb19c8b819ef364/README.md (commit `0d06488de5dfc0ae49b28be5ffb19c8b819ef364`, consultado em 2026-10-22). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
