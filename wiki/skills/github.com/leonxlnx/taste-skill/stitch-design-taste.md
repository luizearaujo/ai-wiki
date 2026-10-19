---
type: skill
name: Stitch Design Taste
slug: stitch-design-taste
url: https://www.skills.sh/leonxlnx/taste-skill/stitch-design-taste
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/stitch-skill/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, design-system, google-stitch, design-md, anti-slop, agent-skills]
---

# Stitch Design Taste

> Skill de sistema de design semântico para o Google Stitch: gera um `DESIGN.md` que traduz regras anti-slop em linguagem visual descritiva, com valores precisos que o agente do Stitch consegue interpretar.

## O que é

`stitch-design-taste` produz um arquivo `DESIGN.md` otimizado para a geração de telas no Google Stitch. Em vez de prescrever apenas classes ou componentes, ela traduz diretivas de engenharia de frontend em "Visual Descriptions" — atmosfera, paleta, tipografia, comportamento de componente, layout, movimento e anti-padrões — acompanhadas de hex codes, escalas e medidas.

O `DESIGN.md` gerado funciona como fonte única de verdade para prompts ao Stitch. A skill pressupõe acesso ao Stitch em `labs.google/stitch` e, opcionalmente, o servidor MCP do Stitch para integração com Cursor, Antigravity ou Gemini CLI.

## Como funciona

O processo tem nove etapas:

1. **Definir a atmosfera** — densidade (de "Art Gallery Airy" a "Cockpit Dense"), variância (de "Predictable Symmetric" a "Artsy Chaotic") e movimento (de "Static Restrained" a "Cinematic Choreography"), com baseline 8/6/4.
2. **Mapear a paleta** — máximo de um acento, saturação abaixo de 80%, proibição do "AI Purple/Blue Neon", bases neutras absolutas, uma única paleta e nunca preto puro.
3. **Estabelecer regras tipográficas** — Inter banido em contextos premium; Geist, Outfit, Cabinet Grotesk ou Satoshi; serifadas genéricas banidas; monoespaçado obrigatório para números quando a densidade passa de 7.
4. **Definir o hero** — imagens inline entre palavras, sem sobreposição, sem texto de preenchimento ("Scroll to explore"), estrutura assimétrica quando a variância passa de 4 e no máximo um CTA primário.
5. **Descrever componentes** — botões com feedback tátil e sem glow, cards só quando a elevação comunica hierarquia, inputs com label acima e erro abaixo, skeletons no lugar de spinners, estados vazios e erros compostos.
6. **Princípios de layout** — grid em vez de matemática de flexbox, `max-width` de contenção, `min-h-[100dvh]` no lugar de `h-screen` e proibição da fileira de três cards iguais.
7. **Regras responsivas** — colapso single-column abaixo de 768 px, sem scroll horizontal, tipografia com `clamp()`, alvos de toque de 44 px e imagens inline que empilham no mobile.
8. **Filosofia de movimento** — física de mola (stiffness 100, damping 20), micro-interações perpétuas, orquestração escalonada e animação só de `transform`/`opacity`.
9. **Anti-padrões** — lista explícita de "NEVER DO": emoji, Inter, preto puro, glow neon, acentos supersaturados, cursores customizados, sobreposição, três colunas iguais, nomes genéricos, números redondos falsos, clichês de copy, texto de preenchimento e imagens quebradas.

O formato de saída tem sete seções: atmosfera, paleta e papéis, tipografia, componentes, layout, movimento e anti-padrões.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill stitch-design-taste
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Landing de produto de infraestrutura:** atmosfera "clinical yet warm", paleta Zinc com um acento coral, Geist + Geist Mono e hero assimétrico.
- **Dashboard denso:** densidade acima de 7, números em monoespaçado e cards substituídos por divisores `border-top`.
- **Marca editorial:** serifada moderna distinta (Fraunces, Editorial New) apenas em contexto editorial, nunca em dashboard.

## Saídas esperadas

Um arquivo `DESIGN.md` com atmosfera, paleta hex, tipografia, comportamentos de componente, layout, movimento e lista de proibições, pronto para alimentar o Stitch.

## Quando usar (e quando não usar)

- **Use quando:** o fluxo de design passa pelo Google Stitch e é preciso um contexto de design persistente e interpretável pelo agente.
- **Evite quando:** o trabalho é em código direto sem Stitch, ou quando o projeto já tem um `DESIGN.md`/design system próprio que deve prevalecer.

## Limitações e cuidados

- O resultado é um documento de intenção: depende da interpretação do Stitch e de o usuário colar o contexto corretamente.
- As regras são opinativas e derivadas da estética anti-slop; podem conflitar com marcas existentes.
- A integração via MCP é opcional e não foi verificada.
- O conteúdo foi lido do `SKILL.md` renderizado; o formato real de consumo pelo Stitch não foi testado.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **393.502**, primeira aparição em 20 de março de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conceitos: [Design system com agentes](../../../../concepts/design-system-com-agentes.md), [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).
- Alternativas: [Impeccable](../../pbakaus/impeccable/impeccable.md) (PRODUCT.md/DESIGN.md), [UI/UX Pro Max](../../nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md).

## Perguntas abertas

- O Stitch interpreta o `DESIGN.md` de forma consistente entre execuções?
- Há formato canônico de `DESIGN.md` compartilhado com outras skills?
- A skill foi testada com o servidor MCP do Stitch?
- Como o documento lida com design systems existentes?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/stitch-design-taste (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
