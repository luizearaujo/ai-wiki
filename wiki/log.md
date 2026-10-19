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

## [2026-10-19] ingest | affaan-m/ECC
- Criada `repos/github.com/affaan-m/ecc.md` a partir do README no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34`, sem clonar o repositório.
- Criada `entities/affaan-m.md`.
- Criado `concepts/agent-harness.md` (compartilhado com as demais ingestões do lote) e atualizado `concepts/agent-skills.md`.
- Atualizados `index.md`, `log.md` e `overview.md`.
- Não lidos: `docs/`, código, guias `the-*-guide.md`, agentes e skills individuais, `CHANGELOG.md`. Qualidade real do catálogo, paridade entre harnesses e fronteira OSS/ECC Pro são a verificar.
- O owner no GitHub é `affaan-m/ECC`; o caminho da wiki usa minúsculas conforme o schema.

## [2026-10-19] ingest | garrytan/gstack
- Criada `repos/github.com/garrytan/gstack.md` a partir do README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037`, sem clonar o repositório.
- Criada `entities/garrytan.md`.
- Criado `concepts/orquestracao-multiagente.md` (compartilhado com as demais ingestões do lote) e atualizados `concepts/claude-md.md` e `concepts/model-context-protocol.md`.
- Atualizados `index.md`, `log.md` e `overview.md`.
- Não lidos: código, `docs/`, `ARCHITECTURE.md`, `ETHOS.md`, `USING_GBRAIN_WITH_GSTACK.md`. Versão corrente única, cobertura de testes por host e custo de tokens de um sprint são a verificar.
- O README cita versões v1.91.13.0 e iOS QA v1.43.0.0+ sem um cabeçalho único de release.

## [2026-10-19] ingest | HarnessMD/munder-difflin
- Criada `repos/github.com/harnessmd/munder-difflin.md` a partir do README no commit `436d65a74a69d347c57641fbace4eb822bf98600`, sem clonar o repositório.
- Criada `entities/harnessmd.md`.
- Atualizados `concepts/agent-harness.md`, `concepts/orquestracao-multiagente.md`, `index.md`, `log.md` e `overview.md`.
- Não lidos: `HIVE.md`, `SPEC.md`, `DESIGN.md`, `docs/ARCHITECTURE.md`, `TELEMETRY.md`, `CONTRIBUTING.md`, código-fonte e assets. Aplicação de gates humanos, desempenho da memória e fronteira grátis/Pro são a verificar.
- README ainda referencia o owner antigo `chaitanyagiri/munder-difflin` em links, clone e mídias; o repositório canônico observado é `HarnessMD/munder-difflin`. Licença do código é MIT, mas os assets de pixel art têm licença separada da LimeZu.

## [2026-10-19] lint | lote ECC, gstack e Munder Difflin
- Verificados todos os links relativos da wiki; corrigidos links quebrados em `repos/github.com/msitarzewski/agency-agents.md` (`../../` → `../../../`).
- Verificado frontmatter obrigatório das páginas de repositório, entidade e conceito; todas as novas páginas têm `## Fontes`.
- Índice reordenado alfabeticamente por seção e atualizado com as 8 páginas novas e as 3 entidades.
- `overview.md` atualizado com temas, mapa por área, observações, lacunas e fontes do lote.

## [2026-10-19] ingest | calesthio/OpenMontage
- Criada `repos/github.com/calesthio/openmontage.md` a partir do README no commit `c8066452325cb57c8fc1ba8c2a71b6e8842e6b65`, sem clonar o repositório.
- Criadas `entities/calesthio.md` e `concepts/producao-de-video-agentica.md`.
- Atualizados `concepts/agent-harness.md`, `concepts/agent-skills.md`, `concepts/orquestracao-multiagente.md`, `index.md`, `log.md` e `overview.md`.
- Não lidos: código, `docs/`, `AGENT_GUIDE.md`, `PROJECT_CONTEXT.md`, manifestos de pipeline e skills. Gates humanos, qualidade dos provedores e custo real de produção são a verificar.
- Divergência: README declara "10+ pipelines"; a descrição da API do GitHub informa 12.

