---
type: skill
name: Design Taste Frontend v2 Experimental
slug: design-taste-frontend-v2-experimental
url: https://www.skills.sh/leonxlnx/taste-skill/design-taste-frontend-v2-experimental
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/taste-skill-v2-experimental/SKILL.md
author: leonxlnx
version: v2 experimental (arquivo único)
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, anti-slop, frontend, dials, legado, agent-skills]
---

# Design Taste Frontend v2 Experimental

> Versão experimental em arquivo único da segunda geração da taste-skill: infere o brief, deriva três dials, escolhe o design system honesto e proíbe os padrões "com cara de IA" — preservada para projetos que dependem do comportamento exato dela.

## O que é

A `design-taste-frontend-v2-experimental` é uma skill de regras de frontend anti-slop entregue como um único documento longo (cerca de 85 mil caracteres na página). Ela se declara fora de escopo para dashboards, tabelas de dados e UI de produto com múltiplas etapas: o alvo são landing pages, portfólios e redesigns.

A própria página a apresenta como a antiga v2 experimental, mantida para projetos que dependem do comportamento exato; a versão padrão atual é [Design Taste Frontend](design-taste-frontend.md). A diferença estrutural é o formato: aqui tudo vive em um arquivo, sem scripts de sorteio, gate de lint ou inspeção por screenshots.

## Como funciona

O documento é numerado e conduz o agente por catorze seções:

0. **Inferência do brief** — ler tipo de página, palavras de clima, referências, público, ativos de marca e restrições silenciosas; emitir uma "Design Read" de uma linha antes de qualquer código; se o brief for ambíguo, fazer uma única pergunta.
1. **Os três dials** — `DESIGN_VARIANCE` (8), `MOTION_INTENSITY` (6) e `VISUAL_DENSITY` (4), com tabela que converte sinais ("minimalist", "premium consumer", "Awwwards", "public-sector") em valores e presets por caso de uso.
2. **Mapa brief → design system** — quando usar pacote oficial (Fluent UI, Material 3, Carbon, Polaris, Atlassian, Primer, GOV.UK, USWDS, Bootstrap, Radix, shadcn/ui, Tailwind v4) e quando a direção é apenas estética, sem biblioteca dona.
3. **Arquitetura padrão** — stack, estado, ícones, política de emoji, mecânica responsiva e verificação obrigatória de dependências.
4. **Diretivas de engenharia de design** — correção de viés em tipografia, cor, layout, estados e formulários.
5. **Proatividade contextual** — esqueletos canônicos de sticky-stack, horizontal-pan e revelação escalonada, além de padrões de animação proibidos.
6. **Guardas de performance e acessibilidade** — aceleração por hardware, `prefers-reduced-motion`, modo escuro, Core Web Vitals e custo de DOM.
7. **Definições técnicas dos dials** — referência para aplicar os valores globalmente.
8. **Protocolo de modo escuro** — estratégia de tokens, padrão por contexto e teste nos dois modos.
9. **AI tells** — catálogo de padrões visuais, tipográficos, de layout, conteúdo e recursos externos que denunciam geração por modelo, incluindo a proibição de travessão (em-dash).
10. **Vocabulário de referência** — nomes de padrões de hero, navegação, grid, card, scroll, mídia, tipografia e micro-interação.
11. **Protocolo de redesign** — detectar modo, auditar antes de tocar, regras de preservação, alavancas de modernização e árvore de decisão entre evolução e redesign completo.
12. **Biblioteca de blocos** — contrato de arquivos, frontmatter e seções obrigatórias.
13. **Fora de escopo.**
14. **Pré-voo final.**

Os apêndices trazem comandos de instalação por design system e uma distinção explícita entre o que é oficial e o que é aproximação (por exemplo, "liquid glass" na web).

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill design-taste-frontend-v2-experimental
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Landing de SaaS técnico:** design read "B2B SaaS para compradores técnicos, linguagem Linear, Tailwind + Geist + movimento contido"; dials em 7/6/4.
- **Redesign preservando marca:** usar o protocolo da seção 11, manter ativos existentes e aplicar as alavancas na ordem de prioridade.
- **Serviço público:** dials em 3/2/5 e `govuk-frontend` ou `uswds`, sem recriar o CSS oficial à mão.

## Saídas esperadas

Código frontend em React, Next.js, HTML/CSS ou Tailwind, com uma Design Read declarada, dials justificados, tokens e estados completos, design system oficial quando o brief pedir, e nenhum dos padrões listados como AI tells.

## Quando usar (e quando não usar)

- **Use quando:** for necessário reproduzir o comportamento exato desta geração experimental, ou comparar decisões com a versão padrão.
- **Evite quando:** o trabalho é novo e pode usar a [versão padrão](design-taste-frontend.md), que adiciona sorteio de direção, scripts e inspeção no navegador; ou quando o alvo é dashboard, tabela de dados ou UI de produto multi-etapas — explicitamente fora de escopo.

## Limitações e cuidados

- É um documento único e longo: depende de o agente carregar e aplicar todas as seções sem ferramenta de verificação.
- Não há scripts de sorteio, lint, inspeção ou captura de screenshots.
- A página declara a versão como experimental e recomenda a atual para trabalho novo.
- Vários comandos e referências internas citados no texto não foram inspecionados; o conteúdo veio do `SKILL.md` renderizado.
- O rótulo "6 days ago" da data de primeira aparição foi observado em 2026-10-19 e corresponde a cerca de 2026-10-13.

## Estado e adoção

- Versão: **v2 experimental**, arquivo único.
- Instalações observadas em 2026-10-19: **18.329**, primeira aparição há cerca de 6 dias (por volta de 2026-10-13).
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Substituída por: [Design Taste Frontend](design-taste-frontend.md) (v2 padrão).
- Variantes: [v1](design-taste-frontend-v1.md); alias [Taste Skill](taste-skill.md).
- Conceito: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).

## Perguntas abertas

- Quais seções desta versão foram incorporadas à v2 padrão e quais foram descartadas?
- O formato de arquivo único tem custo de contexto maior ou menor que o run em múltiplos arquivos?
- Há casos em que esta versão produz resultado melhor que a padrão?
- A seção de biblioteca de blocos chegou a ser implementada?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/design-taste-frontend-v2-experimental (consultada em 2026-10-19); `SKILL.md` renderizado na página, cerca de 85 mil caracteres.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
