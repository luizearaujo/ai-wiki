---
type: repo
url: https://github.com/affaan-m/ECC
host: github.com
owner: affaan-m
repo: ecc
commit: 76aaa77df6adc5b889e689007bf99b9a4f74af34
license: MIT
language: JavaScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, harness, skills, orquestracao, memoria, seguranca, claude-code]
---

# affaan-m/ECC

> Sistema de otimização de harness de agente que instala no Claude Code — e em outros harnesses — um processo de engenharia com planejamento, TDD, revisão em contexto novo, memória persistente e varredura de segurança, distribuído como 71 agentes, 311 skills e 97 comandos legados.

## O que é

O ECC ("agent harness operating system", na formulação do README) parte de uma premissa simples: um agente já consegue escrever código, mas não mantém sozinho um processo de engenharia entre sessões. O projeto instala esse processo uma vez — `plan -> test -> implement -> review -> verify -> remember -> improve` — em vez de repeti-lo em cada prompt.

O público declarado é quem usa Claude Code intensamente e quer que o agente planeje antes de construir, verifique com testes, revise o próprio trabalho a partir de contexto limpo, registre o que aprendeu e transforme acertos repetidos em skills reutilizáveis. O README afirma funcionar melhor com Claude Code, ter caminhos nativos de plugin para Codex e Qoder e adaptadores com paridade limitada para Cursor, OpenCode, Gemini, Zed, GitHub Copilot, Antigravity, Qwen e outros harnesses.

O pacote publicado inclui **71 agentes**, **311 skills**, **97 shims de comando** mantidos durante a migração para uma superfície *skills-first*, hooks, regras por linguagem, memória, aprendizado contínuo ("instincts") e o scanner AgentShield.

## Como funciona

O repositório é a fonte de verdade; adaptadores de plataforma empacotam ou mapeiam os mesmos workflows em vez de manter cópias separadas. A estrutura publicada no README:

```text
ECC/
|-- agents/           # 71 subagentes especializados para delegação
|-- skills/           # 311 workflows reutilizáveis carregados sob demanda
|-- commands/         # 97 shims de slash command mantidos
|-- rules/            # padrões comuns e por linguagem, opt-in
|-- hooks/            # automação e enforcement em eventos do harness
|-- scripts/          # instalação, reparo, sincronização, orquestração
|-- .claude-plugin/   # manifesto de marketplace do Claude Code
|-- .codex/           # configuração e roles de referência para Codex
|-- .opencode/        # plugin, comandos e instruções para OpenCode
|-- .cursor/          # regras e adaptador de hooks para Cursor
|-- docs/             # guias públicos de setup, arquitetura e operação
```

As camadas resolvem problemas diferentes e o README insiste nessa separação para não despejar o repositório inteiro no contexto:

| Camada | Papel | Comportamento no contexto |
|---|---|---|
| Skills | Workflows reutilizáveis (TDD, segurança, pesquisa) | Carregadas quando a tarefa exige |
| Agentes | Trabalhadores com escopo, contexto e permissões próprios | Isolam planejamento, implementação e revisão |
| Rules | Padrões duráveis de projeto ou linguagem | Sempre carregadas; instalar seletivamente |
| Hooks | Scripts disparados por eventos do harness | Executam fora do contexto do modelo |
| Instincts | Padrões aprendidos de sessões reais, com confiança | Recuperados quando relevantes |

O fluxo TDD é o exemplo canônico: `/ecc:plan` gera um plano editável, `tdd-workflow` exige evidência RED antes da implementação, o código é implementado até GREEN, `/code-review` revisa em contexto novo, correções entram com testes de regressão e a verificação final cobre build, lint, tipos e testes.

### Memory Vault

O ECC inclui uma memória portátil em Markdown (`ecc.memory.v1`) para trocar contexto entre harnesses. Memórias de projeto e time ficam em `.ecc/memory/`; memórias de usuário, em `~/.ecc/memory/`. O README trata memória como **contexto não revisado, não política executável**: o corpo é aceito só por `--stdin` ou `--body-file`, entradas são create-only na primeira release e a promoção para documentação governada é humana.

