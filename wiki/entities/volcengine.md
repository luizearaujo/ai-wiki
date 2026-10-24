---
type: entity
kind: org
url: https://github.com/volcengine
created: 2026-10-24
updated: 2026-10-24
tags: [memoria-de-agente, mcp]
---

# Volcengine

> Braço de cloud e IA da ByteDance; mantém o OpenViking, banco de contexto open-source para agentes.

## O que é

Volcengine (Volcano Engine) é a plataforma de cloud/IA da [ByteDance](bytedance.md), já citada nesta wiki como provedora de serviços comerciais de modelos e busca no README do DeerFlow. Mantém sua própria organização no GitHub, de onde publica o OpenViking.

## Repositórios e projetos

- [volcengine/OpenViking](../repos/github.com/volcengine/openviking.md) — banco de contexto open-source (AGPLv3) que unifica memória, conhecimento e skills de agente num filesystem virtual `viking://`; oferece também um serviço hospedado (OpenViking Service) e edição self-managed via licença.

## Relevância no ecossistema

Mostra a mesma empresa (ByteDance) publicando, por organizações distintas, tanto um harness completo (DeerFlow, via `bytedance`) quanto uma camada de memória/contexto para agentes (OpenViking, via `volcengine`) — e promovendo serviços comerciais próprios (modelos Doubao, hosting do OpenViking Service) a partir de projetos open-source.

## Relações

- Colabora com: [ByteDance](bytedance.md) (organização-mãe); projetos citados como parceiros do OpenViking (NoKV, loopx, Hermes Agent, NVIDIA cuVS).
- Associado a: BytePlus, Doubao.
- Concorre com: outros backends de memória de agente, como mem0 e Honcho, citados como alternativas no README do DeerFlow.

## Fontes

- README de [volcengine/OpenViking](../repos/github.com/volcengine/openviking.md), commit `4ab22a4923452362b60aef2826c2083ce36168d2` (consultado em 2026-10-24).
- Metadados da API do GitHub, consultados em 2026-10-24.
