---
type: repo
url: https://github.com/remotion-dev/skills
host: github.com
owner: remotion-dev
repo: skills
commit: 039e8a2fc78b67efc228d5645367838b85818a1c
license: desconhecida
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agent-skills, remotion, video, react]
---

# remotion-dev/skills

> Skills oficiais do Remotion (framework de vídeo programático em React) que ensinam agentes de código — Claude Code, Codex, Kimi Code, Cursor — as boas práticas de criação, markup, render e manutenção de projetos Remotion.

## O que é

O repositório empacota o conhecimento operacional do Remotion como Agent Skills, cobrindo todo o ciclo de um projeto: criar, escrever markup React para composições e animações, pré-visualizar no Studio, renderizar, mapear rotas geográficas, legendar, atualizar dependências e tornar o código editável no Studio.

## Como funciona

Doze skills, cada uma acionável por comando de barra:

| Skill | Função |
|---|---|
| `/remotion-best-practices` | Engloba as demais; usar quando não se sabe qual skill específica se aplica. |
| `/remotion-create` | Cria um novo projeto ou composição Remotion. |
| `/remotion-markup` | Boas práticas de markup React: composições, animações, layout, tipografia, mídia, efeitos, áudio, fontes, timing. |
| `/remotion-studio` | Abre o Studio para pré-visualizar o vídeo. |
| `/remotion-render` | Executa o render para vídeo ou still. |
| `/remotion-maps` | Animações de mapa: mapas estáticos, rotas e marcadores animados, explicadores geográficos (Mapbox, MapLibre, MapTiler, GeoJSON) e flyovers 3D com CesiumJS. |
| `/remotion-captions` | Orientação para legendas e subtítulos. |
| `/remotion-saas` | Orientação de arquitetura para apps e produtos construídos sobre Remotion. |
| `/remotion-interactivity` | Torna elementos selecionáveis/editáveis no Studio. |
| `/remotion-docs` | Busca a documentação do Remotion e devolve qualquer página como Markdown — referências de API, props de componentes e guias de pacotes. |
| `/remotion-upgrade` | Atualiza Remotion, pacotes relacionados, pacotes Mediabunny compatíveis e as próprias skills instaladas. |
| `/remotion-multimedia` | Orientação para manipulação de vídeo/áudio no browser com Mediabunny (metadados). |

## Instalação e uso rápido

```bash
npx skills add remotion-dev/skills
```

Alternativa ao criar um novo projeto Remotion:

```bash
bun create video
```

(o fluxo de criação oferece a opção de já instalar as skills).

## Exemplos de uso

Exemplos citados no README:

```text
/remotion-create Make a promo video for a record store
/remotion-markup Create an animated title card using Inter.
/remotion-maps Animate a route from Los Angeles to New York and make the camera follow it.
/remotion-saas Turn my video into a SaaS.
/remotion-docs How to set up Remotion Lambda?
```

## Quando usar (e quando não usar)

- **Use quando:** o projeto usa ou vai usar Remotion para gerar vídeo programaticamente com React, e o time quer que o agente siga as práticas oficiais em vez de inventar padrões.
- **Use quando:** a tarefa envolve mapas animados, legendas ou upgrade de dependências do próprio Remotion — skills com escopo bem definido para cada caso.
- **Evite quando:** o projeto de vídeo não usa Remotion — as skills são específicas do framework, diferente de orquestradores de pipeline mais genéricos como [calesthio/OpenMontage](../calesthio/openmontage.md), que trata o Remotion como um dos provedores possíveis.

## Limitações e cuidados

- **Somente o README foi lido.** O conteúdo de cada `SKILL.md` e os scripts associados não foram inspecionados.
- O README é gerado automaticamente a partir de `packages/skills/scripts/sync-readme.ts` — o texto reflete a sincronização mais recente, não uma escrita manual por release.
- `/remotion-upgrade` também atualiza as skills instaladas junto com o pacote Remotion — não há detalhe de como isso se comporta quando a skill mudou de forma incompatível.
- A API do GitHub não detectou licença para o repositório.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~5,4 mil estrelas, ~593 forks, 21 issues abertas; criado em 2026-01-19, último push em 2026-10-19.
- **Licença:** desconhecida (não detectada pela API do GitHub; não declarada no README).
- **Linguagem principal:** TypeScript.

## Relações

- **Mantido por:** [Remotion (remotion-dev)](../../../entities/remotion-dev.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — skills oficiais de fornecedor, mesmo padrão de `anthropics/skills`, `vercel-labs/agent-skills` e `cloudflare/skills`; [Produção de vídeo agêntica](../../../concepts/producao-de-video-agentica.md) — Remotion é citado como provedor de renderização em [calesthio/OpenMontage](../calesthio/openmontage.md).
- **Relacionado a:** [calesthio/OpenMontage](../calesthio/openmontage.md) — orquestra pipelines de vídeo e usa o Remotion como um dos provedores de renderização; [heygen-com/hyperframes](../heygen-com/hyperframes.md) — outro motor de renderização de vídeo para agentes, baseado em HTML puro em vez de React.

## Perguntas abertas

- Como as doze skills se comportam em conjunto quando instaladas todas ao mesmo tempo — qual o custo de contexto do catálogo completo?
- O `/remotion-upgrade` lida com breaking changes nas próprias skills, ou só nos pacotes npm do Remotion?
- Qual a cobertura real de `/remotion-docs` — busca por texto simples ou algum índice semântico da documentação?

## Fontes

- README: https://github.com/remotion-dev/skills (commit `039e8a2fc78b67efc228d5645367838b85818a1c`, consultado em 2026-10-19). Somente o README foi lido; os `SKILL.md` individuais e `packages/skills/scripts/sync-readme.ts` não foram consultados.
- Metadados do repositório e do perfil `remotion-dev` via API do GitHub (consultados em 2026-10-19).
