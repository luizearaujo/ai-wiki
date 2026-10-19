---
type: skill
name: Design Taste Frontend v1
slug: design-taste-frontend-v1
url: https://www.skills.sh/leonxlnx/taste-skill/design-taste-frontend-v1
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/taste-skill-v1/SKILL.md
author: leonxlnx
version: v1 (declarada como "original")
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, anti-slop, frontend, legado, agent-skills]
---

# Design Taste Frontend v1

> Versão original da skill de gosto visual para frontend, preservada para projetos que dependem do comportamento exato da v1; roda apenas quando chamada pelo nome.

## O que é

A v1 é a primeira geração da `taste-skill`: um conjunto de diretrizes de engenharia de frontend de alta agência, com três "dials" fixos (variância 8, intensidade de movimento 6, densidade visual 4), convenções de stack React/Next.js e uma lista extensa de padrões proibidos. A própria página a descreve como opt-in: só é executada quando chamada explicitamente.

Ela antecede o processo de direção sorteada e inspeção em navegador da [v2](design-taste-frontend.md). O valor atual é de compatibilidade: projetos que dependem do texto e das regras exatas da v1 podem continuar usando a mesma instalação.

## Como funciona

A skill abre com a configuração de baseline (8/6/4) e trata o usuário como override conversacional. Em seguida fixa convenções:

- **React ou Next.js**, com Server Components por padrão; estado global só em Client Components e interatividade isolada em folhas `use client`.
- **Tailwind CSS** para 90% do estilo, com verificação de versão (v3 vs v4) e guarda de configuração do PostCSS.
- **Dependências verificadas** no `package.json` antes de qualquer import.
- **CSS Grid** em vez de matemática de percentuais em flexbox; `min-h-[100dvh]` em vez de `h-screen`.
- **Ícones** de `@phosphor-icons/react` ou `@radix-ui/react-icons`, com espessura padronizada.
- **Proibição de emoji** em código, markup, texto e alt text.

As seis regras de correção de viés cobrem tipografia determinística (Geist, Outfit, Cabinet Grotesk ou Satoshi; serif proibida em dashboards), calibração de cor (um acento, saturação abaixo de 80%, proibição do "lilás de IA"), diversificação de layout (hero centralizado proibido quando variância > 4), materialidade e anti-excesso de cards, estados completos de interação (loading, vazio, erro, feedback tátil) e padrões de formulário (label acima, erro abaixo).

A seção de proatividade criativa prescreve liquid glass com borda interna, física magnética com `useMotionValue`, micro-interações perpétuas, transições de layout e orquestração escalonada. As guardas de performance limitam grão a pseudo-elementos fixos, animação a `transform`/`opacity` e z-index a camadas sistêmicas.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill design-taste-frontend-v1
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Dashboard denso:** densidade > 7 proíbe cards genéricos; separar dados com `border-t`/`divide-y` e usar monoespaçado em números.
- **Hero de marketing:** com variância 8, trocar o hero centralizado por split screen, conteúdo à esquerda e ativo à direita, ou espaço negativo assimétrico.
- **Projeto legado:** manter a v1 quando o resultado atual é aceito e uma reescrita para a v2 mudaria decisões já revisadas.

## Saídas esperadas

Código React/Next.js ou HTML/Tailwind com tokens, estados de interação completos, movimento com física de mola, e nenhum dos padrões listados como "AI tells".

## Quando usar (e quando não usar)

- **Use quando:** for necessário reproduzir o comportamento exato da v1, ou quando o projeto já foi construído com essas regras.
- **Evite quando:** o objetivo é um trabalho novo de direção de arte. A v2 oferece um processo mais completo (sorteio de direção, ideia do assunto, inspeção em navegador); a v1 é um catálogo de regras, não um run.

## Limitações e cuidados

- É uma skill de regras fixas: não sorteia direção nem verifica o resultado renderizado.
- O baseline 8/6/4 é opinativo e pode não servir a um brief conservador.
- A referência a shadcn/ui exige customização; usar o padrão é explicitamente banido.
- O conteúdo foi lido a partir do `SKILL.md` renderizado; o arquivo cru e as referências não foram inspecionados.

## Estado e adoção

- Versão: v1, mantida por compatibilidade.
- Instalações observadas em 2026-10-19: **329.021** (329,2 mil), primeira aparição em 25 de maio de 2026.
- Auditorias: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: licença MIT; JavaScript; 99.159 estrelas no commit de referência.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Substituída por: [Design Taste Frontend](design-taste-frontend.md) (v2, run completo).
- Variante experimental: [v2 experimental](design-taste-frontend-v2-experimental.md).
- Conceito: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).

## Perguntas abertas

- Por quanto tempo a v1 continuará recebendo correções de segurança?
- Há diferenças funcionais entre esta página e o alias `taste-skill`?
- A v1 e a v2 compartilham as mesmas dependências de scripts?
- Qual o custo de manter duas gerações no mesmo repositório?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/design-taste-frontend-v1 (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
