---
type: skill
name: High-End Visual Design
slug: high-end-visual-design
url: https://www.skills.sh/leonxlnx/taste-skill/high-end-visual-design
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/soft-skill/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, frontend, motion, micro-interacao, agent-skills]
---

# High-End Visual Design

> Skill de estilo clássico, opt-in, que personifica um arquiteto de UI e coreógrafo de movimento de nível Awwwards: varia arquétipos a cada execução e aplica uma linguagem "Apple-esque / Linear-tier" com profundidade tátil.

## O que é

`high-end-visual-design` é uma das skills de estilo fixo do pacote `taste-skill`. A página a descreve como opt-in: só roda quando chamada pelo nome. O texto se apresenta como um "Principal UI/UX Architect & Motion Choreographer" cujo objetivo é produzir experiências digitais de agência de US$ 150 mil, não apenas sites.

O eixo é o **Variance Mandate**: nunca gerar o mesmo layout ou estética duas vezes seguidas. O agente combina um arquétipo de clima e um arquétipo de layout a cada execução, sempre dentro de uma linguagem premium declarada.

## Como funciona

O documento tem oito seções:

1. **Meta e diretiva central** — persona, objetivo e mandato de variância.
2. **Diretiva "Absolute Zero"** — fontes banidas (Inter, Roboto, Arial, Open Sans, Helvetica), ícones pesados, bordas e sombras genéricas, navbars coladas ao topo, grids simétricos de três colunas e transições lineares.
3. **Motor de variância criativa** — escolher um arquétipo de clima (Ethereal Glass, Editorial Luxury, Soft Structuralism) e um de layout (Asymmetrical Bento, Z-Axis Cascade, Editorial Split), cada um com colapso mobile prescrito.
4. **Micro-estética tátil** — o "Double-Bezel" (shell externo + núcleo interno com raio concêntrico), botões-pílula com ícone aninhado em círculo próprio, macro-whitespace e eyebrow tags.
5. **Coreografia de movimento** — nav flutuante em vidro, morph do hambúrguer em "X", overlay de tela cheia, revelação escalonada de links, física de hover magnética e entradas por `IntersectionObserver`.
6. **Guardas de performance** — animar só `transform` e `opacity`, `backdrop-blur` apenas em elementos fixos/sticky, grão em pseudo-elemento fixo e z-index reservado a camadas sistêmicas.
7. **Protocolo de execução** — pensar, montar o scaffold, arquitetar com Double-Bezel, coreografar e entregar.
8. **Checklist pré-output** — onze verificações antes de entregar.

A skill usa convenções de React/Tailwind no texto, mas o protocolo de saída aceita React/Tailwind/HTML.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill high-end-visual-design
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Landing de SaaS de IA:** clima Ethereal Glass com fundo OLED, orbes radiais e cards com blur; layout Bento assimétrico.
- **Site de imobiliária de luxo:** clima Editorial Luxury com cremes quentes, serifada variável e grão de filme; layout Editorial Split.
- **Portfólio de estúdio:** Soft Structuralism com fundo claro, tipografia grotesca massiva e sombras ambientes difusas.

## Saídas esperadas

Código React/Tailwind ou HTML com arquétipos escolhidos explicitamente, containers em Double-Bezel, CTAs com ícone aninhado, seções com pelo menos `py-24`, transições em cubic-bezier customizado, entradas animadas e colapso single-column abaixo de 768 px.

## Quando usar (e quando não usar)

- **Use quando:** o pedido é uma superfície visual premium e o usuário quer uma estética de agência com movimento elaborado.
- **Evite quando:** o brief pede sobriedade, acessibilidade radical ou consistência com um design system oficial; a skill é opinativa e não oferece um modo neutro.

## Limitações e cuidados

- Por ser opt-in e baseada em persona, depende de chamada explícita; não é o comportamento padrão do pacote.
- As regras são fixas e opinativas: não há auditoria do resultado renderizado nem gate automatizado.
- O texto prescreve `backdrop-blur` pesado e orbes radiais, que podem conflitar com metas de performance e com diretrizes de marca.
- O conteúdo foi lido do `SKILL.md` renderizado; scripts e referências internas não foram inspecionados.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **457.059**, primeira aparição em 15 de março de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Família: [Design Taste Frontend](design-taste-frontend.md) (v2 padrão), [v1](design-taste-frontend-v1.md), [v2 experimental](design-taste-frontend-v2-experimental.md).
- Estilos vizinhos: [Minimalist UI](minimalist-ui.md), [Industrial Brutalist UI](industrial-brutalist-ui.md).
- Conceito: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).

## Perguntas abertas

- Como a skill evita repetição entre execuções se o sorteio é silencioso?
- Os arquétipos de clima foram calibrados com alguma amostra de sites?
- Há suporte a `prefers-reduced-motion` no texto publicado?
- A persona de agência muda decisões quando o brief é conservador?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/high-end-visual-design (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
