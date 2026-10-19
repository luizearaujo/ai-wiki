---
type: repo
url: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
host: github.com
owner: nextlevelbuilder
repo: ui-ux-pro-max-skill
commit: 56ea9cf174ed86786187daa9de0e6247cb0747e4
license: MIT
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, skills, design-ui, design-system, ux, cli, python, acessibilidade]
---

# nextlevelbuilder/ui-ux-pro-max-skill

> Repositório da skill UI/UX Pro Max: uma base local pesquisável de estilos, paletas, tipografia, diretrizes de UX e regras por stack, empacotada com um gerador de design system e um instalador CLI para mais de 20 agentes de código.

## O que é

O repositório combina três artefatos em um só projeto: a **skill** propriamente dita, o **motor de busca e raciocínio** em Python que responde às consultas do agente, e o **CLI** `ui-ux-pro-max-cli` que gera os arquivos específicos de cada plataforma a partir de templates. A página da skill já documenta o contrato de uso e as prioridades de UX; esta página cobre o repositório como produto e como código.

O README posiciona o projeto como **open source (Basic)** com um tier **Premium** pago. A versão aberta inclui a inteligência de UI/UX, o gerador de design system e as diretrizes das 22 stacks; o tier pago acrescenta identidade de marca, logos, programas de identidade corporativa, banners, apresentações, iconografia, geração de imagens e arquitetura de design tokens para equipes. A fronteira entre os tiers é declarada no README, mas o conteúdo premium não foi inspecionado.

## Como funciona

### Estrutura do repositório

| Diretório | Papel declarado |
|---|---|
| `src/ui-ux-pro-max/` | Fonte de verdade: `data/*.csv`, `scripts/*.py` e `templates/` por plataforma. |
| `cli/` | Instalador que gera arquivos de plataforma a partir dos templates; publicado no npm. |
| `.claude/`, `.factory/` | Ambientes locais de desenvolvimento e teste das skills. |

Os arquivos de `.cursor/`, `.windsurf/`, `.kiro/` e similares não são mantidos à mão: o CLI os gera dinamicamente. O README pede que a instalação seja feita sempre pelo CLI, para garantir templates e estrutura compatíveis com o pacote publicado.

### Catálogo de design

O conjunto de dados versionado sustenta as recomendações:

- **192 tipos de produto** e **192 regras de raciocínio** por indústria, cada uma com padrão de landing page, prioridade de estilo, humor de cor, personalidade tipográfica, efeitos e anti-padrões.
- **79 estilos pesquisáveis**, dos quais 50 ativos, 29 suplementares e 9 depreciados; nomes legados redirecionam para um estilo canônico.
- **192 paletas**, **74 pares de fontes**, **34 padrões de landing page**, **25 tipos de gráfico** e **119 diretrizes de UX**.
- **22 stacks** de implementação, de HTML + Tailwind e React a SwiftUI, Jetpack Compose, WPF, JavaFX e Uno Platform.
- Catálogo de **1.934 fontes Google aprovadas** (com 8 exclusões de revisão) e **105 linhas curadas de ícones** baseadas no Phosphor, validadas contra um manifesto upstream de 1.512 ícones.

### Geração de design system

O fluxo do comando `--design-system` faz cinco buscas paralelas — tipo de produto, estilo, paleta, padrão de landing e tipografia — e passa o resultado por um motor de raciocínio que aplica regras de indústria, ordena estilos por BM25, filtra anti-padrões e processa regras de decisão em JSON. A saída reúne padrão de página, estilo, cores, tipografia, efeitos, o que evitar e um checklist de pré-entrega.

O parâmetro `--persist` grava `design-system/<slug>/MASTER.md` e overrides em `pages/<nome>.md`. A recuperação é hierárquica: a página específica, quando existe, sobrescreve o Master; caso contrário, vale o Master. É o mesmo padrão de design system persistente descrito na página da skill.

### Distribuição e releases

O CLI instala a skill em cerca de 20 assistentes (`--ai claude`, `cursor`, `windsurf`, `codex`, `gemini`, `universal` etc.), com opção `--global`, `--dry-run`, `--offline`, além de `update` e `uninstall`. O pacote npm chama-se `ui-ux-pro-max-cli`, mas o binário é `uipro`; releases antigas de `uipro-cli` são declaradas obsoletas.

O projeto usa **semantic-release** com Conventional Commits: a branch `dev` gera prereleases beta e `main` gera estáveis. As versões são sincronizadas entre `skill.json`, os arquivos de plugin e marketplace do Claude, e `cli/package.json`/lockfile. O README cita a linha v2.x, incluindo a correção de symlinks a partir de v2.5.1.

## Instalação e uso rápido

Pelo marketplace do Claude Code:

```bash
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

Pelo CLI (recomendado pelo README):

```bash
npm install -g ui-ux-pro-max-cli
cd /path/to/your/project
uipro init --ai claude
```

Pré-requisito dos scripts de busca: **Python 3.x**, apenas biblioteca padrão, sem instalação de dependências e sem chamadas de rede. O README orienta o usuário humano a instalar o Python; agentes são instruídos a pedir, não instalar.

Chamada direta do gerador:

```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py \
  "beauty spa wellness" --design-system -p "Serenity Spa"
