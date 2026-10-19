---
type: repo
url: https://github.com/Leonxlnx/taste-skill
host: github.com
owner: leonxlnx
repo: taste-skill
commit: b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2
license: MIT
language: JavaScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, agent-skills, design-ui, direcao-de-arte, anti-slop, frontend, claude-code, codex]
---

# Leonxlnx/taste-skill

> Família de Agent Skills que dá "gosto" a agentes de código: direção de arte sorteada de um estudo de sites reais, imagens de acervos abertos e verificação da página em navegador de verdade, como antídoto à landing page genérica gerada por modelo.

## O que é

O README posiciona o Taste Skill como um conjunto de skills que fazem o agente **desenhar** um site em vez de montar "a landing page média". A tese central é o **anti-slop**: o problema de uma página gerada por modelo não é erro técnico, mas ausência de decisão — título centralizado, cards com ícone, gradiente suave e tipografia monoespaçada produzem algo que se parece com a média de tudo o que o modelo viu.

A proposta é substituir padrões por decisões verificáveis: uma direção de arte escolhida entre opções pesquisadas, uma ideia tirada do próprio assunto do cliente, imagens reais com licença e crédito, e um ciclo em que o agente inspeciona as próprias screenshots e corrige o resultado.

O README também anuncia o **TasteCode**, um app desktop gratuito e open source (`Leonxlnx/tastecode`) que empacota a skill com um agente de design que briefa, constrói e revisa a interface visualmente.

## Como funciona

### O run padrão (v2)

O README declara que a skill padrão foi construída a partir de um estudo de **247 sites curados** e descreve seis etapas:

1. Ler o brief e listar o que só aquele cliente tem.
2. Um script sorteia **três de vinte** direções pesquisadas, e o agente escolhe uma.
3. Encontrar a ideia: uma frase que ligue o material do cliente à direção escolhida.
4. Construir com imagens e vídeos reais de acervos abertos, com crédito.
5. Verificar a página em navegador real em **três larguras** e reprová-la por slop.
6. Olhar as próprias screenshots e corrigir os três principais problemas, em até três rodadas.

O README estima **30 a 45 minutos** e algumas centenas de milhares de tokens por build. A versão 2.1 acrescenta um run próprio para **telas de aplicativo** — dashboards, admin, settings, inbox — com estilos destilados de telas de produto reais e regras de app (painéis discretos, números alinhados, cor gasta em dados, navegação que se recolhe no celular), além de checagens de enquadramento da página orientadas pelos 100 Awwwards Sites of the Day mais recentes.

### Família de skills

| Skill / instalação | Papel no repositório |
|---|---|
| `design-taste-frontend` ([página](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md)) | Skill padrão v2: direção de arte, imagens reais e inspeção em navegador para páginas e telas de app. |
| `design-taste-frontend-v2-experimental` ([página](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v2-experimental.md)) | Reescrita em arquivo único e orientada a dials, padrão antes da v2. |
| `design-taste-frontend-v1` ([página](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v1.md)) | Versão original, preservada para projetos que dependem do comportamento exato. |
| `high-end-visual-design` ([página](../../../skills/github.com/leonxlnx/taste-skill/high-end-visual-design.md)) | Clássica: UI calma e polida, contraste suave, whitespace e movimento com mola. |
| `minimalist-ui` ([página](../../../skills/github.com/leonxlnx/taste-skill/minimalist-ui.md)) | Clássica: UI editorial com paleta contida e estrutura nítida. |
| `industrial-brutalist-ui` ([página](../../../skills/github.com/leonxlnx/taste-skill/industrial-brutalist-ui.md)) | Clássica: tipografia suíça, contraste duro e layout experimental. |
| `gpt-taste` ([página](../../../skills/github.com/leonxlnx/taste-skill/gpt-taste.md)) | Variante mais estrita para GPT e Codex, com mais variância de layout e movimento. |
| `stitch-design-taste` ([página](../../../skills/github.com/leonxlnx/taste-skill/stitch-design-taste.md)) | Regras para Google Stitch, com export opcional de `DESIGN.md`. |

