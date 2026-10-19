# AI Wiki — schema do agente

Wiki pessoal de conhecimento sobre IA, construída a partir de repositórios de código e artefatos para agentes, como skills. Este arquivo é o **schema** da wiki: define estrutura, convenções e workflows que devem ser seguidos em toda operação. Leia-o antes de qualquer ingestão, consulta ou manutenção, e evolua-o junto com a wiki.

A ideia original está em [`llm-wiki-md`](llm-wiki-md), cópia do gist [`karpathy/llm-wiki`](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). O padrão está documentado em [`wiki/concepts/wiki-pessoal-com-llms.md`](wiki/concepts/wiki-pessoal-com-llms.md).

## Princípios

- A wiki é o artefato persistente: conhecimento compilado uma vez e mantido atual, em vez de recalculado a cada consulta.
- O usuário fornece as fontes e as perguntas; o agente escreve e mantém as páginas.
- Toda afirmação relevante deve ser rastreável até uma fonte (URL e, quando houver, commit).
- Prefira atualizar uma página existente a criar uma duplicata.
- Resuma e referencie; não copie blocos longos de código ou documentação.
- Contradições não são apagadas: são sinalizadas e contextualizadas.
- O escopo é IA: modelos, agentes, frameworks, ferramentas, infraestrutura, avaliação, pesquisa aplicada, skills e servidores MCP. Fontes fora desse escopo exigem confirmação antes da ingestão.

## Estrutura

```
/
├── CLAUDE.md                    # este schema
├── README.md                    # porta de entrada: contagens e links de todas as páginas
├── llm-wiki-md                  # ideia original
├── raw/
│   └── repos/<host>/<owner>/<repo>/   # clones opcionais, só com pedido explícito (não versionados)
├── templates/
│   ├── repo.md
│   ├── skill.md
│   ├── concept.md
│   ├── entity.md
│   └── analysis.md
└── wiki/
    ├── index.md                 # catálogo de todas as páginas
    ├── log.md                   # registro cronológico append-only
    ├── overview.md              # síntese em evolução do ecossistema
    ├── categorias.md            # catálogo temático por categoria
    ├── repos/<host>/<owner>/<repo>.md
    ├── skills/<host>/<owner>/<repo>/<slug>.md
    ├── concepts/<slug>.md
    ├── entities/<slug>.md
    └── analyses/<slug>.md
```

### Camadas

- **`raw/`** — fontes imutáveis e opcionais. Clones `--depth 1` em `raw/repos/` só são criados quando o usuário pedir explicitamente. Nunca edite esses arquivos e nunca os versione: a página da wiki registra URL + commit, o que torna a fonte reproduzível.
- **`wiki/`** — camada gerada e mantida pelo agente. O usuário lê; o agente escreve.
- **`README.md`** — porta de entrada do repositório: contagens por tipo e links para todas as páginas. Deve espelhar `wiki/index.md` e ser atualizado no mesmo commit de qualquer inclusão, alteração ou remoção de página.
- **`wiki/categorias.md`** — porta de entrada temática: agrupa as páginas por área e deve acompanhar toda página de conteúdo criada, alterada ou removida.
- **`CLAUDE.md` + `templates/`** — schema e formato das páginas.
- **Repositórios** — documentados apenas a partir do `README.md` na referência registrada. Não clone o repositório nem leia `docs/`, código-fonte ou manifestos sem autorização explícita.
- **Skills** — documentadas a partir da página de origem (marketplace/catálogo) e do repositório-fonte. Não clone um repositório apenas para documentar uma skill; se precisar do conteúdo interno, leia o `SKILL.md` cru quando isso for autorizado.

## Regras inegociáveis

