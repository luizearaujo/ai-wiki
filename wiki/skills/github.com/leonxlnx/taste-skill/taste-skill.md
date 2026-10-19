---
type: skill
name: Taste Skill (alias de design-taste-frontend-v1)
slug: taste-skill
url: https://www.skills.sh/leonxlnx/taste-skill/taste-skill
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/taste-skill/SKILL.md
author: leonxlnx
version: v1 (alias)
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, anti-slop, frontend, alias, legado, agent-skills]
---

# Taste Skill (alias de design-taste-frontend-v1)

> Entrada de catálogo com slug `taste-skill` que serve o conteúdo da v1 e instala a skill sob o nome `design-taste-frontend-v1`; tem uma única instalação observada.

## O que é

Esta página documenta uma inconsistência do catálogo, não uma skill independente. A listagem do repositório `leonxlnx/taste-skill` no skills.sh tem 16 entradas; uma delas usa o slug `taste-skill`, mas publica o mesmo título e o mesmo conteúdo da [v1](design-taste-frontend-v1.md), e o comando de instalação aponta para `--skill design-taste-frontend-v1`.

O corpo renderizado é idêntico ao da v1 (cerca de 20 mil caracteres): baseline de dials 8/6/4, convenções React/Next.js, Tailwind, regras de correção de viés, proatividade criativa e guardas de performance. A descrição da página diz que a v1 é preservada para compatibilidade e que o padrão atual é `design-taste-frontend`.

## Como funciona

Por ser um alias, o comportamento é o da v1. O agente recebe as mesmas regras:

- **Baseline fixo** de variância 8, movimento 6 e densidade 4.
- **Stack** React ou Next.js com Server Components por padrão, interatividade isolada em folhas `use client` e Tailwind para a maior parte do estilo.
- **Seis regras de correção de viés** para tipografia, cor, layout, materialidade, estados e formulários.
- **Lista de AI tells** proibidos, incluindo emoji, Inter, gradiente "de IA" e hero centralizado com variância alta.

A diferença observável está só no nome de instalação e no slug da URL.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill design-taste-frontend-v1
```

O comando publicado na página do alias instala a skill pelo nome `design-taste-frontend-v1`, não por `taste-skill`.

## Exemplos de uso

Derivados do conteúdo publicado:

- **Compatibilidade:** um projeto que já referencia `design-taste-frontend-v1` pode ser instalado pelo comando desta página.
- **Migração:** para trabalho novo, preferir [Design Taste Frontend](design-taste-frontend.md); para comportamento antigo, a v1 é a referência.

## Saídas esperadas

As mesmas da v1: código React/Next.js ou HTML/Tailwind com tokens, estados completos e nenhum dos padrões banidos.

## Quando usar (e quando não usar)

- **Use quando:** for preciso resolver a URL do catálogo ou entender por que a listagem mostra duas entradas com o mesmo nome.
- **Evite quando:** a intenção é instalar a skill; nesse caso, use o comando da [v1](design-taste-frontend-v1.md) ou da [v2 padrão](design-taste-frontend.md), que têm nomes inequívocos.

## Limitações e cuidados

- O slug e o nome publicado divergem (`taste-skill` vs. `design-taste-frontend-v1`), o que pode confundir automações que deduzem o nome a partir da URL.
- A entrada tinha **1 instalação** observada em 2026-10-19, compatível com um alias recém-publicado ou pouco divulgado.
- O conteúdo é duplicado da v1; manter as duas páginas exige sincronizar mudanças futuras.
- O conteúdo veio do `SKILL.md` renderizado; o arquivo cru não foi lido.

## Estado e adoção

- Versão: **v1 (alias)**.
- Instalações observadas em 2026-10-19: **1**, primeira aparição em 14 de setembro de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: licença MIT; JavaScript; 99.159 estrelas no commit de referência.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conteúdo equivalente: [Design Taste Frontend v1](design-taste-frontend-v1.md).
- Versão padrão: [Design Taste Frontend](design-taste-frontend.md).
- Conceito: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).

## Perguntas abertas

- O alias é intencional (por exemplo, para preservar URLs antigas) ou um artefato de publicação?
- Por que a data de primeira aparição é posterior à da v1 e da v2?
- As duas entradas serão consolidadas em uma só?
- O comando de instalação continuará apontando para `design-taste-frontend-v1`?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/taste-skill (consultada em 2026-10-19); `SKILL.md` renderizado na página, idêntico ao da v1.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
