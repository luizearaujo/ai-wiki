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

## [2026-10-19] ingest | HKUDS/Vibe-Trading
- Criada `repos/github.com/hkuds/vibe-trading.md` a partir do README no commit `097b29feab9793e3c302e1a7a4f3c0dac6344904`, sem clonar o repositório.
- Criada `entities/hkuds.md`.
- Atualizados `concepts/analise-financeira-multiagente.md`, `categorias.md`, `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: código, testes, engines de backtest, conectores de corretora, guards de execução e documentação interna. Somente o README foi consultado; a implementação do mandato, da separação paper/live e do modo TAP é a verificar.
- Métricas da API do GitHub observadas em 2026-10-19: ~35,9 mil estrelas, ~5,8 mil forks, criado em 2026-04-01 e último push em 2026-10-19; release v0.1.16 em 2026-09-29; licença MIT, Python.

## [2026-10-19] ingest | Fincept-Corporation/FinceptTerminal
- Criada `repos/github.com/fincept-corporation/finceptterminal.md` a partir do README no commit `3d8617cae3f13c93874d4bee4fb0f2846e9c83bc`, sem clonar o repositório.
- Criada `entities/fincept-corporation.md`.
- Atualizados `concepts/analise-financeira-multiagente.md`, `categorias.md`, `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: código C++/Python, `docs/`, manifestos, testes e a implementação dos agentes, conectores e paper trading. Somente o README foi consultado; a separação paper/live, os limites de execução e o isolamento do Python embutido são a verificar.
- Divergência registrada: o README declara AGPL-3.0-or-later, mas a API do GitHub retorna `NOASSERTION`. O README também publica preços conflitantes para o Quantcept (US$ 3/US$ 8 e US$ 14/US$ 24 por 30 dias).
- Métricas da API do GitHub observadas em 2026-10-19: ~32,7 mil estrelas, ~4,7 mil forks, 9 issues abertas, criado em 2024-08-29 e último push em 2026-10-13; licença reportada `NOASSERTION`, linguagem C++.

## [2026-10-19] ingest | cloudflare/agentic-inbox
- Criada `repos/github.com/cloudflare/agentic-inbox.md` a partir do README no commit `48039bb6785af34e592c2966f87cde2b255c4c80`, sem clonar o repositório.
- Criadas `entities/cloudflare.md` e `concepts/email-para-agentes.md`.
- Atualizados `categorias.md` (nova categoria "Comunicação e caixas de entrada agênticas"), `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: código, `wrangler.jsonc`, testes, frontend e implementação das nove ferramentas. Somente o README foi consultado; a imposição de confirmação de envio e o comportamento do MCP são a verificar.
- O README declara que não há autorização por mailbox: a política do Cloudflare Access é a única fronteira de confiança, e o MCP em `/mcp` aceita `mailboxId` arbitrário.
- Métricas da API do GitHub observadas em 2026-10-19: ~8,4 mil estrelas, ~1,1 mil forks, 55 issues abertas, criado em 2026-04-10 e último push em 2026-04-23; licença Apache-2.0, TypeScript.

## [2026-10-19] ingest | heygen-com/hyperframes
- Criada `repos/github.com/heygen-com/hyperframes.md` a partir do README no commit `aa63a8c70d8549d55533efdc7ed6d6559331b38c`, sem clonar o repositório.
- Criada `entities/heygen.md`.
- Atualizados `concepts/producao-de-video-agentica.md`, `categorias.md`, `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: código, pacotes publicados, as 21 skills, catálogo de blocos, `DESIGN.md`/`frame.md`, testes e `ADOPTERS.md`. Somente o README foi consultado; determinismo entre ambientes, a fronteira entre o framework aberto e os serviços hospedados e a segurança do renderer com HTML de terceiros são a verificar.
- Métricas da API do GitHub observadas em 2026-10-19: ~67,3 mil estrelas, ~6,1 mil forks, 379 issues abertas, criado em 2026-03-10 e último push em 2026-10-19; licença Apache-2.0, TypeScript.