As **classic skills** são opt-in: só rodam quando chamadas pelo nome. As duas versões anteriores da skill principal expõem três dials de 1 a 10 — `DESIGN_VARIANCE`, `MOTION_INTENSITY` e `VISUAL_DENSITY`; a v2 não tem dials: a direção vem do sorteio e os limites, do inspetor.

### Mudanças em relação à documentação anterior da wiki

O README atual registra movimentos que as páginas de skill já existentes não refletem:

- As skills de geração de imagem (`imagegen-frontend-web`, `imagegen-frontend-mobile`, `brandkit`, `image-to-code`) **migraram para o repositório `Leonxlnx/imagegen-skills`**, mantendo os mesmos nomes de instalação. As páginas [Imagegen Frontend Web](../../../skills/github.com/leonxlnx/taste-skill/imagegen-frontend-web.md), [Imagegen Frontend Mobile](../../../skills/github.com/leonxlnx/taste-skill/imagegen-frontend-mobile.md), [Brandkit](../../../skills/github.com/leonxlnx/taste-skill/brandkit.md) e [Image to Code](../../../skills/github.com/leonxlnx/taste-skill/image-to-code.md) documentam o estado anterior.
- `redesign-existing-projects` está **retirada**: redesign e revisão passaram a fazer parte da skill padrão, que audita a página no navegador antes de alterar.
- `full-output-enforcement` **deixou de existir** no README atual; a página [Full-Output Enforcement](../../../skills/github.com/leonxlnx/taste-skill/full-output-enforcement.md) é histórica.
- A listagem anterior do catálogo tinha 16 entradas, incluindo a [entrada alias `taste-skill`](../../../skills/github.com/leonxlnx/taste-skill/taste-skill.md), que não aparece na tabela atual do README.

## Instalação e uso rápido

