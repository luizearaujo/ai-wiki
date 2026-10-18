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

## [2026-10-17] ingest | multica-ai/andrej-karpathy-skills
- Criada `repos/github.com/multica-ai/andrej-karpathy-skills.md` a partir do README no commit `2c606141936f1eeef17fa3043a72095b4765b9c2`, sem clonar o repositório.
- Criados `concepts/claude-md.md` e `entities/multica-ai.md`.
- Atualizados `concepts/agent-skills.md`, `index.md`, `log.md` e `overview.md`.
- Registrado o redirecionamento de `forrestchang/andrej-karpathy-skills` para `multica-ai/andrej-karpathy-skills`; os comandos de instalação do README ainda usam o owner antigo.
- Não lidos `CLAUDE.md`, `CURSOR.md` e `.cursor/rules/karpathy-guidelines.mdc`; licença MIT declarada no README, mas não detectada pela API do GitHub.

## [2026-10-18] ingest | croffasia/itsaplan
- Criada `repos/github.com/croffasia/itsaplan.md` a partir do README no commit `a54d8c3c4e88193777de0f75601d403c3b96bc1a`, sem clonar o repositório.
- Criada `entities/croffasia.md`.
- Atualizados `index.md`, `log.md` e `overview.md`.
- Não lidos: `docs/`, `CONTRIBUTING.md`, `SECURITY.md`, `packages/runner`; mecanismo de segurança para skills externas e modelo de execução concorrente do Mastra são a verificar.

## [2026-10-18] ingest | littledivy/mimic
- Criada `repos/github.com/littledivy/mimic.md` a partir do README no commit `8cf998ac0b365806d8e522d34107cc504ecaa345`, sem clonar o repositório.
- Criada `entities/littledivy.md`.
- Atualizados `index.md`, `log.md` e `overview.md`.
- Não lidos: `docs/pinning.md`, `docs/dpop.md` e código-fonte; detalhes de bypass de certificate pinning e restrições DPoP são a verificar.

## [2026-10-18] ingest | DeusData/codebase-memory-mcp
- Criada `repos/github.com/deusdata/codebase-memory-mcp.md` a partir do README no commit `354ccecbe612a9fdb624396a6738fa87f2617434`, sem clonar o repositório.
- Criados `concepts/grafo-de-conhecimento-de-codigo.md` e `entities/deusdata.md`.
- Atualizados `index.md`, `log.md` e `overview.md`.
- Não lidos: `docs/`, código-fonte, SECURITY.md, CONFIGURATION.md, manifestos de release. CBM Lens Beta e estado de suporte Windows por cliente são a verificar.

## [2026-10-18] ingest | msitarzewski/agency-agents
- Criada `repos/github.com/msitarzewski/agency-agents.md` a partir do README no commit `652b2692f8d8ec2b1f1a38e559073e287dfdc469`, sem clonar o repositório.
- Criada `entities/msitarzewski.md`.
- Atualizados `index.md`, `log.md` e `overview.md`.
- Não lidos os arquivos de agente individuais (150+), scripts ou demais conteúdos; cobertura de agentes e qualidade de cada especialista são a verificar.

## [2026-10-18] ingest | SynkraAI/aiox-core
- Criada `repos/github.com/synkraai/aiox-core.md` a partir do README no commit `4ef6530ff03b83aea953e4a426f95e012b8b70c5`, sem clonar o repositório.
- Criada `entities/synkraai.md`.
- Atualizados `index.md`, `log.md` e `overview.md`.
- Divergência de licença: README/badge indica MIT, API do GitHub retornou `other/NOASSERTION`; `docs/legal/license-clarification.md` não foi lido.
- Não lidos: `docs/`, código-fonte, arquivos de agente em `.aiox-core/agents/`, `CONTRIBUTING.md`, manifestos de squads.