## [2026-10-19] ingest | AgriciDaniel/claude-ads
- Criada `repos/github.com/agricidaniel/claude-ads.md` a partir do README no commit `fc3908e786c318776df89a3a098333da377364be`, sem clonar o repositório.
- Criadas `entities/agricidaniel.md` e `concepts/auditoria-de-midia-paga.md`.
- Atualizados `categorias.md` (nova categoria "Marketing, mídia paga e conteúdo"), `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: código Python, `ads/`, `skills/`, `agents/`, `control-plane/`, `claude_ads_core/`, testes, evals e Cockpit. Somente o README foi consultado; a imposição dos gates de escrita, a cobertura real de evidência e o estado de release são a verificar.
- O README declara status "development candidate", com os 12 perfis de saúde desativados e a escrita limitada a rascunhos até o gate de mutação passar.
- Distribuição dupla: release público MIT e espelho comunitário para membros do AI Marketing Hub Pro. Releases têm checksum e SBOM, mas não assinatura.
- Métricas da API do GitHub observadas em 2026-10-19: ~10,1 mil estrelas, ~1,5 mil forks, 3 issues abertas, criado em 2026-02-11 e último push em 2026-10-17; licença MIT, Python.

## [2026-10-19] ingest | jo-inc/camofox-browser
- Criada `repos/github.com/jo-inc/camofox-browser.md` a partir do README no commit `39c82094013480b373df6600d44c7f036f58356e`, sem clonar o repositório.
- Criadas `entities/jo-inc.md` e `concepts/navegacao-web-agentica.md`.
- Atualizados `categorias.md` (repositório em "Engenharia e interfaces agent-first"), `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: código, testes, plugins (OpenClaw, Claude Code), worker de telemetria, scripts de build e documentação interna. Somente o README foi consultado; o isolamento de sessão, a cifragem de cookies, a coleta de telemetria e a durabilidade da anti-detecção são a verificar.
- Ferramenta de finalidade controversa (anti-detecção e anti-scraping): a página documenta o mecanismo e registra explicitamente que a wiki não avalia termos de serviço, direitos autorais ou legislação aplicáveis ao uso.
- Métricas da API do GitHub observadas em 2026-10-19: ~11,7 mil estrelas, ~1,2 mil forks, 240 issues abertas, criado em 2026-01-26 e último push em 2026-10-16; licença MIT, JavaScript, branch padrão `master`.

## [2026-10-19] lint | lote de sete ingestões (AutoHedge, Vibe-Trading, FinceptTerminal, agentic-inbox, HyperFrames, Claude Ads, Camofox Browser)
- Verificados frontmatter, seção `## Fontes`, links relativos e âncoras, cobertura no índice e em `categorias.md`, contagens e listas do `README.md`, ordenação alfabética e páginas órfãs em 109 páginas de conteúdo.
- Corrigidos links relativos quebrados em `repos/github.com/agricidaniel/claude-ads.md` e `repos/github.com/jo-inc/camofox-browser.md`: referências a `entities/` e `concepts/` passaram de `../../` para `../../../`, e repositórios irmãos passaram a usar `../owner/repo.md` em vez de `../github.com/owner/repo.md`.
- Resultado: contagens do README batem com o índice (22 repositórios, 28 skills, 25 conceitos, 32 entidades, 0 análises); todas as listas estão em ordem alfabética; nenhum link quebrado ou âncora ausente; nenhuma página órfã; nenhum frontmatter incompleto; `overview.md` e `categorias.md` ficam fora do índice por serem páginas de navegação, como previsto no schema.
- Contradições mantidas e sinalizadas (não apagadas): licença do FinceptTerminal (README `AGPL-3.0-or-later`, API `NOASSERTION`); preços conflitantes do Quantcept no mesmo README; contagens divergentes de skills do Anthropic Cybersecurity Skills (817 vs. 818) e de pipelines do OpenMontage (10+ vs. 12); status "development candidate" do Claude Ads, que ainda assim está publicado.
- Normalizados dois `status` fora do enum do schema (`active (movida)` → `active`) em `skills/github.com/leonxlnx/taste-skill/image-to-code.md` e `imagegen-frontend-mobile.md`; o aviso de mudança de repositório continua no corpo e nas tags.
- Nenhuma nova lacuna conceitual identificada além das já registradas em `overview.md`.