```bash
npm install -g ecc-universal@2.2.3
ecc memory init --scope project
ecc memory handoff --from hermes --target codex --title "..." --body-file ./handoff.md
ecc memory search "authentication migration" --target-harness codex
ecc memory doctor
```

O servidor MCP opcional `ecc-memory-mcp` expõe apenas `memory_save`, `memory_search`, `memory_read` e `memory_doctor`; cada servidor precisa subir com uma identidade `ECC_MEMORY_HARNESS` fixa, e escopo de usuário exige `ECC_MEMORY_ALLOW_USER_SCOPE=1`.

### AgentShield

O AgentShield audita a própria configuração do agente como superfície de ataque: `CLAUDE.md`, `settings.json`, configuração MCP, hooks, definições de agente e skills. São cinco categorias — detecção de segredos (14 padrões), auditoria de permissões, análise de injeção em hooks, perfil de risco de servidores MCP e revisão de configuração de agente — com 102 regras de análise estática declaradas no README.

```bash
agentshield scan --path .
agentshield scan --path . --fix
agentshield scan --path . --opus --stream
agentshield init
```

O modo `--opus` roda três agentes Opus em pipeline de red team, blue team e auditor. A saída pode ser terminal (nota A–F), JSON, Markdown ou HTML, com exit code 2 em achados críticos para gates de build.

## Instalação e uso rápido

Pré-requisitos para o pacote universal: Node.js 18+, Git e, no caminho de plugin do Claude Code, Claude Code 2.1+. O README recomenda escolher **um** caminho de instalação por harness e não empilhar um install manual completo sobre o plugin.

```bash
npx ecc-universal@2.2.3 setup
```

Para Claude Code, o resultado é o plugin `ecc@ecc`; confirme com `/plugin list ecc@ecc`. Também há instaladores seletivos/manuais, perfis de hooks (`minimal`, `standard`, `strict`) e alvos por harness (`--target kimi`, `--target copilot`, `--profile full` etc.). Em Codex e Qoder o caminho é plugin nativo; nos demais, adaptadores seletivos.

Entradas de uso documentadas:

| Objetivo | Ponto de partida |
|---|---|
| Construir uma feature | `/ecc:plan "..."` e depois `tdd-workflow` |
| Corrigir um bug | teste que falha reproduzindo o bug, depois `tdd-workflow` |
| Revisar código novo | `/code-review` |
| Consertar build | `/build-fix` |
| Limpar base de código | `/refactor-clean` |
| Ver pressão de contexto | `/context-budget` |
| Encerrar/retomar sessão | `/save-session`, `/resume-session` |
| Auditar configuração do agente | `/security-scan` ou `agentshield scan --path .` |

O README também recomenda uma configuração de tokens: modelo `sonnet` por padrão (`~60%` menos custo, segundo o projeto), effort `medium`, autocompactação em 50% e subagentes em `haiku`; manter menos de 10 MCPs e menos de 80 tools ativos por projeto.

## Exemplos de uso

Exemplo derivado do README para uma feature com TDD:

```text
/ecc:plan "Add usage-based billing alerts"
  -> confirmar ou editar o plano
  -> ativar tdd-workflow
  -> capturar evidência RED antes da implementação
  -> implementar até GREEN
  -> revisar em contexto novo
  -> corrigir achados com testes de regressão
  -> verificar build, lint, tipos e testes
```

O resultado esperado não é só código, mas uma trilha: plano, teste que falha, teste que passa, achados de revisão e verificação final.

## Quando usar (e quando não usar)

- **Use quando:** você já trabalha com um harness de código suportado, quer um processo de engenharia repetível e valoriza TDD, revisão em contexto isolado, memória entre sessões e auditoria de configuração. O ECC é especialmente indicado para quem quer um catálogo amplo e multi-harness em vez de montar hooks e skills manualmente.
- **Evite quando:** você precisa de paridade total entre harnesses (o README declara que ela não existe), trabalha em ambiente com orçamento de contexto apertado e não quer gerenciar instalação seletiva, ou não pode auditar hooks e comandos de shell que passam a fazer parte do runtime. Para um fluxo mais enxuto e centrado em um único harness, vale comparar com [garrytan/gstack](../garrytan/gstack.md); para uma equipe visual com agentes de terminal, com [HarnessMD/munder-difflin](../harnessmd/munder-difflin.md).

