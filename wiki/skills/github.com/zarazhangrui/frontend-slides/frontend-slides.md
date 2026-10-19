---
type: skill
name: Frontend Slides
slug: frontend-slides
url: https://www.skills.sh/zarazhangrui/frontend-slides/frontend-slides
source_url: https://github.com/zarazhangrui/frontend-slides
source_path: SKILL.md
author: zarazhangrui
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [apresentacoes, slides, html, design, frontend, agent-skills]
---

# Frontend Slides

> Skill que ensina o agente a criar apresentações HTML autocontidas e ricas em animação — do zero, a partir de um PPTX ou aprimorando um deck existente — com um palco fixo 16:9 e descoberta visual de estilo.

## O que é

Frontend Slides é uma skill de [zarazhangrui](../../../../entities/zarazhangrui.md) distribuída pelo skills.sh. Ela ataca um problema específico: agentes tendem a gerar interfaces genéricas e "on distribution" — o que a skill chama de *AI slop*. Em vez disso, a skill conduz o agente por um processo de descoberta visual, gera três prévias de estilo e só então produz o deck.

O resultado é um único arquivo HTML, sem npm nem build, com CSS e JavaScript inline, que roda inteiramente no navegador. A skill também converte arquivos PowerPoint e aprimora apresentações HTML existentes.

## Como funciona

### Princípios

1. **Zero dependências** — um arquivo HTML com CSS/JS inline.
2. **Show, don't tell** — o usuário escolhe vendo prévias visuais, não descrevendo preferências abstratas.
3. **Design distintivo** — evitar fontes, paletas e layouts genéricos.
4. **Divulgação progressiva** — ler índices leves de estilo primeiro; carregar o `design.md` completo só depois da escolha.
5. **Palco 16:9 fixo** — todo deck vive em um canvas de 1920×1080 escalado uniformemente; o conteúdo não reflui para celular.

### Fases

| Fase | O que faz |
|---|---|
| 0 | Detecta o modo: novo deck, conversão de PPTX ou aprimoramento de HTML existente |
| 1 | Coleta propósito, duração, conteúdo, densidade (speaker-led ou reading-first) e imagens |
| 2 | Gera três prévias de estilo: um preset seguro, um template ousado e um wildcard/custom |
| 3 | Gera o deck, lendo `viewport-base.css`, `html-template.md` e `animation-patterns.md`; verifica overflow e sobreposição em screenshots |
| 4 | Converte PPTX com `scripts/extract-pptx.py`, preservando texto, imagens, ordem e notas |
| 5 | Entrega: limpa prévias, abre no navegador e explica navegação, personalização e edição inline |
| 6 | Opcional: publica na Vercel ou exporta PDF via scripts |

O deck inclui edição inline de texto (hover no canto superior esquerdo ou tecla `E`, `Ctrl+S` para salvar), navegação por setas/espaço e suporte a `prefers-reduced-motion`.

### Arquivos de apoio

A skill depende de `STYLE_PRESETS.md` (12 presets), `bold-template-pack/` (índice, prévias e `design.md` por template), `viewport-base.css` (obrigatório em todo deck), `html-template.md`, `animation-patterns.md` e scripts de conversão, deploy e exportação. O carregamento é deliberadamente progressivo para não inflar o contexto.

## Instalação e uso

Comando publicado na página de origem:

```bash
npx skills add https://github.com/zarazhangrui/frontend-slides --skill frontend-slides
```

Depois de instalar, peça o deck ao agente. A skill detecta o modo e conduz as perguntas.

Requisitos variam por modo: nenhum para gerar HTML; Python com `python-pptx` para converter PPTX; Node/Vercel CLI para publicar; um navegador para as verificações visuais e o PDF.

## Exemplos de uso

Exemplos derivados do método publicado, não instruções oficiais:

- **Pitch deck:** "Crie um pitch deck de 12 slides para uma startup de energia solar, densidade baixa, estética editorial e animações discretas."
- **Aula:** "Faça uma apresentação de 20 slides sobre fotossíntese para ensino médio, modo reading-first, com tabelas e diagramas."
- **Conversão:** "Converta `apresentacao.pptx` para um deck HTML no estilo que você gerar, preservando imagens e notas do palestrante."
- **Aprimoramento:** "Melhore este deck HTML existente: mantenha o conteúdo, ajuste tipografia, ritmo e animações, e verifique overflow."
- **Compartilhamento:** depois da entrega, aceitar a oferta de publicar na Vercel ou exportar PDF.

## Saídas esperadas