## [2026-10-19] ingest | JustVugg/colibri
- Criada `repos/github.com/justvugg/colibri.md` a partir do README no commit `e0db083cdc9e563e0766cc6fc661ef23c32298e0`, sem clonar o repositório.
- Criadas `entities/vincenzo-fornaro.md` e `concepts/streaming-de-experts-em-moe.md`.
- Atualizados `categorias.md` (nova categoria "Inferência local e runtime de modelos"; repositório também listado em "Protocolos, integrações e confiabilidade" pelo `coli mcp`), `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: `docs/`, código C/Python, testes, releases, checkpoints e dashboard. Somente o README foi consultado; benchmarks, a generalização do cache aprendido, o isolamento do servidor e o modo System One são a verificar.
- O README declara o invariante "posicionamento só decide velocidade" e explicita que ainda não mediu uma GPU discreta no caminho Vulkan; os números vêm em parte da comunidade.
- Licença do código Apache-2.0; cada checkpoint mantém a licença do autor (GLM-5.2 MIT, Qwen-Image-2.1 apenas não comercial).
- Métricas da API do GitHub observadas em 2026-10-19: ~42,8 mil estrelas, ~4,8 mil forks, 151 issues abertas, criado em 2026-07-01 e último push em 2026-10-19; licença Apache-2.0, linguagem C, branch padrão `main`.

## [2026-10-19] ingest | OpenBMB/MiniCPM
- Criada `repos/github.com/openbmb/minicpm.md` a partir do README no commit `316cfb1cea39f39cfa16b4f5703b77495c2340be`, sem clonar o repositório.
- Criadas `entities/openbmb.md`, `concepts/llms-compactos-on-device.md` e `concepts/atencao-esparsa-para-contexto-longo.md`.
- Atualizados `categorias.md` (repositório, conceitos e entidade em "Inferência local e runtime de modelos"; repositório também em "Skills, instruções e personalidades de agente" pelos cookbooks como Agent Skills), `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: `docs/`, `skills/`, código de treino, notebooks, testes, pesos, datasets UltraData e cookbooks. Somente o README foi consultado; a receita de RL + OPD, o parser de tool calls, os benchmarks e as licenças dos datasets são a verificar.
- Alegações de SOTA são relativas ao conjunto de comparação escolhido pelo projeto (MiniCPM5-2B: média 53,9; maior baseline 51,1); registradas como afirmações datadas, não como ranking independente.
- Licença Apache-2.0 para o repositório e os modelos, segundo o README e a API; a UI do MiniCPM-Desk-Pet é fork de projeto AGPL-3.0, em repositório separado.
- Métricas da API do GitHub observadas em 2026-10-19: ~11,6 mil estrelas, 809 forks, 22 issues abertas, criado em 2024-01-29 e último push em 2026-09-21; licença Apache-2.0, linguagem Jupyter Notebook, branch padrão `main`.

## [2026-10-19] ingest | vastsa/PI-Desktop
- Criada `repos/github.com/vastsa/pi-desktop.md` a partir do README no commit `87a48b953e8bada43a7a63f8922846198b9efb61`, sem clonar o repositório.
- Criadas `entities/vastsa.md` e `concepts/plugins-de-agente.md`.
- Atualizados `concepts/agent-harness.md` e `concepts/orquestracao-multiagente.md` com exemplos do PI-Desktop; `categorias.md` (repositório, conceito e entidade em "Harnesses e orquestração de agentes"), `index.md`, `log.md`, `overview.md` e `README.md`.
- Não lidos: `docs/` (incluindo arquitetura, especificação e guia de plugins), código Electron/TypeScript/Rust, testes, releases, templates e marketplace. Somente o README foi consultado; sandbox de plugins, isolamento de Worker Sessions, enforcement de permissões, curadoria do marketplace e importação de sessões são a verificar.
- A descrição da API do GitHub cita Electron + Rust host core + pi Agent Harness; o README confirma o host core em Rust e o runtime `pi`, mas não nomeia o Electron — registrado como observação datada, não como afirmação do README.
- Licença LGPL-3.0; produto declarado em Early Preview (linha 0.21.x), o que relativiza estabilidade de API de plugins e formato `.piplug`.
- Métricas da API do GitHub observadas em 2026-10-19: ~7,0 mil estrelas, 677 forks, 211 issues abertas, criado em 2023-03-22 e último push em 2026-10-19; licença LGPL-3.0, linguagem TypeScript, branch padrão `main`.

## [2026-10-19] ingest | karpathy/llm-wiki (gist)
- Criada `concepts/wiki-pessoal-com-llms.md` a partir do gist `karpathy/llm-wiki` na revisão `ac46de1ad27f92b28ac95459c782c07f6b8c964a`; conteúdo idêntico à cópia local `llm-wiki-md` (MD5 `7953122eebc7aca33db25cd86a89a19a`).
- Criada `entities/andrej-karpathy.md`.
- Atualizados `concepts/claude-md.md` (link de volta para o padrão), `categorias.md` (nova categoria "Conhecimento pessoal e curadoria"), `index.md`, `log.md`, `overview.md` e `README.md`; `CLAUDE.md` passou a registrar a URL do gist como fonte da ideia original.
- Não lidos: revisões anteriores do gist, comentários e eventuais arquivos além de `llm-wiki.md`. Somente o conteúdo publicado na revisão acima foi consultado.
- O endpoint de gists da API do GitHub retornou HTTP 502 durante a operação; datas de criação (2026-04-04) e última atualização (2026-10-16) foram extraídas da página HTML do gist. Metadados do autor vieram de `api.github.com/users/karpathy`.
- O gist é um documento de ideia, não um repositório de código; a página foi registrada como conceito, não como repositório.

