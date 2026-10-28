---
type: repo
url: https://github.com/tobi/qmd
host: github.com
owner: tobi
repo: qmd
commit: 86d2365d17fc682e491c2c53d1e4a884aee8682a
license: MIT
language: TypeScript
status: active
created: 2026-10-28
ingested: 2026-10-28
updated: 2026-10-28
tags: [busca-hibrida, bm25, busca-vetorial, rerank, mcp, agent-skills, indexacao, cli, sdk]
---

# tobi/qmd

> CLI, servidor MCP e SDK que indexam notas, documentação e transcrições em Markdown localmente, combinando BM25, busca vetorial e reranking por LLM — tudo on-device, sem enviar conteúdo a um provedor externo.

## O que é

QMD ("Query Markup Documents") é um motor de busca on-device para "tudo que você precisa lembrar": notas Markdown, transcrições de reunião, documentação e bases de conhecimento. Combina busca full-text BM25 (SQLite FTS5), busca semântica por vetores e reranking por LLM, rodando inteiramente local via `node-llama-cpp` com modelos GGUF baixados sob demanda. O README o posiciona como "ideal para seus fluxos agênticos" — os formatos de saída (`--json`, `--files`, `--md`) são desenhados para consumo por agente, não só por humano.

## Como funciona

### Pipeline de busca híbrida

1. **Expansão de query** — um modelo pequeno (`qmd-query-expansion-1.7B`, fine-tuned) gera variações da pergunta original; sub-queries tipadas (`lex`, `vec`, `hyde`) são roteadas exclusivamente para BM25 (`lex`) ou busca vetorial (`vec`/`hyde`).
2. **Recuperação paralela** — a query original (peso 2×) e as variações buscam em BM25 e vetores simultaneamente.
3. **Fusão por RRF** (Reciprocal Rank Fusion, k=60) — combina as listas de resultado; documentos em #1 em qualquer lista ganham bônus de +0,05, #2–3 ganham +0,02; mantém os 30 melhores candidatos.
4. **Reranking por LLM** (`qwen3-reranker-0.6b`) — pontua cada candidato (yes/no com confiança por logprob).
5. **Blend sensível à posição** — top 1–3: 75% RRF / 25% reranker; top 4–10: 60/40; top 11+: 40/60 (confia mais no reranker quanto mais abaixo no ranking).

O README justifica o desenho: RRF puro dilui acertos exatos quando as queries expandidas não combinam; o bônus de topo preserva o que já bateu exato na query original; o blend por posição evita que o reranker destrua resultados de recuperação já confiáveis.

### Coleções e contexto

- `qmd collection add <caminho> --name <nome>` registra um diretório (com glob mask configurável) como coleção indexável; um "update hook" opcional (`qmd collection update-cmd`) roda um comando (ex. `git pull`) antes de cada reindexação.
- `qmd context add qmd://<coleção> "<descrição>"` adiciona contexto hierárquico por caminho — o README chama isso de "a funcionalidade-chave", porque devolve a descrição junto de cada resultado e ajuda o LLM a escolher melhor entre documentos parecidos.
- Chunking para embeddings é por padrão baseado em regex com ~900 tokens e 15% de overlap, buscando pontos de quebra "naturais" do Markdown (cabeçalhos, blocos de código, linhas em branco, pontuados por um algoritmo de distância); `--chunk-strategy auto` troca para chunking consciente de AST via tree-sitter em arquivos de código (`.ts`, `.tsx`, `.js`, `.jsx`, `.py`, `.go`, `.rs`) — Markdown sempre usa regex, independente da flag.
- Metadados tipados via um bloco de frontmatter `qmd.metadata` (strings, números, booleanos, arrays homogêneos) habilitam um filtro recursivo (AST JSON com `eq`/`ne`/`in`/`contains`/`prefix`/`type`/`exists` etc.), disponível em CLI, SDK, MCP e HTTP; `qmd collection metadata` descobre quais chaves e valores já estão indexados antes de escrever um filtro.

### Superfícies de uso

- **CLI**: `qmd search` (BM25 só), `qmd vsearch` (vetorial só), `qmd query` (híbrido + rerank, "melhor qualidade"), `qmd get`/`qmd multi-get` para recuperar documentos por caminho, docid ou glob.
- **MCP server**: `qmd mcp` expõe as ferramentas `query`, `get`, `multi_get`, `status` e `metadata`; roda via stdio (padrão) ou HTTP (`qmd mcp --http`, com daemon opcional). O transporte HTTP valida `Origin`/`Host` contra DNS rebinding e não tem autenticação própria — o README recomenda colocar autenticação na frente se exposto fora do host.
- **SDK**: biblioteca Node/Bun (`createStore()`, `store.search()`, `store.get()`, `store.addCollection()` etc.), com `dbPath` sempre explícito (sem default), para uso embutido em outra aplicação.
- **Plugin de Claude Code**: `claude plugin marketplace add tobi/qmd` + `claude plugin install qmd@qmd`, ou configuração manual do MCP em `~/.claude/settings.json` / `claude_desktop_config.json`.

### Confiança em config versionada

Um `.qmd/index.yml` local viaja com `git clone` e é adotado automaticamente. Três categorias de campo que alcançam fora do projeto — comandos `update`, caminhos de coleção fora do diretório, e URIs de modelo customizados — exigem aprovação explícita (`qmd trust`) quando há terminal; sem terminal (agentes, CI, MCP), esses campos são **ignorados silenciosamente**, e só a indexação dentro do projeto continua.

## Instalação e uso rápido

