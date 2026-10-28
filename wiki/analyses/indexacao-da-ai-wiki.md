---
type: analysis
related: [concepts/wiki-pessoal-com-llms.md, repos/github.com/egonex-ai/understand-anything.md, repos/github.com/graphify-labs/graphify.md, repos/github.com/tobi/qmd.md, analyses/claude-code-graphify-obsidian.md, concepts/grafo-de-conhecimento-de-codigo.md]
created: 2026-10-28
updated: 2026-10-28
tags: [indexacao, busca, grafo-de-conhecimento, pkm, escala]
---

# Indexação da ai-wiki: o que configurar neste repositório

> Esta wiki já passou do limiar em que `index.md` sozinho basta, segundo seu próprio conceito-fonte; das ferramentas já documentadas aqui, `Understand-Anything` encaixa melhor no padrão de wiki-LLM, `Graphify` resolve visualização em grafo, e `qmd` resolve busca com o menor custo de infraestrutura — ingerida como página própria em 2026-10-28, depois desta análise.

## Contexto

O usuário perguntou o que pode ser configurado neste repositório (`ai-wiki`) para indexar melhor o conteúdo, pedindo para avaliar ferramentas já documentadas na wiki que possam auxiliar — não uma busca por ferramentas novas fora do que já foi ingerido.

## Análise

### O sinal de que vale configurar algo

O próprio conceito [Wiki pessoal com LLMs](../concepts/wiki-pessoal-com-llms.md) — o padrão que esta wiki declara seguir — registra o limite do `index.md` linear: "funciona bem até a ordem de ~100 fontes e algumas centenas de páginas, sem infraestrutura de embeddings." Contagem atual deste repositório (2026-10-28): **106 repositórios, 39 skills, 38 conceitos, 115 entidades, 303 páginas Markdown em `wiki/`, 3,1 MB**. Ou seja, já no ponto em que o próprio padrão-fonte diz que a busca linear por `index.md`/`categorias.md` passa a ter atrito — não um problema ainda, mas o momento certo para configurar algo antes que piore.

Vale notar: o gargalo não é técnico (grep/Read ainda funcionam), é de **recall humano e de agente**: com 115 entidades e 106 repositórios, encontrar "qual página já cobre X" por leitura do índice fica cada vez mais caro, e a regra 10 do schema ("procure uma página existente antes de criar uma nova") depende exatamente dessa busca.

### Ferramentas já documentadas na wiki, avaliadas para este caso

