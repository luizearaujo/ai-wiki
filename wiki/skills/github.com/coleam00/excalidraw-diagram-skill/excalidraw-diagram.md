---
type: skill
name: Excalidraw Diagram
slug: excalidraw-diagram
url: https://github.com/coleam00/excalidraw-diagram-skill
source_url: https://github.com/coleam00/excalidraw-diagram-skill
source_path: .
author: coleam00
version: desconhecida
license: desconhecida
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [diagramas, excalidraw, visualizacao]
---

# Excalidraw Diagram

> Skill que dá a agentes de código a capacidade de gerar diagramas Excalidraw a partir de descrições em linguagem natural, com layout que reflete o conceito e um loop de validação visual via Playwright.

## O que é

Repositório de skill única: o próprio repositório é a skill, sem produto ou CLI separados. Ensina o agente a produzir diagramas que "argumentam visualmente" — em vez de caixas e setas uniformes, usa fan-out para relações um-para-muitos, linhas do tempo para sequências e convergência para agregação. Diagramas técnicos podem incluir trechos de código reais e payloads JSON reais.

## Como funciona

- `SKILL.md` define a metodologia de design e o workflow.
- O agente mapeia o conceito para uma estrutura visual e gera o JSON do Excalidraw.
- Um pipeline de render baseado em Playwright deixa o agente ver sua própria saída, identificar problemas (texto sobreposto, setas desalinhadas, espaçamento desigual) e corrigi-los antes de entregar.
- Cores e estilo de marca ficam isolados em `references/color-palette.md`; editar esse arquivo troca a paleta de todos os diagramas sem alterar o resto da metodologia.
- Outros arquivos de referência citados pela página de origem: `references/element-templates.md` (templates JSON por tipo de elemento), `references/json-schema.md` (referência do formato JSON do Excalidraw), `references/render_excalidraw.py` e `render_template.html` (renderização para PNG), `references/pyproject.toml` (dependências Python).

**A verificar:** o `SKILL.md` cru não foi lido nesta ingestão; o resumo acima vem da página do repositório no GitHub (README), não do arquivo de instruções em si.

## Instalação e uso

1. Clonar ou baixar o repositório.
2. Copiar para o diretório `.claude/skills/` do projeto, renomeando para `excalidraw-diagram`.
3. Configurar o renderizador: pedir ao agente de código para seguir o `SKILL.md`, ou manualmente com `uv sync` e `uv run playwright install chromium` dentro de `references/`.

## Exemplos de uso

> Exemplos derivados da descrição publicada, não são instruções oficiais da skill.

- Pedir ao agente, em linguagem natural, um diagrama de como o protocolo AG-UI transmite eventos de um agente de IA para uma UI de frontend — exemplo citado na própria página do repositório.

## Saídas esperadas

Um arquivo JSON no formato Excalidraw (e opcionalmente um PNG renderizado), com layout que espelha a relação conceitual descrita (hierarquia, sequência, fan-out, convergência) e, quando pertinente, trechos de código ou JSON reais embutidos no diagrama.

## Quando usar (e quando não usar)

- **Use quando:** precisar de um diagrama técnico editável (formato Excalidraw) gerado a partir de descrição textual, com verificação visual automatizada antes da entrega.
- **Evite quando:** precisar de um artefato HTML autocontido e compartilhável sem dependências Python/Playwright — nesse caso, skills como [Diagram Design](../../cathrynlavery/diagram-design/diagram-design.md) (HTML/SVG) podem ser mais diretas.

## Limitações e cuidados

- Depende de ambiente Python com `uv` e Playwright/Chromium instalados para o pipeline de render e validação visual.
- A qualidade da saída depende do agente seguir a metodologia descrita no `SKILL.md`, não verificado diretamente nesta ingestão.
- Personalização de marca limitada à paleta de cores; o restante da metodologia é descrito como universal.
- Licença não indicada na página consultada.

## Estado e adoção

- Versão: desconhecida (não há changelog ou tag citada na página consultada).
- Repositório com ~5,0k estrelas e 584 forks observados por fonte externa em 2026-10 (não confirmado diretamente pela API do GitHub nesta ingestão).
- Preço/licença: gratuito; licença não identificada no repositório.

## Relações

- Autor: [coleam00](../../../../entities/coleam00.md) (Cole Medin).
- Conceitos: [Artefatos HTML autocontidos](../../../../concepts/artefatos-html-autocontidos.md) (pipeline de render usa um template HTML, ainda que a saída principal seja JSON do Excalidraw).
- Alternativas: [Diagram Design](../../cathrynlavery/diagram-design/diagram-design.md) (diagramas editoriais em HTML/SVG), [tt-a1i/archify](../../../../repos/github.com/tt-a1i/archify.md) (diagrama HTML autocontido a partir de ideia, plano ou repositório).

## Perguntas abertas

- O `SKILL.md` cru detalha critérios de validação mais específicos do que o resumo do README sugere?
- Qual a licença real do repositório?

## Fontes

- Página de origem: https://github.com/coleam00/excalidraw-diagram-skill (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/coleam00/excalidraw-diagram-skill (metadados via API do GitHub, consultados em 2026-10-19; HEAD em `8646fcc9f74f38539c6cdb4c969723336a96ddcd`).
