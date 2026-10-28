---
type: repo
url: https://github.com/Graphify-Labs/graphify
host: github.com
owner: graphify-labs
repo: graphify
commit: 86c57be8204673c2a1b9849a3292a7dd3ab373d8
license: Apache-2.0
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-28
tags: [agentes, grafo-de-conhecimento, code-intelligence, skills, tree-sitter, mcp]
---

# Graphify-Labs/graphify

> Skill e CLI que mapeia um projeto — código, docs, PDFs, imagens e mídia — em um grafo de conhecimento consultável, com arestas explicadas e sem vector store.

## O que é

O Graphify transforma uma base de código em um grafo navegável que o agente consulta em vez de fazer `grep` arquivo por arquivo. O comando `/graphify` gera três artefatos em `graphify-out/`: `graph.html` (grafo interativo), `GRAPH_REPORT.md` (destaques, comunidades e caminhos) e `graph.json` (o grafo completo, consultável depois sem reler os arquivos).

O README posiciona o produto contra índices vetoriais: não há embeddings nem vector store, e sim um grafo real que se percorre. Cada aresta é marcada como `EXTRACTED` (explícita na fonte) ou `INFERRED` (resolvida pelo Graphify), o que separa o que foi lido do que foi deduzido.

O projeto tem uma edição local open-source e o **Graphify Cloud**, serviço comercial sempre ligado (monorepo, cross-repo, verificação formal, conectores Sentry/Jira e revisão de código), com teste gratuito de 14 dias.

## Como funciona

1. **Parsing local de código.** Código é analisado com tree-sitter AST, de forma determinística e sem LLM; nada sai da máquina.
2. **Semântica opcional.** Docs, PDFs, imagens e vídeo passam por um passo semântico usando o modelo do assistente ou uma API configurada. Vídeo e áudio são transcritos localmente com faster-whisper.
3. **Resolução de grafo.** Arestas de `calls`, `imports`, `inherits`, `mixes_in` etc. são resolvidas entre arquivos em ~40 linguagens.
4. **Comunidades e nós de destaque.** O grafo é dividido em comunidades (Leiden) com rótulos sem LLM; os nós mais conectados viram "god nodes".
5. **Consulta.** `graphify query "<pergunta>"` devolve um subgrafo; `graphify path A B` traça o caminho mais curto; `graphify explain X` descreve um nó e suas conexões.
6. **Integração com o assistente.** `graphify install` registra a skill e, em plataformas com hooks ou arquivos de instrução, orienta o agente a consultar o grafo antes de buscar no código.

O README lista ainda: comentários `# NOTE:`/`# WHY:` e citações a ADR/RFC como nós ligados ao código; exportação para HTML de call-flow via Mermaid; `--wiki` para gerar uma wiki em Markdown; merge de grafos; hook de rebuild em commit/checkout; dashboard de PRs com impacto no grafo; e suporte opcional a MCP, Neo4j, FalkorDB, Postgres e Ollama.

**Exportação para Obsidian (fonte: docs, não o README).** A documentação em docs.graphify.com/guides/exports lista um exportador adicional não mencionado no README: `graphify export obsidian --dir /caminho/do/vault`, descrito como gerador de "notas e links compatíveis com o Obsidian", feito para preservar notas próprias e a configuração `.obsidian` já existentes no vault de destino. A própria documentação recomenda revisar o conteúdo gerado antes de sincronizá-lo com um vault compartilhado. Essa afirmação não foi confirmada no README (`86c57be8204673c2a1b9849a3292a7dd3ab373d8`) e é registrada aqui com a página de docs como fonte separada. Ver uso no contexto de [Workflow Claude Code + Graphify + Obsidian](../../../analyses/claude-code-graphify-obsidian.md).

### Benchmarks declarados

