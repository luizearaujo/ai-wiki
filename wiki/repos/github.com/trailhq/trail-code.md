---
type: repo
url: https://github.com/trailhq/Trail-Code
host: github.com
owner: trailhq
repo: trail-code
commit: b1211efd3eef0efa121b93800e5dd8e547aead77
license: MIT
language: TypeScript
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agentes, grafo-de-conhecimento-de-codigo, memoria-de-agente, mcp]
---

# trailhq/Trail-Code

> Camada de contexto autoaprendiz para agentes de código: um mapa do repositório (o "graft map") somado a "learnings" — decisões e preferências que o time e os agentes salvam das próprias conversas e reaproveitam entre sessões.

## O que é

Trail-Code (antes **graft**, pacote `@nanonets/graft`) resolve o problema de o agente de código "esquecer" tudo a cada sessão: ele grepa e abre arquivo por arquivo para redescobrir o que já foi mapeado antes, e pode desfazer decisões de um colega por nunca ter sabido delas. O projeto tem duas partes, ambas rodando na máquina do usuário:

1. **O graft map**: um índice de todo arquivo, função e quem chama o quê, construído via tree-sitter.
2. **Learnings**: decisões, preferências, habilidades e guardrails que o próprio agente salva a partir das conversas, com três escopos — pessoal (`~/.trail`, nunca commitado), de repositório (`.trail/`, commitado com o código) e de equipe (um workspace Trail, descrito como "em breve").

É dirigido a times que usam Claude Code, Cursor, Codex, Gemini CLI e outros agentes de código sobre um mesmo repositório.

## Como funciona

