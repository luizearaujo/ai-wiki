---
type: concept
aliases: [design taste, gosto visual para agentes, direção de arte para agentes]
status: stable
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, anti-slop, agent-skills, frontend]
---

# Design taste para agentes

> Conjunto de métodos que dá a agentes de código um critério visual explícito — direção sorteada, regras mensuráveis, referências e verificação no navegador — em vez de deixar a estética cair na média dos dados de treino.

## Definição

Modelos de linguagem produzem interfaces que parecem a média de tudo o que viram: título centralizado em três linhas, rótulo pequeno acima, fileira de cards com ícone, gradiente suave e legenda monoespaçada. "Design taste para agentes" nomeia a resposta a esse problema: transformar gosto visual em instruções operacionalizáveis que um agente consiga seguir, medir e revisar.

O termo não designa uma técnica única. Na wiki, ele cobre quatro famílias de abordagem:

| Abordagem | Como funciona | Exemplos |
| --- | --- | --- |
| **Regras de prosa** | Diretivas fixas com proibições, paletas e números. | [Design Taste Frontend v1](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v1.md), [High-End Visual Design](../skills/github.com/leonxlnx/taste-skill/high-end-visual-design.md) |
| **Dials + processo** | Configuração numérica (variância, movimento, densidade) guiando decisões, com run em etapas. | [Design Taste Frontend](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md), [v2 experimental](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v2-experimental.md) |
| **Base pesquisável** | Consultas determinísticas a estilos, paletas, tipografia e diretrizes versionadas. | [UI/UX Pro Max](../skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md) |
| **Referência visual** | Gerar imagens de alta qualidade, analisá-las e implementar a partir delas. | [Imagegen Frontend Web](../skills/github.com/leonxlnx/taste-skill/imagegen-frontend-web.md), [Image Taste Frontend](../skills/github.com/leonxlnx/taste-skill/image-taste-frontend.md) |

Há ainda uma quinta camada, transversal: **verificação no resultado renderizado**, por screenshots, inspetor ou rubrica de crítica — presente em [Design Taste Frontend](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) e [Impeccable](../skills/github.com/pbakaus/impeccable/impeccable.md).

## Como funciona

Apesar da variedade, as abordagens compartilham um mecanismo:

1. **Ler o brief antes de decidir** — tipo de página, público, referências, ativos existentes e restrições silenciosas. A estética é inferida, não imposta.
2. **Escolher uma direção** — sorteio de arquétipos, leitura de sinais do prompt, preset de caso de uso ou consulta a uma base.
3. **Aplicar regras de casa** — tipografia (fontes com caráter, tracking, escala), cor (um acento, saturação limitada, neutros consistentes), layout (assimetria, grid, espaço), estados completos e movimento com física.
4. **Banir os "AI tells"** — emoji, Inter, preto puro, glow roxo/azul, três cards iguais, nomes genéricos, números redondos, clichês de copy e texto de preenchimento.
5. **Olhar o resultado** — screenshots em múltiplas larguras, rubrica de crítica e correção iterativa; sem essa etapa, a skill mede proibições, não qualidade.

## Onde aparece

- [Design Taste Frontend](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) — o run mais completo: sorteio, ideia do assunto, regras mensuráveis e ciclo de screenshots.
- [Design Taste Frontend v2 Experimental](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v2-experimental.md) — a mesma tese em arquivo único e dials.
- [Design Taste Frontend v1](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v1.md) — catálogo de regras fixas, preservado por compatibilidade.
- [High-End Visual Design](../skills/github.com/leonxlnx/taste-skill/high-end-visual-design.md), [Minimalist UI](../skills/github.com/leonxlnx/taste-skill/minimalist-ui.md), [Industrial Brutalist UI](../skills/github.com/leonxlnx/taste-skill/industrial-brutalist-ui.md), [GPT Taste](../skills/github.com/leonxlnx/taste-skill/gpt-taste.md) — estilos e processos opt-in.
- [Redesign Existing Projects](../skills/github.com/leonxlnx/taste-skill/redesign-existing-projects.md) — o mesmo critério aplicado a projetos existentes.
- [Frontend Design](../skills/github.com/anthropics/skills/frontend-design.md) — a versão da Anthropic: processo em duas passagens (plano de tokens, depois construção) e uma lista própria de clichês de design gerado por IA a evitar.
- [UI/UX Pro Max](../skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md) — base de conhecimento pesquisável.
- [Impeccable](../skills/github.com/pbakaus/impeccable/impeccable.md) — direção em quatro modos e playbook de comandos.
- [Stitch Design Taste](../skills/github.com/leonxlnx/taste-skill/stitch-design-taste.md) e [Brandkit](../skills/github.com/leonxlnx/taste-skill/brandkit.md) — saídas em `DESIGN.md` e em imagem.

## Trade-offs

- **Vantagens:** reduz o visual médio de modelo, torna decisões auditáveis, permite consistência entre execuções e dá ao usuário vocabulário para revisar o resultado.
- **Limitações:** regras opinativas podem conflitar com marcas existentes; listas de proibições não medem qualidade; o processo completo custa contexto e tempo; a verificação depende de navegador e screenshots.

## Relações

- Relacionado a: [Design system com agentes](design-system-com-agentes.md), [Image-to-code](image-to-code.md), [Auditoria de UX](auditoria-de-ux.md), [Agent skills](agent-skills.md).
- Contrasta com: geração de UI sem brief e sem verificação, tratada como "média estatística".
- Pré-requisito para: consistência visual em projetos mantidos por agentes ao longo do tempo.

## Perguntas abertas

- Regras de prosa, dials ou base pesquisável produzem resultados melhores em avaliação cega?
- Como medir "gosto" sem cair em preferência do avaliador?
- O ciclo de screenshots melhora o resultado o suficiente para justificar o custo?
- Skills de estilo fixo envelhecem na mesma velocidade que as tendências visuais?

## Fontes

- https://www.skills.sh/leonxlnx/taste-skill — catálogo com 16 entradas consultado em 2026-10-19.
- https://www.skills.sh/leonxlnx/taste-skill/design-taste-frontend — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://www.skills.sh/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://www.skills.sh/pbakaus/impeccable/impeccable — `SKILL.md` renderizado, consultado em 2026-10-19.
