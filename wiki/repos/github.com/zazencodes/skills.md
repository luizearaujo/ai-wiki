---
type: repo
url: https://github.com/zazencodes/skills
host: github.com
owner: zazencodes
repo: skills
commit: 9f2d7c8f0e112e03d0e440676afd49fde3c9dff2
license: MIT
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, claude-code, codex, cli]
---

# zazencodes/skills

> Catálogo pequeno e versionado de cinco Agent Skills que Alexander Galea (ZazenCodes) usa no próprio trabalho diário com Claude Code e Codex, distribuído como plugin do Claude Code ou via `skills.sh` — distinto do monorepo de vídeos [zazencodes/zazencodes-season-3](zazencodes-season-3.md), mas com pelo menos uma skill em comum.

## O que é

Diferente de [zazencodes/zazencodes-season-3](zazencodes-season-3.md) (um arquivo de código-companheiro de vídeos, sem produto único), este repositório é ele mesmo um produto pequeno e coeso: um catálogo de skills reais, versionado com [changesets](https://github.com/changesets/changesets), com release no GitHub (`v0.1.1`) e licença MIT. O README é direto: "Agent skills I use every day with Claude Code, Codex and other coding agents."

Clonado (`git clone --depth 1`, autorizado explicitamente pelo usuário) para uma análise mais precisa — o pedido original era verificar se este repositório enriquecia o que já havia sido levantado sobre o zazencodes-season-3. A resposta é sim: a pasta `src/cross-platform-agent-skills/skills/init-agents-md` do monorepo de vídeos é uma cópia anterior da skill `init-agents-md` publicada aqui, com uma diferença real de comportamento entre as duas versões (ver [Relações](#relações)).

## Como funciona

Cinco skills, cada uma em `skills/<nome>/SKILL.md`, seguindo o formato aberto [Agent Skills](https://agentskills.io):

| Skill | O que faz | Precisa de |
|---|---|---|
| [Codex Image Gen](../../../skills/github.com/zazencodes/skills/codex-image-gen.md) | Gera e edita imagens via a ferramenta de imagem embutida na CLI `codex`, usando o login do ChatGPT em vez de uma chave de API. | `codex`, Python 3 |
| [Gemini Web Research](../../../skills/github.com/zazencodes/skills/gemini-web-research.md) | Delega pesquisa web substancial a sessões do Gemini (`agy`, Google Antigravity) em painéis do tmux, e sintetiza os relatórios. | `agy`, tmux |
| [Git Commit Conventions](../../../skills/github.com/zazencodes/skills/git-commit-conventions.md) | Divide o trabalho em um commit por lote de mudanças relacionadas, com mensagens curtas e autoria do próprio usuário. | git |
| [Init AGENTS.md](../../../skills/github.com/zazencodes/skills/init-agents-md.md) | Escreve um `AGENTS.md` curto e específico do repositório e sincroniza `CLAUDE.md` com ele. | — |
| [Random Number Generator](../../../skills/github.com/zazencodes/skills/random-number-generator.md) | Gera inteiros, floats, amostras ponderadas, embaralhamentos e tokens/inteiros criptograficamente seguros via um script Python da biblioteca padrão. | Python 3 |

O versionamento é gerenciado por `changesets`: `package.json` lista as cinco skills, mas o `CHANGELOG.md` só documenta até a `0.1.0` (quatro skills) e a `0.1.1` (um patch em `codex-image-gen`) — a quinta skill, `random-number-generator`, já está no catálogo instalável mas não tem entrada própria no changelog consultado nesta ingestão.

## Instalação e uso rápido

Duas formas, mutuamente exclusivas (instalar as duas duplica as skills):

```bash
# Como plugin do Claude Code (todo o conjunto, de uma vez)
claude plugin marketplace add zazencodes/skills
claude plugin install zazencodes-skills@zazencodes

# Via skills.sh (Claude Code, Codex e outros agentes; copia os arquivos, editáveis)
npx skills@latest add zazencodes/skills
npx skills@latest add zazencodes/skills --skill <nome>   # uma só
```

Atualização: `claude plugin update zazencodes-skills@zazencodes` (plugin) ou `npx skills update` (skills.sh). O plugin pode ser configurado para atualização automática em `/plugin` → aba Marketplaces → zazencodes.

## Exemplos de uso

Exemplos derivados da descrição publicada de cada skill — não são instruções oficiais:

- Pedir para gerar uma imagem de capa para um post, sem ter (ou sem querer gastar) uma chave de API da OpenAI — `codex-image-gen` usa o login do `codex` já autenticado.
- Pedir para investigar um tópico amplo em paralelo, abrindo várias sessões do Gemini via `agy` em painéis de tmux — `gemini-web-research`.
- Pedir para "comitar isso" em um working tree com várias mudanças não relacionadas — `git-commit-conventions` divide em um commit por lote de intenção, nunca por arquivo.

## Quando usar (e quando não usar)

- **Use quando:** já usa Claude Code ou Codex no dia a dia e quer as convenções específicas de um único autor (um esquema de commits sem atribuição de IA, geração de imagem sem chave paga, `AGENTS.md` minimalista) em vez de escrever as próprias instruções do zero.
- **Evite quando:** precisa de atribuição de IA nos commits (a skill `git-commit-conventions` proíbe explicitamente `Co-Authored-By`) ou de um fallback para a API da OpenAI em geração de imagem (a skill `codex-image-gen` proíbe explicitamente esse fallback) — são convenções de opinião do autor, não configuráveis dentro da skill.

## Limitações e cuidados

- Repositório novo (criado em 2026-10-05): 1 estrela, 1 fork, 1 issue aberta — observado em 2026-10-21. Pouca adoção até o momento.
- `CHANGELOG.md` está defasado em relação a `package.json`: `random-number-generator` já está listado como skill instalável, mas não tem entrada de changeset própria consultada nesta ingestão.
- As skills refletem convenções pessoais do autor (sem atribuição de IA em commits, sem fallback de API paga em geração de imagem) — não são neutras nem configuráveis, é preciso concordar com elas para instalar sem edição.
- Não foram lidos os scripts completos (`scripts/*.py`, `scripts/*.sh`) além do que cada `SKILL.md` documenta sobre seu uso; comportamento exato de cada script não foi executado nesta ingestão.

## Estado e adoção

- Versão mais recente: `v0.1.1` (release no GitHub, publicada em 2026-10-05) — observado em 2026-10-21.
- 1 estrela, 1 fork, 1 issue aberta, push mais recente em 2026-10-15 — observado em 2026-10-21.
- Licença: MIT.

## Relações

- Mantido por: [zazencodes (Alexander Galea)](../../../entities/zazencodes.md)
- Repositório relacionado: [zazencodes/zazencodes-season-3](zazencodes-season-3.md) — `src/cross-platform-agent-skills/skills/init-agents-md/SKILL.md`, nesse monorepo de vídeos, é uma versão anterior da skill [Init AGENTS.md](../../../skills/github.com/zazencodes/skills/init-agents-md.md) publicada aqui. As duas divergem num ponto concreto: a versão do monorepo de vídeos cria um `CLAUDE.md` minimalista separado ("mirror" com uma linha apontando para `AGENTS.md`); a versão publicada aqui faz `CLAUDE.md` ser um **symlink** para `AGENTS.md` (`ln -sf AGENTS.md CLAUDE.md`) — abordagens diferentes para o mesmo problema, a segunda mais nova. A pasta `cross-platform-agent-skills` também inclui uma sexta skill, `movie-poster` (gera um poster de filme fictício a partir da análise do código), que não está publicada neste catálogo.
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [CLAUDE.md](../../../concepts/claude-md.md) — pela skill Init AGENTS.md.

## Perguntas abertas

- Por que `random-number-generator` está no catálogo mas não tem entrada no `CHANGELOG.md` consultado — changeset pendente, ou o arquivo não foi atualizado?
- A versão do `init-agents-md` no monorepo de vídeos é anterior ou um ramo paralelo da versão publicada aqui? O histórico de commits de nenhum dos dois repositórios foi inspecionado para decidir.

## Fontes

- README: https://raw.githubusercontent.com/zazencodes/skills/9f2d7c8f0e112e03d0e440676afd49fde3c9dff2/README.md (commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2`, consultado em 2026-10-21).
- Clone local (`git clone --depth 1`, autorizado explicitamente pelo usuário): os cinco `SKILL.md`, `package.json`, `.claude-plugin/marketplace.json`, `CHANGELOG.md` e `LICENSE`, no mesmo commit, consultados em 2026-10-21.
- Metadados: API do GitHub (`api.github.com/repos/zazencodes/skills`), consultada em 2026-10-21.
