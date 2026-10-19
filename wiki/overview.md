---
type: overview
created: 2026-10-17
updated: 2026-10-19
tags: [overview]
---

# Panorama do ecossistema de IA

> Síntese em evolução do que a wiki cobre. Atualize quando uma ingestão mudar o quadro geral.

## Temas cobertos

- **Engenharia reversa agêntica:** agentes usando ferramentas locais para investigar artefatos sem código-fonte, cruzar análise estática com runtime e reconstruir comportamento.
- **MCP como camada de integração:** um servidor de ferramentas compartilhado por CLI e agentes, em vez de integrações específicas por cliente.
- **Evidência e proveniência:** resultados de análise com cobertura, limitações e desconhecidos explícitos, para que conclusões de agentes sejam auditáveis.
- **Agent skills como formato de distribuição:** instruções especializadas empacotadas em `SKILL.md`, versionadas em repositórios e instaladas por CLI em vários agentes.
- **Auditoria de UX assistida por agentes:** frameworks de avaliação de produto operacionalizados como instruções reutilizáveis, com métodos e limitações próprios.
- **Instruções persistentes para agentes:** arquivos como `CLAUDE.md` fixam convenções, comandos e critérios de comportamento entre sessões, em contraste com skills carregadas por tarefa.
- **Bibliotecas de personalidades de agente:** coleções de arquivos `.md` que definem especialidade, voz, regras críticas, entregáveis e métricas para agentes de IA, instaláveis em vários clientes; o Agency Agents é o maior exemplo documentado na wiki.
- **Grafo de conhecimento de código como camada de contexto para agentes:** indexar uma base de código em um grafo persistente permite que o agente responda perguntas estruturais (callers, rotas, dependências) em milissegundos e com ~10–120× menos tokens do que lendo arquivos; o CBM é o primeiro servidor MCP desse tipo documentado na wiki.
- **Geração de cliente a partir de tráfego capturado:** capturar uma sessão HTTP autenticada uma vez e usar Claude para gerar um cliente Python chamável como biblioteca — sem documentação de API nem código HTTP manual.
- **Issue trackers com agentes como membros de equipe:** plataformas de gerenciamento de projetos onde agentes de IA ocupam slots de assignee, recebem issues e executam tarefas no mesmo board que as pessoas — misturando fluxo humano e agêntico sem ferramentas separadas.
- **Orquestração ágil multi-agente:** frameworks que instalam uma equipe completa de agentes especializados em um projeto, com roles análogos a Scrum (analyst, pm, architect, sm, dev, qa, devops) e passagem de contexto via artefatos persistentes (PRDs, histórias, specs) em vez de prompts de sessão — resolvendo inconsistência de planejamento e perda de contexto entre sessões.
- **Agent harness como camada de produto:** em vez de construir um agente do zero, projetos instalam processo, especialistas, memória, hooks e segurança sobre CLIs existentes (Claude Code, Codex, Gemini etc.), com adaptadores para vários hosts e paridade declaradamente parcial.
- **Processo de engenharia como artefato distribuído:** TDD, revisão em contexto novo, QA em navegador, release e documentação são empacotados como skills/slash commands e encadeados por artefatos (plano, design doc, spec, PR), não por memória de sessão.
- **Supervisão multiagente:** orquestração pode ser um pipeline por etapas (gstack), um supervisor que distribui e escala exceções (Munder Difflin) ou um catálogo de subagentes com revisores por linguagem (ECC); em todos os casos, isolamento de contexto e observabilidade são o problema central.
- **Memória persistente como handoff:** memória portátil em Markdown (ECC Memory Vault), base de conhecimento consultável via MCP (GBrain no gstack) e memória semântica compartilhada entre agentes (Munder Difflin) atacam a perda de contexto entre sessões e entre harnesses.
- **Segurança da configuração do agente:** hooks, MCP, permissões e instruções passam a ser tratados como superfície de ataque — auditoria estática (AgentShield), recibos de egresso, envelopes de confiança para conteúdo externo, gates humanos e circuit breakers.
- **Super agent harness para tarefas longas:** o DeerFlow empacota agente líder, subagentes, memória, sandbox, skills e canais de mensagem em um runtime self-hosted sobre LangGraph, reescrito do zero na versão 2.0 e tratado explicitamente como software de alto privilégio.
- **Produção de vídeo agêntica:** pipelines declarados em YAML e skills de direção por etapa permitem que o assistente de código pesquise, escreva, gere ativos, edite e valide um vídeo com checkpoints de custo e decisão — o OpenMontage é o primeiro exemplo documentado.
- **Grafos de código com proveniência de aresta:** além do grafo extraído por parser, projetos como o Graphify inferem relações semanticamente e marcam cada aresta como `EXTRACTED` ou `INFERRED`; a consulta dispensa vector store e o grafo pode ser inspecionado e explicado.
- **Artefatos HTML autocontidos como formato de entrega:** apresentações e diagramas viram um único arquivo HTML com CSS, JS e SVG inline, versionável e fácil de publicar; as skills Frontend Slides e Diagram Design mostram que o valor está no processo de design, não apenas no template.
- **Design system como gate de skill:** a skill Diagram Design exige um style guide na primeira execução e trata consistência de tipografia, paleta, espaçamento e acessibilidade como condição de aceitação, não como preferência.
- **Cibersegurança como biblioteca de skills:** projetos como o Anthropic Cybersecurity Skills empacotam centenas de procedimentos de segurança em `SKILL.md`, mapeados a frameworks (ATT&CK, NIST CSF, ATLAS, D3FEND, AI RMF, F3) e descobertos por frontmatter antes do carregamento completo.
- **Edição de prosa como skill:** skills como o Humanizer tratam os maneirismos de texto gerado por IA como um catálogo de padrões auditável, com regras de preservação de conteúdo e de voz; o objetivo é editar estilo, não detectar autoria.