## [2026-10-19] ingest | bytedance/deer-flow
- Criada `repos/github.com/bytedance/deer-flow.md` a partir do README no commit `fee0cd0c180874325305e995197db99f03fa6a6f`, sem clonar o repositório.
- Criada `entities/bytedance.md`.
- Atualizados `concepts/agent-harness.md`, `concepts/agent-skills.md`, `concepts/orquestracao-multiagente.md`, `concepts/model-context-protocol.md`, `index.md`, `log.md` e `overview.md`.
- Não lidos: `docs/`, código, configurações e exemplos. Desempenho do DeerMem, isolamento real do sandbox e comportamento dos subagentes são a verificar.
- O README descreve a versão 2.0 como reescrita sem código compartilhado com a 1.x; a branch `main-1.x` preserva o framework anterior. Alerta que admin do Gateway equivale a execução de código.

## [2026-10-19] ingest | Graphify-Labs/graphify
- Criada `repos/github.com/graphify-labs/graphify.md` a partir do README no commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8`, sem clonar o repositório.
- Criada `entities/graphify-labs.md`.
- Atualizados `concepts/grafo-de-conhecimento-de-codigo.md`, `concepts/agent-skills.md`, `concepts/model-context-protocol.md`, `index.md`, `log.md` e `overview.md`.
- Não lidos: código, `docs/`, benchmarks, conectores e implementação do passo semântico. Acurácia das arestas `INFERRED`, custo de indexação e fronteira CLI/Graphify Cloud são a verificar.
- O caminho da wiki usa `graphify-labs` em minúsculas; a URL e o nome canônicos preservam `Graphify-Labs`.

## [2026-10-19] ingest | skills.sh/egonex-ai/understand-anything/understand
- Criada `skills/github.com/egonex-ai/understand-anything/understand.md` a partir da página do skills.sh, consultada em 2026-10-19.
- Criada `entities/egonex-ai.md`.
- Atualizados `concepts/grafo-de-conhecimento-de-codigo.md`, `concepts/agent-skills.md`, `index.md`, `log.md` e `overview.md`.
- O repositório-fonte não foi clonado e o `SKILL.md` cru não foi lido; a página, a árvore via API e os metadados do GitHub foram as fontes. Caminho da skill no repositório: `understand-anything-plugin/skills/understand`.
- Métricas publicadas em 2026-10-19: ~5,0 mil instalações e ~86,9 mil stars no repositório. O README descreve outras skills do plugin que não foram documentadas individualmente.

## [2026-10-19] ingest | skills.sh/zarazhangrui/frontend-slides/frontend-slides
- Criada `skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md` a partir da página do skills.sh, consultada em 2026-10-19.
- Criada `entities/zarazhangrui.md`.
- Criados/atualizados `concepts/artefatos-html-autocontidos.md`, `concepts/agent-skills.md`, `index.md`, `log.md` e `overview.md`.
- O repositório-fonte não foi clonado e o `SKILL.md` cru não foi lido; `source_path` é `SKILL.md` na raiz. O caminho da wiki usa `zarazhangrui` em minúsculas.
- Métricas publicadas em 2026-10-19: ~1,1 mil instalações e ~30,9 mil stars; auditoria Snyk indicada como "Warn". A qualidade do deck gerado e a conversão de PPTX são a verificar.

## [2026-10-19] ingest | skills.sh/cathrynlavery/diagram-design/diagram-design
- Criada `skills/github.com/cathrynlavery/diagram-design/diagram-design.md` a partir da página do skills.sh, consultada em 2026-10-19.
- Criada `entities/cathrynlavery.md`.
- Atualizados `concepts/artefatos-html-autocontidos.md`, `concepts/agent-skills.md`, `index.md`, `log.md` e `overview.md`.
- O repositório-fonte não foi clonado e o `SKILL.md` cru não foi lido; `source_path` é `skills/diagram-design`. Site e scripts de exportação não foram verificados.
- Métricas publicadas em 2026-10-19: ~15,5 mil instalações e ~57,4 mil stars. Divergência: a página do skills.sh declara 45 tipos visuais; a descrição da API do GitHub informa 44.

## [2026-10-19] lint | lote OpenMontage, DeerFlow, Graphify e skills
- Verificados todos os links relativos da wiki; nenhum link quebrado encontrado.
- Verificado frontmatter obrigatório e seção `## Fontes` em todas as páginas novas e atualizadas.
- `index.md` reordenado alfabeticamente por seção e atualizado com 3 repositórios, 3 skills, 3 conceitos e 6 entidades.
- `overview.md` atualizado com temas, mapa por área, observações, lacunas e fontes do lote.
- Conceitos compartilhados atualizados: `agent-harness`, `agent-skills`, `orquestracao-multiagente`, `model-context-protocol` e `grafo-de-conhecimento-de-codigo`.

