---
type: skill
name: Design Taste Frontend
slug: design-taste-frontend
url: https://www.skills.sh/leonxlnx/taste-skill/design-taste-frontend
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/taste-skill/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, anti-slop, frontend, tipografia, motion, agent-skills]
---

# Design Taste Frontend

> Skill anti-slop de direção de arte para páginas web: sorteia uma direção visual pesquisada, exige uma ideia tirada do próprio assunto, aplica regras de casa mensuráveis e fecha com um ciclo de inspeção por screenshots.

## O que é

`design-taste-frontend` (tasteskill v2) parte de uma observação: uma página gerada por modelo costuma parecer a média de todas as páginas que o modelo viu — título centralizado em três linhas, rótulo pequeno acima, fileira de cards com ícone, gradiente suave, réguas finas e legenda monoespaçada. Nada está errado, mas nada foi decidido.

A skill substitui esses padrões por decisões em quatro frentes: um script sorteia direções visuais pesquisadas para o agente escolher; a ideia vem do assunto e não da categoria; um estilo de casa sem ornamentos é medido em navegador real; e o agente olha o que produziu em screenshots, aplica uma rubrica e corrige. A base declarada é um estudo de 247 sites de galerias curadas (One Page Love, Awwwards Sites of the Day).

## Como funciona

O fluxo distingue **página** (lida e rolada) de **tela de aplicativo** (dashboard, admin, settings, inbox, editor), que tem run, regras e inspeção próprios em `references/app-screens.md`.

O run prescrito tem dez passos:

1. **Ler o brief e o projeto** — assunto, público, ação principal, stack, marca existente e, sobretudo, que imagens realmente existem.
2. **Escrever o argumento** — listar a página como afirmações com prova, uma linha por seção; seção sem afirmação é removida.
3. **Sortear a direção** com `draw.mjs`: três de vinte direções pesquisadas, com tipo, paleta, hero e composições de seção; escolher a que carrega algo que só aquele cliente tem.
4. **Encontrar a ideia** — preencher a frase "nesta página, [algo do assunto] vira [o dispositivo que a direção pede]", aplicando o teste do concorrente mais próximo.
5. **Escrever as palavras** — copy deck completo antes do markup; headline em até duas linhas, uma frase de apoio e uma ação primária.
6. **Construir** — tokens, hero, seções, imagens (próprias, geradas, de acervos abertos, desenhadas ou tipografia pura), a "coisa viva" interativa e as cenas de scroll.
7. **Passar o gate** com `lint.mjs`, `inspect.mjs` e `scenes.mjs`.
8. **Olhar** — abrir todas as screenshots, aplicar a rubrica de `references/critique.md`, corrigir os três principais problemas, repetir até três rodadas.
9. **Mover** — camada de movimento obrigatória: movimento-assinatura, entradas escalonadas, feedback em controles e uma imagem em movimento, tudo com fallback para `prefers-reduced-motion`.
10. **Relatar** — direção sorteada, redraws, ideia, scores, imagens encontradas com licença e crédito, e conteúdo de amostra a substituir.

Os scripts exigem Node 22+ e Chrome, Edge ou Chromium instalados; `assets.mjs` também precisa de rede, mas não usa chaves de API.

As **regras de casa** são mensuráveis pelo inspetor e valem em qualquer direção. Entre elas: headline em até duas linhas; título claro na primeira tela e heading em toda seção; margens externas iguais; nenhum trecho vazio maior que meia tela; declarações são parágrafos (não headlines gigantes); sem "eyebrows" ou badges acima de títulos; sem monoespaçado fora de código; sem numeração de índice; sem réguas finas; sem gradientes; sem sombras em repouso; sem a paleta "assistente" (creme com terracota, violeta/índigo); sem glass; sem emoji; no máximo duas famílias tipográficas.

Os **laws of the craft** completam com números do estudo: proporção headline/corpo mediana de 4,3; uma a três medidas visíveis; gap entre seções de 120–240 px; uma base, uma tinta e um acento; mídia quadrada em 73% dos sites estudados; botões planos com raio decidido uma vez.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill design-taste-frontend
```

A página não publica instalação global. Os comandos internos usam `<skill>` como a pasta da skill e devem rodar da raiz do projeto, criando `.taste-skill/` no local.

## Exemplos de uso

Exemplos derivados do `SKILL.md` renderizado, não instruções oficiais:

- **Landing de um restaurante:** inventariar nome, rua, materiais, horários e objetos impressos; sortear três direções; escolher a que consegue transformar, por exemplo, o horário do forno em composição.
- **Página com dashboard embutido:** construir a página com o run de página e os fragmentos de interface com o run de app, compartilhando paleta e tipografia.
- **Revisão de página "com cara de IA":** rodar `inspect.mjs`, tratar cada FAIL e defender cada WARN em uma frase.

## Saídas esperadas

Código frontend em qualquer stack, um `design-system`/direction sheet com direção e seed, screenshots de 1440, 768 e 390 px em `.taste-skill/inspect/`, relatório de crítica, lista de imagens com licença e crédito, e um relatório final que declara o que foi verificado.

## Quando usar (e quando não usar)

- **Use quando:** construir, desenhar, redesenhar, reestilizar, polir ou revisar landing pages, sites de marketing, portfólios, product pages, one-pagers, heros e telas de app — em HTML/CSS, React, Next.js, Vue, Svelte, Astro ou Tailwind.
- **Evite quando:** a tarefa é backend, API, banco de dados ou conteúdo sem superfície visual.

## Limitações e cuidados

- O gate mede o que está banido, não se a página é boa; o passo de crítica é qualitativo e depende do julgamento do agente.
- Exige Node 22+, navegador Chromium e, para `assets.mjs`, acesso à rede.
- A skill declara que remover ornamento é só metade do trabalho: sem escala, cor, imagens reais e conteúdo completo, a página fica "fina".
- A biblioteca de direções é curada e opinativa; o próprio `SKILL.md` admite que algumas regras são gosto do autor contra a moda das galerias.
- O conteúdo foi lido a partir do `SKILL.md` renderizado; os scripts e as referências internas não foram inspecionados.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **636.323** (636,7 mil), primeira aparição em 21 de fevereiro de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; criado em 2026-02-19, último push em 2026-10-19. Licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conceitos: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md), [Design system com agentes](../../../../concepts/design-system-com-agentes.md).
- Variantes: [v1](design-taste-frontend-v1.md), [v2 experimental](design-taste-frontend-v2-experimental.md).
- Alternativas: [Impeccable](../../pbakaus/impeccable/impeccable.md), [UI/UX Pro Max](../../nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md).

## Perguntas abertas

- A amostra de 247 sites continua sendo atualizada?
- O `inspect.mjs` funciona de forma equivalente em Chrome, Edge e Chromium headless?
- Como a skill lida com marcas cujo design system viola as regras de casa?
- Os números do estudo são reproduzíveis a partir dos dados publicados?
- Qual o custo de tempo dos dez passos em uma página média?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/design-taste-frontend (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