- um único arquivo HTML autocontido, com CSS/JS inline;
- palco fixo 1920×1080 escalado ao viewport;
- tipografia e paleta coerentes com o estilo escolhido;
- animações e microinterações com suporte a movimento reduzido;
- verificação visual de overflow e sobreposição;
- opcionalmente, URL na Vercel ou PDF estático (sem animações).

## Quando usar (e quando não usar)

- **Use quando:** você quer um deck visualmente distinto, sem depender de PowerPoint/Keynote, ou precisa converter um PPTX para HTML; quer explorar estilos visualmente em vez de especificá-los.
- **Use quando:** o deck precisa rodar offline em qualquer navegador como um único arquivo.
- **Evite quando:** você precisa de edição colaborativa em tempo real, recursos de apresentação corporativa ou um formato binário exigido por parceiros — nesse caso, PowerPoint/Google Slides é mais adequado.
- **Evite quando:** o conteúdo é denso demais para slides e deveria ser um documento; a skill insiste em dividir em mais slides, não em encolher texto.

## Limitações e cuidados

- **Conteúdo publicado, não verificado no repositório.** O `SKILL.md` foi lido pela página do skills.sh; o repositório-fonte não foi clonado nem o arquivo cru foi consultado.
- **Dependência de navegador.** As verificações de overflow e sobreposição dependem de screenshots renderizados; o agente precisa de capacidade de navegador/browser.
- **Publicação e exportação.** A Vercel exige conta e CLI; o PDF é uma captura estática e perde animações e interatividade.
- **Assets locais.** Imagens e vídeos referenciados por CSS `background-image` podem não ser empacotados no deploy; prefira publicar a pasta inteira.
- **Auditoria de segurança.** Gen Agent Trust Hub e Socket aparecem como "Pass", mas Snyk aparece como **"Warn"** em 2026-10-19. Isso não é auditoria do conteúdo da skill; revise antes de usar.
- **Instruções de terceiros.** Como toda skill, o texto vira contexto executável do agente; a estética e as escolhas de design não são garantia de qualidade.
- **Licença.** O repositório é MIT segundo a API; a página do catálogo não declara licença.

## Estado e adoção

- **Versão da skill:** não publicada na página (observada em 2026-10-19).
- **Catálogo:** 1,1 mil instalações, primeira aparição em 2026-01-28 (observado em 2026-10-19).
- **Repositório-fonte:** MIT, JavaScript, ~30,9 mil stars, ~2,4 mil forks; último push em 2026-06-23; commit `9906a34d640d2111f724544cbc50f7f130569ae1` (metadados e árvore consultados via API em 2026-10-19).
- **Preço:** gratuito.

## Relações

- **Autor:** [zarazhangrui](../../../../entities/zarazhangrui.md).
- **Repositório-fonte:** [zarazhangrui/frontend-slides](https://github.com/zarazhangrui/frontend-slides) — contém `SKILL.md` na raiz e uma cópia em `plugins/frontend-slides/skills/frontend-slides/`.
- **Conceitos:** [Artefatos HTML autocontidos](../../../../concepts/artefatos-html-autocontidos.md), [Agent skills](../../../../concepts/agent-skills.md).
- **Alternativas:** [diagram-design](../../cathrynlavery/diagram-design/diagram-design.md) — também gera HTML/SVG autocontido, mas para diagramas; PowerPoint/Google Slides para fluxos corporativos; frameworks de slides com build (reveal.js, Slidev) quando dependências são aceitáveis.

## Perguntas abertas

- Qual é o conteúdo exato de `STYLE_PRESETS.md` e do bold-template-pack?
- Como a skill mede "design distintivo" de forma objetiva, além de heurísticas?
- As verificações visuais funcionam sem navegador e em CI?
- O deploy na Vercel é seguro para conteúdo sensível? Quem controla a conta?
- Como a skill se compara a gerar um deck manualmente com um designer ou com reveal.js?
- A cópia do `SKILL.md` no diretório `plugins/` é idêntica à raiz?

## Fontes

- Página de origem: https://www.skills.sh/zarazhangrui/frontend-slides/frontend-slides (consultada em 2026-10-19). A página publica o `SKILL.md`, incluindo princípios, fases, arquivos de apoio e scripts.
- Repositório-fonte: https://github.com/zarazhangrui/frontend-slides (metadados e árvore consultados via API do GitHub em 2026-10-19; commit `9906a34d640d2111f724544cbc50f7f130569ae1`). O repositório não foi clonado e o `SKILL.md` cru não foi lido.