| Benchmark | Métrica | graphify | Campo |
|---|---|---|---|
| LOCOMO (n=300) | recall@10 | 0,497 | mem0 0,048; supermemory 0,149 |
| LOCOMO (n=300) | acurácia de QA | 45,3% | supermemory 49,7%; mem0 27,3% |
| LongMemEval-S (n=50) | acurácia de QA | 76% | empatado com RAG denso |
| ERPNext cross-tool (n=6) | cobertura de fatos-chave | 82,0% | baseline grep/read 70,8% |
| Construção do grafo | créditos de LLM | 0 | por token na maioria dos sistemas |

Os resultados são do projeto, com harness e juiz próprios; o README afirma validação cega por um segundo juiz (90,6% de concordância, kappa 0,81). Trate como alegação datada, não como benchmark independente.

## Instalação e uso rápido

Requisitos: Python 3.10+ e `uv` (recomendado) ou `pipx`.

```bash
uv tool install graphifyy      # o pacote PyPI tem dois "y"
graphify install               # detecta o assistente e registra a skill
```

Depois, no assistente:

```text
/graphify .
```

O comando gera `graphify-out/graph.html`, `GRAPH_REPORT.md` e `graph.json`. O README alerta que o pacote oficial é `graphifyy` e que outros pacotes `graphify*` no PyPI não são afiliados.

Instalação com escopo de projeto:

```bash
graphify install --project
graphify install --project --platform codex
```

Extras opcionais incluem `pdf`, `office`, `google`, `video`, `mcp`, `neo4j`, `falkordb`, `svg`, `leiden`, `ollama`, `openai`, `gemini`, `anthropic`, `bedrock`, `sql`, `postgres`, `terraform`, `robot`, `chinese` e `all`.

## Exemplos de uso

Comandos publicados no README:

```bash
/graphify .                        # grafo da pasta atual
/graphify ./docs --update          # reextrai só o que mudou
/graphify . --cluster-only         # refaz o clustering sem reextrair
/graphify . --no-viz               # só relatório + JSON
/graphify . --wiki                 # wiki em Markdown a partir do grafo
graphify query "what connects auth to the database?"
graphify path "UserService" "DatabasePool"
graphify explain "RateLimiter"
graphify add https://arxiv.org/abs/1706.03762
graphify hook install
graphify prs --triage
```

Exemplos de uso, derivados do README:

- **Onboarding em repositório desconhecido:** gerar o grafo e perguntar quais módulos concentram chamadas e dependências.
- **Análise de impacto:** usar `path`/`explain` antes de editar um componente central.
- **Revisão de PR:** usar `graphify prs 42` para ver o impacto no grafo.
- **Contexto para agentes:** instalar o hook/instruções para que o agente prefira `query` a `grep`.

## Quando usar (e quando não usar)

- **Use quando:** você quer responder perguntas estruturais sobre código com menos tokens, prefere análise local e determinística, quer rastrear o que foi extraído versus inferido, ou quer um grafo que inclua docs, PDFs e mídia.
- **Evite quando:** o problema é busca semântica em texto livre (RAG vetorial pode ser melhor); o projeto é pequeno o bastante para leitura direta; você precisa de análise dinâmica ou de código compilado sem fonte; ou não pode instalar Python/uv.

## Limitações e cuidados

- **Somente o README foi lido.** Código, `ARCHITECTURE.md`, `BENCHMARKS.md`, docs e skills não foram verificados.
- **Grafo estático não é cobertura completa.** Chamadas dinâmicas, reflexão, código gerado em runtime e dependências externas podem não aparecer. O conceito de grafo de código já registra essa lacuna na wiki.
- **Passo semântico envia conteúdo a um backend.** Código fica local, mas docs/PDFs/imagens são enviados ao modelo do assistente ou à API configurada. O README documenta residência de dados e a opção `--code-only`; ainda assim, revise antes de indexar material sensível.
- **Backend e credenciais.** O Graphify auto-detecta provedores por variável de ambiente, com prioridade Gemini → Kimi → Claude → OpenAI → DeepSeek → Azure → Bedrock → Ollama. Kimi roteia para servidores na China; para dados sensíveis, use `GRAPHIFY_BACKEND=ollama` ou desligue backends.
- **Log de consultas.** Toda consulta é gravada em `~/.cache/graphify-queries.log` (JSON Lines), sem subgrafos completos por padrão. Há opt-out documentado.
- **Modelo comercial.** O Graphify Cloud é proprietário e o README o promove em várias seções; a fronteira entre o CLI Apache-2.0 e o serviço não foi verificada no código.
- **Benchmarks do projeto.** Os números não foram reproduzidos nesta ingestão.
- **Extensões ambíguas.** `.inc`, `.h`, `.m` etc. podem ser interpretadas como linguagens diferentes; o `.graphifyrc` permite declarar o mapeamento. Sem isso, o grafo pode ficar populado mas incompleto.

