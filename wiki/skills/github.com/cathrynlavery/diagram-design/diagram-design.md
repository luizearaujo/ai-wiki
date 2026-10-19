---
type: skill
name: Diagram Design
slug: diagram-design
url: https://www.skills.sh/cathrynlavery/diagram-design/diagram-design
source_url: https://github.com/cathrynlavery/diagram-design
source_path: skills/diagram-design
author: cathrynlavery
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [diagramas, design, svg, html, visualizacao, agent-skills]
---

# Diagram Design

> Skill que orienta o agente a criar diagramas como arquivos HTML autocontidos com SVG inline e um sistema de design editorial — em vez de Mermaid genérico.

## O que é

Diagram Design é uma skill de [cathrynlavery](../../../../entities/cathrynlavery.md) para diagramas técnicos e editoriais: arquitetura, fluxo, sequência, máquina de estados, ER/modelo de dados, timeline, swimlane, quadrantes, camadas e outros tipos. O resultado é um arquivo `.html` autocontido, com CSS embutido e SVG inline, legível em qualquer navegador moderno.

A proposta é oposta ao "Mermaid slop": a skill insiste que o diagrama seja uma peça de design, com tipografia, paleta, espaçamento e regras de conexão explícitas. O README do repositório fala em 44 tipos; a página da skill publica "forty-five" (45). A divergência é registrada abaixo.

## Como funciona

O `SKILL.md` publicado na página de origem organiza o trabalho em doze seções:

| Seção | Conteúdo |
|---|---|
| 0 | **Style guide gate** — na primeira vez em um projeto, verificar se o style guide ainda está no padrão e oferecer customização (URL, skill, pasta/design system, tokens, manter padrão ou perfil salvo) |
| 1 | **Filosofia** — "a melhor jogada é deletar": um nó por ideia, conexão só quando carrega informação, coral reservado a 1–2 nós focais, densidade-alvo 4/10, acima de 9 nós provavelmente são dois diagramas |
| 2 | **Quando usar** — só quando o leitor aprende mais com o visual do que com prosa, tabela ou lista |
| 3 | **Seleção** — primeiro um padrão semântico (fan-in, trust boundary, lifecycle etc.), depois o tipo visual mais próximo |
| 4 | **Anti-patterns universais** |
| 5 | **Design system** — papéis semânticos, tokens de cor, tipografia |
| 6 | **Primitivas SVG** — conectores, setas, rótulos e regras obrigatórias |
| 7 | **Layout e espaçamento** — limites de densidade e budget de complexidade |
| 8 | **Summary card pattern** |
| 9 | **Checklist pré-output (taste gate)** |
| 10 | **Templates e variantes** |
| 11 | **Importação** de draw.io, Mermaid e Excalidraw |
| 12 | **Output** — HTML único, SVG inline, acessível |

### Contrato de saída

- arquivo HTML único, CSS embutido (externo permitido apenas Google Fonts), SVG inline, sem imagens externas;
- estático por padrão; JavaScript inline só para controles de animação;
- `<svg>` com `role="img"` e `aria-labelledby` apontando para `<title>` e `<desc>` com IDs `<slug>-title` e `<slug>-desc`;
- `<title>` é o primeiro filho do SVG, com até ~60 caracteres;
- `<desc>` descreve o conteúdo em uma frase, não a geometria;
- exportação para PNG/SVG é manual, via `scripts/export_svg.py` e `scripts/export_png.py`, e entrega apenas o nó SVG, sem molduras editoriais.

O método trata o style guide como estado do projeto: ele resolve um marcador `.diagram-design` e perfis salvos, e evita entregar diagramas com a skin padrão em um projeto com marca.

## Instalação e uso

Comando publicado na página de origem:

```bash
npx skills add https://github.com/cathrynlavery/diagram-design --skill diagram-design
```

Depois de instalar, peça o diagrama ao agente. A skill pergunta pelo tipo/objetivo, verifica o style guide na primeira execução e lê a referência do tipo escolhido antes de desenhar.

## Exemplos de uso

Exemplos derivados do método publicado, não instruções oficiais:

- **Arquitetura:** "Desenhe a arquitetura de um serviço de pagamentos com API gateway, fila, workers e banco, destacando trust boundaries."
- **Antes/depois:** "Crie um architecture delta mostrando o que muda ao migrar de monolito para serviços."
- **Fluxo:** "Faça um flowchart do processo de onboarding, com pontos de decisão e exceções."
- **Sequência:** "Desenhe um diagrama de sequência para login OAuth com refresh token."
- **Dados:** "Modele um ER para clientes, pedidos, itens e pagamentos."
- **Timeline:** "Monte uma timeline editorial da evolução do projeto, com marcos e marcos regulatórios."