## [2026-10-19] fix | catálogo por categoria
- Criado `categorias.md` com o agrupamento temático de repositórios, skills, conceitos e entidades.
- `CLAUDE.md`: adicionado o tipo `category`, a regra de categorização obrigatória e a atualização de `categorias.md` nos workflows de ingestão, consulta e lint.
- Atualizados `index.md`, `README.md` e `log.md`.

## [2026-10-19] ingest | mukul975/Anthropic-Cybersecurity-Skills
- Criada `repos/github.com/mukul975/anthropic-cybersecurity-skills.md` a partir do README no commit `54a798831d2266a3ca61ce68a7acb80b81160d57`, sem clonar o repositório.
- Criados `concepts/ciberseguranca-com-agentes.md` e `entities/mukul975.md`.
- Atualizados `concepts/agent-skills.md`, `categorias.md`, `index.md`, `log.md` e `overview.md`.
- Não lidos: código, docs internas, scripts e as 818 skills. Qualidade das skills, atualidade dos mapeamentos de framework e a divergência 817/818 são a verificar.
- O projeto se declara da comunidade, sem vínculo com a Anthropic, apesar do nome.

## [2026-10-19] ingest | skills.sh/blader/humanizer/humanizer
- Criada `skills/github.com/blader/humanizer/humanizer.md` a partir da página do skills.sh, consultada em 2026-10-19.
- Criados `concepts/humanizacao-de-texto-por-ia.md` e `entities/blader.md`.
- Atualizados `concepts/agent-skills.md`, `categorias.md` (nova categoria "Escrita e comunicação"), `index.md`, `log.md` e `overview.md`.
- O repositório-fonte não foi clonado e o `SKILL.md` cru não foi lido; `source_path` é `SKILL.md` na raiz. A página publica o fluxo, o catálogo de 26 padrões e os modos de saída.
- Métricas publicadas em 2026-10-19: 9,8 mil instalações e 58,1 mil estrelas; auditorias Gen Agent Trust Hub, Socket e Snyk com "Pass". Licença MIT.

## [2026-10-19] ingest | skills.sh/hardikpandya/stop-slop/stop-slop
- Criada `skills/github.com/hardikpandya/stop-slop/stop-slop.md` a partir da página do skills.sh, consultada em 2026-10-19.
- Criado `entities/hardikpandya.md`.
- Atualizados `concepts/humanizacao-de-texto-por-ia.md`, `concepts/agent-skills.md`, `categorias.md`, `index.md`, `log.md` e `overview.md`.
- O repositório-fonte não foi clonado e o `SKILL.md` cru e as referências (`phrases.md`, `structures.md`, `examples.md`) não foram lidos; `source_path` é `SKILL.md` na raiz.
- Métricas publicadas em 2026-10-19: 17,5 mil instalações e 18,1 mil estrelas; auditorias Gen Agent Trust Hub, Socket e Snyk com "Pass". Licença MIT; API do GitHub não informa linguagem principal.

## [2026-10-19] ingest | TauricResearch/TradingAgents
- Criada `repos/github.com/tauricresearch/tradingagents.md` a partir do README no commit `e8f5503e9b86d5c2710b0c76b1f686703968c9df`, sem clonar o repositório.
- Criados `concepts/analise-financeira-multiagente.md` e `entities/tauricresearch.md`.
- Atualizados `concepts/orquestracao-multiagente.md`, `concepts/memoria-de-agente.md`, `categorias.md` (nova categoria "Análise financeira e trading"), `index.md`, `log.md` e `overview.md`.
- Não lidos: código, docs internas, paper, arquivos de configuração e resultados de backtest. Qualidade preditiva, desempenho real e integridade temporal do código são a verificar.
- Métricas da API do GitHub observadas em 2026-10-19: ~112 mil estrelas, ~21,6 mil forks, criado em 2024-12-28 e último push em 2026-10-16; licença Apache-2.0, Python.