## Mapa por área

| Área | Repositórios | Observações |
| --- | --- | --- |
| Engenharia reversa e análise de software | [morluto/rea](repos/github.com/morluto/rea.md) | CLI + MCP local; binários nativos, apps JavaScript/Electron, .NET, Android, firmware e runtime; providers bring-your-own. |
| Protocolos para agentes | — | MCP aparece como infraestrutura transversal; primeira página em [Model Context Protocol](concepts/model-context-protocol.md). |
| Skills para agentes | [calesthio/OpenMontage](repos/github.com/calesthio/openmontage.md), [bytedance/deer-flow](repos/github.com/bytedance/deer-flow.md), [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) | [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md), [Understand](skills/github.com/egonex-ai/understand-anything/understand.md), [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) e [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md); formato descrito em [Agent skills](concepts/agent-skills.md). OpenMontage usa 700+ arquivos de skills em três camadas; DeerFlow carrega skills progressivamente. |
| Instruções e diretrizes para agentes | [multica-ai/andrej-karpathy-skills](repos/github.com/multica-ai/andrej-karpathy-skills.md) | Quatro princípios de comportamento em um `CLAUDE.md`; distribuição como arquivo ou plugin; variação para Cursor. Formato descrito em [CLAUDE.md](concepts/claude-md.md). |
| Personalidades de agente por especialidade | [msitarzewski/agency-agents](repos/github.com/msitarzewski/agency-agents.md) | 150+ arquivos `.md`, cada um com identidade, regras críticas, entregáveis e métricas; organizados em 16 divisões (Engenharia, Segurança, Marketing, GIS etc.); instaláveis via app ou script em Claude Code, Cursor, Codex e mais. |
| Grafo de conhecimento de código | [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md), [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) | CBM: servidor MCP local em C puro; 162 linguagens via tree-sitter + Hybrid LSP; SQLite persistente; 17 ferramentas; ~120× menos tokens (comparação do projeto). Graphify: skill + CLI Python, ~40 linguagens, arestas `EXTRACTED`/`INFERRED`, comunidades de Leiden, sem vector store, serviço Cloud. Skill [Understand](skills/github.com/egonex-ai/understand-anything/understand.md) documenta a abordagem via plugin. |
| Geração de cliente a partir de tráfego | [littledivy/mimic](repos/github.com/littledivy/mimic.md) | Captura tráfego iOS/web (mitmproxy, cURL, HAR), extrai auth estável e usa Claude para gerar um cliente Python chamável; certificate pinning e DPoP/sender-constrained tokens são os dois bloqueadores principais. |
| Issue tracker com agentes como membros | [croffasia/itsaplan](repos/github.com/croffasia/itsaplan.md) | Alternativa self-hosted ao Linear/Jira (AGPL-3.0); agentes internos (Mastra) ou externos (`@itsaplan/runner` → Claude Code, Codex etc.) trabalham no mesmo Kanban que as pessoas; REST API + MCP + webhooks. |
| Orquestração ágil multi-agente | [SynkraAI/aiox-core](repos/github.com/synkraai/aiox-core.md) | Framework CLI-first com 12 agentes (planejamento + desenvolvimento + meta); fluxo em duas fases: PRD/Arquitetura → histórias hiperdetalhadas → execução com contexto completo; ADE com 7 epics para desenvolvimento autônomo; Squads extensíveis a qualquer domínio. |
| Agent harness de código | [affaan-m/ECC](repos/github.com/affaan-m/ecc.md), [garrytan/gstack](repos/github.com/garrytan/gstack.md) | ECC instala processo, 71 agentes, 311 skills, memória e AgentShield em vários hosts; gstack organiza 23 especialistas e oito power tools no ciclo Think → Plan → Build → Review → Test → Ship → Reflect. Ambos usam Markdown e hooks sobre CLIs existentes. |
| Harness desktop multiagente | [HarnessMD/munder-difflin](repos/github.com/harnessmd/munder-difflin.md) | App Electron que embrulha 12 CLIs em PTYs, com orquestrador Michael, hive de memória/mailbox/blackboard, escritório visual, board de tarefas e edição Pro; pré-release 0.5.6. |
| Super agent harness | [bytedance/deer-flow](repos/github.com/bytedance/deer-flow.md) | Python/LangGraph, web + TUI; agente líder e subagentes com contexto isolado ou snapshot; skills progressivas; MCP; sandbox Docker/E2B; memória DeerMem; browser Playwright; canais de mensagem. MIT, com serviços comerciais da ByteDance promovidos no README. |
| Produção de vídeo agêntica | [calesthio/OpenMontage](repos/github.com/calesthio/openmontage.md) | Pipelines YAML + skills de direção; 100+ ferramentas e 60+ provedores; Remotion, HyperFrames e FFmpeg; score de provedores em 7 dimensões; validação pré-composição e pós-render; AGPL-3.0. |
| Artefatos HTML autocontidos | — | Skills [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) (deck 16:9 de arquivo único) e [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) (SVG acessível com style guide); síntese em [Artefatos HTML autocontidos](concepts/artefatos-html-autocontidos.md). |
| Avaliação de UX | — | Primeira síntese em [Auditoria de UX](concepts/auditoria-de-ux.md); aplicação documentada na skill UX Audit Rethink. |
| Cibersegurança e operações de segurança | [mukul975/Anthropic-Cybersecurity-Skills](repos/github.com/mukul975/anthropic-cybersecurity-skills.md) | Biblioteca de 818 skills em 34 domínios, mapeadas a ATT&CK, NIST CSF 2.0, ATLAS, D3FEND, AI RMF e F3; projeto da comunidade, sem vínculo com a Anthropic. Síntese em [Cibersegurança com agentes](concepts/ciberseguranca-com-agentes.md). |
| Escrita e edição de prosa | — | Skills [Humanizer](skills/github.com/blader/humanizer/humanizer.md) (26 padrões em seis famílias, fluxo de quatro etapas, três modos de saída) e [Stop Slop](skills/github.com/hardikpandya/stop-slop/stop-slop.md) (oito regras, lista de checagens, nota de 1–10 em cinco dimensões); síntese em [Humanização de texto gerado por IA](concepts/humanizacao-de-texto-por-ia.md). |