## Saídas esperadas

- um arquivo HTML autocontido com SVG inline;
- diagrama estático, acessível e legível em navegador moderno;
- estilo coerente com o style guide do projeto (ou decisão explícita de manter o padrão);
- opcionalmente, exportação PNG/SVG sob pedido;
- nenhum wrapper editorial na exportação — apenas o SVG.

## Quando usar (e quando não usar)

- **Use quando:** você precisa de um diagrama técnico ou editorial com acabamento de design, quer um artefato HTML/SVG versionável e não quer depender de Mermaid ou de uma ferramenta externa.
- **Use quando:** o projeto tem (ou pode definir) um style guide e você quer consistência entre diagramas.
- **Evite quando:** você só precisa de um diagrama rápido em texto (a própria skill sugere uma ferramenta de unicode/plain text); o conteúdo é uma lista ou tabela; ou a mudança é puramente de atributos e uma tabela comunica melhor.
- **Evite quando:** você precisa de edição colaborativa em uma ferramenta de diagramas; draw.io/Excalidraw podem ser melhores para o fluxo de trabalho, embora a skill importe esses formatos.

## Limitações e cuidados

- **Conteúdo publicado, não verificado no repositório.** O `SKILL.md` foi lido pela página do skills.sh; o repositório-fonte não foi clonado nem o arquivo cru foi consultado.
- **Divergência de contagem.** A página diz 45 tipos; a descrição da API do GitHub diz 44. Não foi verificado qual está correta.
- **Dependência de design system.** O gate inicial pode interromper a geração até o usuário configurar um style guide; isso é intencional, mas adiciona atrito.
- **Fontes externas.** O output permite Google Fonts; em ambiente offline ou com política de privacidade rígida, isso precisa ser tratado.
- **Acessibilidade parcial.** O contrato cobre `role`, `title` e `desc`, mas não garante contraste, tamanho de texto ou experiência para leitores de tela em diagramas complexos.
- **Exportação manual.** Não há geração automática de PNG/SVG; os scripts precisam de Python e dependências.
- **Instruções de terceiros.** A skill vira contexto executável do agente; revise o conteúdo antes de usar em projeto sensível.
- **Auditorias de segurança.** Gen Agent Trust Hub, Socket e Snyk aparecem como "Pass" em 2026-10-19; isso não é auditoria do conteúdo da skill.

## Estado e adoção

- **Versão da skill:** não publicada na página (observada em 2026-10-19).
- **Catálogo:** 15,5 mil instalações, primeira aparição em 2026-04-19, três auditorias "Pass" (observado em 2026-10-19).
- **Repositório-fonte:** MIT, HTML, ~57,4 mil stars, ~3,7 mil forks; último push em 2026-10-16; commit `550fd66edff058bc73056c3416b76d69cfe865ba` (metadados e árvore consultados via API em 2026-10-19).
- **Preço:** gratuito.
- **Site:** [diagramdesign.dev](https://diagramdesign.dev).

## Relações

- **Autor:** [cathrynlavery](../../../../entities/cathrynlavery.md).
- **Repositório-fonte:** [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design) — `SKILL.md` em `skills/diagram-design/`, com referências, scripts e assets.
- **Conceitos:** [Artefatos HTML autocontidos](../../../../concepts/artefatos-html-autocontidos.md), [Agent skills](../../../../concepts/agent-skills.md).
- **Alternativas:** [Frontend Slides](../../../../skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — mesma filosofia de HTML autocontido, mas para apresentações; Mermaid, draw.io e Excalidraw para fluxos mais rápidos ou colaborativos.

## Perguntas abertas

- São 44 ou 45 tipos de diagrama? A diferença está em um tipo novo ou em contagem divergente?
- Como o style guide é versionado e compartilhado entre projetos e equipes?
- Qual é a qualidade do SVG gerado em termos de acessibilidade e de tamanho de arquivo?
- A skill funciona bem para diagramas muito grandes ou orienta dividir em visão geral + detalhe?
- Como os scripts de exportação lidam com fontes, DPI e temas claros/escuros?
- Como a skill se compara a Mermaid em manutenção e legibilidade ao longo do tempo?

## Fontes

- Página de origem: https://www.skills.sh/cathrynlavery/diagram-design/diagram-design (consultada em 2026-10-19). A página publica o `SKILL.md`, incluindo gate de style guide, filosofia, seleção, design system, contrato de SVG e exportação.
- Repositório-fonte: https://github.com/cathrynlavery/diagram-design (metadados e árvore consultados via API do GitHub em 2026-10-19; commit `550fd66edff058bc73056c3416b76d69cfe865ba`). O repositório não foi clonado e o `SKILL.md` cru não foi lido.