## [2026-10-19] ingest | addyosmani/agent-skills
- Criada `repos/github.com/addyosmani/agent-skills.md`.
- Criada `entities/addyosmani.md`.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `aeac41d4d005999432bb7312f7ff06383a91d59d` foi lido.

## [2026-10-19] ingest | ComposioHQ/awesome-claude-skills
- Criada `repos/github.com/composiohq/awesome-claude-skills.md`.
- Criada `entities/composiohq.md`. Licença: README declara Apache-2.0; API não detectou arquivo de licença.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `be2a406907dbc61b73e6827ded415c96139d13a2` foi lido.

## [2026-10-19] ingest | dietrichgebert/ponytail
- Criada `repos/github.com/dietrichgebert/ponytail.md`.
- Criada `entities/dietrichgebert.md`.
- Criado `concepts/yagni-para-agentes.md` a partir deste README.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `09c434ab73ca43761c5d8b0c5d341926c2fba710` foi lido.

## [2026-10-19] ingest | Egonex-AI/Understand-Anything
- Criada `repos/github.com/egonex-ai/understand-anything.md`.
- A página da skill `understand` já existia e foi vinculada; a página de repositório cobre o produto como um todo.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `f2d0164f72fe678805c34245a6df36acededfebd` foi lido.

## [2026-10-19] ingest | JuliusBrussee/caveman
- Criada `repos/github.com/juliusbrussee/caveman.md`.
- Criada `entities/juliusbrussee.md`.
- Criado `concepts/economia-de-tokens-em-agentes.md` com números e ressalvas de medição do README.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `bad48a0e1df55e05e3f52249afa35ecc1909ee76` foi lido.

