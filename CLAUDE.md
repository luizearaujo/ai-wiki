# AI Wiki — schema do agente

Wiki pessoal de conhecimento sobre IA, construída a partir de repositórios de código. Este arquivo é o **schema** da wiki: define estrutura, convenções e workflows que devem ser seguidos em toda operação. Leia-o antes de qualquer ingestão, consulta ou manutenção, e evolua-o junto com a wiki.

A ideia original está em [`llm-wiki-md`](llm-wiki-md).

## Princípios

- A wiki é o artefato persistente: conhecimento compilado uma vez e mantido atual, em vez de recalculado a cada consulta.
- O usuário fornece as fontes e as perguntas; o agente escreve e mantém as páginas.
- Toda afirmação relevante deve ser rastreável até um repositório e um commit.
- Prefira atualizar uma página existente a criar uma duplicata.
- Resuma e referencie; não copie blocos longos de código ou documentação.
- Contradições não são apagadas: são sinalizadas e contextualizadas.
- O escopo é IA: modelos, agentes, frameworks, ferramentas, infraestrutura, avaliação, pesquisa aplicada. Repositórios fora desse escopo exigem confirmação antes da ingestão.

## Estrutura

```
/
├── CLAUDE.md                    # este schema
├── llm-wiki-md                  # ideia original
├── raw/
│   └── repos/<host>/<owner>/<repo>/   # clones shallow e descartáveis (não versionados)
├── templates/
│   ├── repo.md
│   ├── concept.md
│   ├── entity.md
│   └── analysis.md
└── wiki/
    ├── index.md                 # catálogo de todas as páginas
    ├── log.md                   # registro cronológico append-only
    ├── overview.md              # síntese em evolução do ecossistema
    ├── repos/<host>/<owner>/<repo>.md
    ├── concepts/<slug>.md
    ├── entities/<slug>.md
    └── analyses/<slug>.md
```

### Camadas

- **`raw/`** — fontes imutáveis. Para repositórios, são clones `--depth 1` em `raw/repos/`. Nunca edite esses arquivos e nunca os versione: a página da wiki registra URL + commit, o que torna a fonte reproduzível.
- **`wiki/`** — camada gerada e mantida pelo agente. O usuário lê; o agente escreve.
- **`CLAUDE.md` + `templates/`** — schema e formato das páginas.

## Regras inegociáveis

1. Não modifique nada em `raw/`.
2. Toda página em `wiki/` (exceto `index.md` e `log.md`) começa com frontmatter YAML.
3. Toda ingestão, consulta arquivada ou remoção atualiza `wiki/index.md` e `wiki/log.md`.
4. Links internos usam caminhos relativos em Markdown, não wikilinks do Obsidian — a wiki precisa renderizar no GitHub.
5. Toda página de repositório registra o commit usado como fonte.
6. Datas no formato ISO (`YYYY-MM-DD`).
7. Conteúdo em português; termos técnicos consagrados podem ficar em inglês.
8. Nomes de arquivo em minúsculas, ASCII e kebab-case. Para repositórios, preserve `owner/repo` em minúsculas no caminho.
9. Não crie páginas vazias ou stubs sem conteúdo. Conceito central sem página própria deve ser anotado como lacuna em `overview.md`.
10. Antes de criar uma página, procure uma existente sobre o mesmo assunto.

## Frontmatter

Campos comuns: `type`, `created`, `updated`, `tags`.

### Repositório

```yaml
---
type: repo
url: https://github.com/owner/repo
host: github.com
owner: owner
repo: repo
commit: <sha completo>
license: MIT            # SPDX ou "desconhecida"
language: Python        # linguagem principal
status: active          # active | maintenance | archived | deprecated | unknown
created: 2026-10-17     # criação da página
ingested: 2026-10-17    # última ingestão da fonte
updated: 2026-10-17
tags: [agentes, orquestracao]
---
```

### Conceito

```yaml
---
type: concept
aliases: [RAG, Retrieval-Augmented Generation]
status: draft           # draft | stable
created: 2026-10-17
updated: 2026-10-17
tags: []
---
```

### Entidade (organização, pessoa ou projeto)

```yaml
---
type: entity
kind: org               # org | person | project
url: https://github.com/owner
created: 2026-10-17
updated: 2026-10-17
tags: []
---
```

### Análise (resposta de consulta arquivada)

```yaml
---
type: analysis
related: []             # caminhos relativos para as páginas usadas
created: 2026-10-17
updated: 2026-10-17
tags: []
---
```

### Overview (síntese do ecossistema)

```yaml
---
type: overview
created: 2026-10-17
updated: 2026-10-17
tags: []
---
```

## Workflows

### 1. Ingestão de repositório

Gatilho: o usuário informa uma URL de repositório. Por padrão, execute a ingestão de ponta a ponta e apresente o resumo no final. Peça confirmação apenas se a URL for ambígua, se o repositório cobrir vários produtos sem relação clara, ou se o conteúdo conflitar com páginas existentes de forma que a decisão de síntese seja do usuário.