Instalação via CLI `npx skills` (projeto `vercel-labs/agent-skills`):

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
```

Sem `--skill`, as classic skills também são instaladas, mas permanecem inertes até serem chamadas pelo nome.

| Caminho | Comando publicado |
|---|---|
| Plugin Claude Code | `/plugin marketplace add Leonxlnx/taste-skill` e `/plugin install taste-skill@taste-skill` |
| Plugin Codex | `codex plugin marketplace add Leonxlnx/taste-skill` e `codex plugin add taste-skill@taste-skill` |
| Clone com symlink | `./install.sh design-taste-frontend` (`--codex`, `--all-agents`, `--list`) |

Requisitos da skill padrão: **Node 22+** e Chrome, Edge ou Chromium instalados. A skill não instala nada e não usa chaves de API; precisa de rede apenas para buscar imagens. O plugin Claude Code fica sob o namespace `taste-skill:`.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Landing de um cliente real:** informar brief e ativos; o agente sorteia direções, escolhe uma, busca fotos de acervos abertos com crédito e entrega a página após o ciclo de inspeção.
- **Dashboard ou tela de app:** o run de app escolhe um estilo destilado de telas de produto, monta shell, dados, gráficos e tabelas e aplica as regras de app.
- **Revisão de página "com cara de IA":** instalar a skill, apontar para a página existente e usar a auditoria em navegador antes de qualquer mudança.
- **Projeto que depende do comportamento antigo:** instalar explicitamente `design-taste-frontend-v1` ou uma das classic skills.

## Quando usar (e quando não usar)

- **Use quando:** a saída é uma interface web — landing page, site de marketing, portfólio, product page, dashboard ou tela de app — e o objetivo é direção visual em vez de média genérica.
- **Use quando:** o projeto precisa de imagens reais e creditadas sem contratar banco de imagens.
- **Evite quando:** a tarefa é backend, API ou conteúdo sem superfície visual.
- **Evite quando:** o fluxo exige determinismo estrito, já que a direção é sorteada e o julgamento final é qualitativo.
- **Alternativas documentadas:** [UI/UX Pro Max](../nextlevelbuilder/ui-ux-pro-max-skill.md) — base pesquisável de estilos e stacks; [Impeccable](../pbakaus/impeccable.md) — linguagem de design com comandos e verificação.

## Limitações e cuidados

- **Somente o README foi lido.** Scripts, referências internas, licenças das imagens e a implementação do inspetor não foram verificados.
- **Custo alto por build:** o próprio README estima 30–45 minutos e centenas de milhares de tokens para a skill padrão.
- **O gate mede o que é banido, não se a página é boa.** A etapa de crítica é qualitativa e depende do julgamento do agente.
- **Dados de estudo não reproduzidos:** as amostras de 247 sites e dos 100 Awwwards são citadas, mas não foram auditadas.
- **Divergência com a wiki:** as páginas de `brandkit`, `imagegen-*`, `image-to-code`, `full-output-enforcement` e `redesign-existing-projects` descrevem um estado anterior do repositório. **A verificar** se o catálogo skills.sh ainda publica essas entradas e se os conteúdos foram realmente movidos ou apenas redistribuídos.
- **Licenciamento de mídia:** a skill declara usar apenas domínio público, CC0, CC BY e CC BY-SA, com crédito na página; a verificação disso é responsabilidade do usuário.
- **Sem versionamento semântico publicado no README:** as versões aparecem no changelog, não há política de compatibilidade para as skills clássicas.
- **Marca e cripto:** o README afirma não haver token oficial; qualquer criptoativo com o nome do projeto é não afiliado.

## Estado e adoção

- **Atividade e popularidade observadas em 2026-10-19:** 99.223 estrelas, 6.745 forks, 2 issues abertas; repositório criado em 2026-02-19, último push em 2026-10-19.
- **Licença:** MIT.
- **Linguagem principal (API):** JavaScript.
- **Sites do projeto:** [tasteskill.dev](https://tasteskill.dev) e [tastecode.dev](https://tastecode.dev).
- **Financiamento:** patrocínio no GitHub, programa open source da Vercel e patrocinadores comerciais listados no README.
- **Distribuição:** repositório de skills, plugin de Claude Code, plugin de Codex, CLI `npx skills` e app desktop TasteCode.

## Relações

- **Mantido por:** [Leon Lin (leonxlnx)](../../../entities/leonxlnx.md).
- **Skills documentadas:** [Design Taste Frontend](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md), [v1](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v1.md), [v2 experimental](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend-v2-experimental.md), [High-End Visual Design](../../../skills/github.com/leonxlnx/taste-skill/high-end-visual-design.md), [Minimalist UI](../../../skills/github.com/leonxlnx/taste-skill/minimalist-ui.md), [Industrial Brutalist UI](../../../skills/github.com/leonxlnx/taste-skill/industrial-brutalist-ui.md), [GPT Taste](../../../skills/github.com/leonxlnx/taste-skill/gpt-taste.md), [Stitch Design Taste](../../../skills/github.com/leonxlnx/taste-skill/stitch-design-taste.md).
- **Conceitos:** [Design taste para agentes](../../../concepts/design-taste-para-agentes.md) — a ideia central; [Design system com agentes](../../../concepts/design-system-com-agentes.md) — tokens e direção; [Image-to-code](../../../concepts/image-to-code.md) — fluxo imagem primeiro, código depois; [Agent skills](../../../concepts/agent-skills.md) — mecanismo de distribuição; [Artefatos HTML autocontidos](../../../concepts/artefatos-html-autocontidos.md) — formato de saída comum.
- **Alternativas:** [UI/UX Pro Max](../nextlevelbuilder/ui-ux-pro-max-skill.md), [Impeccable](../pbakaus/impeccable.md).
- **Deriva de:** [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) — CLI `npx skills` usado na instalação.

## Perguntas abertas

- As skills de imagem continuam disponíveis neste repositório ou apenas em `Leonxlnx/imagegen-skills`? O README e as páginas da wiki divergem.
- Qual é a diferença observável entre a skill padrão e a v1 além da presença de dials e do estudo de 247 sites?
- O sorteio de direções é reprodutível por seed, e como o usuário audita a escolha?
- Quanto do custo de 30–45 minutos vem de busca de imagens, de browser e do modelo?
- Como a skill se comporta em stacks sem navegador disponível no ambiente do agente?
- O TasteCode reutiliza a mesma skill e o mesmo gate, ou tem regras próprias?
- As páginas antigas do catálogo skills.sh serão removidas ou redirecionadas?

## Fontes

- README: https://github.com/Leonxlnx/taste-skill/blob/main/README.md (commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19).
- Páginas de skill já existentes na wiki, usadas para verificar divergências de estado.
