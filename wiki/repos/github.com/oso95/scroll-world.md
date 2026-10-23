---
type: repo
url: https://github.com/oso95/scroll-world
host: github.com
owner: oso95
repo: scroll-world
commit: 71cc36d3bb150248ae36a2c552f9cbf88802a79c
license: MIT
language: JavaScript
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [agent-skills, geracao-de-video, landing-page, scroll, difusao]
---

# oso95/scroll-world

> Agent skill que constrói uma landing page imersiva em "voo contínuo" — a câmera atravessa cenas geradas por IA conforme o usuário rola a página, sem cortes — para qualquer marca ou setor.

## O que é

`scroll-world` é uma skill compatível com `SKILL.md` (Claude Code, Codex e qualquer agente que leia esse formato) que gera uma landing page do tipo "fly through the world": conforme a pessoa rola a página, uma câmera voa de fora para dentro de uma cena, depois flui para a próxima sem cortes — uma viagem contínua por um mundo gerado para a marca ou setor pedido. O README cita como referência o site de logística da Emons, aplicando a mesma técnica a qualquer assunto.

Não é um template nem um gerador de imagens isolado: a skill entrevista o usuário, gera os ativos (imagens e vídeo) e entrega o motor de scroll que reproduz o resultado como uma página web.

## Como funciona

1. **Entrevista** — assunto/setor e pitch, brand kit (importado de uma URL, fornecido pelo usuário ou proposto pela skill), direção de arte, a sequência de cenas que a câmera visita, se deve gerar também a versão mobile (cadeia renderizada nativamente em 9:16, não um corte da versão widescreen) e o orçamento — a skill mostra níveis de render e fonte das imagens estáticas com custo estimado em créditos, aprovado antes de gerar qualquer coisa.
2. **Geração dos ativos** — uma imagem estática por cena (dioramas isométricos via GPT Image 2, pela Higgsfield ou pela CLI do Codex) e um clipe de câmera "dive-in" por cena, mais clipes "conectores" entre cenas consecutivas, gerados a partir dos frames reais das cenas vizinhas para que cada emenda seja idêntica quadro a quadro. A opção mobile renderiza uma cadeia retrato paralela, com o mesmo travamento de frames.
3. **Montagem** — um motor de scroll (`scrub-engine.js`), guiado por configuração, reproduz toda a cadeia como um único voo, servindo os clipes e pôsteres em retrato automaticamente em telas de celular.

A técnica de câmera é a mesma de páginas de produto com scroll da Apple: o scroll controla apenas o tempo, a câmera de fato se move (não é parallax). A skill é agnóstica de framework — entrega o pipeline, os templates de prompt e um motor de scrub em JavaScript puro que roda em HTML simples, Next.js, Vue ou uma página servida por Python.

## Instalação e uso rápido

```bash
# Claude Code, como plugin (recomendado)
/plugin marketplace add oso95/scroll-world
/plugin install scroll-world@scroll-world

# Codex e outros agentes, via CLI de skills da Vercel
npx skills add oso95/scroll-world
npx skills add oso95/scroll-world -a codex

# manual
git clone https://github.com/oso95/scroll-world
cp -R scroll-world/skills/scroll-world ~/.claude/skills/
```

Pré-requisitos: [Monid CLI](https://monid.ai) com chave e saldo (backend padrão de vídeo, cobrado por clipe em USD); [Higgsfield CLI](https://higgsfield.ai) autenticado, com créditos (renderiza as cenas estáticas, o fallback `kling3_0`, e toda a cadeia quando o Monid está ausente); `ffmpeg`/`ffprobe`; Python 3 com Pillow; opcionalmente a [Codex CLI](https://github.com/openai/codex), para gerar as cenas estáticas via `image_gen` cobrado na assinatura do ChatGPT em vez de créditos da Higgsfield.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- Pedir uma landing page de voo contínuo para uma marca de logística, com cenas de armazém, frota e centro de distribuição.
- Gerar a mesma página com uma cadeia mobile nativa em 9:16, aprovada previamente pelo orçamento estimado.
- Invocar `/scroll-world` no Claude Code, ou `$scroll-world` no Codex, e pedir diretamente a página.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é uma landing page vistosa de "voo pelo mundo" para divulgar uma marca, produto ou setor, e há orçamento para gerar vídeo/imagem por API.
- **Evite quando:** não há tolerância a custo variável por geração (Monid cobrado por clipe, Higgsfield por crédito) ou quando as chaves de API exigidas (Monid, Higgsfield) não estão disponíveis.
- **Alternativa na wiki:** o fork [ChecheChat/scroll-world](#relações) tem o mesmo README, sem o backend Monid — ver "Relações".

## Limitações e cuidados

- **Somente o README foi lido.** O `SKILL.md`, os templates de prompt, o motor de scrub e o script de knockout não foram inspecionados.
- **Custo variável e não trivial:** o README estima uma cadeia de 6 cenas em 1080p em ≈ US$ 27 via Monid; a opção mobile dobra as gerações de vídeo. O preço da Higgsfield não é exposto pela CLI, então a skill calibra pelo saldo ao vivo.
- **Dependência de serviços de terceiros pagos** (Monid, Higgsfield) sem os quais a geração de vídeo não funciona, salvo o caminho alternativo via Codex CLI para as imagens estáticas.
- Os ativos gerados (`.mp4`/`.webp`) não são distribuídos no repositório — são produzidos por projeto.

## Estado e adoção

- Versão: não publicada no README.
- Atividade observada em 2026-10-23: 10.383 estrelas, 1.148 forks, 10 issues abertas; repositório criado em 2026-07-06, último push em 2026-07-29.
- Licença: MIT.
- Linguagem principal (API): JavaScript.

## Relações

- Mantido por: [oso95](../../../entities/oso95.md).
- **Fork:** [ChecheChat/scroll-world](https://github.com/ChecheChat/scroll-world) é um fork direto no GitHub (API: `parent`/`source` = `oso95/scroll-world`), com README quase idêntico — a única diferença notável é a ausência do backend Monid, usando só a Higgsfield CLI. Sem estrelas ou forks próprios em 2026-10-23; não tem página própria nesta wiki por não representar um projeto distinto.
- Conceitos: [Produção de vídeo agêntica](../../../concepts/producao-de-video-agentica.md) — pipeline de geração e montagem de vídeo acionado por uma skill; [Geração de imagem e vídeo com modelos de difusão](../../../concepts/geracao-de-imagem-e-video-com-difusao.md) — dioramas e clipes gerados via APIs de imagem/vídeo (GPT Image 2, Seedance, Kling); [Artefatos HTML autocontidos](../../../concepts/artefatos-html-autocontidos.md) — a página final é HTML com um motor de scroll em JS puro; [Agent skills](../../../concepts/agent-skills.md) — distribuição via plugin, CLI de skills ou cópia manual.

## Perguntas abertas

- Qual é a taxa de sucesso do travamento de frames ("seam rule") entre conectores em cenas visualmente muito diferentes?
- O custo real por projeto varia como em relação à estimativa prévia mostrada ao usuário?
- Como a skill se comporta quando Monid e Higgsfield ficam indisponíveis simultaneamente?

## Fontes

- README: https://github.com/oso95/scroll-world/blob/main/README.md (commit `71cc36d3bb150248ae36a2c552f9cbf88802a79c`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-23), incluindo a relação de fork com `ChecheChat/scroll-world`.
- README de `ChecheChat/scroll-world` no commit `2912048246d057cdfe134dfc0b4dfb7e6a12f30e` (consultado em 2026-10-23, para comparação).