1. Não modifique nada em `raw/`.
2. Toda página em `wiki/` (exceto `index.md` e `log.md`) começa com frontmatter YAML.
3. Toda ingestão, consulta arquivada ou remoção atualiza `wiki/index.md`, `wiki/log.md`, `wiki/categorias.md` e o `README.md` da raiz.
4. Links internos usam caminhos relativos em Markdown, não wikilinks do Obsidian — a wiki precisa renderizar no GitHub.
5. Toda página de repositório registra o commit do `README.md` usado como fonte; toda página de skill registra a URL de origem e o repositório-fonte.
6. Datas no formato ISO (`YYYY-MM-DD`).
7. Conteúdo em português; termos técnicos consagrados podem ficar em inglês.
8. Nomes de arquivo em minúsculas, ASCII e kebab-case. Para repositórios, preserve `owner/repo` em minúsculas no caminho; para skills, preserve `<owner>/<repo>/<slug>`.
9. Não crie páginas vazias ou stubs sem conteúdo. Conceito central sem página própria deve ser anotado como lacuna em `overview.md`.
10. Antes de criar uma página, procure uma existente sobre o mesmo assunto.
11. Não clone repositórios para documentação de rotina: leia apenas o `README.md` (repositórios) ou a página de origem (skills). Clones e arquivos internos exigem pedido explícito.
12. Toda página de conteúdo aparece em pelo menos uma categoria em `wiki/categorias.md`; páginas transversais podem aparecer em mais de uma.
13. Se o usuário informar mais de um repositório ou skill na mesma mensagem, não crie, edite ou atualize nenhuma página, índice, categoria, README ou log por conta própria. Apresente antes um resumo de uma linha por item — o que é e se já existe na wiki — e só ingira os itens que o usuário confirmar explicitamente. Essa regra vale mesmo que nenhum item seja ambíguo.

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
commit: <sha completo>  # HEAD usado ao ler o README
license: MIT            # SPDX ou "desconhecida"
language: Python        # linguagem principal (API do host; "desconhecida" se indisponível)
status: active          # active | maintenance | archived | deprecated | unknown
created: 2026-10-17     # criação da página
ingested: 2026-10-17    # última ingestão da fonte
updated: 2026-10-17
tags: [agentes, orquestracao]
---
```

### Skill (instruções empacotadas para agentes)

```yaml
---
type: skill
name: Nome da skill
slug: slug-da-skill
url: https://marketplace/...        # página de origem consultada
source_url: https://github.com/owner/repo
source_path: skills/slug            # caminho no repositório-fonte, se conhecido
author: owner
version: <versão | desconhecida>    # versão da skill; não confundir com a do repo
license: <SPDX | desconhecida>
status: active                      # active | archived | unknown
created: 2026-10-17
updated: 2026-10-17
tags: []
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

### Categoria (catálogo temático)

```yaml
---
type: category
created: 2026-10-17
updated: 2026-10-17
tags: [navegacao, categorias]
---
```

## Workflows

### 1. Ingestão de repositório

Gatilho: o usuário informa uma URL de repositório. Por padrão, execute a ingestão de ponta a ponta e apresente o resumo no final. A fonte de conteúdo é **apenas o `README.md`**: não clone o repositório nem leia `docs/`, código-fonte ou manifestos, salvo pedido explícito. Peça confirmação se a URL for ambígua, se o repositório cobrir vários produtos sem relação clara, se o README não existir ou for insuficiente para uma página útil, ou se o conteúdo conflitar com páginas existentes de forma que a decisão de síntese seja do usuário.

**Se o usuário informar mais de um repositório na mesma mensagem**, não ingira nada automaticamente (regra inegociável 13): faça a triagem (resolva nomes ambíguos, confira o que já existe na wiki, confirme que cada repositório existe) e apresente um resumo de uma linha por item antes de criar qualquer página. Ingira só os itens confirmados.