```

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Landing page de SaaS:** `uipro init --ai cursor` instala a skill; o pedido em linguagem natural aciona a geração do design system.
- **Design system persistente:** `search.py "SaaS dashboard" --design-system --persist -p "MyApp"` cria `MASTER.md`; `--page "dashboard"` cria o override da página.
- **Consulta por domínio:** `--domain style`, `--domain typography`, `--domain chart`, `--domain ux`, `--domain icons`.
- **Consulta por stack:** `--stack react`, `--stack html-tailwind`, `--stack javafx`.
- **Dashboard de operações:** o README cita um exemplo comunitário antes/depois gerado por `search.py "internal operations dashboard" --design-system --density 8 --motion 3 --variance 4`, rotulado como ilustrativo, não benchmark.

## Quando usar (e quando não usar)

- **Use quando:** você quer uma fonte única e versionada de decisões de UI/UX para vários agentes e stacks, com recomendação reproduzível e design system persistente por projeto.
- **Use quando:** a equipe precisa instalar a mesma skill em muitos harnesses e manter os arquivos gerados sincronizados por CLI.
- **Evite quando:** o trabalho é backend, modelagem de dados ou infraestrutura sem interface visual; ou quando o processo exige curadoria própria de design e um catálogo externo não é aceitável.
- **Evite quando:** a organização precisa do tier Premium (marca, imagens, tokens corporativos) — esse conteúdo não é aberto.
- **Alternativas documentadas:** [Impeccable](../../../skills/github.com/pbakaus/impeccable/impeccable.md) para direção de arte e revisão; [Design Taste Frontend](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) para regras anti-slop de frontend; [Understand](../../../skills/github.com/egonex-ai/understand-anything/understand.md) para compreensão de código, não de design.

## Limitações e cuidados

- **Somente o README foi lido.** Código do CLI, `search.py`, CSVs e templates não foram inspecionados; as contagens são as publicadas pelo README.
- **Open core:** parte do produto é paga. O README não informa preço, licença do tier Premium nem o que exatamente fica indisponível sem assinatura.
- **Qualidade do catálogo é curadoria, não avaliação:** não há no README benchmark independente de que os design systems gerados superam um bom prompt ou um designer humano; o único exemplo visual é rotulado como ilustrativo.
- **Dependência de Python:** harnesses sem Python 3.x não conseguem executar as buscas; a skill depende de o ambiente do usuário ter o interpretador.
- **Superfície de instalação ampla:** o CLI escreve em diretórios de configuração de muitos agentes. `--dry-run` e `--offline` existem, mas o README não detalha validação de integridade dos arquivos gerados.
- **Upload para Claude.ai:** o ZIP do repositório excede o limite de 200 arquivos do diálogo de upload; o README não publica um pacote separado para esse fluxo.
- **Atualizações de catálogo:** o workflow `refresh-catalogs.yml` roda semanalmente com permissões de leitura e não faz commit; a promoção dos candidatos é manual. A defasagem entre a fonte upstream e o catálogo publicado **A verificar**.

## Estado e adoção

- **Releases citadas no README:** v2.0 (Design System Generator) e correção de symlinks a partir de v2.5.1; releases automatizadas por semantic-release.
- **Atividade e popularidade observadas em 2026-10-19:** 137.519 estrelas, 14.608 forks, 91 issues abertas; criado em 2025-11-30; último push em 2026-10-15.
- **Licença:** MIT. **Linguagem principal (API):** Python.
- **Homepage:** [uupm.cc](https://uupm.cc); pacote npm `ui-ux-pro-max-cli`.
- **Distribuição:** skill instalável por marketplace do Claude Code, CLI npm e cópia em `.agents/skills/` no modo universal.

## Relações

- **Mantido por:** [Next Level Builder](../../../entities/nextlevelbuilder.md).
- **Skill documentada:** [UI/UX Pro Max](../../../skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md) — contrato de uso, prioridades de UX e fluxo de consulta.
- **Conceitos:** [Design system com agentes](../../../concepts/design-system-com-agentes.md) — o `MASTER.md` e os overrides são uma implementação do padrão; [Design taste para agentes](../../../concepts/design-taste-para-agentes.md) — abordagem baseada em catálogo e busca em vez de prosa; [Auditoria de UX](../../../concepts/auditoria-de-ux.md) — checklists e anti-padrões.
- **Alternativas:** [Impeccable](../../../skills/github.com/pbakaus/impeccable/impeccable.md), [Design Taste Frontend](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md).

## Perguntas abertas

- Qual é a licença e o preço do tier Premium, e como o conteúdo pago é separado do repositório?
- Com que frequência o catálogo de estilos, paletas e fontes é promovido do upstream para o repositório?
- O motor BM25 e as 192 regras foram avaliados contra designers ou métricas de conversão?
- Como o CLI evita sobrescrever customizações locais ao atualizar templates?
- O suporte a 22 stacks tem profundidade equivalente ou concentra-se nas stacks web?
- Qual é a política de compatibilidade entre versões do CLI e arquivos gerados?

## Fontes

- README: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/blob/main/README.md (commit `56ea9cf174ed86786187daa9de0e6247cb0747e4`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19).
- Página existente da skill: [UI/UX Pro Max](../../../skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md).
