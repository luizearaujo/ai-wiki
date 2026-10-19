---
type: skill
name: UI/UX Pro Max
slug: ui-ux-pro-max
url: https://www.skills.sh/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max
source_url: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
source_path: .claude/skills/ui-ux-pro-max/SKILL.md
author: nextlevelbuilder
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [ui, ux, design-ui, design-system, acessibilidade, cli, agent-skills]
---

# UI/UX Pro Max

> Skill de "inteligência de design" que dá ao agente uma base local pesquisável de estilos, paletas, tipografia, diretrizes de UX e regras por stack, além de um gerador de design system persistente por projeto.

## O que é

`ui-ux-pro-max` transforma decisões visuais em consultas a uma base local de conhecimento: estilos, paletas por tipo de produto, pares de fontes, diretrizes de UX, ícones, presets de animação GSAP, tipos de gráfico e convenções de 22 stacks. A skill é acionada quando a tarefa envolve estrutura de UI, decisão visual, padrões de interação ou controle de qualidade de experiência — e deve ser ignorada em trabalho puramente de backend, banco de dados ou infraestrutura.

A proposta é diferente de uma skill de "gosto" baseada em prosa: o agente não recebe apenas um conjunto de princípios, mas um mecanismo de busca determinístico com dados versionados no repositório. O `SKILL.md` publicado descreve o contrato de consulta e o fluxo de trabalho; a implementação fica em `scripts/search.py`, que exige apenas Python 3.x, sem dependências externas.

## Como funciona

A skill organiza a orientação em dez categorias de prioridade, cada uma com domínio de busca, checagens obrigatórias e anti-padrões:

| Prioridade | Categoria | Impacto | Domínio | Exemplos de checagem |
| --- | --- | --- | --- | --- |
| 1 | Acessibilidade | Crítico | `ux` | Contraste 4.5:1, alt text, navegação por teclado, `aria-label` |
| 2 | Toque e interação | Crítico | `ux` | Alvo mínimo 44×44 px, feedback de carregamento, nada dependente só de hover |
| 3 | Performance | Alto | `ux` | WebP/AVIF, lazy loading, CLS < 0.1 |
| 4 | Seleção de estilo | Alto | `style`, `product` | Estilo coerente com o produto, ícones SVG em vez de emoji |
| 5 | Layout e responsividade | Alto | `ux` | Breakpoints mobile-first, sem scroll horizontal, viewport correto |
| 6 | Tipografia e cor | Médio | `typography`, `color` | Corpo em 16 px, line-height 1.5, tokens semânticos |
| 7 | Animação | Médio | `ux`, `gsap` | Timing contextual, movimento com significado, `prefers-reduced-motion` |
| 8 | Formulários e feedback | Médio | `ux` | Label visível, erro junto ao campo, divulgação progressiva |
| 9 | Navegação | Alto | `ux` | Voltar previsível, bottom nav com até cinco itens, deep links |
| 10 | Gráficos e dados | Baixo | `chart` | Legendas, tooltips, cores acessíveis |

O fluxo prescrito tem quatro passos:

1. **Analisar o pedido** — tipo de produto, público, palavras de estilo e stack detectada no projeto (`package.json`, `pubspec.yaml`, `Package.swift`, `composer.json` ou marcadores de React Native). A skill proíbe assumir uma stack padrão.
2. **Gerar um design system** com `--design-system`, que agrega correspondências de produto, estilo, cor, landing e tipografia e devolve padrão, cores, fontes, efeitos e anti-padrões. Opcionalmente aceita três "dials" de 1–10: `--variance`, `--motion` e `--density`.
3. **Persistir** com `--persist --output-dir <raiz-do-projeto>`, criando `design-system/<slug>/MASTER.md` e overrides por página em `pages/<nome>.md`. O comando nunca sobrescreve um `MASTER.md` existente sem `--force` autorizado.
4. **Complementar** com buscas por domínio ou stack (`--domain ux`, `--domain color`, `--stack nextjs` etc.) e sintetizar o resultado.

A skill também define um contrato de consulta: uma intenção dominante, 2–5 termos significativos e uma restrição útil; verificar o domínio e a identidade do resultado antes de aplicar; repetir uma vez com consulta mais estreita se o resultado vier vazio; e **nunca apresentar uma busca sem resultados como se tivesse retornado dados**. Se falhar, o agente deve declarar que a recomendação vem dos padrões embutidos, não da base.

