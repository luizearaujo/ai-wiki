---
type: entity
kind: org
url: https://github.com/cloudflare
created: 2026-10-19
updated: 2026-10-19
tags: [organizacao, infraestrutura, edge, workers, email, agentes]
---

# Cloudflare

> Empresa de infraestrutura de edge network que publica projetos abertos para agentes, incluindo o Agentic Inbox (cliente de e-mail self-hosted com agente e servidor MCP) e o pacote oficial de Agent Skills para a Cloudflare Developer Platform.

## O que é

Cloudflare é a empresa por trás da rede de edge, CDN, DNS, proteção contra DDoS e da plataforma de computação serverless Workers. A organização no GitHub foi criada em 2010-06-25, declara 580 repositórios públicos e cerca de 17,8 mil seguidores, com escritórios em San Francisco, Londres, Austin, Lisboa e Singapura.

Nesta wiki, a organização aparece pelo [Agentic Inbox](../repos/github.com/cloudflare/agentic-inbox.md), uma aplicação de referência que combina Email Routing, Durable Objects, R2, Workers AI e o Agents SDK. O projeto é parte de uma linha maior de infraestrutura para agentes: Workers como runtime, Durable Objects como estado isolado, R2 como armazenamento de objetos e MCP como interface para ferramentas externas.

## Repositórios e produtos

- [cloudflare/agentic-inbox](../repos/github.com/cloudflare/agentic-inbox.md) — cliente de e-mail self-hosted com agente de IA e servidor MCP; Apache-2.0, TypeScript; ~8,4 mil estrelas em 2026-10-19.
- [cloudflare/skills](../repos/github.com/cloudflare/skills.md) — 18 Agent Skills oficiais para Workers, Agents SDK, Durable Objects, Sandbox e o restante da plataforma, com o servidor MCP principal da Cloudflare incluído; Apache-2.0; ~3,1 mil estrelas em 2026-10-19.
- **Cloudflare Workers** — runtime serverless usado pelo projeto.
- **Durable Objects** — estado isolado por mailbox com SQLite.
- **R2** — armazenamento de anexos.
- **Email Routing / Email Service** — recebimento e envio de e-mail.
- **Workers AI** — inferência do agente.
- **Cloudflare Access** — política de autenticação que, no Agentic Inbox, é a única fronteira de confiança.
- Demais repositórios públicos: 580 no total, não inventariados nesta ingestão.

## Relevância no ecossistema

A Cloudflare ocupa uma posição diferente dos demais mantenedores da wiki: não publica apenas uma ferramenta de agente, mas a **infraestrutura** sobre a qual agentes rodam. O Agentic Inbox é útil como referência de arquitetura — estado por mailbox, agente com ferramentas de e-mail e MCP no mesmo Worker — e como exemplo dos limites do modelo: uma política única de Access, sem autorização por mailbox, é simples de operar e arriscada em ambiente compartilhado.

**A verificar:** a relação entre esse repositório e os produtos comerciais de e-mail da Cloudflare, e se há planos de autorização granular.

## Relações

- **Criou:** [Agentic Inbox](../repos/github.com/cloudflare/agentic-inbox.md), a plataforma Workers usada por ele, e as [Agent Skills oficiais](../repos/github.com/cloudflare/skills.md) da Developer Platform.
- **Conceitos:** [Email para agentes](../concepts/email-para-agentes.md), [Model Context Protocol (MCP)](../concepts/model-context-protocol.md), [Memória de agente](../concepts/memoria-de-agente.md), [Agent skills](../concepts/agent-skills.md).

## Fontes

- https://github.com/cloudflare — perfil da organização via API do GitHub em 2026-10-19 (repositórios públicos, seguidores, criação, localização e blog).
- https://github.com/cloudflare/agentic-inbox — README no commit `48039bb6785af34e592c2966f87cde2b255c4c80`; metadados da API do GitHub observados em 2026-10-19.
- [cloudflare/skills](../repos/github.com/cloudflare/skills.md) — README no commit `86505e44f87d801aa1864a3c4109e9a8ae5c409f`; metadados da API do GitHub observados em 2026-10-19.