1. **Normalize a URL.** Aceite `https://<host>/<owner>/<repo>`, com ou sem `.git`, e URLs com `/tree/<ref>/<subdir>`. Extraia `host`, `owner`, `repo`; converta `owner` e `repo` para minúsculas nos caminhos, preservando o nome original na URL e no título. Se houver subdiretório, documente o repositório, mas destaque a parte que motivou o pedido.
2. **Descubra o HEAD sem clonar.** Use `git ls-remote https://<host>/<owner>/<repo> HEAD` (ou a API do host) e registre o SHA. Esse é o commit usado como referência.
3. **Leia apenas o `README.md`.** Busque o arquivo nessa referência — por exemplo, `https://raw.githubusercontent.com/<owner>/<repo>/<sha>/README.md`. Se o nome não for esse (variações de caixa, `README.rst`), descubra-o pela API do host. Não abra nenhum outro arquivo do repositório.
4. **Levante metadados pela API** (quando disponível): licença, linguagem principal, status, tópicos, última release e data do último push. Estrelas, forks e issues mudam: registre-os apenas como observação datada, nunca como fato estável.
5. **Escreva a página** com `templates/repo.md` em `wiki/repos/<host>/<owner>/<repo>.md`. Documente o que o README publica: propósito, como funciona, instalação, uso, exemplos, pré-requisitos, limitações e posicionamento. Marque como **A verificar** tudo o que o README não cobrir e diga explicitamente que somente ele foi lido. Em reingestão, compare o novo SHA com o anterior e registre o que mudou.
6. **Identifique o que merece página.** A página do repositório é obrigatória. Crie ou atualize a página da entidade `owner` quando houver contexto suficiente. Crie páginas de conceito apenas para ideias centrais e capazes de sustentar uma página útil; demais termos ficam no texto ou como lacuna em `overview.md`.
7. **Faça o bookkeeping:** adicione a entrada em `wiki/index.md`, à(s) categoria(s) adequada(s) em `wiki/categorias.md` e ao `README.md` (contagem e lista da seção "Conteúdo atual"), acrescente a entrada no fim de `wiki/log.md`, crie links bidirecionais (repositório ↔ conceitos/entidades) e atualize `wiki/overview.md` somente se o repositório mudar o quadro geral.
8. **Verifique:** links relativos resolvem, frontmatter completo, página listada no índice, em pelo menos uma categoria e no `README.md`, contagens e listas do README iguais às do índice, sem duplicata, informações datadas corretamente.
9. **Commit e push.** Sempre, ao final de toda ingestão, crie um commit com a mensagem `add <URL-do-repositório>` (ex.: `add https://github.com/owner/repo`) e execute `git push`. Faça isso sem pedir confirmação ao usuário.

### 2. Ingestão de skill

Gatilho: o usuário informa a URL de uma skill (marketplace, catálogo ou caminho em um repositório). Documente a skill a partir da página de origem; **não clone o repositório** só para isso, salvo pedido explícito.

**Se o usuário informar mais de uma skill (ou uma mistura de repositórios e skills) na mesma mensagem**, não ingira nada automaticamente (regra inegociável 13): apresente um resumo de uma linha por item antes de criar qualquer página, e ingira só os itens confirmados.

1. **Leia a página de origem.** Extraia nome, autor, repositório-fonte, descrição, categoria, comandos de instalação, metadados (instalações, estrelas, primeira aparição), preço, licença e links.
2. **Identifique a fonte canônica.** Registre `source_url` e `source_path`. Se o `SKILL.md` estiver acessível e o usuário autorizar, leia o arquivo cru; caso contrário, documente apenas o que a página publica e marque explicitamente o que não foi verificado.
3. **Escreva a página** com o template `templates/skill.md` em `wiki/skills/<host>/<owner>/<repo>/<slug>.md`.
4. **Entidade e conceitos.** Crie ou atualize a entidade do autor. Crie página de conceito para a ideia central (ex.: agent skills, auditoria de UX) quando houver material suficiente.
5. **Exemplos de uso** são permitidos, mas devem ser rotulados como exemplos derivados da descrição publicada, não como instruções oficiais da skill.
6. **Faça o bookkeeping e verifique** como na ingestão de repositório: índice, categorias, README (contagens e listas), log, links bidirecionais, frontmatter e links relativos.
7. **Commit e push.** Sempre, ao final de toda ingestão de skill, crie um commit com a mensagem `add <URL-da-skill>` e execute `git push`. Faça isso sem pedir confirmação ao usuário.

