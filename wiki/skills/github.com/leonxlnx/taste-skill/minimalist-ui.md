---
type: skill
name: Minimalist UI
slug: minimalist-ui
url: https://www.skills.sh/leonxlnx/taste-skill/minimalist-ui
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/minimalist-skill/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, minimalismo, editorial, tipografia, frontend, agent-skills]
---

# Minimalist UI

> Skill de estilo "minimalismo utilitário premium": monofonia quente, contraste tipográfico editorial, grids bento planos e pastéis dessaturados, sem gradientes nem sombras pesadas.

## O que é

`minimalist-ui` é uma das skills de estilo fixo do pacote `taste-skill`. O texto se chama "Premium Utilitarian Minimalism & Editorial UI" e define um protocolo para interfaces com aparência de documento, inspiradas em plataformas de workspace de alto nível.

A estética é declaradamente anti-SaaS genérico: paleta monocromática quente, tipografia com serifada editorial nos títulos, muito espaço em branco estrutural e componentes quase planos. A cor entra só como acento semântico em pastéis lavados.

## Como funciona

O protocolo tem oito partes:

1. **Visão geral** — nome e intenção editorial.
2. **Restrições negativas absolutas** — proíbe Inter, Roboto e Open Sans; bibliotecas de ícones finos como Lucide, Feather e Heroicons; sombras padrão do Tailwind; fundos primários coloridos; gradientes, neon e glassmorphism; pílulas em containers grandes; emoji; nomes fictícios; e clichês de copy.
3. **Arquitetura tipográfica** — sans geométrica para corpo e UI (SF Pro Display, Geist Sans, Helvetica Neue, Switzer), serifada editorial para heróis e citações (Lyon Text, Newsreader, Playfair Display, Instrument Serif) com tracking negativo e line-height 1.1, e monoespaçada para código e metadados.
4. **Paleta** — branco puro ou osso quente (#F7F6F3, #FBFBFA), bordas #EAEAEA, texto off-black (#111111, #2F3437) e quatro pastéis com textos escuros correspondentes.
5. **Componentes** — grids bento assimétricos com bordas de 1 px e raio de 8–12 px; CTAs pretos com raio de 4–6 px e hover em #333333; badges-pílula em caixa alta; acordeões sem caixa, separados por borda inferior; `kbd` estilizado; e chrome de janela de macOS simulado.
6. **Iconografia e imagens** — Phosphor Bold/Fill ou Radix UI Icons, ilustrações monocromáticas e fotografia dessaturada com grão quente; placeholders via `picsum.photos`.
7. **Movimento sutil** — entradas de 600 ms com cubic-bezier(0.16, 1, 0.3, 1), hover de 200 ms, revelações escalonadas de 80 ms, blob radial opcional em camada fixa e suporte obrigatório a `prefers-reduced-motion`.
8. **Protocolo de execução** — estabelecer macro-whitespace, limitar a largura do texto, aplicar a hierarquia, garantir bordas de 1 px, animar entradas e evitar seções planas vazias.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill minimalist-ui
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Site de documentação de produto:** serifada editorial no hero, corpo em Geist, bordas #EAEAEA e acordeões sem caixa.
- **Landing de workspace:** grid bento com um card grande e dois menores, CTAs pretos e badges pastel.
- **Blog editorial:** hero com serifada apertada, fotos dessaturadas e grão sutil de 4%.

## Saídas esperadas

HTML, React, Tailwind ou Vue com paleta monocromática quente, hierarquia tipográfica editorial, bordas de 1 px, sombras quase inexistentes, acentos pastel e movimento discreto com fallback de movimento reduzido.

## Quando usar (e quando não usar)

- **Use quando:** o brief pede uma interface calma, editorial, tipo documento ou workspace premium.
- **Evite quando:** o produto precisa de cor expressiva, densidade alta de dados ou uma estética brutalista; as skills vizinhas cobrem esses casos.

## Limitações e cuidados

- É um protocolo de estilo fixo, opt-in, sem processo de sorteio ou verificação no navegador.
- A combinação de serifada editorial com UI pode não servir a dashboards e produtos densos.
- Proíbe bibliotecas de ícones muito comuns, o que pode conflitar com um design system existente.
- O conteúdo foi lido do `SKILL.md` renderizado; referências internas não foram inspecionadas.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **423.465**, primeira aparição em 17 de março de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Estilos vizinhos: [High-End Visual Design](high-end-visual-design.md), [Industrial Brutalist UI](industrial-brutalist-ui.md).
- Família: [Design Taste Frontend](design-taste-frontend.md).
- Conceito: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).

## Perguntas abertas

- A paleta quente funciona em modo escuro ou a skill é exclusivamente clara?
- Como o estilo se comporta em dashboards com muitos dados?
- Há teste de contraste das combinações pastel/texto?
- O protocolo foi derivado de alguma plataforma específica?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/minimalist-ui (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
