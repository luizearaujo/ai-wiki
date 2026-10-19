---
type: skill
name: Industrial Brutalist UI
slug: industrial-brutalist-ui
url: https://www.skills.sh/leonxlnx/taste-skill/industrial-brutalist-ui
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/brutalist-skill/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, brutalismo, tipografia, data-ui, frontend, agent-skills]
---

# Industrial Brutalist UI

> Skill de estilo "brutalismo industrial e telemetria tática": funde tipografia suíça, manuais de manufatura e terminais aeroespaciais em grids rígidos, escala extrema e degradação analógica simulada.

## O que é

`industrial-brutalist-ui` é uma skill de estilo fixo do pacote `taste-skill`, apresentada como "Industrial Brutalism & Tactical Telemetry Interface Engineering". O objetivo declarado é construir ambientes digitais que projetem funcionalidade crua, precisão mecânica e alta densidade de dados, descartando padrões de UI de consumo.

O sistema funciona como dois paradigmas visuais compatíveis, dos quais se escolhe **um** por projeto:

- **Swiss Industrial Print** — substrato claro de papel, tipografia sans pesada monolítica, grid estrutural visível com linhas divisórias, espaço negativo assimétrico, numerais gigantes sangrando a viewport e vermelho primário como alerta.
- **Tactical Telemetry & CRT** — modo escuro exclusivo, dados tabulares densos, monoespaçada dominante, molduras técnicas (colchetes ASCII, crosshairs) e limitações de hardware simuladas (glow de fósforo, scanlines, baixa profundidade de bits).

## Como funciona

O documento se organiza em oito seções:

1. **Meta** — nome e descrição da disciplina.
2. **Arquétipos visuais** — os dois paradigmas acima, com a regra de não misturá-los.
3. **Arquitetura tipográfica** — macro-tipografia neo-grotesca em `clamp(4rem, 10vw, 15rem)`, tracking negativo de -0.03 a -0.06 em e leading de 0.85–0.95; micro-tipografia monoespaçada de 10–14 px com tracking positivo; e serifada de alto contraste usada com parcimônia e pós-processada.
4. **Sistema de cor** — uma paleta de substrato por projeto: papel (#F4F4F0, #EAE8E3) com tinta (#050505–#111111) e vermelho de aviação (#E61919, #FF2A2A) no modo claro; CRT (#0A0A0A, #121212) com fósforo (#EAEAEA), o mesmo vermelho e verde terminal opcional em um único elemento no modo escuro.
5. **Layout** — grid de blueprint, compartimentalização com bordas sólidas, densidade bimodal e raio zero em todos os cantos.
6. **Componentes e simbologia** — decoração sintática em ASCII, marcadores ®/©/™ como geometria, crosshairs, códigos de barras, faixas de alerta e strings técnicas.
7. **Textura e pós-processamento** — meio-tom e dithering 1-bit, scanlines de CRT via `repeating-linear-gradient`, ruído SVG global em baixa opacidade.
8. **Diretivas de engenharia** — grid determinístico com `gap: 1px`, tags semânticas (`data`, `samp`, `kbd`, `output`, `dl`) e `clamp()` só na macro-tipografia.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill industrial-brutalist-ui
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Landing de ferramenta de infraestrutura:** modo Swiss Print, títulos em Archivo Black com tracking negativo, réguas de 1 px e vermelho só em alertas.
- **Dashboard de segurança:** modo Tactical Telemetry, tabelas monoespaçadas densas, crosshairs e glow de fósforo discreto.
- **Página de release:** numerais gigantes sangrando a viewport, strings como `REV 2.6` e `UNIT / D-01` e scanlines de fundo.

## Saídas esperadas

Interfaces web em HTML/CSS, React ou Tailwind com grid rígido, tipografia em dois extremos de escala, paleta de substrato única, raio zero e texturas analógicas aplicadas por CSS/SVG.

## Quando usar (e quando não usar)

- **Use quando:** o brief pede uma estética industrial, técnica, editorial-suíça ou de terminal, com alta densidade e personalidade forte.
- **Evite quando:** o produto precisa de acessibilidade ampla, tom acolhedor ou consistência com design systems de consumo; a estética é deliberately hostil.

## Limitações e cuidados

- É um protocolo fixo, opt-in, sem verificação automatizada do resultado.
- Scanlines, ruído e dithering podem reduzir legibilidade e precisam de disciplina de contraste.
- A regra de raio zero e os símbolos técnicos podem conflitar com guias de marca.
- O conteúdo foi lido do `SKILL.md` renderizado; referências internas não foram inspecionadas.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **395.519**, primeira aparição em 19 de março de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Estilos vizinhos: [Minimalist UI](minimalist-ui.md), [High-End Visual Design](high-end-visual-design.md).
- Família: [Design Taste Frontend](design-taste-frontend.md).
- Conceito: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).

## Perguntas abertas

- Como a estética lida com acessibilidade e leitores de tela em dados densos?
- Os dois paradigmas são realmente intercambiáveis em qualquer produto?
- As texturas analógicas têm custo de performance medido?
- Há versão clara e escura do mesmo sistema ou só uma por projeto?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/industrial-brutalist-ui (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