1. **Normalize a URL.** Aceite `https://<host>/<owner>/<repo>`, com ou sem `.git`, e URLs com `/tree/<ref>/<subdir>`. Extraia `host`, `owner`, `repo`; converta `owner` e `repo` para minúsculas nos caminhos, preservando o nome original na URL e no título. Se houver subdiretório, documente o repositório, mas destaque a parte que motivou o pedido.
2. **Clone a fonte.**

```bash
dir="raw/repos/$host/$owner/$repo"
mkdir -p "$(dirname "$dir")"
if [ -d "$dir/.git" ]; then
  git -C "$dir" fetch --depth 1 origin HEAD
  git -C "$dir" checkout --detach FETCH_HEAD
else
  git clone --depth 1 "https://$host/$owner/$repo.git" "$dir"
fi
sha="$(git -C "$dir" rev-parse HEAD)"
```

3. **Levante metadados.** Commit (`sha`), licença (`LICENSE*`), linguagem principal, status do projeto, última release/tag e tópicos. Se `gh` estiver disponível e o host for GitHub, use `gh api repos/$owner/$repo` para complementar. Estrelas e números mudam: registre-os apenas como observação datada, nunca como fato estável.
4. **Leia na ordem:** README → `docs/` (índice e getting started) → manifestos (`package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`) → `LICENSE` → `CHANGELOG`/releases → árvore de diretórios (2–3 níveis) → entrypoints e arquivos centrais. Em repositórios grandes, priorize documentação, manifestos e entrypoints em vez de ler todo o código.
5. **Identifique o que merece página.** A página do repositório é obrigatória. Crie ou atualize a página da entidade `owner` quando houver contexto suficiente. Crie páginas de conceito apenas para ideias centrais e capazes de sustentar uma página útil; demais termos ficam no texto ou como lacuna em `overview.md`.
6. **Escreva a página** com o template `templates/repo.md` em `wiki/repos/<host>/<owner>/<repo>.md`. Em reingestão, compare o novo SHA com o anterior, registre o que mudou e preserve a síntese que continua válida.
7. **Faça o bookkeeping:** adicione a entrada em `wiki/index.md`, acrescente a entrada no fim de `wiki/log.md`, crie links bidirecionais (repositório ↔ conceitos/entidades) e atualize `wiki/overview.md` somente se o repositório mudar o quadro geral.
8. **Verifique:** links relativos resolvem, frontmatter completo, página listada no índice, sem duplicata, informações datadas corretamente.

### 2. Consulta

1. Leia `wiki/index.md` para localizar páginas relevantes; depois leia as páginas e siga os links necessários.
2. Responda com citações às páginas da wiki e, quando o dado for sensível à versão, ao commit registrado.
3. Se a wiki não tiver a informação, diga o que falta e proponha uma fonte a ingerir. Não invente.
4. **Arquive respostas reutilizáveis.** Comparações, análises e sínteses que o usuário provavelmente reutilizará viram `wiki/analyses/<slug>.md` com o template `templates/analysis.md`. Atualize índice e log com uma entrada de tipo `query`.

### 3. Lint

Rode quando solicitado ou ao final de um lote de ingestões. Procure e corrija:

- links quebrados ou apontando para páginas renomeadas;
- páginas ausentes do `index.md`;
- frontmatter faltando ou inválido;
- contradições entre páginas (sinalize com data e fonte, não apague);
- afirmações que fontes mais novas superaram;
- páginas órfãs (sem links de entrada);
- conceitos importantes citados que não têm página própria (registre em `overview.md`);
- lacunas que uma nova fonte poderia preencher.

Registre o resultado em `wiki/log.md` com uma entrada de tipo `lint`.

## Convenções de escrita

- Abra cada página com um resumo de uma frase em blockquote.
- Use títulos `##` para seções; evite níveis além de `###`.
- Use tabelas para comparações e listas para relações.
- Prefira frases curtas e densas; explique o "porquê", não só o "o quê".
- Marque incerteza com **A verificar** e diga o que falta.
- Use status `deprecated`/`archived` com a data em que o estado foi observado.
- Toda página termina com a seção `## Fontes` listando URLs e commits consultados.

## Formato do índice

```markdown
## Repositórios

- [owner/repo](repos/github.com/owner/repo.md) — resumo de uma linha.

## Conceitos

- [Nome do conceito](concepts/nome.md) — resumo de uma linha.

## Entidades

- [Nome](entities/nome.md) — resumo de uma linha.

## Análises

- [Título](analyses/titulo.md) — resumo de uma linha.
```

Mantenha a ordenação alfabética dentro de cada seção.

## Formato do log

Append-only, uma entrada por operação, sempre no fim do arquivo:

```markdown
## [2026-10-17] ingest | owner/repo
- Criada `repos/github.com/owner/repo.md`.
- Atualizados `concepts/x.md`, `entities/owner.md`, `index.md`.
```

Prefixos usados: `ingest`, `query`, `lint`, `init`, `fix`. Dica: `grep "^## \[" wiki/log.md | tail -5` mostra as últimas operações.
