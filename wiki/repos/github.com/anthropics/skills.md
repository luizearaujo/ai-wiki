---
type: repo
url: https://github.com/anthropics/skills
host: github.com
owner: anthropics
repo: skills
commit: dbd4588f9e1033efb41dad4bef2f7947c8993d44
license: desconhecida
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agent-skills, claude, anthropic, documentos, especificacao]
---

# anthropics/skills

> Repositório oficial da Anthropic com exemplos de Agent Skills para Claude — de aplicações criativas a workflows enterprise — além da especificação do formato e das skills de documento (docx, pdf, pptx, xlsx) que também alimentam o Claude em produção.

## O que é

O repositório documenta a implementação da Anthropic do padrão Agent Skills (especificação em [agentskills.io](http://agentskills.io)). Skills são pastas de instruções, scripts e recursos que o Claude carrega dinamicamente para melhorar o desempenho em tarefas especializadas — de documentos com a identidade visual de uma empresa a workflows específicos de uma organização.

O README é explícito sobre o propósito: as skills aqui servem para **demonstração e inspiração**, não como garantia de comportamento idêntico ao que o Claude executa internamente — ainda que algumas capacidades mostradas também estejam disponíveis no produto.

## Como funciona

- **Estrutura mínima:** cada skill é uma pasta com `SKILL.md` contendo frontmatter YAML (`name`, `description`) e instruções em Markdown; o repositório inclui um `template/` como ponto de partida.
- **Conjuntos de skills:** `./skills` reúne exemplos de Criativo & Design, Desenvolvimento & Técnico, Enterprise & Comunicação e Skills de Documento; `./spec` publica a especificação Agent Skills; `./template` traz o modelo básico.
- **Skills de documento (docx/pdf/pptx/xlsx):** são as mesmas que alimentam os recursos de criação de arquivos do Claude em produção. O README as classifica como **source-available, não open source** — distinção explícita em relação ao restante do repositório (Apache 2.0).
- **Três superfícies de uso:** Claude Code (via plugin marketplace), Claude.ai (já disponíveis em planos pagos) e Claude API (upload de skills customizadas, via Skills API).

## Instalação e uso rápido

Claude Code, como marketplace de plugins:

```
/plugin marketplace add anthropics/skills
```

Depois, no menu "Browse and install plugins", selecionar `anthropic-agent-skills` → `document-skills` ou `example-skills` → `Install now`; ou instalar direto:

```
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills
```

Claude.ai: as skills de exemplo já estão disponíveis em planos pagos; instruções para skills próprias em "Using skills in Claude".

Claude API: skills pré-construídas e upload de skills próprias via Skills API (`docs.claude.com/en/api/skills-guide`).

## Exemplos de uso

Template básico de skill publicado no README:

```markdown
---
name: my-skill-name
description: A clear description of what this skill does and when to use it
---

# My Skill Name

[Add your instructions here that Claude will follow when this skill is active]

## Examples
- Example usage 1
- Example usage 2

## Guidelines
- Guideline 1
- Guideline 2
```

Exemplo de uso citado no README, após instalar o plugin `document-skills`: pedir ao Claude Code "Use the PDF skill to extract the form fields from `path/to/some-file.pdf`".

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é entender o formato oficial de Agent Skills da Anthropic, usar como referência para criar skills próprias, ou acessar as skills de documento que também rodam em produção no Claude.
- **Evite quando:** se espera paridade garantida entre o comportamento das skills de exemplo aqui e o comportamento do Claude em produção — o próprio README alerta que podem diferir.
- **Evite quando:** se precisa das skills de documento sob uma licença open source — elas são source-available, com termos distintos do restante do repositório.

## Limitações e cuidados

- **Somente o README foi lido.** O conteúdo de `./spec`, `./template` e das skills individuais (incluindo `docx`, `pdf`, `pptx`, `xlsx`) não foi inspecionado.
- Licença mista: Apache 2.0 para a maior parte do repositório, mas as skills de documento são explicitamente "source-available, not open source" — a API do GitHub não detecta uma licença única para o repositório (`NOASSERTION`), registrada no frontmatter como `desconhecida`.
- O README avisa diretamente: "the implementations and behaviors you receive from Claude may differ from what is shown in these skills" — tratar como referência, não como especificação de comportamento.
- Skills de parceiros (como Notion) são apenas destacadas por link externo, sem conteúdo hospedado neste repositório.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~182,2 mil estrelas, ~21,6 mil forks, 1.422 issues abertas; criado em 2025-09-22, último push em 2026-10-09.
- **Licença:** mista — Apache 2.0 para a maior parte; skills de documento são source-available sob termos próprios. API do GitHub reporta `NOASSERTION`.
- **Linguagem principal:** Python.

## Relações

- **Mantido por:** [Anthropic (anthropics)](../../../entities/anthropics.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — este repositório é a referência oficial da Anthropic para o formato, com especificação própria em `./spec`.
- **Relacionado a:** [ComposioHQ/awesome-claude-skills](../composiohq/awesome-claude-skills.md) — catálogo que lista skills oficiais e da comunidade, incluindo as deste repositório; [vercel-labs/agent-skills](../vercel-labs/agent-skills.md), [github/awesome-copilot](../github/awesome-copilot.md), [remotion-dev/skills](../remotion-dev/skills.md) e [cloudflare/skills](../cloudflare/skills.md) — coleções de skills de outros fornecedores seguindo o mesmo padrão Agent Skills.

## Perguntas abertas

- Em que pontos específicos o comportamento das skills de exemplo diverge do que o Claude executa em produção?
- Quais são os termos exatos da licença "source-available" das skills de documento?
- Como a especificação em `./spec` se relaciona com o padrão publicado em agentskills.io — é a mesma coisa, um subconjunto ou uma implementação de referência?

## Fontes

- README: https://github.com/anthropics/skills (commit `dbd4588f9e1033efb41dad4bef2f7947c8993d44`, consultado em 2026-10-19). Somente o README foi lido; `./spec`, `./template` e as skills individuais não foram consultados.
- Metadados do repositório e do perfil `anthropics` via API do GitHub (consultados em 2026-10-19).