### 3. Consulta

1. Leia `wiki/index.md` (ou `wiki/categorias.md` para navegação por assunto) para localizar páginas relevantes; depois leia as páginas e siga os links necessários.
2. Responda com citações às páginas da wiki e, quando o dado for sensível à versão, ao commit registrado.
3. Se a wiki não tiver a informação, diga o que falta e proponha uma fonte a ingerir. Não invente.
4. **Arquive respostas reutilizáveis.** Comparações, análises e sínteses que o usuário provavelmente reutilizará viram `wiki/analyses/<slug>.md` com o template `templates/analysis.md`. Atualize índice, categorias, README (contagem e lista de análises) e log com uma entrada de tipo `query`.

### 4. Lint

Rode quando solicitado ou ao final de um lote de ingestões. Procure e corrija:

- links quebrados ou apontando para páginas renomeadas;
- páginas ausentes do `index.md`, de `wiki/categorias.md` ou do `README.md`, e categorias inadequadas;
- contagens ou listas do `README.md` divergentes de `wiki/index.md`;
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

## Skills

- [Nome da skill](skills/github.com/owner/repo/slug.md) — resumo de uma linha.

## Conceitos

- [Nome do conceito](concepts/nome.md) — resumo de uma linha.

## Entidades

- [Nome](entities/nome.md) — resumo de uma linha.

## Análises

- [Título](analyses/titulo.md) — resumo de uma linha.
```

Mantenha a ordenação alfabética dentro de cada seção.

## Formato do README

O `README.md` da raiz é a porta de entrada do repositório e deve espelhar `wiki/index.md`:

- A seção "Conteúdo atual" traz uma tabela com uma linha por tipo de página, contagem entre parênteses e links de todas as páginas separados por ` · `, em ordem alfabética.
- A linha de análises mostra `Análises (n)`; quando não houver nenhuma, use o texto `_Nenhuma análise arquivada ainda._` sem link.
- As linhas de Categorias e Panorama apontam para `wiki/categorias.md` e `wiki/overview.md`.
- Sempre que uma página for criada, renomeada, alterada (título ou resumo) ou removida, atualize a contagem e a lista correspondente no mesmo commit. Nunca deixe o README divergir do índice.

## Formato do catálogo de categorias

`wiki/categorias.md` agrupa as páginas por área, não por tipo. Cada categoria tem uma frase de escopo e listas separadas por tipo de página:

```markdown
## Nome da categoria

> Uma frase descrevendo o escopo e o critério de inclusão.

**Repositórios**
- [owner/repo](repos/github.com/owner/repo.md) — resumo de uma linha.

**Skills**
- [Nome da skill](skills/github.com/owner/repo/slug.md) — resumo de uma linha.

**Conceitos**
- [Nome do conceito](concepts/nome.md)

**Entidades**
- [Nome](entities/nome.md)
```

Regras: mantenha as listas em ordem alfabética; uma página pode aparecer em mais de uma categoria; não crie categoria para um único item se houver uma categoria vizinha adequada; categorias novas devem ter título claro e uma frase de escopo.

## Formato do log

Append-only, uma entrada por operação, sempre no fim do arquivo:

```markdown
## [2026-10-17] ingest | owner/repo
- Criada `repos/github.com/owner/repo.md`.
- Atualizados `concepts/x.md`, `entities/owner.md`, `index.md`.
```

Prefixos usados: `ingest` (repositórios e skills), `query`, `lint`, `init`, `fix`. Dica: `grep "^## \[" wiki/log.md | tail -5` mostra as últimas operações.
