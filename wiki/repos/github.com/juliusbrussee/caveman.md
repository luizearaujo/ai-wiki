---
type: repo
url: https://github.com/JuliusBrussee/caveman
host: github.com
owner: juliusbrussee
repo: caveman
commit: bad48a0e1df55e05e3f52249afa35ecc1909ee76
license: Apache-2.0
language: Go
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, agent-skills, tokens, compressao-de-contexto, proxy, cli, custo, claude-code]
---

# JuliusBrussee/caveman

> Skill e proxy que reduzem o consumo de tokens de agentes de código comprimindo o que o agente fala e o que ele lê, sem alterar código, comandos, caminhos ou mensagens de erro.

## O que é

O README apresenta o `caveman` como um experimento nascido de piada em abril de 2026 e que passou de 100 mil estrelas: em vez de trocar o modelo ou encurtar o contexto manualmente, ele interfere em duas frentes — a **saída** do agente, que passa a responder em estilo telegráfico, e a **entrada**, comprimindo logs, JSON, CSV, YAML e saída de testes antes de o modelo lê-los.

A versão 4.0 organiza o produto em seis partes independentes ("six rocks"), ligadas por padrão e controláveis por interruptor. O README distingue o **skill** (apenas o estilo de resposta, sem proxy) do **CLI/proxy** (instalação completa, que também roteia modelos, comprime entradas e mantém scripts). O projeto é Apache-2.0 e se declara executado na máquina do usuário, com as próprias chaves e logins.

## Como funciona

### Seis componentes

| Componente | O que faz | Número citado no README |
|---|---|---|
| **Say less** | Respostas curtas em "voz de caverna"; código e payloads permanecem exatos | 63 → 20 tokens no mesmo diagnóstico |
| **Read less** | Comprime logs, JSON, CSV, YAML e saída de testes antes da leitura pelo modelo | 33,2% menos tokens de entrada por sessão |
| **Auto** | Escolhe modelo e esforço para cada pedido | 54% mais barato que Opus 5.5 em xhigh, com placar próximo |
| **Blocks** | Modo código: mantém no repositório os scripts que o agente escreve e os reutiliza | 397 → 76 tokens em uma execução de testes |
| **Waste fixes** | `caveman learn` ranqueia onde os tokens vão; mantém o cache de prompt aquecido em pausas | Não medido no README |
| **Browse** | Entrega páginas web comprimidas ao agente | 121 tokens em vez de 15.704 para uma tabela de 200 linhas |

`caveman status` mostra o que está ligado; `caveman off <componente>` desliga um item. Auto exige conta gratuita; os demais não.

### A voz

O README descreve a voz como um estilo controlado, não gramática quebrada. As regras publicadas:

- **Resposta primeiro:** `[coisa] [ação] [razão]. [próximo passo].`, sem saudação nem recapitulação.
- **Uma ideia por frase:** inspirada no ASD-STE100 (inglês controlado de manuais de manutenção aeronáutica), com até 20 palavras, voz ativa e um termo por conceito.
- **Significado preservado:** artigos podem sumir; negações, números e unidades não.
- **Payload literal:** código, comandos, caminhos e erros ficam caractere por caractere.
- **Sem teatro:** nada de interjeições nem conversa entre chamadas de ferramenta.
- **Exceções:** avisos de segurança, ações irreversíveis e usuários confusos recebem frases completas.
- **Prompt intocado:** o texto do usuário nunca é reescrito; o README cita pesquisa da Adobe segundo a qual "cavernizar" o prompt piora as respostas.

Há três intensidades: `/caveman`, `/ultracave` e `/megacave` (esta em chinês clássico), com 20, 14 e 13 tokens no exemplo do React.

### Compressão de entrada

O compressor atua sobre arquivos e saída de ferramentas. No conjunto de seis tipos de arquivo citado, o total cai de 130.611 para 22.994 tokens (82,4%); na sessão inteira do Claude Code, a redução medida é de 33,2%, porque o prompt de sistema e as ferramentas não encolhem. O README admite que HTML ainda não tem compressor e que esse caso ficou **9,9% pior** na sessão. Os arquivos originais permanecem no disco e podem ser relidos pelo agente.

### Auto, Blocks e Cloud

