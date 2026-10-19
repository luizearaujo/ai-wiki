---
type: repo
url: https://github.com/heygen-com/hyperframes
host: github.com
owner: heygen-com
repo: hyperframes
commit: aa63a8c70d8549d55533efdc7ed6d6559331b38c
license: Apache-2.0
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [video, html, agentes, skills, renderizacao, animacao, ffmpeg]
---

# heygen-com/HyperFrames

> Framework open-source que transforma HTML, CSS, mídia e animações seekable em vídeos MP4 determinísticos, com CLI e 21 skills para agentes de código.

## O que é

HyperFrames é descrito como "an open-source framework for turning HTML, CSS, media, and seekable animations into deterministic MP4 videos". Pode ser usado localmente pela CLI, por agentes de código via skills ou como núcleo de renderização por workflows hospedados.

O público é composto por desenvolvedores e agentes que já escrevem HTML. O README posiciona o projeto como alternativa ao Remotion: em vez de componentes React e um bundler, a composição é HTML puro com atributos de dados, sem build step. O projeto é usado em produção na [HeyGen](../../../entities/heygen.md), com exemplos públicos de tldraw e TanStack.

## Como funciona

Uma composição é um arquivo HTML com atributos de tempo e trilha:

- `data-composition-id`, `data-start`, `data-width` e `data-height` definem o palco;
- elementos com `class="clip"` mais `data-start`, `data-duration` e `data-track-index` viram clipes em trilhas;
- mídia (vídeo, áudio) é controlada pelo framework;
- animação é seekable: GSAP, CSS, Lottie, Three.js, Anime.js, WAAPI ou adapter próprio registrado em `window.__timelines`.

O renderer percorre cada frame em headless Chrome e codifica com FFmpeg, o que produz o mesmo resultado para a mesma entrada. O README trata determinismo como requisito de CI, testes de regressão e renderização automatizada.

### Skills para agentes

O projeto publica **21 skills**, organizadas em três níveis:

| Nível | Skills |
| --- | --- |
| **Router** | `/hyperframes` — mapa de capacidades, confirma o briefing e escolhe o workflow. |
| **Creation workflows** | `/product-launch-video`, `/faceless-explainer`, `/pr-to-video`, `/embedded-captions`, `/talking-head-recut`, `/motion-graphics`, `/music-to-video`, `/slideshow`, `/general-video`, `/remotion-to-hyperframes`. |
| **Domain skills** | `/hyperframes-core`, `-animation`, `-keyframes`, `-creative`, `/media-use`, `/hyperframes-cli`, `-audio`, `-registry`, `/figma`. |

As skills ensinam o ciclo de produção: planejar, escrever HTML válido, conectar animações seekables, adicionar mídia, lint, preview e render. O README recomenda instalar apenas o **core set**; o router baixa cada workflow sob demanda, em vez de instalar as 21 de uma vez.

### Stack e pacotes

| Pacote | Função |
| --- | --- |
| `hyperframes` | CLI de criação, preview, lint e render. |
| `@hyperframes/core` | Tipos, parsers, geradores, linter, runtime e frame adapters. |
| `@hyperframes/engine` | Captura página-para-vídeo com Puppeteer e FFmpeg. |
| `@hyperframes/producer` | Pipeline de captura, encode e mixagem de áudio. |
| `@hyperframes/studio` | Editor de composições no navegador. |
| `@hyperframes/player` | Web component `<hyperframes-player>`. |
| `@hyperframes/shader-transitions` | Transições WebGL. |
| `@hyperframes/aws-lambda` | SDK e deploy para renders distribuídos. |

O README também descreve **frame.md**, uma camada que traduz um `design.md` web para o frame de vídeo e gera um superset de `DESIGN.md` que o agente usa para compor sem "adivinhar escala" ou reaproveitar chrome de web.

## Instalação e uso rápido

Pré-requisitos: Node.js 22+ e FFmpeg.

```bash
npx hyperframes init my-video
cd my-video
npx hyperframes preview   # preview no navegador com live reload
npx hyperframes render    # renderiza para MP4
```

Instalação como plugin do Claude Code:

```bash
claude plugin marketplace add heygen-com/hyperframes
claude plugin install hyperframes@hyperframes
```

Instalação de skills standalone (OpenCode e outros agentes):

```bash
npx skills add heygen-com/hyperframes
```

O README recomenda `npx hyperframes skills update` para instalar exatamente o core set em execuções não interativas. `skills add --all` instala as 21 skills; o picker interativo abre sem nada selecionado. Há ainda `bun run package:agent-plugin` e `bun run package:codex-plugin` para gerar pacotes portáveis com checksum e limite de upload.

## Exemplos de uso

Exemplos derivados do README.

```html
<div id="stage" data-composition-id="launch" data-start="0"
     data-width="1920" data-height="1080">
  <video class="clip" data-start="0" data-duration="6"
         data-track-index="0" src="intro.mp4" muted playsinline></video>

  <h1 id="title" class="clip" data-start="1" data-duration="4"
      data-track-index="1">Launch day</h1>

  <audio data-start="0" data-duration="6" data-track-index="2"
         data-volume="0.5" src="music.wav"></audio>

  <script src="https://cdn.jsdelivr.net/npm/gsap@3/dist/gsap.min.js"></script>
  <script>
    const tl = gsap.timeline({ paused: true });
    tl.from("#title", { opacity: 0, y: 40, duration: 0.8 }, 1);
    window.__timelines = window.__timelines || {};
    window.__timelines.launch = tl;
  </script>
</div>
```