## [2026-10-19] ingest | Leonxlnx/taste-skill
- Criada `repos/github.com/leonxlnx/taste-skill.md`.
- As 13 páginas de skills do catálogo já existiam e foram vinculadas à nova página de repositório.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2` foi lido.

## [2026-10-19] ingest | mattpocock/skills
- Criada `repos/github.com/mattpocock/skills.md`.
- Criada `entities/mattpocock.md`.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `5beb35b040e3de97e54fa9e386d7e42d15c295c2` foi lido.

## [2026-10-19] ingest | nextlevelbuilder/ui-ux-pro-max-skill
- Criada `repos/github.com/nextlevelbuilder/ui-ux-pro-max-skill.md`.
- A página da skill `ui-ux-pro-max` já existia e foi vinculada à nova página de repositório.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `56ea9cf174ed86786187daa9de0e6247cb0747e4` foi lido.

## [2026-10-19] ingest | pbakaus/impeccable
- Criada `repos/github.com/pbakaus/impeccable.md`.
- A página da skill `impeccable` já existia e foi vinculada à nova página de repositório.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `0665bd812ae0908fcab17b96fd4f840defb882d9` foi lido.

## [2026-10-19] ingest | tt-a1i/archify
- Criada `repos/github.com/tt-a1i/archify.md`.
- Criada `entities/tt-a1i.md`.
- Atualizados `index.md`, `categorias.md`, `README.md` e `log.md`. Somente o `README.md` no commit `25cf37080fc8b1dbe758a4efc3935b55f3327083` foi lido.

## [2026-10-19] ingest | Instituto-IA-LNCC/manaca-1b-base
- Criada `repos/github.com/instituto-ia-lncc/manaca-1b-base.md` a partir do README no commit `408cba1fb765cdc496df2a518fe32f192270e5ee`, sem clonar o repositório.
- Criada `entities/instituto-ia-lncc.md` (organização do Instituto de IA do LNCC).
- Atualizados `index.md`, `categorias.md` (nova categoria "Modelos abertos e treinamento de LLMs"), `overview.md`, `README.md` e `log.md`.
- Não lidos: `paper/`, `docs/`, `corpus/`, `models/`, `scripts/`, `reports/`, `docker/`, os pesos no Hugging Face e o preprint arXiv 2608.30114. Somente o README foi consultado; arquitetura, corpus, dinâmica de treino, hardware e benchmarks são afirmações do projeto.
- Divergência de licença: README e badge declaram CC BY 4.0; a API do GitHub reporta `NOASSERTION` e o arquivo `LICENSE` não foi lido.
- O comando de clone do README aponta para `brunoleomenezes/manaca-1b-base`, não para a organização `Instituto-IA-LNCC` onde o repositório está; registrado como link de instalação defasado.
- Benchmarks (CALAME-PT, ARC-Ch-PT, HellaSwag-PT, LAMBADA-PT) são publicados pelo próprio projeto, com harness comum e testes pareados declarados; não reproduzidos por esta wiki.
- Métricas da API do GitHub observadas em 2026-10-19: 249 estrelas, 16 forks, 2 issues abertas, criado em 2026-08-31 e último push em 2026-09-23; linguagem Python, branch padrão `main`.

## [2026-10-19] query | triagem de 7 repositórios (lote do usuário)
- Usuário informou 7 URLs: `fosowl/agenticseek`, `collabsio/coolify`, `d4vinci/scrapling`, `openbb-finance/openbb`, `documenso/documenso`, `twentyhq/twenty`, `myshell-ai/openvoice`.
- Resumo apresentado ao usuário antes de qualquer alteração na wiki, conforme pedido explícito.
- `collabsio/coolify` não existe no GitHub; owner correto é `coollabsio/coolify`. `openbb-finance/openbb` redireciona (HTTP 301) para `openbq-org/OpenBB`.
- Decisão do usuário: não ingerir `coollabsio/coolify` (PaaS genérico, MCP apenas citado) nem `documenso/documenso` (sem nenhuma menção a IA/MCP) — fora do escopo da wiki. Confirmada ingestão dos outros 5.

## [2026-10-19] ingest | Fosowl/agenticSeek
- Criada `repos/github.com/fosowl/agenticseek.md` a partir do README no commit `b46bcca482218643236999221720586e7f410e04`, sem clonar o repositório.
- Criada `entities/fosowl.md`.
- Atualizado `concepts/agent-harness.md` e `concepts/navegacao-web-agentica.md` com o padrão de roteamento entre agentes e a navegação stealth do agenticSeek.
- Atualizados `index.md`, `categorias.md` (categoria "Harnesses e orquestração de agentes"), `overview.md` e `README.md`.
- Não lidos: código-fonte, `docs/CONTRIBUTING.md`, scripts de instalação. Taxa real de sucesso do roteamento de agente e do preenchimento de formulários são a verificar.
- `safe_mode` é descrito pelo próprio README como filtro de comandos "best-effort", não um sandbox; a contenção de rede depende da capability `NET_ADMIN`.

## [2026-10-19] ingest | D4Vinci/Scrapling
- Criada `repos/github.com/d4vinci/scrapling.md` a partir do README no commit `fd531313a499092d8471bf24a0e08dc5771f2b40`, sem clonar o repositório.
- Criada `entities/d4vinci.md`.
- Atualizados `concepts/model-context-protocol.md`, `concepts/agent-skills.md` e `concepts/navegacao-web-agentica.md` com o servidor MCP, a Agent Skill e o `StealthyFetcher` do Scrapling.
- Atualizados `index.md`, `categorias.md` (categoria "Protocolos, integrações e confiabilidade"), `overview.md` e `README.md`.
- Não lidos: código-fonte, documentação completa em readthedocs, implementação do servidor MCP e da Agent Skill. Taxa real de bypass de Cloudflare e redução de conteúdo enviado ao modelo são a verificar.
- README inclui aviso de isenção de responsabilidade sobre leis de scraping e termos de serviço; decisão de uso é do operador.

## [2026-10-19] ingest | openbq-org/OpenBB
- Criada `repos/github.com/openbq-org/openbb.md` a partir do README no commit `78020ee4b864ab50b8c1f56373877c2b4e7fb623`, sem clonar o repositório.
- Criada `entities/openbq-org.md`.
- Atualizado `concepts/model-context-protocol.md` com a menção a servidores MCP da Open Data Platform.
- Atualizados `index.md`, `categorias.md` (categorias "Análise financeira e trading" e "Protocolos, integrações e confiabilidade"), `overview.md` e `README.md`.
- Não lidos: código-fonte, `backends-for-openbb`, `agents-for-openbb` e a documentação em docs.openbb.co. Ferramentas exatas de um servidor MCP do ODP são a verificar.
- A URL historicamente usada, `openbb-finance/openbb`, redireciona (HTTP 301, confirmado via API do GitHub) para o repositório atual na organização `openbq-org`; a página documenta o destino do redirecionamento e registra a mudança como observação datada.

## [2026-10-19] ingest | twentyhq/twenty
- Criada `repos/github.com/twentyhq/twenty.md` a partir do README e do arquivo `LICENSE` no commit `31d95e98a2217e187d6f7d51f7ab69bb048e22bc`, sem clonar o repositório.
- Criada `entities/twentyhq.md`.
- Atualizado `concepts/agent-skills.md` com as skills oficiais `twenty-agent-skills`.
- Atualizados `index.md`, `categorias.md` (categoria "Trabalho, projetos e colaboração humano-agente"), `overview.md` e `README.md`.
- Não lidos: `SKILLS.md`, o pacote `twenty-agent-skills`, código-fonte e a documentação completa em docs.twenty.com.
- Licença mista por arquivo e por pacote (AGPLv3 + módulos Enterprise comerciais + pacotes MIT via `package.json`); a API do GitHub reporta `NOASSERTION` por não conseguir mapear o esquema a um único SPDX — registrado no frontmatter como `desconhecida`.

## [2026-10-19] ingest | myshell-ai/OpenVoice
- Criada `repos/github.com/myshell-ai/openvoice.md` a partir do README no commit `74a1d147b17a8c3092dd5430504bd83ef6c7eb23`, sem clonar o repositório.
- Criadas `entities/myshell-ai.md` e `concepts/clonagem-de-voz.md` (novo conceito: primeiro modelo de áudio/TTS desta wiki).
- Atualizados `index.md`, `categorias.md` (categoria "Geração de mídia e artefatos HTML", cujo escopo passou a citar voz), `overview.md` e `README.md`.
- Não lidos: `docs/USAGE.md`, `docs/QA.md`, código e pesos; o paper arXiv:2312.01479 citado pelo README não foi lido.
- Atividade recente baixa: último push observado em 2025-04-19, cerca de um ano e meio antes desta ingestão. README não discute salvaguardas contra uso indevido da clonagem de voz.

## [2026-10-19] lint | lote de 5 ingestões (agenticSeek, Scrapling, OpenBB, Twenty, OpenVoice)
- Verificados frontmatter, seção `## Fontes`, links relativos e âncoras, cobertura no índice e em `categorias.md`, ordenação alfabética e contagens do `README.md` nas 11 páginas novas/atualizadas deste lote (5 repositórios, 5 entidades, 1 conceito).
- Resultado: `index.md` e `README.md` com 41 repositórios, 28 skills, 33 conceitos, 48 entidades e 0 análises, contagens e listas coincidentes; nenhum link quebrado encontrado nas páginas novas.
- Commit único cobrindo as 5 ingestões (em vez de um commit por repositório), por terem sido processadas em lote a partir de um único pedido do usuário com triagem e confirmação prévias.

