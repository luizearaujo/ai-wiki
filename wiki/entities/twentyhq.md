---
type: entity
kind: org
url: https://github.com/twentyhq
created: 2026-10-19
updated: 2026-10-19
tags: [crm, agent-skills, open-source]
---

# twentyhq

> Organização que mantém o [Twenty](../repos/github.com/twentyhq/twenty.md), CRM open source que se descreve como "desenhado para IA".

## O que é

twentyhq é a organização no GitHub por trás do Twenty, cuja bio oficial é "We are building a modern Open Source CRM". Mantém o produto principal, a CLI de desenvolvimento de apps (`create-twenty-app`), o SDK de definição de objetos (`twenty-sdk`) e o pacote de skills oficiais para agentes de código (`twenty-agent-skills`).

## Repositórios e projetos

- [twentyhq/twenty](../repos/github.com/twentyhq/twenty.md) — CRM com objetos, campos, views e workflows definidos como código; licença mista (AGPLv3 + módulos Enterprise + pacotes MIT); TypeScript.

## Relevância no ecossistema

O Twenty é o primeiro CRM documentado nesta wiki que distribui skills oficiais para agentes de código (Claude Code, Codex, Cursor, Pi) como parte do próprio produto, instaláveis pela mesma CLI `skills` usada por outros projetos do ecossistema (ver [Agent skills](../concepts/agent-skills.md)).

## Relações

- Mantém: [Twenty](../repos/github.com/twentyhq/twenty.md).
- Distribui: skills oficiais em `packages/twenty-agent-skills`, instaláveis via CLI `skills`.

## Fontes

- README de [twentyhq/twenty](../repos/github.com/twentyhq/twenty.md), commit `31d95e98a2217e187d6f7d51f7ab69bb048e22bc` (consultado em 2026-10-19).
- Perfil do GitHub (`api.github.com/orgs/twentyhq`), consultado em 2026-10-19.