- **Auto** adiciona um modelo "Auto" ao seletor do agente, que decide modelo e esforço por pedido. O README reporta 43,7% das tarefas resolvidas a US$ 3,59 por tentativa, contra 44,3% a US$ 7,83 com Opus 5.5 em xhigh; o próprio README ressalva que o experimento está pela metade, que a diferença de 0,5 ponto está dentro do intervalo de confiança (±7) e que a maior parte da economia vem de baixar o esforço em pedidos fáceis.
- **Blocks** é o modo código: o agente escreve um script uma vez, o script fica versionado e é reutilizado. Vem com oito blocos (`json-peek`, `jsonl-stats`, `test-summary`, `first-error`, `wait-for`, `grep-defs`, `http-json`, `replace-in-file`), está em pré-release e é declarado Python-only, sem sandbox.
- **Caveman Cloud** é o produto separado para agentes que o usuário constrói: observabilidade de execuções, avaliações, mudanças propostas com aprovação por pull request e classificação dos números entre medidos, inferidos e verificados.
- **Middleware** oferece a mesma compressão dentro de chamadas ao Vercel AI SDK, LangChain, OpenAI ou Anthropic.

## Instalação e uso rápido

Instalação completa, com Node.js 22.13+:

```bash
npx @caveman-ai/cli@latest
```

