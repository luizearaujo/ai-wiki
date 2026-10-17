# Log

> Registro cronológico e append-only. Formato: `## [YYYY-MM-DD] operação | alvo`.
> Dica: `grep "^## \[" wiki/log.md | tail -5` mostra as últimas operações.

## [2026-10-17] init | Estrutura inicial da wiki
- Criado `CLAUDE.md` com o schema, convenções e workflows.
- Criados `raw/repos/`, `templates/` e `wiki/` (`repos/`, `concepts/`, `entities/`, `analyses/`).
- Criados `wiki/index.md`, `wiki/log.md` e `wiki/overview.md`.

## [2026-10-17] fix | Consistência do schema
- Adicionado `created` ao frontmatter e ao template de repositório.
- Documentado o tipo `overview` e adicionada a seção `## Fontes` em `wiki/overview.md`.
- Explicitada a conversão de `owner`/`repo` para minúsculas no caminho.
- Corrigido o placeholder `url` do template de entidade.

## [2026-10-17] ingest | morluto/rea
- Clonado o repositório no commit `09de00b4108a5d738ebe56903e0110ef63820aca`.
- Criada `repos/github.com/morluto/rea.md` com arquitetura, alvos, uso rápido, estado e perguntas abertas.
- Criados `concepts/model-context-protocol.md`, `concepts/engenharia-reversa-agentica.md` e `concepts/evidencia-e-proveniencia.md`.
- Criada `entities/morluto.md`.
- Atualizados `index.md` e `overview.md`.

## [2026-10-17] fix | Links e números voláteis em morluto/rea
- Adicionado o link reverso de `repos/github.com/morluto/rea.md` para `entities/morluto.md`.
- Arredondada a contagem de issues abertas para evitar drift entre consultas.