## [2026-10-19] query | triagem de 7 repositórios (lote 2 do usuário)
- Usuário informou 7 URLs: `mattpocock/skills`, `anthropics/skills`, `vercel-labs/agent-skills`, `github/awesome-copilot`, `remotion-dev/skills`, `claudflare/skills`, `firecrawl/cli`.
- `mattpocock/skills` já estava na wiki, idêntico (mesmo commit `5beb35b040e3de97e54fa9e386d7e42d15c295c2` e mesmas métricas) — não reingerido.
- `claudflare/skills` não existe no GitHub; owner correto é `cloudflare/skills`. Confirmado com o usuário antes de ingerir.
- Resumo apresentado ao usuário antes de qualquer alteração na wiki; confirmada a ingestão dos 5 repositórios restantes.

## [2026-10-19] ingest | anthropics/skills
- Criada `repos/github.com/anthropics/skills.md` a partir do README no commit `dbd4588f9e1033efb41dad4bef2f7947c8993d44`, sem clonar o repositório.
- Criada `entities/anthropics.md`.
- Atualizado `concepts/agent-skills.md` com a implementação de referência da Anthropic.
- Atualizados `index.md`, `categorias.md` (categoria "Skills, instruções e personalidades de agente"), `overview.md` e `README.md`.
- Não lidos: `./spec`, `./template` e as skills individuais (incluindo as de documento). Licença mista (Apache 2.0 + skills de documento source-available); API do GitHub reporta `NOASSERTION`, registrado como `desconhecida`.

## [2026-10-19] ingest | vercel-labs/agent-skills
- Criada `repos/github.com/vercel-labs/agent-skills.md` a partir do README no commit `063bee94c3f4df8453406c830b0a7df0f2860278`, sem clonar o repositório.
- Criada `entities/vercel-labs.md`.
- Atualizado `concepts/agent-skills.md` com a coleção oficial da Vercel.
- Atualizados `index.md`, `categorias.md` (categoria "Skills, instruções e personalidades de agente"), `overview.md` e `README.md`.
- Não lidos: os oito `SKILL.md` individuais, scripts e o índice de descoberta publicado em releases. MIT.

## [2026-10-19] ingest | github/awesome-copilot
- Criada `repos/github.com/github/awesome-copilot.md` a partir do README no commit `cb64ad12e32737ae764becd6885462e9b4c7cb00`, sem clonar o repositório.
- Criada `entities/github.md`.
- Atualizado `concepts/agent-skills.md` com o catálogo comunitário do GitHub Copilot.
- Atualizados `index.md`, `categorias.md` (categoria "Skills, instruções e personalidades de agente"), `overview.md` e `README.md`.
- Não lidos: `docs/README.agents.md`, `docs/README.instructions.md`, `docs/README.skills.md`, `docs/README.plugins.md`, `cookbook/README.md`, `AGENTS.md`, `SECURITY.md`. MIT. Catálogo comunitário: hospedado pela organização oficial do GitHub, mas conteúdo de terceiros, sem auditoria declarada.

