---
type: concept
aliases: [code knowledge graph, grafo de código, CBM graph]
status: draft
created: 2026-10-18
updated: 2026-10-19
tags: [code-intelligence, grafo, mcp, agentes, tree-sitter]
---

# Grafo de conhecimento de código

> Representação estruturada de uma base de código como grafo de nós (funções, classes, módulos, rotas, recursos de infraestrutura) e arestas tipadas (chamadas, importações, herança, dependências), persistida localmente e consultável por agentes sem precisar ler arquivos.

## O que é

Um grafo de conhecimento de código indexa símbolos e seus relacionamentos a partir da análise estática do código-fonte. Ao contrário de uma busca por texto (grep) ou da leitura sequencial de arquivos, o grafo permite responder perguntas estruturais — "quem chama X?", "quais rotas HTTP existem?", "quais funções não têm callers?" — em milissegundos e com uma fração dos tokens que a exploração arquivo por arquivo consumiria.

A ideia é separar a inteligência (o agente/LLM) do conhecimento estrutural (o grafo): o grafo é construído uma vez e consultado repetidamente, em vez de ser recalculado a cada sessão.

## Componentes típicos

- **Parser**: análise sintática (tree-sitter, LSP) para extrair símbolos e relacionamentos.
- **Armazenamento**: SQLite, Neo4j ou estruturas em memória com persistência opcional.
- **Tipos de aresta**: `CALLS`, `IMPORTS`, `INHERITS`, `HTTP_CALLS`, `SPAWNS`, `CONFIGURES`, `DEPLOYS` etc. A riqueza dos tipos de aresta determina quais perguntas o grafo pode responder. Alguns projetos distinguem arestas **extraídas** da análise estática das **inferidas** semanticamente, como o Graphify faz com `EXTRACTED` e `INFERRED`.
- **Interface de consulta**: Cypher-like, BM25 full-text, busca semântica por embeddings, ou ferramentas MCP.

## Diferença de abordagens relacionadas

| Abordagem | Escopo | Quando usar |
|-----------|--------|-------------|
| Grafo de conhecimento de código | Estrutura estática do código | Navegação, rastreamento de chamadas, análise de impacto |
| RAG sobre código | Embeddings de trechos de código | Busca por similaridade semântica, geração de código |
| Engenharia reversa agêntica | Artefatos compilados sem fonte | Análise de binários, análise dinâmica |
| LSP | Resolução de tipos em tempo real | Autocompletar, go-to-definition em IDEs |

O grafo de conhecimento de código e o LSP são complementares: o grafo persiste e é consultável em lote; o LSP é transiente e orientado a cursor.

## Implementações documentadas na wiki

- [DeusData/codebase-memory-mcp](../repos/github.com/deusdata/codebase-memory-mcp.md) — C puro, 162 linguagens, 17 ferramentas MCP, Hybrid LSP, SQLite, CBM Lens Beta.
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — skill + CLI em Python, tree-sitter para ~40 linguagens e passo semântico opcional para docs e mídia; arestas `EXTRACTED`/`INFERRED`, comunidades de Leiden e **sem vector store**, com consulta, caminhos e explicação.
- [Skill understand](../skills/github.com/egonex-ai/understand-anything/understand.md) — método em sete fases que grava `knowledge-graph.json` e o apresenta em um dashboard interativo, com atualização incremental e validação antes de publicar.
- [Workflow Claude Code + Graphify + Obsidian](../analyses/claude-code-graphify-obsidian.md) — exporta o grafo do Graphify como notas interligadas em um vault do Obsidian, separando grafo estruturado (`graph.json`) de grafo visual de links (Obsidian).

## Lacunas

- Comparação com abordagens baseadas em Neo4j (ex.: LlamaIndex KnowledgeGraphIndex, Microsoft GraphRAG aplicado a código).
- Limitações de grafos estáticos vs análise dinâmica (execução real, cobertura de testes).
- Custo de manutenção do índice em repositórios de alta frequência de commits.

## Fontes

- [DeusData/codebase-memory-mcp](../repos/github.com/deusdata/codebase-memory-mcp.md) — README no commit `354ccecbe612a9fdb624396a6738fa87f2617434`, consultado em 2026-10-18.
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — README no commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8` (consultado em 2026-10-19).
- [Skill understand](../skills/github.com/egonex-ai/understand-anything/understand.md) — página do skills.sh (consultada em 2026-10-19).