- **Camada 1 (graft map), sem modelo**: `trail build` roda tree-sitter sobre o repositório e gera `graft/.graph/wiring.json` (grafo de símbolos por chamada) mais um grafo de nós em Markdown. Cada consulta revalida a árvore de trabalho (dezenas de ms) e só reconstrói o que mudou, incluindo edições não commitadas.
- **Camada 2 (`--deep`, opcional, com chave de provedor)**: duas passagens de LLM resumem cada arquivo e agrupam os resumos em um conjunto curado de nós com links tipados (`depends_on`, `uses`, `implements`, etc.).
- **Learnings são arquivos Markdown** em `.trail/learnings/`, com frontmatter (`title`, `author`, `date`, `cost.tokens`, `touches`) e seções "Decided" / "Tried and ruled out" / "Watch out". Viajam pelo git, sem servidor.
- **`trail check`** compara o diff da branch atual com os learnings e skills do time antes de um PR, sinalizando conflito com a decisão registrada (quem decidiu e por quê).
- **Integração por agente**: `trail init` detecta os agentes instalados e escreve, para cada um, o arquivo de instrução nativo (`AGENTS.md`, `GEMINI.md`, `.github/copilot-instructions.md`) ou um skill/rule próprio (`.claude/skills/trail/SKILL.md`, `.cursor/rules/trail.mdc`). Claude Code recebe a integração mais profunda: statusline, hooks (`SessionStart`, `UserPromptSubmit`, `PostToolUse`, `Stop`), contexto por prompt e "blast radius" pós-edição.
- **Servidor MCP** (`trail mcp`) expõe seis ferramentas (`trail_find_code`, `trail_file_api`, `trail_trace_calls`, `trail_find_all`, `trail_repo_map`, `trail_check_freshness`) para agentes que falam MCP; os nomes antigos `graft_*` continuam respondendo.
- Suporta 23 linguagens em dois níveis de fidelidade (extratores dedicados para TypeScript/JavaScript, Python, Go, Java, Kotlin, PHP, Swift, R, Vue; nível amplo via tree-sitter genérico para Rust, C, C++, C#, Ruby, Scala, Elixir, Solidity, Dart, Clojure, Nix, Lua, OCaml, Zig), com uma camada opcional de arestas via LSP (`--lsp`).

## Instalação e uso rápido

```bash
npm install -g @trailhq/trail-code
trail init        # detecta agentes, constrói o graft map, cria .trail/, escreve hooks/skills
```

`trail init --dry-run` mostra o que seria escrito sem gravar nada; `trail init --agents <ids>` restringe a lista de agentes. Quem já usava `graft` não perde nada: o comando `graft` e o pacote `@nanonets/graft` continuam funcionando e migram para `trail` na primeira sessão aberta pelo Claude Code.

## Exemplos de uso

- `trail ask "<tarefa>"` — nós e trechos de código ranqueados, sem chamar modelo.
- `trail callers <símbolo> -d N` — raio de impacto (quem depende do símbolo, N níveis de profundidade).
- `trail note --title "<assunto>"` — salva uma decisão como learning a partir do stdin.
- `trail check --base origin/main` — verifica o diff da branch contra os learnings do time.
- `trail blast --base origin/main --format markdown` — comentário de PR com o raio de impacto da mudança.

## Quando usar (e quando não usar)

- **Use quando:** vários agentes de código (ou vários membros do time, cada um com seu agente) trabalham no mesmo repositório e você quer reduzir redescoberta de contexto e decisões desfeitas sem querer.
- **Evite quando:** o fluxo já é de um único agente/sessão contínua sem handoff entre pessoas, ou quando `CLAUDE.md`/`AGENTS.md` escritos à mão já bastam; o próprio README posiciona o Trail-Code como complemento, não substituto, desses arquivos.

## Limitações e cuidados

- Benchmarks (SWE-bench Verified, sweep de 162 execuções, PocketBase) são do próprio mantenedor, não auditados por terceiros — tratar como alegação do projeto, não como medição independente.
- "Learnings" de equipe (terceiro escopo) e os "kinds" Skills/Guardrails estão marcados como "soon" no próprio README: ainda não implementados.
- `trail build --deep` envia conteúdo de código ao provedor de modelo escolhido, sob a chave do usuário; sem `--deep`, nada sai da máquina.
- Conectar um "Trail workspace" (futuro) passa a enviar learnings e metadados de busca/check para a Trail — o README é explícito sobre esse limite.
- Somente o README foi lido; não há leitura de `docs/`, código-fonte ou issues além do que ele descreve.

## Estado e adoção

- Renomeado de **graft** para **Trail-Code** durante o desenvolvimento; o pacote antigo (`@nanonets/graft`) e o comando `graft` continuam ativos por compatibilidade.
- Sem releases no GitHub no momento da ingestão (`/releases/latest` retornou 404); distribuição é via npm (`@trailhq/trail-code`).
- Repositório criado em 2026-07-03, com push mais recente em 2026-10-21 (mesmo dia da ingestão) — observado em 2026-10-21.
- Licença: MIT.

## Relações

- Mantido por: [trailhq](../../../entities/trailhq.md)
- Conceitos: [Grafo de conhecimento de código](../../../concepts/grafo-de-conhecimento-de-codigo.md), [Memória de agente](../../../concepts/memoria-de-agente.md), [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md)
- Alternativas (grafo de código): [Graphify-Labs/graphify](../graphify-labs/graphify.md), [Egonex-AI/Understand-Anything](../egonex-ai/understand-anything.md); (memória de agente): [thedotmack/claude-mem](../thedotmack/claude-mem.md)

## Perguntas abertas

- Como o "Trail workspace" (visão de equipe entre repositórios) vai funcionar na prática, e que dados exatamente ele agrega?
- Os benchmarks reportados resistem a uma reprodução independente?

## Fontes

- README: https://raw.githubusercontent.com/trailhq/Trail-Code/b1211efd3eef0efa121b93800e5dd8e547aead77/README.md (commit `b1211efd3eef0efa121b93800e5dd8e547aead77`, consultado em 2026-10-21). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/trailhq/Trail-Code`), consultada em 2026-10-21.