| Ferramenta | Fit para indexar **esta** wiki | Por quê |
|---|---|---|
| [Egonex-AI/Understand-Anything](../repos/github.com/egonex-ai/understand-anything.md) | **Alto** | É o único, dos documentados, construído explicitamente para o padrão de wiki mantida por LLM — o README cita o mesmo gist `karpathy/llm-wiki` que é a fonte desta wiki. O comando `/understand-knowledge <caminho>` roda um `article-analyzer` dedicado que extrai entidades, afirmações e relações implícitas de artigos de wiki, além de um parser determinístico que já lê wikilinks e categorias de `index.md`. Entrega busca fuzzy e semântica ("quais páginas tratam de X?"), grafo force-directed com clustering de comunidades, e dashboard navegável sem precisar de LLM depois da primeira análise. |
| [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) | **Médio-alto** | Não foi desenhado para wikis especificamente, mas processa docs/Markdown nativamente e tem duas saídas diretamente úteis aqui: `--wiki` (gera uma wiki em Markdown a partir do grafo — o inverso do que já existe) e o exportador `graphify export obsidian` (documentado em `docs.graphify.com`, não no README — ver a análise [Workflow Claude Code + Graphify + Obsidian](claude-code-graphify-obsidian.md)). A consulta por `graphify query`/`explain`/`path` evita reler páginas inteiras, e a separação `EXTRACTED`/`INFERRED` dá rastreabilidade parecida com a exigência de fontes já praticada aqui. Determinístico e sem vector store — mais barato e mais auditável que o Understand-Anything. |
| [tobi/qmd](../repos/github.com/tobi/qmd.md) | **Alto** | É literalmente a ferramenta que o concept `Wiki pessoal com LLMs` já sugeria para esta escala: busca local híbrida BM25/vetorial com reranking, CLI, servidor MCP e SDK. Ingerida em 2026-10-28, depois desta análise: MIT, mantida por Tobias Lütke (CEO da Shopify), 30.707 estrelas. Resolve busca sem adicionar um pipeline de grafo — o candidato mais barato de configurar dos três, por ser puramente retrieval, sem camada semântica de LLM sobre a estrutura das páginas. |
| [DeusData/codebase-memory-mcp](../repos/github.com/deusdata/codebase-memory-mcp.md) | **Baixo** | Documentado como servidor MCP de grafo de código com Hybrid LSP e 162 linguagens — a proposta é indexar código-fonte com símbolos e referências de linguagem, não prosa em Markdown interligada por wikilinks. Pouco retorno para o conteúdo real deste repositório. |
| [lfnovo/open-notebook](../repos/github.com/lfnovo/open-notebook.md) / [MODSetter/SurfSense](../repos/github.com/modsetter/surfsense.md) | **Baixo, por desenho** | Resolvem busca full-text/vetorial sobre documentos do próprio usuário, mas são aplicações separadas (self-hosted via Docker/app desktop) que apontariam para `wiki/` como corpus externo — não é algo que se "configura no repositório", é outra aplicação ao lado dele. Avaliado e descartado para o escopo da pergunta (configuração *deste* repositório), mas registrado como alternativa caso o objetivo mude para um notebook de consulta separado da wiki. |

### Por que Understand-Anything > Graphify > qmd, nesta ordem, para este caso específico

1. **Understand-Anything** é o mais alinhado ao problema declarado (é "para" wikis LLM, não adaptado). Custo: depende de LLM para a camada semântica (resumos, relações implícitas) na primeira execução — o próprio README avisa sobre custo de tokens em bases grandes; execuções seguintes são incrementais.
2. **Graphify** é a opção mais barata e auditável (determinístico, sem vector store, sem LLM na estrutura), mas exige mais trabalho de adaptação porque não foi feito para wikis — o `--wiki` gera uma wiki a partir de um grafo de código, não o inverso do que esta wiki precisa. Vale mais pela exportação Obsidian, se o objetivo for navegação visual, não busca textual.
3. **qmd** resolve só busca, sem grafo — a opção certa se o problema real for "achar a página certa rápido" e não "visualizar como as páginas se conectam". É a mais alinhada ao espírito "sem infraestrutura de embeddings pesada" do concept original: BM25 e vetorial rodam em modelos GGUF pequenos (~300MB–1,1GB), on-device, sem depender de um backend externo para a busca em si (só o reranking e a expansão de query, que também rodam local via `node-llama-cpp`).

### O que isso significa, concretamente, para configurar neste repositório

Nenhuma dessas ferramentas substitui `wiki/index.md` e `wiki/categorias.md` — ambos continuam sendo a camada de bookkeeping obrigatória pelo schema (regra 3). O que mudaria é ter uma camada de busca/grafo **sobre** `wiki/`, consultada antes de abrir arquivo por arquivo:

