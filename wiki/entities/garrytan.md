---
type: entity
kind: person
url: https://github.com/garrytan
created: 2026-10-19
updated: 2026-10-19
tags: [agentes, harness, claude-code, y-combinator]
---

# garrytan (Garry Tan)

> Presidente e CEO da Y Combinator e autor do gstack, uma configuração de Claude Code que organiza o trabalho em um sprint de produto com especialistas, revisão adversarial, QA em navegador e release.

## O que é

Garry Tan é presidente e CEO da Y Combinator. Segundo o README do gstack, antes da YC foi um dos primeiros engenheiros/PMs/designers da Palantir, cofundou a Posterous (vendida ao Twitter) e construiu o Bookface, a rede social interna da YC. É sediado em San Francisco e mantém o blog blog.garrytan.com e a conta [@garrytan](https://x.com/garrytan).

O gstack nasceu de uma tese sobre produtividade individual com agentes: o README cita Andrej Karpathy e Peter Steinberger/OpenClaw para argumentar que uma pessoa com o tooling certo pode entregar como um time. As alegações de produtividade, incluindo ganhos de LOC normalizados, são do autor e vêm com metodologia própria.

## Repositórios e projetos

- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — 23 especialistas e oito power tools em Markdown, distribuídos como slash commands; sprint Think → Plan → Build → Review → Test → Ship → Reflect; suporte a múltiplos hosts; GBrain; QA em navegador; licença MIT.
- `garrytan/gbrain` — base de conhecimento persistente para agentes, integrada ao gstack por `/setup-gbrain` e `/sync-gbrain`. Não ingerida nesta wiki.
- Outros projetos citados no README: Bookface, 40+ repositórios públicos e privados usados na metodologia de produtividade.

## Relevância no ecossistema

O gstack é um exemplo influente de **harness como processo de engenharia**: em vez de um agente generalista, ele distribui papéis de uma empresa (CEO, engenheiro-chefe, designer, QA, segurança, release) e faz cada etapa consumir o artefato da anterior. Também empurra a fronteira de ferramentas: QA em navegador real, revisão por um segundo modelo, coordenação entre agentes de fornecedores diferentes e recibos de egresso para chamadas de rede.

A visibilidade do autor na YC amplia o alcance do projeto e do debate sobre produtividade assistida por IA, incluindo a controvérsia sobre contagem de linhas de código que o README aborda diretamente.

## Relações

- Associado a: Y Combinator (presidente e CEO), Palantir, Posterous, Bookface (histórico citado no README).
- Mantém: [garrytan/gstack](../repos/github.com/garrytan/gstack.md), `garrytan/gbrain`.
- Comparável a: [affaan-m](../entities/affaan-m.md) e [HarnessMD](../entities/harnessmd.md) — outros autores de harnesses documentados na wiki.

## Fontes

- Perfil do GitHub: https://github.com/garrytan (API em 2026-10-19).
- README de [garrytan/gstack](../repos/github.com/garrytan/gstack.md) no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037` (consultado em 2026-10-19).
