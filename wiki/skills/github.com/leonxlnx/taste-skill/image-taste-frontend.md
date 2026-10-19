---
type: skill
name: Image Taste Frontend
slug: image-taste-frontend
url: https://www.skills.sh/leonxlnx/taste-skill/image-taste-frontend
source_url: https://github.com/leonxlnx/taste-skill
source_path: não localizado na árvore atual do repositório
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, image-to-code, geracao-de-imagem, frontend, codex, agent-skills]
---

# Image Taste Frontend

> Skill de image-to-code para Codex: exige gerar as imagens de design primeiro, analisá-las em profundidade e só então implementar o site para corresponder a elas.

## O que é

`image-taste-frontend` é a variante de image-to-code voltada ao Codex do pacote `taste-skill`. O texto se apresenta como "Image-First Website Design to Code" e cobre hero sections, landing pages, marketing sites, sites de produto, portfólios, páginas editoriais e redesigns em que a qualidade visual importa.

O diagnóstico de partida é uma lista de falhas típicas de modelos: uma única imagem gigante comprimindo muitas seções, texto pequeno demais, hero escuro centralizado, spam de cards, layouts repetidos, cards dentro de cards, containers arredondados gigantes, micro-rótulos e pills, designs bonitos mas não extraíveis e implementações que se afastam da referência.

## Como funciona

O documento tem 38 seções agrupadas em quatro blocos. O workflow obrigatório é:

1. **Gerar a imagem** — a geração de imagem vem primeiro para qualquer tarefa visual; não começar por código livre.
2. **Analisar em profundidade** — extrair texto, tipografia, espaçamento, botões, componentes, cores e sistema de design das imagens.
3. **Implementar** — só depois traduzir a referência para frontend, mantendo disciplina antideriva.

Regras estruturais:

- **Baseline de dez dials** — variância 8, densidade 3, direção de arte 8, clareza de implementação 9, prioridade de imagem 9, generosidade de espaço 9, precisão de análise 10, avidez de geração 10 e disciplina de simplicidade de UI 9.
- **Gerar imagens suficientes** — não ser preguiçoso com a contagem; imagens grandes e analisáveis são preferíveis a boards comprimidos.
- **Regra específica do Codex** — imagens grandes por seção, não uma folha comprimida; gerar imagens novas para seções ou detalhes em vez de recortar as antigas.
- **Análise limpa** — descrever o que está visível, sem inventar detalhes; padrão de extração seção a seção.
- **Hero minimalista e primeira dobra responsiva** — o hero precisa ser visível e legível em um laptop pequeno.
- **Anti-caixa-aninhada e redução de micro-UI** — evitar containers dentro de containers, pills, rótulos minúsculos e jargão de interface falso.
- **Regras de extração** — texto, tipografia, espaçamento, botões/componentes e cor, cada uma com disciplina de cópia para o código.
- **Antideriva e resolução de detalhes ausentes** — quando a imagem não mostra algo, decidir de forma consistente em vez de inventar um visual novo.
- **Anti-AI-slop e tipografia primeiro** — mesmas proibições do ecossistema, com ênfase em hierarquia e ritmo de seção.
- **Packs de seção** — 4, 8 e 12 seções, no mesmo formato das skills vizinhas.
- **Consistência multi-imagem e checagem de clareza** — imagem 2, 3 ou 8 não pode derivar para outro site.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill image-taste-frontend
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Landing de startup:** gerar uma imagem por seção, analisar tipografia e espaçamento e implementar seção a seção.
- **Redesign visual:** gerar referências novas em vez de recortar screenshots antigas e comparar a implementação com elas.
- **Página editorial:** hero minimalista com tipografia forte, imagens grandes e poucos elementos de interface.

## Saídas esperadas

Imagens de referência por seção, uma análise de design extraída delas e código frontend que corresponda à referência, com desvios justificados apenas quando a imagem não cobre o detalhe.

## Quando usar (e quando não usar)

- **Use quando:** o harness é o Codex e a tarefa é visual, com geração de imagens disponível.
- **Evite quando:** não há geração de imagem, ou o pedido é backend/UI sem superfície visual.

## Limitações e cuidados

- Não foi possível localizar um `SKILL.md` correspondente na árvore atual do repositório, embora a página do catálogo publique o conteúdo; a origem exata do arquivo é **A verificar**.
- Depende de o harness permitir geração de imagem e de o modelo seguir a ordem imagem → análise → código.
- A precisão da implementação depende da qualidade e da legibilidade das imagens geradas.
- O conteúdo foi lido a partir do `SKILL.md` renderizado; scripts e referências não foram inspecionados.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **3.553**, primeira aparição em 21 de abril de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conceito: [Image-to-code](../../../../concepts/image-to-code.md).
- Variantes: [Imagegen Frontend Web](imagegen-frontend-web.md), [Image to Code](image-to-code.md), [Imagegen Frontend Mobile](imagegen-frontend-mobile.md).
- Base de estilo: [Design Taste Frontend](design-taste-frontend.md).

## Perguntas abertas

- Onde está o `SKILL.md` desta skill no repositório atual?
- Como a skill se comporta em harnesses sem geração de imagem?
- Há avaliação da fidelidade entre imagem e código?
- Qual a diferença prática em relação a `imagegen-frontend-web`?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/image-taste-frontend (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
