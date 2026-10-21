---
type: concept
aliases: [CLAUDE.md, Instruções persistentes para agentes, Memória de projeto do Claude Code]
status: draft
created: 2026-10-17
updated: 2026-10-21
tags: [agentes, claude-code, contexto, diretrizes]
---

# CLAUDE.md

> Arquivo de instruções persistentes que um agente de código lê como contexto do projeto, usado para fixar convenções, comandos e critérios de comportamento entre sessões.

## Definição

`CLAUDE.md` é um arquivo Markdown colocado na raiz de um projeto (ou distribuído como plugin) para orientar o Claude Code. Diferentemente de um prompt avulso, ele não é reescrito a cada sessão: o agente o carrega como contexto persistente, e o arquivo passa a fazer parte do repositório, podendo ser versionado, revisado e mesclado com instruções específicas do projeto.

Na wiki, o próprio `CLAUDE.md` deste repositório exemplifica o uso mais estruturado do formato: um schema que define estrutura, convenções e workflows que o agente deve seguir.

## Como funciona

O padrão descrito no ecossistema:

1. O arquivo fica na raiz do projeto e é lido pelo agente como instruções do projeto.
2. Ele pode ser criado do zero, acrescentado a um arquivo existente ou instalado como plugin que disponibiliza as instruções em vários projetos.
3. O conteúdo é mesclado com regras específicas do projeto; o README de `andrej-karpathy-skills` recomenda essa combinação em vez da substituição.
4. Outros agentes adotam equivalentes: o mesmo repositório inclui uma regra de Cursor em `.cursor/rules/`, e o README remete a `CURSOR.md` para a adaptação.

Os detalhes de carregamento — quando o arquivo é lido, quanto contexto consome, como diretrizes conflitantes são priorizadas e se há suporte a imports — não foram verificados nesta wiki. **A verificar.**

## Onde aparece

- [multica-ai/andrej-karpathy-skills](../repos/github.com/multica-ai/andrej-karpathy-skills.md) — diretrizes de comportamento distribuídas como um único `CLAUDE.md` e também como plugin do Claude Code.
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — a instalação pede uma seção "gstack" no `CLAUDE.md` para rotear navegação; `/sync-gbrain` também insere e remove um bloco de orientação de busca.
- O [`CLAUDE.md`](../../CLAUDE.md) deste repositório — schema da wiki, com estrutura, frontmatter e workflows.
- [Init AGENTS.md](../skills/github.com/zazencodes/skills/init-agents-md.md) — skill que automatiza a criação: inspeciona o repositório, redige um `AGENTS.md` curto e torna `CLAUDE.md` um symlink para ele, em vez de dois arquivos que podem divergir. Uma versão anterior da mesma skill, em [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md), usa um `CLAUDE.md` espelhado mínimo em vez de symlink — duas soluções diferentes para o mesmo problema de manter os dois arquivos equivalentes.

## Trade-offs

- **Vantagens:** formato simples e legível; versionável junto com o código; dispensa runtime ou instalação de ferramentas; permite reunir convenções, comandos e critérios de comportamento em um só lugar; pode ser distribuído como plugin.
- **Limitações:** ocupa contexto em toda sessão, mesmo quando irrelevante; não é um mecanismo de enforcement — o agente pode interpretar ou ignorar instruções; diretrizes longas competem com o conteúdo da tarefa; não há formato único entre agentes (Cursor e outros usam arquivos próprios); conflitos com regras do projeto precisam ser resolvidos textualmente.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — skills carregam instruções sob demanda por tarefa; um `CLAUDE.md` tende a valer para toda sessão. Os dois formatos podem coexistir. [Agent harness](agent-harness.md) — harnesses costumam usar o `CLAUDE.md` como ponto de entrada para regras e roteamento. [Wiki pessoal com LLMs](wiki-pessoal-com-llms.md) — o `CLAUDE.md` é a camada de schema que instrui o agente a manter a wiki.
- **Contrasta com:** [Model Context Protocol](model-context-protocol.md) — MCP expõe ferramentas e dados em runtime; `CLAUDE.md` fornece apenas instruções.
- **Pré-requisito para:** comportamento consistente do agente em tarefas recorrentes do projeto, como estilo, testes e comandos de build.

## Perguntas abertas

- Qual é o custo de contexto de um `CLAUDE.md` longo e como o agente decide o que carregar?
- Como diretrizes globais, de projeto e de plugin são priorizadas quando entram em conflito?
- Como o mesmo conteúdo é adaptado para Cursor, Codex e outros agentes?
- É possível medir objetivamente o efeito das diretrizes no comportamento do agente?

## Fontes

- README de `multica-ai/andrej-karpathy-skills` no commit `2c606141936f1eeef17fa3043a72095b4765b9c2` (consultado em 2026-10-17).
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037` (consultado em 2026-10-19).
- `CLAUDE.md` deste repositório, como exemplo de uso estruturado do formato (consultado em 2026-10-17).
- [Init AGENTS.md](../skills/github.com/zazencodes/skills/init-agents-md.md) — `SKILL.md` de `zazencodes/skills` no commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2`, comparado com a versão em `zazencodes/zazencodes-season-3` no commit `555467c365e6750278efba09349369109f62f65f` (clone local, consultado em 2026-10-21).