## [2026-10-19] ingest | skills.sh/google-labs-code/design.md — 4 skills
- Criadas `skills/github.com/google-labs-code/design.md/typed-service-contracts.md`, `tdd-red-green-refactor.md`, `ink.md` e `agent-dx-cli-scale.md` a partir das páginas do skills.sh, consultadas em 2026-10-19.
- Criada `entities/google-labs-code.md`.
- Criados `concepts/cli-agent-first.md`, `concepts/contratos-tipados-de-servico.md` e `concepts/tdd-para-agentes.md`.
- Atualizados `categorias.md` (nova categoria "Engenharia e interfaces agent-first"), `index.md`, `log.md`, `overview.md` e `README.md`.
- O repositório-fonte não foi clonado e os `SKILL.md` crus não foram lidos; o conteúdo veio do `SKILL.md` renderizado nas páginas do skills.sh. Caminhos observados via árvore da API: `.agents/skills/typed-service-contracts/`, `.agents/skills/tdd/`, `.agents/skills/ink/` e `.agents/skills/agent-dx-cli-scale/`.
- Métricas publicadas em 2026-10-19: 669, 647, 169 e 166 instalações; primeira aparição em 2026-04-22; auditorias Gen Agent Trust Hub, Socket e Snyk com "Pass". Repositório no commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`, Apache-2.0, TypeScript, ~28,4 mil estrelas.
- O README do repositório descreve o formato DESIGN.md e sua CLI, mas não menciona as quatro skills.

## [2026-10-19] lint | lote google-labs-code/design.md
- Verificados 745 links relativos na wiki e no `README.md`; nenhum quebrado e nenhum âncora inválida.
- Verificados frontmatter obrigatório e seção `## Fontes` nas 8 páginas novas; todas conformes, sem `TODO`, sem cabeçalho acima de `###` e com cercas de código balanceadas.
- `index.md` com 65 páginas de conteúdo, sem faltantes, extras ou duplicatas; seções em ordem alfabética.
- `categorias.md` cobre todas as 65 páginas; as quatro skills aparecem na nova categoria e no índice cruzado da categoria de skills.
- `README.md` atualizado para 15 repositórios, 10 skills, 18 conceitos e 22 entidades, com entradas em ordem alfabética.
- `overview.md` atualizado com o novo tema, linha no mapa, quatro observações, cinco lacunas e fontes.

## [2026-10-19] fix | cabeçalho duplicado em overview.md
- Removido o `## Lacunas e próximos passos` repetido introduzido no lote de `google-labs-code/design.md`; o arquivo voltou a ter um único cabeçalho.
- Verificados todos os arquivos Markdown da wiki: nenhum cabeçalho duplicado e nenhuma âncora quebrada.

## [2026-10-19] ingest | skills.sh/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max
- Criada `skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md` a partir da página do skills.sh, consultada em 2026-10-19.
- Criada `entities/nextlevelbuilder.md`.
- Criados `concepts/design-taste-para-agentes.md` e `concepts/design-system-com-agentes.md`.
- O repositório-fonte não foi clonado; o conteúdo veio do `SKILL.md` renderizado. `source_path` observado na árvore: `.claude/skills/ui-ux-pro-max/SKILL.md`.
- Métricas publicadas em 2026-10-19: 403.620 instalações, primeira aparição em 19 de janeiro de 2026; auditorias Gen Agent Trust Hub, Socket e Snyk com "Pass". Repositório no commit `56ea9cf174ed86786187daa9de0e6247cb0747e4`, MIT, Python, 137.481 estrelas e 14.603 forks.

## [2026-10-19] ingest | skills.sh/pbakaus/impeccable/impeccable
- Criada `skills/github.com/pbakaus/impeccable/impeccable.md` a partir da página do skills.sh, consultada em 2026-10-19.
- Criada `entities/pbakaus.md`.
- O repositório-fonte não foi clonado; o conteúdo veio do `SKILL.md` renderizado. `source_path` observado na árvore: `.agents/skills/impeccable/SKILL.md`.
- Métricas publicadas em 2026-10-19: 343.949 instalações, primeira aparição em 8 de abril de 2026; Gen Agent Trust Hub "Pass", Socket "Warn", Snyk "Pass". Repositório no commit `0665bd812ae0908fcab17b96fd4f840defb882d9`, Apache-2.0, Rust, 82.979 estrelas e 5.018 forks.

