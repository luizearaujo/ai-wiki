---
type: concept
aliases: [LLM Wiki, LLM-wiki, wiki mantida por LLM, personal knowledge wiki, wiki pessoal]
status: draft
created: 2026-10-19
updated: 2026-10-28
tags: [conhecimento, wiki, agentes, curadoria, proveniencia, rag, obsidian]
---

# Wiki pessoal com LLMs

> Padrão em que um agente de IA mantém uma wiki persistente e interligada entre as fontes brutas e o usuário, compilando o conhecimento uma vez e mantendo-o atual em vez de recuperar trechos a cada pergunta.

## Definição

Na experiência mais comum com LLMs e documentos — RAG, NotebookLM, uploads de arquivos — o modelo recupera trechos na hora da consulta e redescobre o conhecimento a cada pergunta. Não há acumulação: uma pergunta que exige sintetizar cinco documentos obriga o modelo a encontrar e montar os fragmentos novamente todas as vezes.

O padrão *LLM Wiki* propõe uma camada intermediária: uma coleção de arquivos Markdown estruturada e interligada, mantida pelo agente. Ao receber uma fonte nova, o agente não apenas a indexa — ele a lê, extrai o que importa e integra ao que já existe, atualizando páginas de entidade, revisando resumos, registrando contradições e fortalecendo ou contestando a síntese corrente. O conhecimento é **compilado uma vez e mantido atual**.

A consequência prática é que a wiki se torna um artefato que **compõe**: referências cruzadas já estão feitas, contradições já estão sinalizadas e a síntese já reflete tudo o que foi lido. O usuário fornece as fontes, explora e faz perguntas; o agente escreve e faz o bookkeeping. O gist compara a divisão a um ambiente de programação: Obsidian é a IDE, o LLM é o programador e a wiki é o código.

## Como funciona

### Três camadas

| Camada | Papel | Quem controla |
|---|---|---|
| **Fontes brutas** | Artigos, papers, imagens, dados e notas originais; imutáveis e fonte da verdade | Usuário |
| **Wiki** | Markdown gerado pelo agente: resumos, entidades, conceitos, comparações, panorama e síntese | Agente |
| **Schema** | Documento que define estrutura, convenções e workflows — por exemplo `CLAUDE.md` ou `AGENTS.md` | Usuário e agente, co-evoluindo |

O schema é o que distingue um mantenedor de wiki disciplinado de um chatbot genérico. Ele fixa como ingerir, consultar e fazer lint, e é ajustado conforme o domínio e o estilo de trabalho.

### Operações

| Operação | Fluxo descrito no gist |
|---|---|
| **Ingest** | Ler a fonte, discutir os pontos principais, escrever a página de resumo, atualizar o índice, atualizar páginas de entidade e conceito afetadas e acrescentar uma entrada no log. Uma única fonte pode tocar 10–15 páginas. |
| **Query** | Buscar as páginas relevantes, lê-las e sintetizar uma resposta com citações — em Markdown, tabela, apresentação Marp, gráfico ou canvas. Respostas boas podem ser arquivadas como páginas novas. |
| **Lint** | Procurar contradições, afirmações superadas por fontes mais novas, páginas órfãs, conceitos sem página própria, referências cruzadas ausentes e lacunas que uma nova fonte poderia preencher. |

A ingestão pode ser feita uma fonte por vez, com o usuário revisando os resumos e orientando ênfases, ou em lote com menos supervisão. O gist recomenda documentar o workflow escolhido no schema para as sessões futuras.

### Índice e log

- **`index.md`** é orientado a conteúdo: catálogo de todas as páginas, com link, resumo de uma linha e metadados opcionais, organizado por categoria. É lido primeiro em cada consulta. Segundo o gist, funciona bem até a ordem de ~100 fontes e algumas centenas de páginas, sem infraestrutura de embeddings.
- **`log.md`** é cronológico e append-only. Um prefixo consistente em cada entrada (`## [data] ingest | Título`) torna o histórico parseável com ferramentas de linha de comando — por exemplo, `grep "^## \[" log.md | tail -5`.

### Ferramentas opcionais

O gist trata a implementação como modular:

- **Obsidian** para navegar, ver o grafo e editar; o Web Clipper converte artigos web em Markdown.
- **Download local de imagens** para que o agente possa consultá-las sem depender de URLs que quebram.
- **Dataview** para gerar tabelas dinâmicas a partir do frontmatter YAML.
- **Marp** para gerar apresentações a partir de páginas da wiki.
- [**qmd**](../repos/github.com/tobi/qmd.md) como busca local híbrida BM25/vector com re-ranking, disponível como CLI, servidor MCP e SDK; alternativamente, um script de busca próprio.
- **Git** como camada de versionamento, ramificação e colaboração — a wiki é apenas um repositório de Markdown.

### Por que funciona

O argumento central é econômico: a parte tediosa de manter uma base de conhecimento não é ler nem pensar, mas o bookkeeping — atualizar referências cruzadas, manter resumos corretos, registrar contradições e preservar consistência entre dezenas de páginas. Humanos abandonam wikis porque o custo de manutenção cresce mais rápido que o valor. O LLM não se entedia, não esquece uma referência e consegue tocar 15 arquivos em uma passada, o que aproxima de zero o custo marginal de manutenção.