## Tendências e observações

- Ferramentas para agentes estão migrando de plugins específicos para **servidores MCP locais com CLI compartilhada**, o que permite o mesmo workflow em vários clientes.
- O modelo **bring-your-own provider** (Hopper, Ghidra, IDA, JADX etc.) reduz o escopo do projeto, mas transfere ao usuário a responsabilidade por licenças e pela verificação real de cada plataforma.
- **Evidência estruturada** — cobertura, limitações e desconhecidos — é o que torna a análise por agentes auditável; sem isso, a explicação do agente não é distinguível de uma inferência plausível.
- Catálogos MCP grandes podem custar muito contexto; respostas com views, paginação e exportação preservam a evidência completa sem enviá-la inteira ao modelo.
- O REA é um caso de adoção expressiva (o README celebra 300 mil estrelas) e o próprio README avisa que o projeto muda rápido e recebe correções com frequência; registrar a versão e o commit usados continua essencial.
- **Skills e MCP são camadas complementares:** skills empacotam instruções e métodos; MCP expõe ferramentas e dados em runtime. Um agente pode usar as duas ao mesmo tempo.
- Catálogos de skills expõem métricas voláteis (instalações, estrelas) e, às vezes, não publicam a versão da skill; a fonte canônica continua sendo o repositório-fonte.
- A distribuição de skills por CLI cria uma **superfície de supply chain**: instruções de terceiros passam a fazer parte do comportamento do agente. Guardas contra prompt injection dentro de uma skill são um sinal do risco, não uma garantia.
- O Agency Agents amplia essa superfície: 150+ arquivos de terceiros que moldam o comportamento do agente, instalados por script ou app nativo. Cada arquivo `.md` é uma instrução de sistema com personalidade e regras críticas; sem verificação de integridade documentada, a fonte importa.
- O CBM toma uma rota oposta: binário estático com SLSA 3, OpenSSF Scorecard e checksums SHA-256 por release; não faz nenhuma requisição de rede por conta própria. O custo é que atualizar exige rodar o install script manualmente ou via gerenciador de pacotes.
- **Grafo estático ≠ cobertura completa**: um grafo de código responde apenas ao que o parser indexou; chamadas dinâmicas, dispatch por reflexão e código gerado em runtime não aparecem. O README do CBM documenta explicitamente as lacunas de cobertura e disponibiliza um workspace "Coverage" no Lens.
- **Diretrizes e skills ocupam camadas diferentes:** um `CLAUDE.md` fornece contexto persistente do projeto; uma skill é acionada por tarefa. Os formatos podem coexistir, mas custo de contexto e precedência em conflitos ainda não são claros.
- A transferência de `andrej-karpathy-skills` de `forrestchang` para `multica-ai` ilustra como **links de instalação podem ficar defasados** mesmo quando o host redireciona o caminho antigo.
- **Orquestração via artefatos explícitos vs. via memória de sessão:** o AIOX aposta em documentos PRD + arquivos de histórias como unidade de contexto persistente entre sessões; cada agente lê um arquivo, não um histórico de chat. Essa escolha resolve perda de contexto mas exige disciplina de bookkeeping (gerar e manter os artefatos). O ADE (7 epics) é a tentativa de automatizar esse bookkeeping.
- **Divergência de licença entre API e README** — o AIOX reporta `other/NOASSERTION` na API do GitHub mas MIT no README. Projetos com módulo premium separado (AIOX Pro) podem ter repositório único com dois regimes de licença; a API do GitHub não distingue módulos. Padrão a observar em outros projetos freemium open-source.
- **Harness é a nova camada de distribuição:** ECC, gstack e Munder Difflin não competem com o modelo nem com o CLI; eles empacotam comportamento, processo e integrações sobre Claude Code, Codex e outros. O diferencial passa a ser o contexto e a orquestração, não a geração de tokens.
- **Paridade multi-harness é declaradamente parcial:** os três projetos listam hosts com níveis diferentes (stable/full, beta/experimental, instruction-only). O mesmo workflow pode se comportar de forma diferente em Cursor, Codex ou Copilot, e hooks são o componente menos portável.
- **Skills-first:** o ECC está migrando de comandos para skills (97 shims legados) e o gstack expressa todo o processo em Markdown. O artefato versionável — `SKILL.md`, regra ou slash command — virou a unidade de distribuição do comportamento do agente.
- **Memória sem consenso de formato:** o ECC aposta em Markdown portátil com handoff entre harnesses; o gstack usa uma base consultável via MCP (GBrain); o Munder minera memória Markdown em um índice semântico compartilhado. Não há padrão comum, e memória é tratada como contexto não confiável, não como política.
- **Segurança migra para a configuração do agente:** auditar `CLAUDE.md`, hooks, MCP e permissões (AgentShield), registrar egresso (gstack) e impor gates humanos/circuit breaker (Munder) são respostas ao fato de que instruções e hooks são código executável.
- **Freemium convive com OSS:** ECC mantém o repositório MIT e vende um GitHub App hospedado; o Munder mantém o código MIT e vende uma edição Pro, além de assets com licença separada (LimeZu). A licença do repositório não descreve todo o produto.
- **Links de instalação envelhecem:** o Munder Difflin ainda referencia `chaitanyagiri/munder-difflin` no README mesmo após a transferência para `HarnessMD`; o caso replica o padrão já visto em `andrej-karpathy-skills`. Redirecionamentos do host não corrigem comandos copiados em docs e posts.
- **Números de adoção são voláteis e promocionais:** ECC (~284 mil stars), gstack (~137 mil) e Munder (~8,9 mil) observados em 2026-10-19. Os READMEs misturam métricas do GitHub com alegações de produtividade e custo; trate-as como afirmações datadas do projeto.
- **Reescrita como estratégia de harness:** o DeerFlow 2.0 não compartilha código com a versão 1.x e mantém a antiga na branch `main-1.x`. É um caso raro de projeto grande que descarta a arquitetura anterior para virar um harness completo; o custo é a ruptura para usuários e integrações existentes.
- **Harness de alto privilégio exige postura explícita:** o DeerFlow declara que admin do Gateway equivale a execução de código, recomenda loopback por padrão e exige controles adicionais para expor a rede. O README trata a segurança como responsabilidade de implantação, não como detalhe do produto.
- **Subagentes como otimização, não default:** o DeerFlow afirma que subagentes são úteis para subtarefas independentes e não a resposta padrão para qualquer tarefa complexa — uma calibragem explícita contra o entusiasmo por paralelismo.
- **Proveniência de aresta torna o grafo auditável:** ao marcar `EXTRACTED` e `INFERRED`, o Graphify permite distinguir o que o parser viu do que o modelo deduziu. Isso responde diretamente à lacuna de "grafo estático ≠ cobertura completa": a aresta inferida é útil, mas não tem o mesmo status de evidência.
- **Grafo sem vector store é uma tese, não só uma implementação:** o Graphify consulta estrutura e comunidades sem embeddings; o passo semântico é opcional e voltado a docs e mídia. O trade-off é depender de boa extração e de consultas explícitas, em vez de similaridade difusa.
- **Freemium também em grafos:** Graphify é Apache-2.0 com Graphify Cloud pago (teste de 14 dias); a fronteira entre CLI e serviço não está documentada no README. O padrão se soma a ECC, Munder e DeerFlow: a licença do repositório não descreve todo o produto.
- **Skills de artefato vendem processo, não template:** Frontend Slides faz descoberta de conteúdo e três prévias de estilo antes de gerar; Diagram Design exige style guide e valida acessibilidade do SVG. Em ambos, o diferencial é o fluxo de decisão e verificação embutido na skill.
- **HTML autocontido reduz atrito de entrega:** um único arquivo com CSS/JS/SVG inline dispensa build, servidor e dependências; o custo aparece em manutenção, tamanho e dificuldade de colaboração — e, no caso de diagramas, em depender de um contrato de acessibilidade que o gerador pode violar.
- **Pipelines de vídeo tornam a produção reproduzível:** OpenMontage grava manifesto, skill de direção, checkpoint e custo por etapa; trocar o runtime de renderização sem atualizar o proposal é tratado como violação de governança. A reprodução ainda depende de provedores externos e de credenciais.
- **Licença forte em ferramenta de produção:** OpenMontage é AGPL-3.0, mais restritiva que MIT/Apache dos demais harnesses; uso comercial e integração em serviço exigem atenção jurídica que os outros projetos não impõem.
- **Divergências de contagem são comuns:** OpenMontage declara "10+ pipelines" no README e 12 na descrição da API; Diagram Design publica 45 tipos de diagrama na página do skills.sh e 44 na descrição do repositório. Números de vitrine devem ser lidos como afirmações datadas, não como especificação.
- **Auditoria de skill é publicada, mas heterogênea:** as páginas do skills.sh exibem verificações de terceiros (Gen Agent Trust Hub, Socket, Snyk) com resultados como "Pass", "Warn" ou "Fail". É um sinal de ecossistema, mas os critérios variam e não substituem a leitura do `SKILL.md`.
- **Domínio especializado escala por catálogo, não por prompt:** o Anthropic Cybersecurity Skills mostra que uma área inteira pode ser coberta por centenas de skills pequenas, descobertas por frontmatter (~30 tokens) e carregadas sob demanda. O ganho é cobertura e consistência de procedimento; o custo é governança — ninguém revisa 818 workflows a cada atualização.
- **Nome de projeto não implica afiliação:** o repositório usa "Anthropic" no nome e no padrão de skills, mas se declara projeto da comunidade, sem vínculo com a Anthropic. O mesmo padrão de confusão já apareceu em links de instalação defasados; nome, licença e mantenedor precisam ser verificados separadamente.
- **Divergência de contagem interna:** o README usa 818 skills em uma passagem e 817 em outra, contra 34 domínios. É mais uma evidência de que números de catálogo são afirmações datadas do projeto, não especificação estável.
- **Estilo também vira artefato distribuído:** o Humanizer mostra que instruções de escrita podem ser versionadas, auditadas e instaladas como qualquer skill de engenharia. O catálogo de padrões é derivado de observação empírica da Wikipédia e evolui junto com os modelos — não é uma norma editorial estável.
- **Risco de trocar um padrão por outro:** aplicar regras de humanização sem uma amostra de voz pode criar um novo registro uniforme. As próprias skills reconhecem que a amostra do autor deve sobrepor o catálogo.
- **Humanização ainda não tem forma canônica:** Humanizer e Stop Slop atacam o mesmo problema com soluções diferentes — catálogo granular com força por padrão e modos de saída, contra oito regras com nota final. A coexistência indica que o campo está em experimentação de formato, não em consolidação de método.

