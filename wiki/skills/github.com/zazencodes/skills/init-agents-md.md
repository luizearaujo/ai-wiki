---
type: skill
name: Init AGENTS.md
slug: init-agents-md
url: https://github.com/zazencodes/skills/tree/main/skills/init-agents-md
source_url: https://github.com/zazencodes/skills
source_path: skills/init-agents-md
author: zazencodes
version: 0.1.1
license: MIT
status: active
created: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, claude-md, agents-md, claude-code, codex]
---

# Init AGENTS.md

> Escreve um `AGENTS.md` curto e específico do repositório, inspecionando o projeto primeiro, e garante que `CLAUDE.md` seja um symlink para ele — em vez de dois arquivos de instrução divergindo com o tempo.

## O que é

Skill do catálogo [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md) para o problema de manter instruções de projeto (`AGENTS.md`/`CLAUDE.md`) curtas, específicas do repositório e sincronizadas entre si, em vez de genéricas ou duplicadas. Dispara quando o agente precisa inspecionar uma base de código e redigir um `AGENTS.md`, preservar detalhes úteis de um `CLAUDE.md` existente, ou garantir que os dois arquivos fiquem equivalentes.

**Nota de proveniência**: uma versão anterior desta mesma skill está publicada em [zazencodes/zazencodes-season-3](../../../../repos/github.com/zazencodes/zazencodes-season-3.md) (pasta `src/cross-platform-agent-skills/skills/init-agents-md/`), com uma diferença real de comportamento — ver [Relações](#relações).

## Como funciona

Workflow descrito no `SKILL.md`:

1. **Checar arquivos atuais.** Se `AGENTS.md` já existe, parar e perguntar ao usuário antes de sobrescrever. Se `CLAUDE.md` existe como arquivo regular (não symlink), lê-lo como material de partida para o novo `AGENTS.md`. Se `CLAUDE.md` não existe ou já é symlink, planeja criar o symlink depois.
2. **Explorar o repositório.** Inspeção suficiente para explicar a forma real do projeto e seus workflows — começando pelo `README` como guia inicial, preferindo `rg`/`rg --files`/`ls` e leituras pontuais a dumps amplos.
3. **Redigir o `AGENTS.md`.** Mínimo necessário: cortar o que é genérico, óbvio ou duplicado de outra documentação; começar com `# AGENTS.md`; colocar `## Project Instructions` perto do topo (em branco se não houver nada específico); nomear seções pela forma real do repositório, não por placeholders genéricos; focar em o que é o repositório, onde está o código importante, os workflows/comandos principais, expectativas de teste/validação e armadilhas importantes.
4. **Symlink do `CLAUDE.md`.** Se `CLAUDE.md` existia como arquivo regular, remover depois de extrair o que for útil; criar um symlink relativo: `ln -sf AGENTS.md CLAUDE.md`.
5. **Checagem final.** Confirmar que `AGENTS.md` é a fonte da verdade, que `CLAUDE.md` é de fato um symlink relativo para ele, que todo comando e caminho citado corresponde ao repositório real, e que o arquivo permanece curto.

Leitura recomendada antes de redigir: `references/agents-md-best-practices.md`, incluído na própria skill.

## Instalação e uso

```bash
# Plugin do Claude Code (junto com as outras quatro skills do catálogo)
claude plugin marketplace add zazencodes/skills
claude plugin install zazencodes-skills@zazencodes

# skills.sh, só esta skill
npx skills@latest add zazencodes/skills --skill init-agents-md
```

## Exemplos de uso

> Exemplos derivados da descrição publicada — não são instruções oficiais da skill.

- Pedir para criar um `AGENTS.md` do zero em um repositório que nunca teve um, deixando a skill inspecionar e decidir as seções.
- Pedir para "sincronizar CLAUDE.md com AGENTS.md" em um projeto onde os dois já existem e divergiram, usando o `CLAUDE.md` existente como material de partida antes de substituí-lo pelo symlink.

## Saídas esperadas

Um `AGENTS.md` curto, específico do repositório, com `## Project Instructions` perto do topo; um `CLAUDE.md` que é um symlink relativo apontando para `AGENTS.md` (`ln -sf AGENTS.md CLAUDE.md`), não mais um arquivo separado.

## Quando usar (e quando não usar)

- **Use quando:** quer um `AGENTS.md` enxuto e um único ponto de manutenção para instruções de projeto, evitando que `AGENTS.md` e `CLAUDE.md` divirjam silenciosamente.
- **Evite quando:** o repositório já usa deliberadamente uma convenção de `CLAUDE.md` mais rico e espelhado (não um symlink) — essa skill impõe o symlink, não oferece as duas abordagens como opção.

## Limitações e cuidados

- A versão publicada aqui impõe symlink; não oferece, como opção configurável, a abordagem de "arquivo espelhado mínimo" que a versão anterior (em `zazencodes-season-3`) usava.
- Symlinks exigem sistema de arquivos e ferramentas que os preservem (alguns ambientes Windows, certos uploads de CI/CD ou zips, não preservam symlinks) — a skill não documenta um fallback para esses casos.
- `references/agents-md-best-practices.md` foi referenciado no `SKILL.md`, mas não lido nesta ingestão.

## Estado e adoção

- Versão: parte do release `v0.1.1` do catálogo [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md); estava presente desde a primeira release (`v0.1.0`), segundo o `CHANGELOG.md`.
- Preço/licença: MIT.

## Relações

- Autor: [zazencodes (Alexander Galea)](../../../../entities/zazencodes.md)
- Repositório-fonte: [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md)
- Conceitos: [CLAUDE.md](../../../../concepts/claude-md.md), [Agent skills](../../../../concepts/agent-skills.md)
- Versão anterior/paralela: a cópia em [zazencodes/zazencodes-season-3](../../../../repos/github.com/zazencodes/zazencodes-season-3.md) (pasta `src/cross-platform-agent-skills/skills/init-agents-md/`) usa uma abordagem diferente — em vez de symlink, mantém `CLAUDE.md` como um arquivo mínimo próprio ("`# CLAUDE.md` mais uma linha dizendo para ler `AGENTS.md`"), a não ser que o repositório já use claramente a convenção de um `CLAUDE.md` espelhado mais completo. Não foi possível determinar, sem inspecionar o histórico de commits de nenhum dos dois repositórios, qual versão é mais recente em relação à outra.

## Perguntas abertas

- A mudança de "arquivo espelhado" para "symlink" foi uma decisão deliberada de simplificação, ou as duas versões evoluíram de forma independente sem sincronia entre o monorepo de vídeos e o catálogo de skills?
- Como a skill se comporta em um ambiente onde symlinks não são preservados (certos pipelines de CI, exportação para zip)?

## Fontes

- `SKILL.md`: https://raw.githubusercontent.com/zazencodes/skills/9f2d7c8f0e112e03d0e440676afd49fde3c9dff2/skills/init-agents-md/SKILL.md (commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2`, lido via clone local autorizado, consultado em 2026-10-21).
- Comparação: `SKILL.md` da pasta `src/cross-platform-agent-skills/skills/init-agents-md/` em [zazencodes/zazencodes-season-3](../../../../repos/github.com/zazencodes/zazencodes-season-3.md) (commit `555467c365e6750278efba09349369109f62f65f`, mesmo clone local), consultado em 2026-10-21.