## [2026-10-19] ingest | remotion-dev/skills
- Criada `repos/github.com/remotion-dev/skills.md` a partir do README no commit `039e8a2fc78b67efc228d5645367838b85818a1c`, sem clonar o repositório.
- Criada `entities/remotion-dev.md`.
- Atualizado `concepts/agent-skills.md` com as doze skills oficiais do Remotion.
- Adicionado link bidirecional em `repos/github.com/calesthio/openmontage.md` (o Remotion já era citado como provedor de renderização).
- Atualizados `index.md`, `categorias.md` (categorias "Skills, instruções e personalidades de agente" e "Geração de mídia e artefatos HTML"), `overview.md` e `README.md`.
- Não lidos: os doze `SKILL.md` individuais. Licença não detectada pela API do GitHub, registrada como `desconhecida`. README gerado automaticamente por `packages/skills/scripts/sync-readme.ts`.

## [2026-10-19] ingest | cloudflare/skills
- Criada `repos/github.com/cloudflare/skills.md` a partir do README no commit `86505e44f87d801aa1864a3c4109e9a8ae5c409f`, sem clonar o repositório.
- Entidade `entities/cloudflare.md` já existia (de `agentic-inbox`); atualizada com o novo repositório e o link para `Agent skills`.
- Atualizados `concepts/agent-skills.md` e `concepts/model-context-protocol.md` com as 18 skills e o servidor MCP principal da Cloudflare.
- Atualizados `index.md`, `categorias.md` (categorias "Skills, instruções e personalidades de agente" e "Protocolos, integrações e confiabilidade"), `overview.md` e `README.md`.
- Não lidos: os 18 `SKILL.md` individuais e a implementação do servidor MCP. Apache-2.0.
- URL informada pelo usuário (`claudflare/skills`) corrigida para `cloudflare/skills` após confirmação explícita.

## [2026-10-19] ingest | firecrawl/cli
- Criada `repos/github.com/firecrawl/cli.md` a partir do README no commit `84c82119a186bc50a27457f81e1d672ec8f28eaf`, sem clonar o repositório.
- Criada `entities/firecrawl.md`.
- Atualizados `concepts/model-context-protocol.md`, `concepts/agent-skills.md` e `concepts/navegacao-web-agentica.md` com o servidor MCP, as três famílias de skills e o comando `interact`.
- Atualizados `index.md`, `categorias.md` (categorias "Skills, instruções e personalidades de agente" e "Protocolos, integrações e confiabilidade"), `overview.md` e `README.md`.
- Não lidos: código-fonte, o catálogo `firecrawl/skills` e a documentação em docs.firecrawl.dev. Licença não detectada pela API do GitHub, registrada como `desconhecida`.
- `firecrawl setup defaults` desativa fetch/search nativo de agentes suportados, tornando o Firecrawl o provedor web padrão — mudança de comportamento global, não apenas instalação de ferramenta; registrado como observação em `overview.md`.
- Provedores de dados de terceiros (Alexandria) exigem aceite de termos por um admin da organização e têm custo de crédito próprio por chamada.

## [2026-10-19] lint | lote de 5 ingestões (anthropics, Vercel, GitHub, Remotion, Cloudflare, Firecrawl)
- Verificados frontmatter, seção `## Fontes`, links relativos e âncoras, cobertura no índice e em `categorias.md`, ordenação alfabética e contagens do `README.md` nas 11 páginas novas (6 repositórios, 5 entidades) e nas atualizações de `cloudflare.md` e `calesthio/openmontage.md`.
- Resultado: `index.md` e `README.md` com 47 repositórios, 28 skills, 33 conceitos, 53 entidades e 0 análises, contagens e listas coincidentes; nenhum link quebrado encontrado.
- Commit único cobrindo as 6 ingestões (em vez de um commit por repositório), por terem sido processadas em lote a partir de um único pedido do usuário com triagem e confirmação prévias; `mattpocock/skills` não gerou mudança (duplicata exata).

