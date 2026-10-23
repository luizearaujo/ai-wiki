---
type: entity
kind: org
url: https://github.com/openai
created: 2026-10-23
updated: 2026-10-23
tags: [codex, plugin, claude-code]
---

# OpenAI (openai)

> Empresa de pesquisa e produtos de IA, criadora do Codex e, nesta wiki, mantenedora do plugin oficial que traz o Codex para dentro do Claude Code.

## O que é

A OpenAI é uma organização de pesquisa e produtos de IA, concorrente direta da Anthropic. Nesta wiki é documentada especificamente como mantenedora do `codex-plugin-cc`, um plugin que integra seu agente de código Codex ao Claude Code — um gesto de interoperabilidade entre ferramentas de fornecedores concorrentes.

## Repositórios e projetos

- [openai/codex-plugin-cc](../repos/github.com/openai/codex-plugin-cc.md) — plugin oficial que expõe review e delegação de tarefas ao Codex como slash commands dentro do Claude Code.
- Codex CLI e Codex app server (`@openai/codex`), citados como dependência do plugin; não ingeridos como página própria nesta wiki.

## Relevância no ecossistema

O `codex-plugin-cc` é notável por ser publicado pela própria OpenAI para rodar dentro do Claude Code (da Anthropic), em vez de manter os dois agentes isolados — um exemplo concreto de interoperabilidade entre harnesses de fornecedores diferentes, citado nesta wiki na categoria de harnesses e orquestração de agentes.

## Relações

- Concorre com: Anthropic, criadora do Claude Code que hospeda o plugin.
- Mantém: [openai/codex-plugin-cc](../repos/github.com/openai/codex-plugin-cc.md).

## Fontes

- Metadados da organização via API do GitHub (`orgs/openai`), consultados em 2026-10-23.
- README de [openai/codex-plugin-cc](../repos/github.com/openai/codex-plugin-cc.md) no commit `db52e28f4d9ded852ab3942cea316258ae4ef346`.
