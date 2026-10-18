# ai-wiki

Wiki pessoal de conhecimento sobre IA, mantida por um agente. Você fornece URLs; o agente escreve e atualiza as páginas.

## O que é

Um repositório de conhecimento compilado sobre o ecossistema de IA: modelos, agentes, frameworks, ferramentas, infraestrutura, skills e servidores MCP. Cada página é gerada a partir da fonte original (README, marketplace, documentação) e mantida atualizada com referência ao commit consultado.

A ideia central é separar **coleta** de **consulta**: o conhecimento é indexado uma vez e fica disponível para qualquer pergunta futura, sem recalcular a partir do zero.

## Conteúdo atual

→ **[Índice completo](wiki/index.md)**

| Tipo | Itens |
|------|-------|
| Repositórios | [codebase-memory-mcp](wiki/repos/github.com/deusdata/codebase-memory-mcp.md) · [agency-agents](wiki/repos/github.com/msitarzewski/agency-agents.md) · [mimic](wiki/repos/github.com/littledivy/mimic.md) · [rea](wiki/repos/github.com/morluto/rea.md) · [andrej-karpathy-skills](wiki/repos/github.com/multica-ai/andrej-karpathy-skills.md) |
| Skills | [UX Audit Rethink](wiki/skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) |
| Conceitos | [MCP](wiki/concepts/model-context-protocol.md) · [Grafo de conhecimento de código](wiki/concepts/grafo-de-conhecimento-de-codigo.md) · [Agent skills](wiki/concepts/agent-skills.md) · [CLAUDE.md](wiki/concepts/claude-md.md) · [Engenharia reversa agêntica](wiki/concepts/engenharia-reversa-agentica.md) · [Auditoria de UX](wiki/concepts/auditoria-de-ux.md) · [Evidência e proveniência](wiki/concepts/evidencia-e-proveniencia.md) |
| Panorama | [overview.md](wiki/overview.md) — síntese em evolução do ecossistema |

## Como funciona

O agente (Claude Code com o schema em [CLAUDE.md](CLAUDE.md)) opera em três modos:

**Ingestão** — forneça uma URL de repositório ou skill:
```
https://github.com/owner/repo
```
O agente lê o `README.md` naquele commit, levanta metadados pela API do GitHub, cria a página em `wiki/`, atualiza o índice e o log, e faz commit + push automaticamente.

**Consulta** — faça uma pergunta:
```
Qual a diferença entre codebase-memory-mcp e rea para análise de código?
```
O agente lê as páginas relevantes do índice e responde com citações. Análises reutilizáveis são arquivadas em `wiki/analyses/`.

**Lint** — ao pedir uma revisão, o agente verifica links quebrados, frontmatter incompleto, páginas ausentes do índice e contradições entre fontes.

## Estrutura

```
wiki/
├── index.md                          # catálogo de todas as páginas
├── log.md                            # histórico append-only de operações
├── overview.md                       # síntese do ecossistema
├── repos/<host>/<owner>/<repo>.md
├── skills/<host>/<owner>/<repo>/<slug>.md
├── concepts/<slug>.md
├── entities/<slug>.md
└── analyses/<slug>.md
```

Cada página começa com frontmatter YAML (`type`, `url`, `commit`, `created`, `updated`, `tags`) e termina com a seção `## Fontes` rastreando o que foi consultado.

## Convenções

- Conteúdo em português; termos técnicos consagrados ficam em inglês.
- Links internos usam caminhos relativos Markdown (renderiza no GitHub).
- Datas no formato ISO (`YYYY-MM-DD`).
- Estrelas, forks e contagens de issues são observações datadas, não fatos estáveis.
- Somente o `README.md` é lido por padrão; arquivos internos e clones exigem pedido explícito.
