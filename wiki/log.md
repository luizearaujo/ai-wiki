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

## [2026-10-17] ingest | mastepanoski/claude-skills — ux-audit-rethink
- Criada `skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md` a partir da página do claudemarketplaces.com, sem clonar o repositório-fonte.
- Criados `concepts/agent-skills.md` e `concepts/auditoria-de-ux.md`.
- Criada `entities/mastepanoski.md`.
- Adicionado `templates/skill.md` e atualizado `CLAUDE.md` com o tipo `skill`.
- Atualizados `index.md` e `overview.md`.
- Não lido o `SKILL.md`: método interno, escala e formato do relatório marcados como a verificar.

## [2026-10-17] fix | Formato de repositório baseado no README
- `CLAUDE.md`: a ingestão de repositório agora lê apenas o `README.md` (via raw/API), sem clonar; metadados complementares vêm da API do host.
- `templates/repo.md` reestruturado no mesmo formato da página de skill: o que é, como funciona, uso, exemplos, quando usar, limitações, estado e fontes.
- `repos/github.com/morluto/rea.md` regravada a partir do README no commit `9e372c6bc914b15e2f778f969da4fd3e11483d78`; os arquivos internos lidos na ingestão anterior deixaram de ser fonte da página.
- Atualizados `entities/morluto.md` e `overview.md`.