Instalação de blocos do catálogo:

```bash
npx hyperframes add flash-through-white   # transição com shader
npx hyperframes add instagram-follow      # overlay social
npx hyperframes add data-chart            # gráfico animado
```

## Quando usar (e quando não usar)

- **Use quando:** você quer vídeo programático e determinístico a partir de HTML, sem React nem bundler.
- **Use quando:** um agente de código precisa produzir ou editar vídeo e você quer instruções de produção, não só uma API de render.
- **Use quando:** o vídeo precisa entrar em CI, testes de regressão ou pipelines automatizados.
- **Use quando:** você quer render local ou distribuído em AWS Lambda.
- **Evite quando:** a equipe já investiu em Remotion e não precisa migrar. O próprio README trata a migração como one-way.
- **Evite quando:** o caso exige edição não linear manual madura. O Studio é descrito como "available, evolving".
- **Evite quando:** você não pode instalar Node 22+, FFmpeg e Chromium headless no ambiente.

## Limitações e cuidados

- **Somente o README foi lido.** Código, pacotes, skills, catálogo, testes e docs não foram consultados. As capacidades e o determinismo são afirmações do projeto.
- **Determinismo depende do ambiente.** "Mesma entrada, mesmos frames" assume versões de Chrome, FFmpeg, fontes e dependências controladas; o README não detalha pinning além de Node 22+.
- **Muitas skills.** São 21; instalar todas consome contexto. O README recomenda o core set, mas o picker interativo e `--all` facilitam instalar demais.
- **Superfície de execução.** O render roda headless Chrome e FFmpeg; composições e mídias de terceiros devem ser tratadas como entrada não confiável.
- **Dependência de mídia externa.** `/media-use` pode gerar TTS, música e imagens por modelos; custos, licenças e qualidade variam por provedor.
- **Git LFS no desenvolvimento.** O repositório usa LFS para baselines de regressão (~240 MB de MP4). Clone sem LFS se só precisa do código.
- **Licença Apache-2.0**, sem taxa por render, mas sem garantia de que todos os serviços ao redor (Studio, playground, Lambda) sejam gratuitos.
- **README promocional.** O texto mistura produto comercial da HeyGen, playground, Studio e o framework; a fronteira entre open source e hospedado não é detalhada.

## Estado e adoção

- **Atividade e popularidade observadas em 2026-10-19:** ~67,3 mil estrelas, ~6,1 mil forks, 379 issues abertas; criado em 2026-03-10 e último push em 2026-10-19.
- **Licença:** Apache-2.0.
- **Linguagem principal:** TypeScript.
- **Commit de referência:** `aa63a8c70d8549d55533efdc7ed6d6559331b38c`.
- **Adoção declarada:** produção na HeyGen; exemplos de tldraw e TanStack em `ADOPTERS.md`.

## Relações

- **Mantido por:** [HeyGen](../../../entities/heygen.md).
- **Conceitos:** [Produção de vídeo agêntica](../../../concepts/producao-de-video-agentica.md) — skills e ciclo de produção; [Agent skills](../../../concepts/agent-skills.md) — 21 skills com router e carregamento sob demanda; [Design system com agentes](../../../concepts/design-system-com-agentes.md) — `frame.md` como superset de `DESIGN.md`; [Artefatos HTML autocontidos](../../../concepts/artefatos-html-autocontidos.md) — composição em HTML puro.
- **Alternativas:** [calesthio/OpenMontage](../../github.com/calesthio/openmontage.md) — orquestra pipelines e usa HyperFrames como renderizador entre outras opções; Remotion (não documentado na wiki) — autoria em React.
- **Stack:** Node.js, TypeScript, Puppeteer, FFmpeg, GSAP, Three.js, AWS Lambda.

## Perguntas abertas

- Quão determinístico é o render entre sistemas operacionais e versões de Chrome/FFmpeg?
- Qual é o custo real de render local versus AWS Lambda para um vídeo de 60 segundos?
- O core set de skills é suficiente para produção ou os workflows exigem as 21?
- Como o `frame.md` se comporta com `DESIGN.md` de ferramentas como Stitch e Impeccable?
- Qual é a fronteira entre o framework Apache-2.0, o Studio, o playground e os serviços da HeyGen?
- Como direitos e atribuição de mídia gerada ou recuperada são registrados?
- O renderer é isolado o suficiente para processar HTML de terceiros?

## Fontes

- README: https://github.com/heygen-com/hyperframes/blob/main/README.md (commit `aa63a8c70d8549d55533efdc7ed6d6559331b38c`, consultado em 2026-10-19). Somente o README foi lido; código, pacotes, skills e documentação interna não foram consultados.
- Metadados do repositório e da organização: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues e datas).