## Estado e adoção

- Versão/releases citadas no README: não há versão única no topo; o pacote é `graphifyy` no PyPI e o repositório é a fonte oficial.
- Observado em 2026-10-19: ~128.781 stars, ~12.417 forks, ~1.556 issues abertas; criado em 2026-04-03; último push em 2026-10-16; branch padrão `v8`.
- Licença: Apache-2.0.
- Linguagem principal na API: Python.
- Site: [graphify.com](https://graphify.com); docs em [docs.graphify.com](https://docs.graphify.com).

## Relações

- Mantido por: [Graphify-Labs](../../../entities/graphify-labs.md)
- Conceitos: [Grafo de conhecimento de código](../../../concepts/grafo-de-conhecimento-de-codigo.md), [Agent skills](../../../concepts/agent-skills.md), [Model Context Protocol](../../../concepts/model-context-protocol.md)
- Relacionado: [DeusData/codebase-memory-mcp](../deusdata/codebase-memory-mcp.md) — servidor MCP de grafo de código em C, com foco em indexação local e 17 ferramentas; [skill understand](../../../skills/github.com/egonex-ai/understand-anything/understand.md) — outra abordagem de grafo de código via skill; [bytedance/deer-flow](../bytedance/deer-flow.md) — harness que usa skills e ferramentas para tarefas longas.
- Integra com: [Obsidian](../../../entities/obsidian.md), via o exportador `graphify export obsidian` documentado em docs.graphify.com.
- Análise: [Indexação da ai-wiki](../../../analyses/indexacao-da-ai-wiki.md) — avalia o Graphify como alternativa determinística ao Understand-Anything para indexar esta própria wiki.
- Projetos citados: tree-sitter, Leiden/graspologic, faster-whisper, yt-dlp, Neo4j, FalkorDB, Ollama.

## Perguntas abertas

- Qual é a diferença prática entre o Graphify e um grafo indexado por servidor MCP como o CBM?
- Como o projeto evita arestas `INFERRED` erradas, e qual é a taxa de erro?
- Como o grafo se mantém atualizado em repositórios com muitos commits, e qual é o custo do hook?
- O Graphify Cloud usa o mesmo parser e formato de grafo do CLI? Há lock-in?
- Como a análise de mídia e PDFs lida com material confidencial e com provedores externos?
- Os benchmarks se sustentam com um harness independente?

## Fontes

- README: https://raw.githubusercontent.com/Graphify-Labs/graphify/86c57be8204673c2a1b9849a3292a7dd3ab373d8/README.md (commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8`, consultado em 2026-10-19 e reconfirmado em 2026-10-19 como ainda o HEAD). Somente o README foi lido para o corpo original da página; código, `ARCHITECTURE.md`, `BENCHMARKS.md` e skills não foram consultados.
- Metadados: API do GitHub (`/repos/Graphify-Labs/graphify`) em 2026-10-19.
- https://docs.graphify.com/guides/exports (consultado em 2026-10-19) — única fonte da exportação para Obsidian; autorizado pelo usuário como exceção à regra de "somente README", para verificar uma afirmação específica de terceiro antes de publicá-la.