O instalador detecta agentes e logins na máquina, mostra o que será alterado e, após confirmação, mantém o agente em modo caveman. O README declara suporte a Claude Code, Codex, Gemini CLI, OpenCode, Aider, Kilo, Qwen, Hermes, OpenClaw e `pi`, entre 30+ agentes ([matriz completa](https://github.com/JuliusBrussee/caveman/blob/main/INSTALL.md)).

Somente o skill, sem proxy:

```bash
npx skills add JuliusBrussee/caveman -g
```

Formas alternativas publicadas: plugin de marketplace do Claude Code, extensão do Gemini CLI, script `install.sh`/`install.ps1` e uso no Claude web/desktop/mobile via Customize → Plugins (não testado de ponta a ponta segundo o README). Para sair: `npx -y github:JuliusBrussee/caveman -- --uninstall` ou `npx skills remove JuliusBrussee/caveman -g`.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Diagnóstico de React:** o agente responde "New object ref each render, so React re-renders. Wrap the prop in `useMemo`." em vez de um parágrafo explicativo.
- **Sessões com logs e testes:** compressão de saída de teste e logs reduz o que entra no contexto.
- **Repetição de scripts:** `caveman-blocks scan` mostra scripts que o agente redigitou no mês; `caveman-blocks init` cria índice e regras no `AGENTS.md` do repositório.
- **Custo por tarefa:** `caveman trial -- claude` faz A/B de uma sessão real; `caveman stats` mostra o histórico de tokens.
- **Arquivos de memória:** `/caveman-compress <file>` reduz `CLAUDE.md` e similares mantendo títulos, blocos de código e caminhos, com backup do original.

## Quando usar (e quando não usar)

- **Use quando:** o custo por token importa, as sessões são longas, a maior parte da entrada vem de logs/JSON/testes e a equipe aceita um proxy local que altera o estilo das respostas.
- **Use quando:** há repetição de scripts de inspeção e vale mantê-los versionados como blocos.
- **Evite quando:** a cobrança é por requisição e não por token — o README observa que respostas mais curtas não economizam nada nesse modelo (ex.: GitHub Copilot).
- **Evite quando:** a tarefa exige prosa completa, explicações didáticas ou nuance que a compressão possa remover; a voz tem exceções, mas não é neutra.
- **Evite quando:** a política da organização proíbe telemetria ou envio de contexto a um serviço de roteamento; Auto passa pelo Caveman Cloud quando o modelo escolhido é da nuvem do projeto.
- **Alternativas:** reduzir contexto por seleção/grafo ([codebase-memory-mcp](../deusdata/codebase-memory-mcp.md)), restringir o escopo da resposta com skills minimalistas ([ponytail](../dietrichgebert/ponytail.md)) ou usar cache de prompt e modelos menores sem proxy.

## Limitações e cuidados

- **Somente o README foi lido.** Não foram verificados o código do proxy, os compressores, a precisão dos benchmarks nem o comportamento em cada agente suportado.
- **Números em grande parte autodeclarados.** O README cita Adobe Research, JetBrains e Elastic, mas os experimentos internos (Read less, Auto, Blocks, Browse) não foram reproduzidos nesta wiki.
- **Custo fixo do skill:** as regras consomem cerca de 1.160 tokens de entrada; em sessões curtas o ganho pode não cobrir esse custo.
- **Auto está incompleto:** o próprio README declara a execução pela metade e diferença de qualidade dentro da margem de erro; a economia vem sobretudo de reduzir esforço.
- **HTML piora:** sem compressor para HTML, a sessão medida ficou 9,9% maior.
- **Blocks é pré-release:** Python-only, sem sandbox, e pode conflitar com o hábito de escrever scripts ad hoc.
- **Telemetria ligada por padrão no CLI:** comandos, contagens de tokens, ID aleatório, SO e IP; prompts, código e caminhos não são enviados segundo o README. Desligar: `caveman telemetry off` ou `DO_NOT_TRACK=1`.
- **Auto e Cloud ampliam a superfície de dados:** o README detalha o que é enviado (pedido atual, anterior, fim da última resposta, nomes de ferramentas e contagens). Quem usa modelos próprios deve revisar a política.
- **Prompt do usuário não é reescrito**, mas a resposta é; avaliar qualidade em tarefas sensíveis continua necessário.
- **Marca registrada:** "Caveman" e o logotipo são marcas de Julius Brussee, apesar da licença Apache-2.0 do código.

## Estado e adoção

- **Versão citada:** 4.0 (notas de release `v4.0.0`; instaladores referenciam `v4.0.1`); Blocks em `v0.1.0-rc.5`.
- **Atividade e popularidade observadas em 2026-10-19:** 113.619 estrelas, 6.579 forks, 64 issues abertas; repositório criado em 2026-04-04, último push em 2026-10-19.
- **Licença:** Apache-2.0.
- **Linguagem principal (API):** Go.
- **Distribuição:** npm (`@caveman-ai/cli`), skills.sh, marketplace de plugins do Claude Code e extensão do Gemini CLI.
- **Sinais externos citados no README:** Adobe Research (paper CAVEWOMAN), JetBrains (A/B com 86 tarefas), Elasticsearch Labs, #1 no Hacker News e no GitHub Trending. Não verificados nesta wiki.

## Relações

- **Mantido por:** [juliusbrussee](../../../entities/juliusbrussee.md).
- **Conceitos:** [Economia de tokens em agentes](../../../concepts/economia-de-tokens-em-agentes.md) — o projeto é a instância mais visível do conjunto de técnicas; [Agent skills](../../../concepts/agent-skills.md) — a voz também é distribuída como skill isolada; [CLAUDE.md](../../../concepts/claude-md.md) — alvo do `/caveman-compress`; [Saída completa de agente](../../../concepts/saida-completa-de-agente.md) — postura oposta à voz telegráfica; [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md) — o componente Browse comprime páginas para o agente.
- **Alternativas:** [dietrichgebert/ponytail](../dietrichgebert/ponytail.md) — reduz o escopo do que é escrito, em vez de comprimir a linguagem; [DeusData/codebase-memory-mcp](../deusdata/codebase-memory-mcp.md) — reduz tokens ao indexar código em grafo, em vez de comprimir a saída.
- **Depende de:** Node.js 22.13+ para o instalador e o CLI.

## Perguntas abertas

- Os compressores de entrada preservam informação suficiente em logs de produção e saídas de teste ambíguas?
- Como o proxy intercepta chamadas de cada um dos 30+ agentes e o que acontece quando um deles muda o formato?
- A economia de 33,2% se mantém em sessões sem arquivos grandes de CSV/log, que dominam o benchmark?
- Qual é o efeito da voz na qualidade de revisões de código e explicações para usuários menos experientes?
- O roteamento do Auto é auditável, e como ele lida com dados sensíveis enviados ao Caveman Cloud?
- Blocks substitui scripts ad hoc sem introduzir dependência de uma coleção mantida por terceiros?

## Fontes

- README: https://github.com/JuliusBrussee/caveman/blob/main/README.md (commit `bad48a0e1df55e05e3f52249afa35ecc1909ee76`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório e do perfil `JuliusBrussee` via API do GitHub (consultados em 2026-10-19).