## [2026-10-19] ingest | skills.sh/leonxlnx/taste-skill — 16 skills
- Criadas em `skills/github.com/leonxlnx/taste-skill/`: `design-taste-frontend.md`, `design-taste-frontend-v1.md`, `design-taste-frontend-v2-experimental.md`, `taste-skill.md`, `high-end-visual-design.md`, `redesign-existing-projects.md`, `minimalist-ui.md`, `industrial-brutalist-ui.md`, `gpt-taste.md`, `full-output-enforcement.md`, `stitch-design-taste.md`, `brandkit.md`, `image-taste-frontend.md`, `image-to-code.md`, `imagegen-frontend-web.md` e `imagegen-frontend-mobile.md`, a partir das páginas do skills.sh consultadas em 2026-10-19.
- Criada `entities/leonxlnx.md`.
- Criados `concepts/image-to-code.md` e `concepts/saida-completa-de-agente.md`.
- Atualizados `concepts/design-taste-para-agentes.md`, `concepts/design-system-com-agentes.md`, `categorias.md` (nova categoria "Design de interface e direção de arte"), `index.md`, `log.md`, `overview.md` e `README.md`.
- O repositório-fonte não foi clonado e os `SKILL.md` crus não foram lidos. Caminhos observados na árvore do commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`; `full-output-enforcement` e `image-taste-frontend` não têm arquivo localizável na árvore atual e estão marcados como **A verificar**.
- O catálogo tem 16 entradas, mas `taste-skill` é um alias da v1 (1 instalação, aponta para `--skill design-taste-frontend-v1`); `image-to-code` e `imagegen-frontend-mobile` foram movidas para `Leonxlnx/imagegen-skills` e não publicam corpo renderizado. `image-to-code` tem Socket "Warn".
- Métricas de adoção observadas em 2026-10-19 variam de 1 a 636.323 instalações; `design-taste-frontend` é a mais instalada (636,7 mil). Repositório MIT, JavaScript, 99.159 estrelas e 6.743 forks.

## [2026-10-19] lint | lote design de interface (18 skills)
- Verificados links relativos, âncoras, frontmatter obrigatório, seção `## Fontes`, ordenação alfabética do índice e cobertura de categorias nas páginas novas.
- `index.md` e `README.md` atualizados para 28 skills, 22 conceitos e 25 entidades, com entradas em ordem alfabética.
- `categorias.md` ganhou a categoria "Design de interface e direção de arte"; `Full-Output Enforcement` e `Saída completa de agente` ficaram em "Engenharia e interfaces agent-first".
- `overview.md` atualizado com novo tema, linha no mapa, sete observações, cinco lacunas e fontes.

## [2026-10-19] fix | README no bookkeeping
- `README.md` passa a ser atualizado em toda inclusão, alteração ou remoção de página: as contagens e listas da seção "Conteúdo atual" espelham `index.md`.
- Adicionada a linha `Análises (0)` ao README.
- `CLAUDE.md` atualizado: árvore de estrutura, camadas, regra inegociável 3, passos de bookkeeping/verificação das ingestões de repositório e skill, arquivamento de consulta, checklist de lint e nova seção "Formato do README".

## [2026-10-19] ingest | The-Swarm-Corporation/AutoHedge
- Criada `repos/github.com/the-swarm-corporation/autohedge.md` a partir do README no commit `c549c7950da112286e76725d49f6a25de8fa99bd`, sem clonar o repositório.
- Criada `entities/the-swarm-corporation.md`.
- Atualizados `concepts/analise-financeira-multiagente.md`, `categorias.md`, `index.md`, `log.md` e `README.md`.
- Não lidos: código, configuração, estratégias, testes e documentação interna. Controles de risco, backtest, paper trading e custódia da chave privada são a verificar.
- Métricas da API do GitHub observadas em 2026-10-19: ~6,4 mil estrelas, ~925 forks, criado em 2024-12-10 e último push em 2026-05-11; licença MIT, Python.