- Se o objetivo é reduzir o tempo de "já existe uma página sobre X?" antes de ingerir algo novo (regra 10 do `CLAUDE.md`): `Understand-Anything` via `/understand-knowledge wiki/` é o candidato mais direto, mantendo o grafo gerado fora de `raw/` (que é imutável) e decidindo se `.ua/knowledge-graph.json` é versionado ou ignorado — o README recomenda commitar para compartilhar, mas isso cresce o repositório.
- Se o objetivo é navegar visualmente as conexões entre páginas (quais conceitos ligam quais repositórios, quais entidades aparecem em várias categorias): `graphify export obsidian` sobre `wiki/`, abrindo como vault do Obsidian — reaproveitando a arquitetura de três camadas já recomendada na análise anterior (fontes / conhecimento gerado / conhecimento curado), que mapeia quase direto para `raw/` / artefato do pipeline / `wiki/` escrito por curadoria.
- Se o objetivo é só busca rápida sem adicionar grafo: `qmd collection add wiki/ --name ai-wiki`, `qmd context add qmd://ai-wiki "Wiki pessoal de IA, por categoria"` e `qmd embed`, depois consultando via `qmd query` ou pelo servidor MCP (`qmd mcp`) direto da sessão de agente — sem precisar rodar nenhum passo semântico por LLM antes da busca em si.

## Conclusão

Sim, há sinal concreto (303 páginas, 106 repositórios, acima do "~100 fontes" que o próprio padrão-fonte desta wiki aponta como limite do índice linear) para configurar uma camada de indexação. Das ferramentas já documentadas aqui, a mais adequada ao propósito específico — indexar uma *wiki* mantida por LLM, não um codebase — é o **Egonex-AI/Understand-Anything**, por ser construído sobre o mesmo padrão-fonte (`karpathy/llm-wiki`) que esta wiki segue. O **Graphify** é a alternativa mais barata e auditável, mais forte para navegação visual via Obsidian do que para busca textual. O **[qmd](../repos/github.com/tobi/qmd.md)**, citado no próprio concept como a ferramenta de referência para esta escala, foi ingerido como página própria depois desta análise — é a opção de busca pura, mais barata que as duas de grafo por não depender de LLM para entender a estrutura das páginas. Nenhuma dessas opções substitui o bookkeeping manual (`index.md`/`categorias.md`/`log.md`) exigido pelo schema; todas operam como camada de consulta adicional sobre ele.

## Perguntas abertas

- O passo semântico do Graphify e a camada de LLM do Understand-Anything enviariam o conteúdo de `wiki/` (resumos, nomes, relações entre páginas) a um backend externo — vale revisar isso com a mesma régua de privacidade já aplicada à página do próprio Graphify antes de rodar sobre conteúdo potencialmente sensível. O qmd, por comparação, só sai do modelo local para reranking/expansão de query, ambos via `node-llama-cpp` on-device.
- Qual seria o critério de sucesso: tempo para achar uma página existente, ou capacidade de navegar visualmente as conexões? A resposta muda a escolha entre qmd (busca) e Graphify/Understand-Anything (grafo).

## Fontes

- [Wiki pessoal com LLMs](../concepts/wiki-pessoal-com-llms.md) — página já existente nesta wiki, usada para o limiar de escala e a citação original a `qmd`.
- [Egonex-AI/Understand-Anything](../repos/github.com/egonex-ai/understand-anything.md) — página já existente, commit `f2d0164f72fe678805c34245a6df36acededfebd`.
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — página já existente, commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8`.
- [tobi/qmd](../repos/github.com/tobi/qmd.md) — ingerida em 2026-10-28, depois desta análise, commit `86d2365d17fc682e491c2c53d1e4a884aee8682a`.
- [Workflow Claude Code + Graphify + Obsidian](claude-code-graphify-obsidian.md) — análise já existente, reaproveitada para a arquitetura de três camadas.
- [DeusData/codebase-memory-mcp](../repos/github.com/deusdata/codebase-memory-mcp.md), [lfnovo/open-notebook](../repos/github.com/lfnovo/open-notebook.md), [MODSetter/SurfSense](../repos/github.com/modsetter/surfsense.md) — páginas já existentes, consultadas apenas por seus resumos em `categorias.md`/`index.md` para a tabela comparativa, sem reabertura do README completo nesta análise.
- Contagem de páginas e tamanho de `wiki/`: `find`/`du` sobre o próprio repositório, em 2026-10-28.