## Lacunas e próximos passos

- [ ] Ingerir uma alternativa ou competidor: outro servidor MCP de engenharia reversa, ou um fluxo Ghidra/IDA + agente.
- [ ] Ler a documentação oficial do REA (com autorização) para aprofundar o `EvidenceLedger` e o roteamento de providers.
- [ ] Comparar o REA com fluxos manuais (Ghidra/IDA) e medir custo/tempo/tokens.
- [ ] Ler `docs/testing.md` (com autorização) para verificar quais providers e plataformas têm lanes de teste com ferramentas reais.
- [ ] Mapear outros repositórios do autor e do ecossistema MCP de análise.
- [ ] Ler o `SKILL.md` de UX Audit Rethink (com autorização) para documentar método, escala e formato de saída.
- [ ] Ingerir outras skills do ecossistema e comparar formatos/distribuição.
- [ ] Comparar auditoria de UX conduzida por agente com avaliação heurística tradicional.
- [ ] Ler `CLAUDE.md`, `CURSOR.md` e `.cursor/rules/karpathy-guidelines.mdc` de `andrej-karpathy-skills` (com autorização) para verificar o texto real das diretrizes e a adaptação ao Cursor.
- [ ] Verificar se os comandos de instalação com `forrestchang/...` continuam funcionando após a transferência do repositório.
- [ ] Comparar `CLAUDE.md` e skills `SKILL.md` em custo de contexto, precedência e efeito observável no comportamento do agente.
- [ ] Comparar ECC, gstack e Munder Difflin em custo de contexto, curva de instalação, paridade entre hosts e qualidade dos artefatos produzidos (plano, revisão, testes).
- [ ] Ler a documentação interna do ECC (`docs/`, `the-security-guide.md`) para verificar como hooks e o Memory Vault funcionam na prática.
- [ ] Ler `ARCHITECTURE.md` e `docs/skills.md` do gstack para verificar a implementação de QA em navegador, GBrain e recibos de egresso.
- [ ] Ler `HIVE.md`, `SPEC.md` e `docs/ARCHITECTURE.md` do Munder Difflin para verificar o hive, os gates humanos e o isolamento entre agentes.
- [ ] Ingerir `garrytan/gbrain` para documentar a memória persistente usada pelo gstack.
- [ ] Investigar o modelo de licenciamento e o limite entre OSS e edição Pro/ECC Pro nos três projetos.
- [ ] Comparar orquestração por pipeline (gstack), por supervisor (Munder) e por subagentes especializados (ECC) em tarefas reais.
- [ ] Ler a documentação interna do DeerFlow (memória DeerMem, sandbox, segurança e canais) com autorização para verificar as afirmações do README.
- [ ] Comparar DeerFlow, ECC, gstack e Munder Difflin em custo de contexto, isolamento e qualidade de tarefas longas.
- [ ] Comparar CBM, Graphify e Understand em acurácia do grafo, tempo de indexação, cobertura de linguagens e custo de consulta.
- [ ] Verificar a fronteira entre o Graphify CLI e o Graphify Cloud, e entre o DeerFlow OSS e os serviços comerciais da ByteDance.
- [ ] Ler os `SKILL.md` de Understand, Frontend Slides e Diagram Design (com autorização) para conferir os métodos publicados nas páginas do skills.sh.
- [ ] Avaliar na prática os gates e a validação de saída do OpenMontage, incluindo o score de provedores em sete dimensões.
- [ ] Comparar apresentações e diagramas gerados por skills com reveal.js, Slidev, Mermaid, draw.io e Excalidraw em qualidade, acessibilidade e manutenção.
- [ ] Auditar uma amostra das 818 skills de cibersegurança quanto a qualidade, atualidade dos mapeamentos de framework e segurança das instruções.
- [ ] Ler `README.md` e arquivos de catálogo do Anthropic Cybersecurity Skills (além do README raiz) para explicar a divergência entre 817 e 818 skills.
- [ ] Ler o `SKILL.md` do Humanizer (com autorização) e comparar os 26 padrões com o catálogo da Wikipédia.
- [ ] Avaliar com revisores cegos se textos reescritos por skills de humanização preservam sentido, voz e precisão factual.
- [ ] Comparar Humanizer e Stop Slop no mesmo conjunto de textos quanto a agressividade, preservação de voz e tempo de execução.

