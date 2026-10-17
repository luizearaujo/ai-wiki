---
type: concept
aliases: [MCP, Model Context Protocol]
status: stable
created: 2026-10-17
updated: 2026-10-17
tags: [protocolo, agentes, ferramentas]
---

# Model Context Protocol (MCP)

> Protocolo aberto que padroniza como aplicações de LLM descobrem e chamam ferramentas, recursos e prompts expostos por servidores externos.

## Definição

O Model Context Protocol (MCP) é um protocolo cliente-servidor, baseado em JSON-RPC, que separa o **agente/host** das **capacidades** que ele pode usar. Um servidor MCP expõe primitivas como *tools* (ações), *resources* (dados legíveis) e *prompts* (instruções reutilizáveis); um cliente MCP as descobre e as coloca à disposição do modelo.

O transporte pode ser local (stdio, com o servidor rodando como subprocesso do cliente) ou remoto (HTTP). A proposta é evitar integrações bespoke para cada combinação de agente e ferramenta: a mesma ferramenta pode ser usada por Claude Code, Codex, Cursor, Gemini CLI e outros clientes.

## Como funciona

1. O cliente inicia ou conecta a um servidor MCP.
2. O cliente descobre as tools disponíveis, incluindo nomes, descrições e schemas de entrada/saída.
3. O modelo escolhe uma tool e o cliente envia a chamada.
4. O servidor executa a ação — localmente ou em um serviço remoto — e devolve um resultado estruturado.
5. O resultado entra no contexto do modelo; o agente decide o próximo passo.

Duas consequências práticas: (a) o catálogo de tools consome contexto, e catálogos grandes podem custar caro; (b) o servidor executa ações com as permissões do processo, então registro, aprovação e isolamento importam.

## Onde aparece

- [morluto/rea](../repos/github.com/morluto/rea.md) — o REA é um servidor MCP local (`src/main.ts` + `src/server/`) que expõe workflows de engenharia reversa a agentes. A CLI usa a mesma camada de aplicação, e o setup registra o servidor nos clientes com backup e aprovação.
- O projeto depende de `@modelcontextprotocol/client` e `@modelcontextprotocol/server` (`package.json`) e documenta contratos de tools, resultados e sessões em `docs/mcp-contracts.md`.

## Trade-offs

- **Vantagens:** integração padronizada entre agentes e ferramentas; reuso do mesmo servidor por vários clientes; execução local com controle de permissões; ecossistema crescente de servidores.
- **Limitações:** custo de contexto do catálogo e dos schemas; variação de suporte entre clientes; necessidade de registro e reinício; riscos de segurança quando o servidor executa ações locais; evolução rápida do protocolo e dos SDKs.
- **Custo concreto observado:** no estudo de caso do REA, uma estimativa `cl100k_base` sobre uma passada do catálogo JSON bruto, argumentos e respostas chegou a ~846 mil tokens — cerca de ~802 mil só do catálogo. O próprio documento ressalva que isso é **serialização de transporte**, não contexto renderizado nem uso real de tokens.

## Relações

- **Relacionado a:** function calling, agent skills, plugins de agentes.
- **Contrasta com:** integrações proprietárias por agente; RAG (MCP expõe ferramentas e dados, não é uma técnica de recuperação).
- **Pré-requisito para:** usar o REA a partir de um agente.

## Perguntas abertas

- Como medir o custo real de contexto de um catálogo MCP em um cliente concreto, e não apenas o tamanho da serialização?
- Quais padrões de autorização, isolamento e auditoria estão emergindo para servidores MCP locais?
- Como evitar divergência entre a versão do servidor, os schemas anunciados e as instruções da skill do agente?

## Fontes

- [morluto/rea](../repos/github.com/morluto/rea.md) — `README.md`, `package.json`, `src/main.ts`, `src/server/`, `docs/mcp-contracts.md`, `docs/installation.md` e `.agents/skills/rea-analysis-optimization/references/kuna-case-study.md` (commit `09de00b4108a5d738ebe56903e0110ef63820aca`, consultado em 2026-10-17).
