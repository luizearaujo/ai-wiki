# ai-wiki

Wiki pessoal de conhecimento sobre IA, mantida por um agente. Você fornece URLs; o agente escreve e atualiza as páginas.

## O que é

Um repositório de conhecimento compilado sobre o ecossistema de IA: modelos, agentes, frameworks, ferramentas, infraestrutura, skills e servidores MCP. Cada página é gerada a partir da fonte original (README, marketplace, documentação) e mantida atualizada com referência ao commit consultado.

A ideia central é separar **coleta** de **consulta**: o conhecimento é indexado uma vez e fica disponível para qualquer pergunta futura, sem recalcular a partir do zero.

## Conteúdo atual

→ **[Índice completo](wiki/index.md)**

| Tipo | Itens |
|------|-------|
| Repositórios (13) | [affaan-m/ECC](wiki/repos/github.com/affaan-m/ecc.md) · [bytedance/deer-flow](wiki/repos/github.com/bytedance/deer-flow.md) · [calesthio/OpenMontage](wiki/repos/github.com/calesthio/openmontage.md) · [croffasia/itsaplan](wiki/repos/github.com/croffasia/itsaplan.md) · [DeusData/codebase-memory-mcp](wiki/repos/github.com/deusdata/codebase-memory-mcp.md) · [garrytan/gstack](wiki/repos/github.com/garrytan/gstack.md) · [Graphify-Labs/graphify](wiki/repos/github.com/graphify-labs/graphify.md) · [HarnessMD/munder-difflin](wiki/repos/github.com/harnessmd/munder-difflin.md) · [littledivy/mimic](wiki/repos/github.com/littledivy/mimic.md) · [morluto/rea](wiki/repos/github.com/morluto/rea.md) · [msitarzewski/agency-agents](wiki/repos/github.com/msitarzewski/agency-agents.md) · [multica-ai/andrej-karpathy-skills](wiki/repos/github.com/multica-ai/andrej-karpathy-skills.md) · [SynkraAI/aiox-core](wiki/repos/github.com/synkraai/aiox-core.md) |
| Skills (4) | [Diagram Design](wiki/skills/github.com/cathrynlavery/diagram-design/diagram-design.md) · [Frontend Slides](wiki/skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) · [Understand](wiki/skills/github.com/egonex-ai/understand-anything/understand.md) · [UX Audit Rethink](wiki/skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) |
| Conceitos (12) | [Agent harness](wiki/concepts/agent-harness.md) · [Agent skills](wiki/concepts/agent-skills.md) · [Artefatos HTML autocontidos](wiki/concepts/artefatos-html-autocontidos.md) · [Auditoria de UX](wiki/concepts/auditoria-de-ux.md) · [CLAUDE.md](wiki/concepts/claude-md.md) · [Engenharia reversa agêntica](wiki/concepts/engenharia-reversa-agentica.md) · [Evidência e proveniência](wiki/concepts/evidencia-e-proveniencia.md) · [Grafo de conhecimento de código](wiki/concepts/grafo-de-conhecimento-de-codigo.md) · [Memória de agente](wiki/concepts/memoria-de-agente.md) · [MCP](wiki/concepts/model-context-protocol.md) · [Orquestração multiagente](wiki/concepts/orquestracao-multiagente.md) · [Produção de vídeo agêntica](wiki/concepts/producao-de-video-agentica.md) |
| Entidades (17) | [affaan-m](wiki/entities/affaan-m.md) · [ByteDance](wiki/entities/bytedance.md) · [calesthio](wiki/entities/calesthio.md) · [cathrynlavery](wiki/entities/cathrynlavery.md) · [croffasia](wiki/entities/croffasia.md) · [DeusData](wiki/entities/deusdata.md) · [Egonex-AI](wiki/entities/egonex-ai.md) · [garrytan](wiki/entities/garrytan.md) · [Graphify Labs](wiki/entities/graphify-labs.md) · [HarnessMD](wiki/entities/harnessmd.md) · [littledivy](wiki/entities/littledivy.md) · [mastepanoski](wiki/entities/mastepanoski.md) · [morluto](wiki/entities/morluto.md) · [msitarzewski](wiki/entities/msitarzewski.md) · [multica-ai](wiki/entities/multica-ai.md) · [SynkraAI](wiki/entities/synkraai.md) · [zarazhangrui](wiki/entities/zarazhangrui.md) |
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
