---
type: repo
url: https://github.com/JohnnyVizz/claude-kit
host: github.com
owner: JohnnyVizz
repo: claude-kit
commit: c871c153ead54ad9547cc717d0f3e5a676c73986
license: MIT
language: TypeScript
status: active
created: 2026-10-28
ingested: 2026-10-28
updated: 2026-10-28
tags: [agent-skills, plugins-de-agente, claude-code, orquestracao-multiagente, mods]
---

# JohnnyVizz/claude-kit

> Três plugins do marketplace do Claude Code: `savvy-flow` (skill + subagentes que planejam, delegam e revisam), e dois mods de interface, `savvy-progress` e `session-band`.

## O que é

`claude-kit` reúne, em um único catálogo (`.claude-plugin/marketplace.json`), as skills e mods públicos do autor para Claude Code. Cada item é um plugin independente em `plugins/`, instalável separadamente.

| Plugin | Tipo | O que faz |
|---|---|---|
| `savvy-flow` | skill + agentes | `/savvy-flow <tarefa>`: o modelo da sessão planeja, delega a subagentes "worker" em camadas e revisa o trabalho deles. |
| `savvy-progress` | mod | Uma barra de progresso acima do prompt e um painel de agentes ativos, feito para o `savvy-flow`; mostra qualquer subagente em execução. |
| `session-band` | mod | Uma faixa acima do prompt com turno, velocidade, custo, contagem regressiva do cache de prompt e contexto; avisa antes do cache expirar. |

`savvy-flow` e `savvy-progress` funcionam isoladamente, mas se complementam: com os dois instalados, o fluxo alimenta a barra e os workers reportam progresso ao painel.

## Como funciona

Os mods (`savvy-progress`, `session-band`) são construídos sobre hooks de função (`hooks/register.tsx`), uma API em early access do Claude Code (testada na versão 2.1.286, sujeita a mudar entre releases) — o mesmo mecanismo usado pelo `hellosverre/claude-skins` (ver página irmã). A skill `savvy-flow` não depende dessa API: é um par SKILL.md + agentes Markdown, no formato padrão de skill/subagente do Claude Code.

Layout do repositório:

```
.claude-plugin/marketplace.json   catálogo lido por `/plugin marketplace add`
plugins/<nome>/
  .claude-plugin/plugin.json      manifesto
  skills/<skill>/SKILL.md         uma skill
  agents/*.md                     subagentes que ela embarca
  hooks/hooks.json                um mod: aponta para o módulo de hooks
  hooks/register.tsx              um mod: o módulo em si
  types/index.d.ts                um mod: seu contrato de estado ($.state)
```

## Instalação e uso rápido

```
/plugin marketplace add johnnyvizz/claude-kit
/plugin install savvy-flow@claude-kit
/plugin install savvy-progress@claude-kit
```

Reiniciar a sessão depois. Skills e agentes de plugin são namespaced: a skill vira `/savvy-flow:savvy-flow`, os agentes `savvy-flow:savvy-careful` etc.

Instalação manual: `git clone` e copiar as pastas de `skills/`/`agents/` para `~/.claude/`, para skills; para mods, `claude --plugin-dir ~/claude-kit/plugins/<nome>` por sessão, ou via `CLAUDE_CODE_PLUGIN_DIRS` em `~/.claude/settings.json` para todas as sessões (incluindo o app desktop). `git pull` no clone atualiza um mod carregado assim; skills copiadas precisam ser copiadas de novo.

Verificação antes de publicar: `claude plugin validate plugins/<nome>` por plugin, `claude plugin validate .` para o catálogo inteiro.

## Exemplos de uso

- Delegar uma tarefa maior ao `savvy-flow`, com o modelo da sessão planejando e subagentes "worker" em camadas executando partes, revisadas antes de fechar.
- Acompanhar o progresso desses workers em tempo real pelo painel do `savvy-progress`.
- Monitorar custo, velocidade e tempo restante do cache de prompt pela faixa do `session-band`, para evitar perder o cache por inatividade.

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é delegar uma tarefa a subagentes com revisão built-in (`savvy-flow`), ou visualizar progresso/custo de sessão diretamente na interface do Claude Code (`savvy-progress`, `session-band`).
- **Evite quando:** a versão do Claude Code é anterior à testada (2.1.286) para os mods — a API de hooks de função é early access e pode mudar; nesse caso, prefira instalar só a skill `savvy-flow`, que não depende dela.

## Limitações e cuidados

- Os dois mods dependem de uma API de hooks de função em early access, testada apenas na versão 2.1.286 do Claude Code — o README avisa que pode mudar entre releases.
- Se um mod instalado pelo marketplace não aparecer, o README recomenda carregá-lo manualmente via `--plugin-dir` como alternativa.
- Esta página documenta apenas o `README.md` da raiz; o conteúdo de `plugins/savvy-flow/skills/savvy-flow/SKILL.md`, os agentes em `agents/*.md` e o código dos hooks não foram lidos.

## Estado e adoção

- Repositório criado em 2026-10-04; push mais recente em 2026-10-12, observado em 2026-10-28.
- 287 estrelas, 70 forks, observado em 2026-10-28.
- Licença: MIT (confirmada pela API do GitHub).

## Relações

- Mantido por: [Johnny (JohnnyVizz)](../../../entities/johnnyvizz.md).
- Conceitos: [Plugins de agente](../../../concepts/plugins-de-agente.md) (mods via hooks de função), [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) (padrão planeja → delega → revisa do `savvy-flow`), [Agent skills](../../../concepts/agent-skills.md).
- Repositório irmão com o mesmo mecanismo de mods: [hellosverre/claude-skins](../hellosverre/claude-skins.md).

## Perguntas abertas

- O que o `SKILL.md` do `savvy-flow` especifica sobre como o planejamento é dividido entre os subagentes "tiered worker"?
- Como `savvy-progress` detecta e lista subagentes de outros plugins além do `savvy-flow`, se é que detecta?

## Fontes

- README: https://raw.githubusercontent.com/JohnnyVizz/claude-kit/c871c153ead54ad9547cc717d0f3e5a676c73986/README.md (commit `c871c153ead54ad9547cc717d0f3e5a676c73986`, consultado em 2026-10-28). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/JohnnyVizz/claude-kit`, `api.github.com/users/JohnnyVizz`), consultada em 2026-10-28.
