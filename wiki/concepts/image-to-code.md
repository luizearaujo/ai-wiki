---
type: concept
aliases: [image-first design to code, image-first frontend, referência visual para frontend]
status: stable
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, image-to-code, geracao-de-imagem, frontend, agent-skills]
---

# Image-to-code

> Fluxo em que o agente gera uma referência visual de alta qualidade, analisa essa referência em profundidade e só então implementa o frontend correspondente, usando a imagem como fonte de verdade do design.

## Definição

Image-to-code é a inversão da ordem usual "prompt → código": primeiro o agente produz a imagem de design (uma por seção ou por tela), depois extrai dela tipografia, espaçamento, componentes e cor, e por fim escreve o código. A imagem deixa de ser ilustração e passa a ser o artefato de especificação.

O conceito aparece de duas formas no ecossistema:

- **Skill dedicada** — [Image Taste Frontend](../skills/github.com/leonxlnx/taste-skill/image-taste-frontend.md) e [Imagegen Frontend Web](../skills/github.com/leonxlnx/taste-skill/imagegen-frontend-web.md) definem o workflow e as regras de geração.
- **Etapa opcional** — [Design Taste Frontend](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) permite imagens próprias, geradas, de acervos abertos ou tipografia pura, mas não exige a geração antes do código.

## Como funciona

O fluxo canônico tem quatro etapas:

1. **Gerar** — uma imagem horizontal por seção; nunca uma única imagem alta comprimindo a página. A contagem padrão é alta: 4, 8 ou 12 seções viram 4, 8 ou 12 imagens.
2. **Analisar** — extrair texto, hierarquia tipográfica, escala, espaçamento, botões, cards, cor e sistema de design. A análise precisa descrever o que está visível sem inventar.
3. **Implementar** — traduzir a referência para código, mantendo disciplina antideriva; gerar novas imagens para detalhes em vez de recortar as antigas.
4. **Verificar** — comparar o resultado renderizado com a referência e corrigir divergências.

Regras que sustentam o fluxo:

| Regra | Motivo |
| --- | --- |
| **Uma imagem por seção** | Uma imagem comprimida torna texto e componentes ilegíveis na extração. |
| **Consistência multi-imagem** | Paleta, tipografia, CTA, raio e tratamento de imagem precisam ser idênticos entre quadros; caso contrário a imagem 8 parece outro site. |
| **Referência implementável** | A imagem deve parecer um site real, com hierarquia e componentes executáveis, não uma peça de arte abstrata. |
| **Anti-drift** | Quando a imagem não mostra um detalhe, a decisão deve ser consistente com o que foi extraído, não uma interpretação nova. |
| **Hero legível em laptop pequeno** | O design precisa sobreviver à primeira dobra real. |

## Onde aparece

- [Image Taste Frontend](../skills/github.com/leonxlnx/taste-skill/image-taste-frontend.md) — workflow código-específico com 38 seções, voltado ao Codex.
- [Imagegen Frontend Web](../skills/github.com/leonxlnx/taste-skill/imagegen-frontend-web.md) — regra de uma imagem por seção e packs de 4/8/12 seções.
- [Image to Code](../skills/github.com/leonxlnx/taste-skill/image-to-code.md) — entrada de catálogo movida para `Leonxlnx/imagegen-skills`, sem conteúdo publicado.
- [Imagegen Frontend Mobile](../skills/github.com/leonxlnx/taste-skill/imagegen-frontend-mobile.md) — variante mobile, também movida.
- [Brandkit](../skills/github.com/leonxlnx/taste-skill/brandkit.md) — image-to-code aplicado a identidade de marca: a imagem é o entregável final.
- [Design Taste Frontend](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) — usa imagens como material de construção e inspeciona o resultado.
- [Impeccable](../skills/github.com/pbakaus/impeccable/impeccable.md) — recomenda gerar imagens de referência antes do código, apontando para a família image-to-code.

## Trade-offs

- **Vantagens:** referência visual rica e analisável; reduz interpretação vaga do prompt; permite comparar implementação e intenção; separa decisão de design de decisão de código.
- **Limitações:** custa tempo e cota de geração; texto em imagens pode sair ilegível; a fidelidade depende da qualidade da análise; gerar uma imagem por seção multiplica chamadas; nem todo harness oferece geração de imagem.

## Relações

- Relacionado a: [Design taste para agentes](design-taste-para-agentes.md), [Design system com agentes](design-system-com-agentes.md), [Auditoria de UX](auditoria-de-ux.md).
- Contrasta com: código direto a partir de prompt, sem referência visual.
- Pré-requisito para: implementação fiel de referências de alta direção de arte.

## Perguntas abertas

- Uma imagem por seção melhora a fidelidade o suficiente para justificar o custo?
- Como medir a fidelidade entre imagem e código?
- O fluxo funciona em harnesses sem geração de imagem?
- A análise automática consegue extrair tokens sem viés de invenção?

## Fontes

- https://www.skills.sh/leonxlnx/taste-skill/image-taste-frontend — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://www.skills.sh/leonxlnx/taste-skill/imagegen-frontend-web — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://www.skills.sh/leonxlnx/taste-skill/image-to-code — página consultada em 2026-10-19 (sem conteúdo renderizado).
- https://www.skills.sh/leonxlnx/taste-skill/brandkit — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://www.skills.sh/pbakaus/impeccable/impeccable — `SKILL.md` renderizado, consultado em 2026-10-19.