```sh
npm install -g @tobilu/qmd   # ou: bun install -g @tobilu/qmd

qmd collection add ~/notes --name notes
qmd context add qmd://notes "Personal notes and ideas"
qmd embed

qmd search "project timeline"           # busca por palavra-chave
qmd vsearch "how to deploy"              # busca semântica
qmd query "quarterly planning process"   # híbrido + rerank
```

Requisitos: Node.js ≥ 22 ou Bun ≥ 1.0; no macOS, SQLite via Homebrew (para suporte a extensão). Três modelos GGUF (~300MB embed, ~640MB rerank, ~1,1GB expansão de query) são baixados do HuggingFace e cacheados em `~/.cache/qmd/models/` no primeiro uso.

## Exemplos de uso

- Indexar a pasta de notas pessoais, documentação de trabalho e transcrições de reunião como coleções separadas, com contexto descritivo em cada uma, e perguntar em linguagem natural via `qmd query`.
- Expor o índice como servidor MCP para o Claude Desktop ou Claude Code consultarem diretamente, em vez de o agente abrir arquivo por arquivo.
- Filtrar busca por metadados (`status: published`, `priority >= 3`) em uma base com frontmatter tipado, descobrindo primeiro quais chaves existem com `qmd collection metadata`.
- Rodar `qmd bench` com um fixture de queries conhecidas para comparar BM25 puro, vetorial puro, híbrido sem rerank e o pipeline completo.

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é busca local (sem enviar conteúdo a um provedor) sobre uma coleção de Markdown/notas/documentação que já existe no disco, com saída pronta para consumo por agente (`--json`, `--files`) e sem exigir infraestrutura de embeddings própria.
- **Evite quando:** o objetivo é visualizar como as páginas se conectam (grafo, clustering, navegação visual) — nesse caso [Egonex-AI/Understand-Anything](../egonex-ai/understand-anything.md) ou [Graphify-Labs/graphify](../graphify-labs/graphify.md) respondem melhor; QMD é busca, não grafo.
- **Evite quando:** CPU/GPU é muito limitada para rodar três modelos GGUF locais (ainda que pequenos) — `--no-rerank` reduz custo, mas abandona a etapa que o próprio README aponta como a que mais eleva a qualidade.

## Limitações e cuidados

- **Somente o README foi lido.** Código (`src/llm.ts`, chunking, bench), testes e `CHANGELOG.md` não foram verificados nesta ingestão.
- **Modelo de confiança parcial para config versionada.** Campos "gated" de um `.qmd/index.yml` commitado são ignorados sem terminal (agentes, CI, MCP) — comportamento seguro por padrão, mas significa que um projeto clonado pode se comportar diferente em uso interativo vs. automatizado, até que `qmd trust` seja rodado uma vez.
- **Reranking consome VRAM/tempo.** Modelos LLM ficam carregados na VRAM entre requisições; contextos de embedding/reranking são descartados após 5 min de inatividade e recriados na próxima consulta (~1s de penalidade).
- **HTTP sem autenticação própria.** O transporte HTTP do MCP valida `Origin`/`Host` contra DNS rebinding, mas não autentica requisições — expor fora do host exige colocar autenticação na frente, segundo o próprio README.
- **Troca de modelo de embedding exige reindexação completa.** Vetores não são compatíveis entre modelos diferentes; mudar `QMD_EMBED_MODEL` exige `qmd embed -f`.
- **Chunking de Markdown é sempre por regex**, mesmo com `--chunk-strategy auto` — o AST via tree-sitter só se aplica a arquivos de código, não a prosa.
- Benchmarks do `qmd bench` são do próprio projeto (fixture de exemplo), não reproduzidos de forma independente nesta ingestão.

## Estado e adoção

- Repositório criado em 2025-12-08; push mais recente em 2026-10-15, observado em 2026-10-28.
- 30.707 estrelas, 1.932 forks, 241 issues abertas, observado em 2026-10-28.
- Licença: MIT (confirmada pela API do GitHub).
- Pacote npm: `@tobilu/qmd`.

## Relações

- Mantido por: [Tobias Lütke (tobi)](../../../entities/tobi.md).
- Conceitos: [Wiki pessoal com LLMs](../../../concepts/wiki-pessoal-com-llms.md) — citado nesse concept como a ferramenta de referência para busca local em escala além do que `index.md` sozinho resolve; [Model Context Protocol](../../../concepts/model-context-protocol.md) — expõe servidor MCP nativo.
- Análise: [Indexação da ai-wiki](../../../analyses/indexacao-da-ai-wiki.md) — avaliação original que motivou esta ingestão, comparando QMD a Understand-Anything e Graphify para indexar esta própria wiki.
- Alternativas de grafo (não de busca) já documentadas: [Egonex-AI/Understand-Anything](../egonex-ai/understand-anything.md), [Graphify-Labs/graphify](../graphify-labs/graphify.md).

## Perguntas abertas

- Qual é a qualidade real do reranking e da expansão de query em corpora fora do inglês, além do suporte multilíngue declarado para embeddings (Qwen3-Embedding, CJK)?
- Como o algoritmo de chunking por regex se comporta em páginas de wiki com muitas tabelas e blocos de código longos, como as desta própria wiki?
- O `qmd doctor` e o probe de GPU cobrem adequadamente ambientes sem GPU dedicada (ex.: a maioria dos ambientes de CI)?

## Fontes

- README: https://raw.githubusercontent.com/tobi/qmd/86d2365d17fc682e491c2c53d1e4a884aee8682a/README.md (commit `86d2365d17fc682e491c2c53d1e4a884aee8682a`, consultado em 2026-10-28). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/tobi/qmd`, `api.github.com/users/tobi`), consultada em 2026-10-28.