O gist relaciona a ideia ao **Memex** de Vannevar Bush (1945): um acervo pessoal e curado, com trilhas associativas entre documentos, privado e mantido ativamente. A parte que Bush não conseguiu resolver — quem faz a manutenção — é justamente a que o LLM assume.

## Onde aparece

- **Esta wiki** ([`ai-wiki`](../../README.md)) — é uma instância declarada do padrão: `CLAUDE.md` funciona como schema, `templates/` fixam formatos, `raw/` guarda fontes imutáveis, `wiki/` é a camada escrita pelo agente e `index.md`/`log.md` fazem a navegação. O arquivo local [`llm-wiki-md`](../../llm-wiki-md) é a cópia da ideia original.
- [CLAUDE.md](claude-md.md) — é o exemplo concreto da camada de schema, com convenções de frontmatter, caminhos, workflows e bookkeeping.
- [Memória de agente](memoria-de-agente.md) — compartilha o objetivo de persistir contexto entre sessões, mas a wiki é um artefato curado e legível, não apenas um histórico de decisões.
- [Evidência e proveniência](evidencia-e-proveniencia.md) — a exigência de rastrear cada afirmação até uma fonte e commit é o que permite auditar a síntese acumulada.
- [Grafo de conhecimento de código](grafo-de-conhecimento-de-codigo.md) — aplica a mesma lógica de representação persistente a código, em vez de documentos e conceitos.
- [Andrej Karpathy](../entities/andrej-karpathy.md) — autor do gist que descreve o padrão.
- [Workflow Claude Code + Graphify + Obsidian](../analyses/claude-code-graphify-obsidian.md) — uma variante de terceiros do mesmo padrão (Obsidian como camada de navegação, um pipeline como gerador de notas), analisada com as mesmas exigências de rastreabilidade desta wiki.
- [Indexação da ai-wiki: o que configurar neste repositório](../analyses/indexacao-da-ai-wiki.md) — aplica o limiar de escala citado aqui ("~100 fontes, algumas centenas de páginas, sem infraestrutura de embeddings") à própria `ai-wiki`, já acima dele, e avalia `qmd`, Understand-Anything e Graphify como resposta.
- [tobi/qmd](../repos/github.com/tobi/qmd.md) — a ferramenta citada acima, ingerida como página própria depois da análise de indexação: busca híbrida BM25/vetorial/rerank, CLI, servidor MCP e SDK.

## Trade-offs

- **Vantagens:** conhecimento acumulado em vez de recalculado; referências cruzadas e contradições já resolvidas; respostas citáveis; um único artefato legível e versionável; funciona sem infraestrutura de RAG em escala moderada; o custo de manutenção é absorvido pelo agente.
- **Limitações:** o agente escreve praticamente tudo, então erros de síntese podem se cristalizar e se propagar; o schema e o bookkeeping precisam ser mantidos; a qualidade depende da curadoria das fontes; o índice linear deixa de bastar quando a wiki cresce muito; não há garantia de que o agente preserve a intenção ou a voz do usuário; atualizações de páginas antigas podem ser menos confiáveis que a leitura da fonte original.
- **Critério prático:** vale quando o conhecimento é acumulativo e relido ao longo do tempo — pesquisa, estudo, acompanhamento pessoal, wiki de equipe. Para perguntas pontuais sobre um conjunto fixo de documentos, RAG continua mais simples.

## Relações

- **Relacionado a:** [CLAUDE.md](claude-md.md) — camada de schema; [Memória de agente](memoria-de-agente.md) — persistência entre sessões; [Evidência e proveniência](evidencia-e-proveniencia.md) — rastreabilidade das afirmações; [Grafo de conhecimento de código](grafo-de-conhecimento-de-codigo.md) — representação persistente aplicada a código.
- **Contrasta com:** RAG por consulta, upload de arquivos em chat e NotebookLM — que recuperam trechos e não acumulam síntese.
- **Pré-requisito para:** transformar explorações em conhecimento permanente; arquivar respostas de consulta como páginas em vez de deixá-las no histórico de chat.

## Perguntas abertas

- Até que ponto o `index.md` substitui busca vetorial, e em que escala a busca local passa a ser necessária?
- Como impedir que uma síntese errada se cristalize e contamine as páginas seguintes?
- Como auditar mudanças feitas pelo agente em páginas antigas e reverter atualizações ruins?
- Como medir o ganho do padrão contra RAG em qualidade, custo de tokens e tempo de manutenção?
- Como tratar fontes que mudam com o tempo e afirmações que deixam de ser verdadeiras?
- Como preservar decisões e voz do usuário quando o agente escreve toda a wiki?
- Que sinais indicam que a wiki precisa de lint, e com que frequência ele deve rodar?

## Fontes

- Gist `karpathy/llm-wiki`: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f (revisão `ac46de1ad27f92b28ac95459c782c07f6b8c964a`, consultada em 2026-10-19; criado em 2026-04-04, última atualização observada em 2026-10-16). Somente o conteúdo do gist foi lido.
- Cópia local [`llm-wiki-md`](../../llm-wiki-md) — idêntica ao conteúdo do gist na revisão acima (MD5 `7953122eebc7aca33db25cd86a89a19a`).
- Metadados do perfil `karpathy` via API do GitHub (consultados em 2026-10-19).
