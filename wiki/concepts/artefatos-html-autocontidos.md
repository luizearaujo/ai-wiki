---
type: concept
aliases: [Artefatos HTML autocontidos, Self-contained HTML, Single-file HTML]
status: draft
created: 2026-10-19
updated: 2026-10-23
tags: [agentes, html, design, svg, skills, artefatos]
---

# Artefatos HTML autocontidos

> Padrão em que o agente entrega um único arquivo HTML com CSS, JavaScript e SVG inline, sem build nem dependências instaláveis, para que o artefato rode em qualquer navegador e seja versionável como texto.

## Definição

Um artefato HTML autocontido é um documento que carrega tudo o que precisa para renderizar: estilos, scripts, imagens vetoriais e, às vezes, imagens raster em base64. Não há `npm install`, bundler, servidor ou plugin de navegador.

No contexto de agentes, o padrão resolve três problemas:

1. **distribuição** — um arquivo pode ser aberto, enviado ou versionado sem ambiente;
2. **determinismo** — o resultado não depende de uma toolchain instalada;
3. **revisão** — o agente e o humano podem ler o arquivo inteiro e comparar diffs.

## Como funciona

O padrão aparece em duas variantes principais:

| Variante | Conteúdo | Exemplo |
|---|---|---|
| **Apresentação** | HTML + CSS + JS inline, palco fixo, animações, navegação, edição de texto | [Frontend Slides](../skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) |
| **Diagrama** | HTML + CSS embutido + SVG inline, sistema de design, acessibilidade | [Diagram Design](../skills/github.com/cathrynlavery/diagram-design/diagram-design.md) |

Boas práticas observadas:

- manter o arquivo **único** e sem dependências de build;
- usar fontes externas apenas quando permitido, com fallback;
- verificar overflow e sobreposição em navegador real ou screenshot;
- incluir acessibilidade (`role`, `title`, `desc`, contraste, movimento reduzido);
- separar tokens de design (cores, tipografia, espaçamento) para permitir customização;
- versionar o arquivo no repositório, não apenas como anexo de conversa.

## Onde aparece

- [Frontend Slides](../skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — apresentações de 1920×1080 com CSS/JS inline, edição inline e exportação estática.
- [Diagram Design](../skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — diagramas em HTML com SVG inline, contrato de acessibilidade e exportação manual.
- [calesthio/OpenMontage](../repos/github.com/calesthio/openmontage.md) — usa HTML/CSS/GSAP (HyperFrames) e React/Remotion como runtimes de composição, gerando vídeo a partir de artefatos programáticos.
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — gera `graph.html` autocontido para visualizar o grafo.
- [Excalidraw Diagram](../skills/github.com/coleam00/excalidraw-diagram-skill/excalidraw-diagram.md) — a saída principal é JSON do Excalidraw, não HTML, mas o pipeline de validação visual renderiza cada diagrama via um template HTML local antes da entrega.
- [oso95/scroll-world](../repos/github.com/oso95/scroll-world.md) — entrega um motor de scroll em JavaScript puro (`scrub-engine.js`) e um `index-template.html` mínimo que reproduzem a landing page gerada em qualquer HTML simples, Next.js, Vue ou página servida por Python, sem assumir stack.

## Trade-offs

- **Vantagens:** portabilidade; nenhuma build; fácil de versionar e revisar; funciona offline; o agente consegue gerar e inspecionar o arquivo inteiro.
- **Limitações:** arquivos grandes e difíceis de manter manualmente; duplicação de CSS/JS entre artefatos; sem modularização; acessibilidade e performance dependem do cuidado do agente; fontes e assets externos podem quebrar a promessa de autocontenção.
- **Critério prático:** vale para artefatos entregáveis e de vida curta (deck, diagrama, relatório visual); para produtos que evoluem, um projeto com build e componentes é mais sustentável.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — o formato é distribuído como skill com instruções e arquivos de apoio; [Agent harness](agent-harness.md) — o agente que gera o artefato.
- **Depende de:** navegador moderno, fontes com fallback e, opcionalmente, scripts de exportação.
- **Contrasta com:** aplicações React/Vue com build; documentos PDF; apresentações binárias (.pptx/.key).

## Perguntas abertas

- Como testar artefatos HTML de forma automatizada em CI (overflow, contraste, acessibilidade)?
- Qual é o limite prático de tamanho antes de o arquivo único virar um problema?
- Como compartilhar tokens de design entre vários artefatos sem build?
- O padrão é uma escolha estética ou uma resposta à falta de ambiente de execução dos agentes?
- Como garantir que fontes e assets externos não quebrem a portabilidade?

## Fontes

- [Frontend Slides](../skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — página do skills.sh (consultada em 2026-10-19).
- [Diagram Design](../skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — página do skills.sh (consultada em 2026-10-19).
- [calesthio/OpenMontage](../repos/github.com/calesthio/openmontage.md) — README no commit `c8066452325cb57c8fc1ba8c2a71b6e8842e6b65` (consultado em 2026-10-19).
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — README no commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8` (consultado em 2026-10-19).
- [oso95/scroll-world](../repos/github.com/oso95/scroll-world.md) — README no commit `71cc36d3bb150248ae36a2c552f9cbf88802a79c` (consultado em 2026-10-23).
