---
type: concept
aliases: [DESIGN.md, PRODUCT.md, design system persistente, design context]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, design-system, agent-skills, contexto-persistente]
---

# Design system com agentes

> Prática de manter a identidade visual como artefato versionado e legível por agentes — tokens, regras e justificativa em arquivos como `DESIGN.md`, `PRODUCT.md` ou `MASTER.md` — para que decisões de design sobrevivam entre sessões.

## Definição

Um design system para agentes não é apenas uma biblioteca de componentes. É um **contexto persistente**: um arquivo (ou conjunto de arquivos) que descreve paleta, tipografia, espaçamento, componentes, movimento e anti-padrões, de modo que um agente possa ler antes de gerar ou alterar uma interface.

A wiki registra quatro variações observadas:

| Artefato | Origem | Conteúdo |
| --- | --- | --- |
| `DESIGN.md` | [Google Labs Code](../entities/google-labs-code.md) e [Stitch Design Taste](../skills/github.com/leonxlnx/taste-skill/stitch-design-taste.md) | Formato que une tokens legíveis por máquina a justificativa em prosa; no Stitch, linguagem visual semântica para geração de telas. |
| `PRODUCT.md` + `DESIGN.md` | [Impeccable](../skills/github.com/pbakaus/impeccable/impeccable.md) | Contexto de produto e de design carregado no início de cada sessão; drift reportado pelo comando `doctor`. |
| `MASTER.md` + overrides | [UI/UX Pro Max](../skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md) | Design system gerado por consulta e persistido em `design-system/<slug>/`, com overrides por página. |
| `DESIGN.md` gerado | [Stitch Design Taste](../skills/github.com/leonxlnx/taste-skill/stitch-design-taste.md) | Documento produzido a partir de regras anti-slop para alimentar o Google Stitch. |

## Como funciona

O ciclo típico tem quatro etapas:

1. **Carregar** — o agente lê o artefato no início da sessão, junto do brief da superfície. Sem isso, cada execução recomeça do zero e deriva.
2. **Aplicar** — tokens e regras restringem a geração: um acento, uma família de fontes, um raio, uma lógica de espaçamento.
3. **Detectar drift** — ferramentas como o `doctor` do Impeccable comparam o código ao documento e reportam divergências. A skill proíbe corrigir drift como efeito colateral de outra tarefa.
4. **Atualizar** — mudanças de identidade passam pelo arquivo, não por edições espalhadas; um redesign substitui o documento, um refinamento o preserva.

O ponto sensível é a **autoridade**: o brief do cliente vence o gosto do modelo, e a ausência de um `DESIGN.md` não torna um projeto greenfield — a verdade visual existente é evidência.

## Onde aparece

- [Impeccable](../skills/github.com/pbakaus/impeccable/impeccable.md) — `PRODUCT.md`/`DESIGN.md`, `init`, `document`, `extract` e `doctor`.
- [UI/UX Pro Max](../skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md) — `--design-system` e `--persist` com `MASTER.md`.
- [Stitch Design Taste](../skills/github.com/leonxlnx/taste-skill/stitch-design-taste.md) — gera `DESIGN.md` para o Stitch.
- [Google Labs Code](../entities/google-labs-code.md) — origem do formato e da CLI `@google/design.md`; as skills [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md) e [TDD Red-Green-Refactor](../skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md) vivem no mesmo repositório.
- [Design Taste Frontend](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) — não usa `DESIGN.md`, mas produz um direction sheet e exige coerência de tokens.

## Trade-offs

- **Vantagens:** consistência entre sessões, decisões auditáveis, menos retrabalho, contexto transferível entre agentes e harnesses.
- **Limitações:** cria estado que pode ficar obsoleto; exige disciplina de atualização; arquivos muito longos consomem contexto; formatos concorrentes ainda não são interoperáveis.

## Relações

- Relacionado a: [Design taste para agentes](design-taste-para-agentes.md), [Agent skills](agent-skills.md), [CLAUDE.md](claude-md.md), [Memória de agente](memoria-de-agente.md).
- Contrasta com: identidade visual implícita apenas no prompt.
- Pré-requisito para: manutenção de interface por agentes em projetos de vida longa.

## Perguntas abertas

- Os formatos `DESIGN.md`, `PRODUCT.md` e `MASTER.md` convergirão para um padrão?
- Como evitar que o documento vire uma segunda fonte de verdade divergente do código?
- Qual o custo de contexto de carregar tokens e regras em cada sessão?
- O `doctor` consegue detectar drift semântico, não só de tokens?

## Fontes

- https://www.skills.sh/pbakaus/impeccable/impeccable — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://www.skills.sh/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://www.skills.sh/leonxlnx/taste-skill/stitch-design-taste — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://github.com/google-labs-code/design.md — página do projeto e metadados via API em 2026-10-19.