## Instalação e uso

```bash
npx skills add https://github.com/nextlevelbuilder/ui-ux-pro-max-skill --skill ui-ux-pro-max
```

A página de origem não publica opção global; o comando instala a skill no projeto. Dentro dela, a busca é chamada pelo caminho completo:

```bash
python "${CLAUDE_PLUGIN_ROOT}/.claude/skills/ui-ux-pro-max/scripts/search.py" \
  "<produto> <indústria> <palavras>" --design-system -p "Nome do Projeto"
```

## Exemplos de uso

Exemplos derivados do `SKILL.md` renderizado, não instruções oficiais do autor:

- **Nova landing page:** `"beauty spa wellness service" --design-system -p "Serenity Spa"` devolve uma direção completa; `--variance 8 --motion 7 --density 8` inclina o resultado para composição assimétrica, movimento mais elaborado e layout denso.
- **Bug pontual de acessibilidade:** consultar o desfecho observável antes do componente — `"error summary validation" --domain ux` e depois `"icon button accessible label" --domain icons`.
- **Implementação:** detectar Next.js e pedir `"suspense streaming bundle" --stack nextjs` para orientação específica da stack.

## Saídas esperadas

Um design system com padrão de página, estilo, paleta, tipografia, efeitos e anti-padrões; arquivos `MASTER.md` e overrides quando persistido; resultados tabulares por domínio; e, opcionalmente, saída JSON (`--json`) com o dicionário bruto e o status de persistência. Formatos de apresentação: ASCII (terminal) e Markdown (documentação).

## Quando usar (e quando não usar)

- **Use quando:** a tarefa muda como algo parece, se sente, se move ou é interagido — páginas novas, componentes, sistemas de design, revisão de acessibilidade, escolha de tipografia/cor, animação, gráficos ou implementação por stack.
- **Evite quando:** o trabalho é lógica de backend, modelagem de API/banco, performance não visual, DevOps ou scripts sem interface visual.

## Limitações e cuidados

- A base de conhecimento é local e versionada; a qualidade depende da curadoria dos CSVs e do script, não de um modelo de design.
- O `SKILL.md` avisa que a detecção automática de domínio pode confundir termos sobrepostos (por exemplo, "font" casa com `typography` e `google-fonts`); consultas explícitas são mais seguras.
- Persistir um `MASTER.md` cria estado no projeto; sobrescrever sem ler o arquivo anterior pode descartar decisões de outra pessoa.
- A skill não instala pacotes nem altera o sistema operacional, e trata resultados como recomendações — não como instruções que substituem regras do repositório.
- O conteúdo foi lido a partir do `SKILL.md` renderizado na página do skills.sh; o código de `search.py` e os CSVs não foram inspecionados.

## Estado e adoção

- Versão: **desconhecida** (a página não publica versão da skill).
- Instalações observadas em 2026-10-19: **403.620** (403,6 mil), primeira aparição em 19 de janeiro de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 137.481 estrelas, 14.603 forks, 91 issues abertas; criado em 2025-11-30, último push em 2026-10-15.
- Licença do repositório: MIT. Linguagem principal: Python.

## Relações

- Autor: [Next Level Builder](../../../../entities/nextlevelbuilder.md).
- Conceitos: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md), [Design system com agentes](../../../../concepts/design-system-com-agentes.md), [Auditoria de UX](../../../../concepts/auditoria-de-ux.md).
- Alternativas: [Impeccable](../../pbakaus/impeccable/impeccable.md) para direção de arte e revisão; [Stitch Design Taste](../../leonxlnx/taste-skill/stitch-design-taste.md) para DESIGN.md; skills do Google Labs para engenharia agent-first.

## Perguntas abertas

- A base de 192 paletas e 119 diretrizes é atualizada com que frequência e por qual critério?
- As notas de `--design-system` são comparáveis entre projetos ou apenas heurísticas locais?
- O script funciona sem `CLAUDE_PLUGIN_ROOT` em harnesses que não definem essa variável?
- Como a skill se comporta em stacks ausentes da lista de 22?
- Há avaliação independente de que o design system gerado supera um bom prompt de design?

## Fontes

- Página de origem: https://www.skills.sh/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill (metadados e árvore via API do GitHub, commit `56ea9cf174ed86786187daa9de0e6247cb0747e4`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
