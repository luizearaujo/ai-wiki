---
type: skill
name: GPT Taste
slug: gpt-taste
url: https://www.skills.sh/leonxlnx/taste-skill/gpt-taste
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/gpt-tasteskill/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, gsap, motion, bento, frontend, agent-skills]
---

# GPT Taste

> Skill de engenharia de design nível Awwwards orientada a GPT/Codex: usa um sorteio determinístico em Python simulado para variar layouts, exige estrutura AIDA, hero de no máximo três linhas e grids bento sem células vazias.

## O que é

`gpt-taste` é uma skill de estilo e processo do pacote `taste-skill`, descrita como "Elite UX/UI & Advanced GSAP Motion Engineer". O diagnóstico de partida é que modelos grandes repetem vícios estatísticos: títulos quebrados em seis linhas por containers estreitos, buracos em grids bento, meta-rótulos baratos ("QUESTION 05", "SECTION 01"), texto de botão ilegível e alternância infinita entre os mesmos layouts esquerda/direita.

A skill ataca esses vícios com regras numéricas, um sorteio determinístico e uma verificação pré-voo obrigatória. O foco é React com Tailwind e GSAP/ScrollTrigger.

## Como funciona

O documento tem oito seções:

1. **Randomização verdadeira com Python** — antes do código, simular um `random.choice()` com semente determinística (por exemplo, contagem de caracteres do prompt) para escolher um hero, uma pilha tipográfica (Satoshi, Cabinet Grotesk, Outfit ou Geist; nunca Inter), três componentes e dois paradigmas de GSAP.
2. **Estrutura AIDA e espaçamento** — nav premium, Attention no hero, Interest em bento denso, Desire em scroll/GSAP e Action no footer; `py-32 md:py-48` entre seções.
3. **Hero e a regra das duas linhas** — containers largos (`max-w-5xl`/`max-w-6xl`) e H1 em no máximo 2–3 linhas; proíbe badges flutuantes, pill-tags e estatísticas no hero.
4. **Grid bento sem lacunas** — `grid-auto-flow: dense`, colunas e linhas que se encaixam matematicamente, e no máximo 3–5 cards intencionais.
5. **GSAP e física de hover** — pin de título com galeria rolando, escala e fade por scroll, scrub de palavras, empilhamento de cards e suporte obrigatório a `prefers-reduced-motion`.
6. **Arsenal de componentes** — imagens inline dentro de títulos, acordeões horizontais, marquee infinito e carrossel de depoimentos.
7. **Conteúdo, ativos e banimentos** — proíbe meta-rótulos para sempre; usa `picsum.photos` com filtros; proíbe fundo chapado; e exige `overflow-x-hidden` na página.
8. **Pré-voo obrigatório `<design_plan>`** — antes de qualquer código, provar o sorteio, a estrutura AIDA, a largura do H1, a densidade do bento, a ausência de meta-rótulos e o contraste dos botões.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill gpt-taste
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Landing de startup:** sorteio escolhe "cinematic center", Geist, três componentes e pin de scroll; o plano prova que o H1 cabe em duas linhas.
- **Página de agência:** hero assimétrico com imagem flutuante sobre o texto e bento denso verificado célula a célula.
- **Página de produto:** sequência AIDA com seção de desejo em scrub de texto e footer com CTA massivo.

## Saídas esperadas

React com Tailwind e GSAP, precedido de um bloco `<design_plan>` que documenta sorteio, estrutura, largura do hero, densidade do grid e checagens de rótulo e contraste.

## Quando usar (e quando não usar)

- **Use quando:** o agente é um GPT/Codex e o projeto é uma landing ou página de marketing com movimento rico.
- **Evite quando:** o ambiente não executa GSAP/React, o brief pede sobriedade, ou o alvo é um dashboard ou UI de produto.

## Limitações e cuidados

- O "sorteio" é uma simulação textual, não uma chamada real a Python; a variação depende de o modelo obedecer ao plano.
- Exige GSAP e React, o que limita o uso em stacks estáticas.
- A regra de bento sem lacunas pode forçar composições artificiais em conteúdos irregulares.
- O conteúdo foi lido do `SKILL.md` renderizado; scripts e referências não foram inspecionados.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **398.124**, primeira aparição em 16 de abril de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Família: [Design Taste Frontend](design-taste-frontend.md), [High-End Visual Design](high-end-visual-design.md).
- Variantes de imagem: [Image Taste Frontend](image-taste-frontend.md), [Imagegen Frontend Web](imagegen-frontend-web.md).
- Conceito: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).

## Perguntas abertas

- O sorteio determinístico produz variação suficiente em prompts parecidos?
- Como a skill se comporta em modelos que não seguem o `<design_plan>`?
- A proibição de meta-rótulos é absoluta em qualquer contexto editorial?
- Há medição de performance para as animações prescritas?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/gpt-taste (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