## Limitações e cuidados

- **Supply chain e configuração executável.** O próprio README alerta para instalar apenas dos canais oficiais (repositório, npm `ecc-universal`/`ecc-agentshield`, plugin `ecc@ecc`, GitHub App e `ecc.tools`) e trata hooks, servidores MCP e instruções de projeto como configuração executável. Espelhos de terceiros não são revisados.
- **Contexto.** O plugin anuncia o catálogo instalado ao modelo; o README recomenda perfis seletivos quando o footprint de contexto importa. Muitos MCPs e tools reduzem a janela útil.
- **Paridade limitada.** Continuous learning, GAN e alguns caminhos de orquestração ainda dependem de Bash ou Python; Windows nativo tem defeitos abertos no observer daemon do continuous-learning v2 e nas escritas do Memory Vault.
- **Métricas e qualidade.** As contagens de 71/311/97 são as publicadas no README na data da ingestão. A qualidade individual de cada skill e agente não foi verificada; apenas o README foi lido.
- **Freemium.** O OSS é MIT, mas o ECC Pro é um GitHub App hospedado para repositórios privados, com análise de PR, pooling de uso e suporte. A fronteira exata entre OSS e Pro não foi verificada em código.
- **Ordenação de metas.** O README é explicitamente promocional e repleto de alegações de produtividade; trate números de custo e ganho como afirmações do projeto, não medições independentes.

## Estado e adoção

- Versão citada no README: **2.2.3** (2026-10-01); a linha 2.0 "Agent Harness Operating System" foi graduada em junho de 2026.
- Observado em 2026-10-19: ~283.668 stars, ~42.134 forks, ~246 issues abertas; último push em 2026-10-19; criado em 2026-01-18.
- Licença: MIT (API do GitHub e README concordam).
- Linguagem principal na API: JavaScript.

## Relações

- Mantido por: [affaan-m](../../../entities/affaan-m.md)
- Conceitos: [Agent harness](../../../concepts/agent-harness.md), [Agent skills](../../../concepts/agent-skills.md), [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md)
- Relacionado: [garrytan/gstack](../garrytan/gstack.md) — também transforma o Claude Code em uma equipe com skills e comandos, mas com foco em processo de sprint e browser/QA; [HarnessMD/munder-difflin](../harnessmd/munder-difflin.md) — harness desktop que orquestra CLIs em uma metáfora de escritório; [SynkraAI/aiox-core](../../../repos/github.com/synkraai/aiox-core.md) — orquestração por agentes com artefatos persistentes.
- Ferramentas citadas: AgentShield (`affaan-m/agentshield`), ECC Pro/GitHub App, Memory Vault.

## Perguntas abertas

- Como o instalador reconcilia estado entre versões e evita que hooks dupliquem execução em upgrades?
- Qual é a paridade real dos adaptadores (Cursor, OpenCode, Gemini, Zed etc.) em hooks, agentes e skills?
- Os "instincts" com confidence score melhoram resultados de forma mensurável ou são apenas um mecanismo de injeção de contexto?
- Como o Memory Vault lida com conflitos e com memória envenenada vinda de outro harness?
- Quais skills e agentes são mantidos ativamente e quais são legado?
- Onde termina o OSS MIT e começa o ECC Pro?

## Fontes

- README: https://raw.githubusercontent.com/affaan-m/ECC/76aaa77df6adc5b889e689007bf99b9a4f74af34/README.md (commit `76aaa77df6adc5b889e689007bf99b9a4f74af34`, consultado em 2026-10-19). Somente o README foi lido; código, `docs/`, guias e arquivos de agente/skill não foram consultados.
- Metadados: API do GitHub (`/repos/affaan-m/ECC`) em 2026-10-19.
