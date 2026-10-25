---
type: repo
url: https://github.com/himself65/trade-skills
host: github.com
owner: himself65
repo: trade-skills
commit: 634c16f17e1314a77173a3593460e87e08c1b080
license: desconhecida
language: JavaScript
status: active
created: 2026-10-25
ingested: 2026-10-25
updated: 2026-10-25
tags: [skills, trading, opcoes, financas, okf, agent-skills, plugin]
---

# himself65/trade-skills

> Plugin marketplace pessoal para Claude Code com uma skill de trading de opções multi-leg, respaldada por uma base de conhecimento OKF com 37 armadilhas e estudos de caso documentados.

## O que é

trade-skills é um repositório de plugin/skill para Claude Code com foco em trading de opções. Contém uma skill (`trade`) que funciona como assistente de opções multi-leg: sugere strikes concretos, estruturas sensíveis ao IV (implied volatility) e cenários ponderados por probabilidade.

O diferencial documentado é a base de conhecimento em **Open Knowledge Format (OKF)**: um grafo de arquivos Markdown tipados com frontmatter YAML, navegável via `index.md` e versionado junto ao código. A base cobre 37 armadilhas e estudos de caso reais — INTC, Mag-7, APP, NOK, TSEM, CBRS, SNOW, MDB, VIX, SATS, 6981, MU, NQ, NBIS, BE — e o framework "structure-to-regime" de mapeamento de estrutura de opções para regime de mercado.

Segue a convenção de layout de [`himself65/finance-skills`](https://github.com/himself65/finance-skills).

> **A verificar:** o `SKILL.md` e os arquivos da base OKF não foram lidos; conteúdo da base de conhecimento, cobertura e qualidade dos estudos de caso são a verificar.

## A skill disponível

### `trade`

Assistente de trading de opções multi-leg com:
- Strikes concretos (não genéricos)
- Estruturas sensíveis ao IV
- Cenários ponderados por probabilidade
- Base de conhecimento lazy-loaded (OKF-conformant)

| Componente | Localização |
|------------|------------|
| Skill | `plugins/trade/skills/trade/` |
| Base OKF | `plugins/trade/skills/trade/references/` |
| Índice do grafo | `references/index.md` |
| Log de mudanças | `references/log.md` |
| Especificação OKF | `references/OKF.md` |

## Open Knowledge Format (OKF)

OKF v0.1 é um formato portátil e vendor-neutral para bases de conhecimento: grafos de arquivos Markdown com frontmatter YAML, navegáveis por `index.md` e versionados em repositório. Cada pitfall, estudo de caso e framework é um "conceito tipado".

A especificação é do Google Cloud ([anúncio](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing/); [spec & tooling](https://github.com/GoogleCloudPlatform/knowledge-catalog/tree/main/okf)). O projeto adota OKF como contrato de conformidade para a base da skill de opções.

**A verificar:** como o agente carrega a base OKF em runtime (lazy-loading), e se há diferença observável vs. uma skill sem base estruturada.

## Instalação

```bash
# Plugin completo no Claude Code
npx plugins add himself65/trade-skills

# Só a skill
npx skills add himself65/trade-skills

# Outros agentes
npx skills add himself65/trade-skills -a <agent-name>

# Desenvolvimento local (a partir de clone)
git clone https://github.com/himself65/trade-skills.git ~/trade-skills
ln -s ~/trade-skills/plugins/trade/skills/trade ~/.claude/skills/trade
```

## Limitações e cuidados

- **Não é conselho financeiro.** Aviso explícito no README; uso para fins educativos e informativos.
- Licença não detectada pela API do GitHub; README indica MIT.
- Os arquivos `SKILL.md` e a base OKF (`references/`) não foram lidos; profundidade real da base de conhecimento é a verificar.
- Repositório focado em opções — sem ferramentas de execução documentadas no README.

## Estado e adoção

- Último push: 2026-10-22.
- Observado em 2026-10-25: ~465 stars, ~93 forks, 0 issues abertas.
- Licença: MIT (declarada no README; não detectada pela API do GitHub).

## Relações

- Mantido por: [himself65](../../../entities/himself65.md)
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [Análise financeira multiagente](../../../concepts/analise-financeira-multiagente.md)
- Relacionado: [Jakeschincariol/trader-skill](../jakeschincariol/trader-skill.md) — coleção de 11 skills de trading complementares (ações, 13F, Pelosi tracker, execução via Alpaca).

## Fontes

- README: https://raw.githubusercontent.com/himself65/trade-skills/634c16f17e1314a77173a3593460e87e08c1b080/README.md (commit `634c16f17e1314a77173a3593460e87e08c1b080`, consultado em 2026-10-25). Somente o README foi lido; `SKILL.md` e arquivos da base OKF não foram consultados.
- Metadados: API do GitHub em 2026-10-25.
