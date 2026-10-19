---
type: skill
name: Brandkit
slug: brandkit
url: https://www.skills.sh/leonxlnx/taste-skill/brandkit
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/brandkit/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, identidade-de-marca, geracao-de-imagem, logo, direcao-de-arte, agent-skills]
---

# Brandkit

> Skill de geração de imagens de identidade de marca: produz um board de brand kit premium em uma única imagem, com estratégia, logo, paleta, tipografia, aplicações e direção de imagem.

## O que é

`brandkit` é uma skill de geração de imagem, não de código. O texto instrui o modelo a agir como diretor de arte de identidade e designer de logo, produzindo boards que pareçam saídos de um estúdio sério — intencionais, premium, mínimos, coerentes e "visualmente caros".

O padrão é uma imagem de visão geral do brand kit em grid 3×3, proporção 4:3 ou 16:10, com gutter consistente, tipografia escassa e uma ideia forte por painel. A skill aceita layouts alternativos (2×3, 2×2, 1×3, 4×2) e dimensões pedidas pelo usuário.

## Como funciona

O fluxo combina estratégia e composição:

- **DNA de referência** — canvas externo escuro, painéis em grid, gutters fortes, densidade contida, tipografia esparsa, mockups de UI, molduras de browser/terminal, texturas de meio-tom/grão/scanline, diagramas de construção e acentos mudos.
- **Princípio central** — o board é um argumento visual sobre por que a marca existe: o que representa, qual é a metáfora, como o logo a expressa, como o sistema escala e por que é apropriável.
- **Intake de marca** — distinguir criação do zero, extensão de marca existente e refresh/rebrand; fazer uma pergunta curta só para o que faltar; preservar ativos fornecidos.
- **Estratégia antes da imagem** — categoria, público, função, promessa emocional, posição cultural, nível de confiança e metáfora simbólica, com tabela de categoria → ideias → lógica de símbolo.
- **Métodos de logo** — monograma com significado, ação do produto, fusão de metáforas, espaço negativo e geometria de construção; usar no máximo dois combinados.
- **Composição do board** — painéis de capa, construção do logo, aplicação digital, essência/tagline, sistema de cor, tipografia, aplicação física, direção de imagem e detalhe de sistema.
- **Modos visuais** — Dark Developer/Builder, Dark Product/Operator, Dark Nature/Calm, Dark Security, Light Editorial/Compliance, Luxury/Beauty/Fashion, Voice/Communication e Cultural/Experimental, cada um com pistas visuais e lógica de logo.
- **Disciplina** — paleta dominante única, texto mínimo, imagens art-directed, mockups de identidade (não demos de feature) e lista extensa de anti-padrões genéricos.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill brandkit
```

A skill depende de um gerador de imagens disponível no harness; ela descreve o prompt internamente e reporta o tamanho real gerado.

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Ferramenta para desenvolvedores:** modo Dark Developer, logo de cursor + moldura, paleta preto + ciano + coral e painel de terminal.
- **Produto de segurança:** modo Dark Security, símbolo de escudo/raposa/olho, radar e chips de alerta.
- **Marca de luxo:** modo Luxury, monograma serifado, papel texturizado, embossing e croppings editoriais.

## Saídas esperadas

Uma imagem de brand kit com 2 a 9 painéis, logo consistente entre aplicações, paleta disciplinada, tipografia legível e textos curtos (nome, tagline, URL, comando e rótulos).

## Quando usar (e quando não usar)

- **Use quando:** for preciso visualizar uma identidade de marca completa, um conceito de logo ou um deck de diretrizes em imagem.
- **Evite quando:** o pedido é implementação de frontend, design system em código ou qualquer tarefa sem geração de imagem.

## Limitações e cuidados

- A qualidade depende do gerador de imagens disponível; texto dentro da imagem pode sair ilegível.
- Dimensões exatas podem não ser suportadas: a skill manda explicar o limite e reportar o tamanho real.
- Boards de uma única imagem não substituem um design system implementável.
- Ativos de marca fornecidos devem ser reutilizados; a skill proíbe redesenhá-los sem pedido.
- O conteúdo foi lido do `SKILL.md` renderizado; o prompt final enviado ao gerador não foi inspecionado.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **389.461**, primeira aparição em 26 de abril de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conceitos: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md), [Design system com agentes](../../../../concepts/design-system-com-agentes.md).
- Skills de imagem vizinhas: [Imagegen Frontend Web](imagegen-frontend-web.md), [Image Taste Frontend](image-taste-frontend.md).

## Perguntas abertas

- Como a skill garante consistência do logo entre painéis em geradores diferentes?
- Há suporte a edição incremental de um board já gerado?
- O intake de uma pergunta cobre marcas complexas?
- Os boards são avaliados por algum critério objetivo?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/brandkit (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
