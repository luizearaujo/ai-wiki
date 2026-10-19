---
type: skill
name: Redesign Existing Projects
slug: redesign-existing-projects
url: https://www.skills.sh/leonxlnx/taste-skill/redesign-existing-projects
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/redesign-skill/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, redesign, auditoria-de-ux, frontend, acessibilidade, agent-skills]
---

# Redesign Existing Projects

> Skill de upgrade visual para sites e apps existentes: varre o código, audita padrões genéricos por área e aplica melhorias pontuais sem trocar framework nem quebrar funcionalidade.

## O que é

`redesign-existing-projects` é a skill de redesign do pacote `taste-skill`. Diferente das skills de estilo, ela não impõe uma estética: parte do que já existe, diagnostica o que parece genérico ou inacabado e propõe correções de alto impacto.

O alvo declarado é elevar projetos ao padrão premium sem reescrever do zero. Ela funciona com qualquer framework CSS ou CSS puro e exige que o agente respeite a stack atual.

## Como funciona

O processo tem três fases — **Scan**, **Diagnose**, **Fix** — seguidas de uma auditoria extensa organizada por área:

- **Tipografia** — fontes padrão ou Inter, headlines sem presença, corpo largo demais, pesos ausentes, números proporcionais, tracking, caixa alta em tudo e palavras órfãs.
- **Cor e superfícies** — preto puro, acentos supersaturados, mais de um acento, cinzas quentes e frios misturados, gradiente "de IA", sombras genéricas, ausência de textura, gradientes uniformes, direção de luz inconsistente e seções escuras aleatórias.
- **Layout** — tudo centralizado, três cards iguais, `100vh`, matemática de flexbox, ausência de `max-width`, alturas forçadas, raio uniforme, falta de sobreposição e profundidade, ritmo vertical e alinhamento óptico.
- **Interatividade e estados** — hover, active, foco visível, loading, vazio, erro, links mortos, indicação de página atual, navegação só com ícones, scroll suave e animação de propriedades de layout.
- **Conteúdo** — nomes genéricos, números redondos falsos, marcas fictícias óbvias, clichês de copy, exclamações, "Oops!", voz passiva, datas iguais e Lorem Ipsum.
- **Componentes** — card genérico, par filled/ghost, badges-pílula, FAQ em acordeão, carrossel de depoimentos, três torres de preço, modais para tudo, avatares circulares e footer de quatro colunas.
- **Iconografia** — Lucide/Feather por padrão, metáforas clichês, espessura inconsistente e favicon ausente.
- **Qualidade de código** — div soup, navegação colapsada inerte, estilos inline, larguras fixas, alt text ausente, z-index arbitrário, código morto e imports alucinados.
- **Omissões estratégicas** — links legais, navegação de volta, 404, validação, skip link e consentimento de cookies.

Depois da auditoria, a skill lista **técnicas de upgrade** (tipografia variável, máscaras de texto, grid quebrado, parallax de cards, scroll com inércia, física de mola, glassmorphism real, bordas com spotlight, grão) e uma **ordem de prioridade de correção**: fonte, paleta, estados, layout, componentes, estados de dados e polimento tipográfico.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill redesign-existing-projects
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Landing antiga em Bootstrap:** trocar a fonte, limpar a paleta e substituir a fileira de três cards por grid assimétrico, mantendo o framework.
- **Dashboard interno:** adicionar skeleton loaders, estado vazio composto, foco visível e alinhar CTAs ao rodapé dos cards.
- **Site institucional:** corrigir nomes e números fictícios, remover clichês de copy e adicionar links legais e página 404.

## Saídas esperadas

Mudanças pontuais no código existente, com uma lista de achados por área, prioridades explícitas e nenhuma migração de framework ou de biblioteca de estilo.

## Quando usar (e quando não usar)

- **Use quando:** existe um projeto real com visual genérico ou inacabado e o objetivo é elevá-lo sem reescrita.
- **Evite quando:** o projeto é greenfield ou o brief pede uma direção de arte nova do zero; nesse caso, as skills de estilo ou a [v2 padrão](design-taste-frontend.md) são mais adequadas.

## Limitações e cuidados

- A auditoria é uma lista de verificação, não uma ferramenta automática: depende de o agente ler o código e aplicar julgamento.
- Algumas recomendações são opinativas e podem conflitar com um design system existente.
- O texto exige testar após cada mudança, mas não define uma suíte de testes.
- O conteúdo foi lido a partir do `SKILL.md` renderizado; referências e scripts não foram inspecionados.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **457.215**, primeira aparição em 1º de março de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Família: [Design Taste Frontend](design-taste-frontend.md), [v1](design-taste-frontend-v1.md), [v2 experimental](design-taste-frontend-v2-experimental.md).
- Conceitos: [Auditoria de UX](../../../../concepts/auditoria-de-ux.md), [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).

## Perguntas abertas

- A ordem de prioridade funciona igualmente bem em projetos grandes?
- Como a skill lida com design systems que violam as próprias regras?
- Há critério para decidir quando o redesign deve substituir o visual antigo?
- As recomendações de acessibilidade seguem WCAG 2.2?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/redesign-existing-projects (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
