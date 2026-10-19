---
type: skill
name: Imagegen Frontend Web
slug: imagegen-frontend-web
url: https://www.skills.sh/leonxlnx/taste-skill/imagegen-frontend-web
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/imagegen-frontend-web/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, geracao-de-imagem, frontend, direcao-de-arte, image-to-code, agent-skills]
---

# Imagegen Frontend Web

> Skill de direção de imagem para frontend web: gera uma imagem horizontal separada por seção de site, com variedade de composição e uma única paleta, para servir de referência implementável.

## O que é

`imagegen-frontend-web` é uma skill de direção de arte de imagens, não de código. O objetivo é produzir referências visuais premium e "conversion-aware" de seções de sites que desenvolvedores ou modelos de código consigam recriar com fidelidade.

A regra de saída mais enfática aparece nas primeiras linhas: gerar **uma imagem horizontal separada para cada seção**, sempre. Uma landing de 8 seções produz 8 imagens; nunca uma única imagem alta comprimindo a página. Se o pedido não especifica contagem, o padrão é alto: 6 imagens para landing, 8 para site completo ou marketing.

## Como funciona

O documento tem 21 seções. As principais:

- **Viés de composição do hero** — o padrão "texto à esquerda, imagem à direita" é permitido, mas não deve ser o primeiro instinto; a skill lista nove alternativas (centrado sobre imagem, bottom-left, top-left, stacked center, image-as-canvas, off-grid editorial, mini minimalista etc.).
- **Baseline de oito dials** — `DESIGN_VARIANCE` 8, `VISUAL_DENSITY` 4, `ART_DIRECTION` 8, `IMPLEMENTATION_CLARITY` 9, `IMAGE_USAGE_PRIORITY` 9, `SPACING_GENEROSITY` 8, `LAYOUT_VARIATION` 8 e `CONVERSION_DISCIPLINE` 8, adaptáveis ao brief.
- **Mapa brief → direção** — "minimalist", "editorial", "cinematic", "SaaS", "agency" e "e-commerce" recebem prescrições diferentes de escala de hero, fundo, gradiente e composição.
- **Motor combinatório** — escolher um paradigma de tema, um caráter de fundo, uma escala de hero e um tratamento de imagem, e comprometer-se com a combinação.
- **Regras de referência** — a saída precisa parecer um site real, não arte abstrata; tipografia e hierarquia legíveis; componentes executáveis.
- **Contagem e fatiamento** — a regra primária: uma seção por imagem, formato horizontal (16:9, 16:10 ou 21:9), tamanhos variados entre seções (grandes, mini e médias).
- **Consistência multi-imagem** — todas as imagens compartilham paleta, tipografia, família de CTA, raio, tratamento de imagem e tom de copy.
- **Anti-AI-slop** — proíbe hero escuro centralizado, glow roxo/azul, blobs, spam de cards, hierarquia fraca, seções clonadas e "luxo" que é só bege com serifada.
- **Packs padrão** — 4, 8 e 12 seções com a ordem típica (hero, trust bar, features, produto, benefícios, depoimentos, preços, FAQ, CTA).
- **Leitura de clareza** — verificação final de variedade, legibilidade e viabilidade de implementação.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill imagegen-frontend-web
```

Depende de um gerador de imagens no harness; se só for possível uma imagem por chamada, a skill exige gerá-las sequencialmente com rótulos "Section X of N".

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Landing de SaaS:** seis imagens horizontais — hero, features, prova social, produto, CTA e footer — com a mesma paleta e família de botões.
- **Site de estúdio criativo:** hero "image-as-canvas" e seções com composições off-grid, variando a posição do texto.
- **Página de e-commerce:** hero mid-editorial com foco no produto, recortes de detalhe e CTAs inequívocos.

## Saídas esperadas

Um conjunto de imagens horizontais, uma por seção, rotuladas e consistentes entre si, mais a indicação da paleta, tipografia e lógica de CTA que o implementador deve extrair.

## Quando usar (e quando não usar)

- **Use quando:** for preciso gerar referências visuais de alta qualidade para um site antes de implementar.
- **Evite quando:** o pedido for código direto, uma única peça de arte, ou quando o harness não tiver geração de imagens.

## Limitações e cuidados

- É uma skill de imagem: não implementa o frontend nem verifica o resultado no navegador.
- A regra de uma imagem por seção pode ser custosa em tempo e cota do gerador.
- Texto dentro de imagens geradas pode sair ilegível, apesar das regras de legibilidade.
- O conteúdo foi lido do `SKILL.md` renderizado; os prompts internos e exemplos não foram inspecionados.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **378.932**, primeira aparição em 25 de abril de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conceito: [Image-to-code](../../../../concepts/image-to-code.md).
- Variantes: [Image Taste Frontend](image-taste-frontend.md) (imagem e implementação), [Imagegen Frontend Mobile](imagegen-frontend-mobile.md), [Brandkit](brandkit.md).
- Alternativas: [Design Taste Frontend](design-taste-frontend.md) (código direto).

## Perguntas abertas

- Quantas imagens o gerador consegue produzir por chamada em cada harness?
- Como a skill mede "implementável" sem implementar?
- Há critério objetivo para a consistência entre imagens?
- O custo de uma imagem por seção inviabiliza projetos grandes?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/imagegen-frontend-web (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
