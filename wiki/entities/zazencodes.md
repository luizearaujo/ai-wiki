---
type: entity
kind: person
url: https://github.com/zazencodes
created: 2026-10-21
updated: 2026-10-21
tags: []
---

# Alexander Galea (zazencodes)

> Engenheiro de IA, M.Sc. em Física e fundador do canal/site ZazenCodes, que publica o código-fonte dos próprios vídeos sobre agentes, LLMs e ferramentas de desenvolvimento.

## O que é

Alexander Galea descreve-se no GitHub como "AI Engineer. M.Sc in Physics. Founder of ZazenCodes", com blog pessoal em galea.dev e newsletter em zazencodes.com/newsletter. Mantém repositórios de código por temporada do canal ZazenCodes no YouTube, cada um reunindo as pastas de código-fonte usadas nos vídeos daquela temporada — cobrindo agentes de IA, skills para agentes de código, modelos locais e ferramentas de desenvolvimento. O próprio repositório da Temporada 3 documenta, em um `AGENTS.md`/`CLAUDE.md` interno, um fluxo de trabalho pessoal em que o README público é atualizado por um agente a partir de metadados locais de vídeo — o código em `src/` frequentemente chega antes da publicação e da entrada no índice.

## Repositórios e projetos

- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) — código-fonte da Temporada 3: 21 pastas cobrindo fábrica de software sobre Claude Code, orquestração hub-and-spoke com o runtime `pi`, harnesses de agente sempre ativos (Pi + Neon, eve da Vercel), skills multiplataforma, MCP com UI e identidade delegada, memória de agente e um demo de decisão não generativa (System 1) com o Jev da TypeSafe AI.
- [Factory](../skills/github.com/zazencodes/zazencodes-season-3/factory.md) — skill `/factory` que orquestra sete subagentes do Claude Code em um loop spec → build → revisão em quatro frentes → aprovação, cada job isolado em seu próprio git worktree.
- [zazencodes/skills](../repos/github.com/zazencodes/skills.md) — catálogo versionado (MIT, release `v0.1.1`) de cinco skills de uso diário: [Codex Image Gen](../skills/github.com/zazencodes/skills/codex-image-gen.md), [Gemini Web Research](../skills/github.com/zazencodes/skills/gemini-web-research.md), [Git Commit Conventions](../skills/github.com/zazencodes/skills/git-commit-conventions.md), [Init AGENTS.md](../skills/github.com/zazencodes/skills/init-agents-md.md) e [Random Number Generator](../skills/github.com/zazencodes/skills/random-number-generator.md). Distinto do monorepo de vídeos, mas com uma skill em comum (`Init AGENTS.md`, publicada aqui com uma versão diferente da que aparece no monorepo).

## Relevância no ecossistema

Produz conteúdo educacional em vídeo sobre o ecossistema prático de agentes de código (Claude Code, Codex, Pi, eve, MCP, agent skills) acompanhado do código correspondente publicamente disponível, o que torna cada vídeo reproduzível a partir do repositório. A amplitude de temas cobertos em uma única temporada — da orquestração de subagentes a identidade delegada em MCP e modelos de decisão não generativos — funciona como um retrato de onde a atenção da comunidade de agentes estava em 2026.

## Relações

- Associado a: canal ZazenCodes no YouTube; zazencodes.com; galea.dev.

## Fontes

- Perfil do GitHub: https://api.github.com/users/zazencodes, consultado em 2026-10-21.
- README e `AGENTS.md`/`CLAUDE.md` internos de zazencodes-season-3 (clone local, commit `555467c365e6750278efba09349369109f62f65f`), consultados em 2026-10-21.
- README e os cinco `SKILL.md` de zazencodes/skills (clone local, commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2`), consultados em 2026-10-21.