## Fontes

- [morluto/rea](repos/github.com/morluto/rea.md) — README no commit `9e372c6bc914b15e2f778f969da4fd3e11483d78`; metadados do GitHub observados em 2026-10-17.
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — https://claudemarketplaces.com/skills/mastepanoski/claude-skills/ux-audit-rethink (consultada em 2026-10-17).
- https://github.com/mastepanoski/claude-skills — metadados e árvore via API do GitHub em 2026-10-17 (commit `b6457af10e586d394056aae9555e78d74a372225`).
- [multica-ai/andrej-karpathy-skills](repos/github.com/multica-ai/andrej-karpathy-skills.md) — README no commit `2c606141936f1eeef17fa3043a72095b4765b9c2`; metadados da API do GitHub observados em 2026-10-17.
- [msitarzewski/agency-agents](repos/github.com/msitarzewski/agency-agents.md) — README no commit `652b2692f8d8ec2b1f1a38e559073e287dfdc469`; metadados da API do GitHub observados em 2026-10-18.
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — README no commit `354ccecbe612a9fdb624396a6738fa87f2617434`; metadados da API do GitHub observados em 2026-10-18.
- [littledivy/mimic](repos/github.com/littledivy/mimic.md) — README no commit `8cf998ac0b365806d8e522d34107cc504ecaa345`; metadados da API do GitHub observados em 2026-10-18.
- [croffasia/itsaplan](repos/github.com/croffasia/itsaplan.md) — README no commit `a54d8c3c4e88193777de0f75601d403c3b96bc1a`; metadados da API do GitHub observados em 2026-10-18.
- [SynkraAI/aiox-core](repos/github.com/synkraai/aiox-core.md) — README no commit `4ef6530ff03b83aea953e4a426f95e012b8b70c5`; metadados da API do GitHub observados em 2026-10-18.
- [affaan-m/ECC](repos/github.com/affaan-m/ecc.md) — README no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34`; metadados da API do GitHub observados em 2026-10-19.
- [garrytan/gstack](repos/github.com/garrytan/gstack.md) — README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037`; metadados da API do GitHub observados em 2026-10-19.
- [HarnessMD/munder-difflin](repos/github.com/harnessmd/munder-difflin.md) — README no commit `436d65a74a69d347c57641fbace4eb822bf98600`; metadados da API do GitHub observados em 2026-10-19.
- [Agent harness](concepts/agent-harness.md) e [Orquestração multiagente](concepts/orquestracao-multiagente.md) — sínteses construídas a partir dos READMEs de ECC, gstack, Munder Difflin e DeerFlow (2026-10-19).
- [bytedance/deer-flow](repos/github.com/bytedance/deer-flow.md) — README no commit `fee0cd0c180874325305e995197db99f03fa6a6f`; metadados da API do GitHub observados em 2026-10-19.
- [Graphify-Labs/graphify](repos/github.com/graphify-labs/graphify.md) — README no commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8`; metadados da API do GitHub observados em 2026-10-19.
- [calesthio/OpenMontage](repos/github.com/calesthio/openmontage.md) — README no commit `c8066452325cb57c8fc1ba8c2a71b6e8842e6b65`; metadados da API do GitHub observados em 2026-10-19.
- [Understand](skills/github.com/egonex-ai/understand-anything/understand.md), [Frontend Slides](skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) e [Diagram Design](skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — páginas do skills.sh consultadas em 2026-10-19.
- [Produção de vídeo agêntica](concepts/producao-de-video-agentica.md), [Memória de agente](concepts/memoria-de-agente.md) e [Artefatos HTML autocontidos](concepts/artefatos-html-autocontidos.md) — sínteses construídas a partir das fontes acima (2026-10-19).
- [mukul975/Anthropic-Cybersecurity-Skills](repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — README no commit `54a798831d2266a3ca61ce68a7acb80b81160d57`; metadados da API do GitHub observados em 2026-10-19.
- [Humanizer](skills/github.com/blader/humanizer/humanizer.md) — página do skills.sh consultada em 2026-10-19; repositório `blader/humanizer` no commit `8c307f367c91bd974002f10f2be2965d642c13df`.
- [Stop Slop](skills/github.com/hardikpandya/stop-slop/stop-slop.md) — página do skills.sh consultada em 2026-10-19; repositório `hardikpandya/stop-slop` no commit `8da1f030185bdfe8471220585162991eaeb970e9`.