## [2026-10-19] ingest | SnailSploit/Claude-Red
- Criada `repos/github.com/snailsploit/claude-red.md` a partir do README no commit `a8de813edc9f66f60d44cfe42d47750e89d9930b`, sem clonar o repositório.
- Criada `entities/snailsploit.md` (Kai Aizen).
- Atualizado `concepts/ciberseguranca-com-agentes.md` com o recorte exclusivamente ofensivo de 78 skills.
- Adicionado link bidirecional em `repos/github.com/mukul975/anthropic-cybersecurity-skills.md`.
- Atualizados `index.md`, `categorias.md` (categorias "Skills, instruções e personalidades de agente" e "Cibersegurança e operações de segurança"), `overview.md` e `README.md`.
- Não lidos: as 78 skills, `install.sh`, `CHANGELOG.md`, `CONTRIBUTING.md` e a licença. MIT pela API e pelo badge do README.
- Biblioteca explicitamente ofensiva (red team, C2, evasão de EDR, phishing); registrada com foco em uso autorizado e sem controles de escopo embutidos.

## [2026-10-19] query | triagem de 9 itens (lote do usuário)
- Usuário informou 9 itens: `obra/superpowers`, `upstash/context7`, `excalidraw-diagram-skill`, `vercel-labs/agent-browser`, `thedotmack/claude-mem`, `nextlevelbuilder/ui-ux-pro-max-skill`, `heygen-com/hyperframes`, `anthropics/skills skill creator`, `anthropics/skills frontend design`.
- `nextlevelbuilder/ui-ux-pro-max-skill` e `heygen-com/hyperframes` já estavam na wiki (repositório e, no primeiro caso, também skill) — não reingeridos.
- `excalidraw-diagram-skill` não tinha owner explícito; resolvido por busca web para `coleam00/excalidraw-diagram-skill`, confirmado via API do GitHub.
- `anthropics/skills skill creator` e `anthropics/skills frontend design` identificados como skills dentro do repositório já ingerido `anthropics/skills`, nos caminhos `skills/skill-creator` e `skills/frontend-design`; `SKILL.md` cru de cada uma foi lido no commit já registrado `dbd4588f9e1033efb41dad4bef2f7947c8993d44`.

## [2026-10-19] ingest | obra/superpowers, upstash/context7, vercel-labs/agent-browser, thedotmack/claude-mem, coleam00/excalidraw-diagram-skill, anthropics/skills (skill-creator, frontend-design)
- Criadas `repos/github.com/obra/superpowers.md` (commit `bb92a77741419a4ab5f06e711a283343f1ada0c3`), `repos/github.com/upstash/context7.md` (commit `c7f80ce5af1ff1403d167579b76784482cf7f3e2`), `repos/github.com/vercel-labs/agent-browser.md` (commit `dac13bb87468fe9d74a040d862720f6cc17a9565`) e `repos/github.com/thedotmack/claude-mem.md` (commit `3fae1eb45ba1a7fbd4818527f48b439991a273da`), todas a partir do README, sem clonar os repositórios.
- Criada `skills/github.com/coleam00/excalidraw-diagram-skill/excalidraw-diagram.md` a partir da página do repositório no GitHub (repositório de skill única, sem página de repositório própria, seguindo o padrão de `cathrynlavery/diagram-design` e `zarazhangrui/frontend-slides`); `SKILL.md` cru não lido.
- Criadas `skills/github.com/anthropics/skills/skill-creator.md` e `skills/github.com/anthropics/skills/frontend-design.md`, com `SKILL.md` cru lido via raw.githubusercontent no commit já registrado de `anthropics/skills`.
- Criadas `entities/obra.md` (Jesse Vincent), `entities/upstash.md`, `entities/thedotmack.md` (Alex Newman) e `entities/coleam00.md` (Cole Medin).
- Atualizadas `entities/vercel-labs.md` (adicionado `agent-browser`) e `entities/anthropics.md` (adicionadas as skills `skill-creator` e `frontend-design`).
- Atualizados `concepts/tdd-para-agentes.md`, `concepts/navegacao-web-agentica.md`, `concepts/model-context-protocol.md`, `concepts/memoria-de-agente.md`, `concepts/design-taste-para-agentes.md` e `concepts/artefatos-html-autocontidos.md` com links de entrada (sem reescrever o corpo).
- Atualizados `index.md`, `categorias.md` (repositórios/skills/entidades adicionados a "Harnesses e orquestração de agentes", "Skills, instruções e personalidades de agente", "Design de interface e direção de arte", "Geração de mídia e artefatos HTML", "Engenharia e interfaces agent-first" e "Protocolos, integrações e confiabilidade") e `README.md` (52 repositórios, 31 skills, 33 conceitos, 58 entidades, 0 análises).
- Não lidos: código-fonte dos quatro repositórios além do README; `SKILL.md` cru de `excalidraw-diagram-skill`; licença exata de `excalidraw-diagram-skill` (não declarada na página consultada).
- Commit único cobrindo as sete ingestões, por terem sido processadas em lote a partir de um único pedido do usuário.
