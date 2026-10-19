---
type: repo
url: https://github.com/HarnessMD/munder-difflin
host: github.com
owner: harnessmd
repo: munder-difflin
commit: 436d65a74a69d347c57641fbace4eb822bf98600
license: MIT
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, harness, orquestracao, multi-agente, electron, memoria, desktop]
---

# HarnessMD/munder-difflin

> Aplicativo desktop que transforma CLIs de agentes já instalados — Claude Code, Codex, Gemini, Grok, Kimi e outros — em funcionários de um escritório virtual, coordenados por um agente-orquestrador chamado Michael, com memória compartilhada, caixas de mensagem e um quadro de tarefas.

## O que é

O Munder Difflin é um harness desktop (Electron + React + TypeScript) que não implementa um agente próprio: ele **embrulha CLIs de terminal reais** em pseudo-terminais e os apresenta como avatares em um escritório 2D. A metáfora é uma paródia de *The Office* — "Munder Difflin" em vez de Dunder Mifflin — e o README a leva a sério: cada sessão ganha uma mesa, uma identidade e uma caixa de correio; o usuário fala com um único agente, seu "clone" Michael, que distribui o trabalho.

A promessa é usar as assinaturas que o usuário já paga, rodando tudo localmente (ou em sandboxes), em vez de cobrar outra assinatura de um produto SaaS de agentes. A descrição da API do GitHub posiciona o projeto como "alternativa open source aos dots, bots e muses do mercado".

CLIs suportados segundo o README: **Claude Code** (`claude`, o padrão), **Antigravity** (`agy`), **OpenAI Codex** (`codex`), **xAI Grok** (`grok`), **Kimi Code** (`kimi`), **Gemini CLI** (`gemini`), **Qwen** (`qwen`), **OpenCode** (`opencode`), **Crush** (`crush`), **pi.dev** (`pi`), **GitHub Copilot** (`copilot`), **Cursor** (`cursor-agent`) e qualquer comando customizado. Também aceita chaves próprias e modelos locais via Ollama, LM Studio ou vLLM.

## Como funciona

O usuário fala com Michael, o agente "GOD" que ocupa o escritório do orquestrador. Ele mantém roster, roteamento, adjudicação, blackboard e task ledger; resolve pedidos rotineiros sozinho e escala apenas itens críticos — gasto, operações destrutivas e mudança de escopo — para uma fila de aprovação humana.

```text
            você ── conversa ──►  ┌─────────────┐
                                  │  GOD agent  │  orquestrador / supervisor
                                  │  (Michael)  │  roster · roteamento · adjudicação
                                  └──────┬──────┘
                                         │ atribui · roteia · escala
                ┌────────────────────────┼────────────────────────┐
                ▼                        ▼                        ▼
          ┌───────────┐           ┌───────────┐           ┌───────────┐
          │  agent A  │ mensagem  │  agent B  │ mensagem  │  agent C  │
          │ provider  │ ────────► │ provider  │ ────────► │ provider  │
          │  + memory │           │  + memory │           │  + memory │
          └───────────┘           └───────────┘           └───────────┘
                └──── hive compartilhado: memória · mailbox · blackboard · log ────┘
```

O **hive** é um repositório git local de arquivos simples. Cada agente escreve no próprio `outbox/`; o router do harness entrega em `inbox/` dos destinatários. Nenhum agente executa git diretamente — o desenho de **committer único** evita corrupção de `index.lock`. O hive combina memória por agente, mailbox atômica, blackboard compartilhado e log de eventos append-only.

Na arquitetura descrita, dois planos alimentam um renderer: o **plano de terminal** possui os PTYs (`node-pty`), o filesystem e o git; o **plano de eventos** roda o hive, o servidor de hooks e o router. O renderer conversa com ambos apenas por uma ponte tipada. A UI desenha os avatares com Pixi.js e os terminais com xterm.js.

## Recursos principais

- **Um processo real por agente.** Cada sessão é o CLI original rodando em PTY, com terminal vivo, histórico e possibilidade de digitar de volta.
- **Escritório visual.** Avatares caminham até estações, envelopes voam entre mesas e o estado reflete o trabalho real.
- **Memória persistente.** Memória Markdown por agente, minerada para um "palácio" compartilhado com índice de recall semântico; o README promete recall em milissegundos.
- **Autonomia com limite.** Configuração por agente e circuit breaker em escada *steer → constrain → stop* para agentes que entram em loop, estouram erros ou orçamento.
- **Command Center.** Kanban com dependências, tickets com chave (ex.: `V53-299`), missões agendadas com heartbeat, monitoramento de frota, busca de memória, log de atividade e CI watcher.
- **IDE embutido.** Monaco com árvore de arquivos, abas, save e trilhos git (CHANGES, HISTORY, COMPARE, grafo de commits, diffs e checkout protegido).
- **Entrada e saída de trabalho.** Slack e webhooks com workers efêmeros, hires compartilháveis via `munderdifflin://hire`, Agent Gallery e catálogo de 227 skills adicionais.
- **Voz local.** Ditado em qualquer app e transcrição de reuniões com os dois lados da chamada ("Stapler", parte do Pro), usando Whisper embarcado por padrão.
- **Múltiplos andares.** Vários escritórios independentes, cada um em sua pasta/janela, com uma licença cobrindo todos.
- **Pro.** Capabilities (catálogo de MCP servers, skills, plugins e ferramentas), agent files exportáveis, Teams entre escritórios de colegas, sidebar ampliada e limites de tokens por período.

## Instalação e uso rápido

O caminho recomendado é baixar o app em [harnessmd.com/download](https://harnessmd.com/download): há builds assinados e notarizados para macOS, além de Windows e Linux; a versão open source fica nas releases do GitHub. O usuário **não precisa de Node nem do repositório** para usar o aplicativo, mas precisa de pelo menos um CLI de agente instalado. A partir da 0.5.3, um CLI ausente aparece como card no terminal do agente, com instalação e login dentro do app.

Para construir a partir do código:

```bash
git clone https://github.com/chaitanyagiri/munder-difflin.git
cd munder-difflin
npm install        # o postinstall recompila node-pty contra a ABI do Electron
npm run dev        # inicia o app Electron com hot reload
```

Pré-requisitos de build: macOS, Windows ou Linux; Node.js 18+ e npm; toolchain C/C++ para o addon nativo do `node-pty`; pelo menos um CLI suportado no `PATH`. Scripts auxiliares: `npm run build` (electron-vite), `npm run preview` e `npm run typecheck`.

> **A verificar:** o README em `HarnessMD/munder-difflin` ainda usa links e comandos do owner antigo, `chaitanyagiri/munder-difflin`, incluindo o comando de clone e as mídias. O redirecionamento do GitHub provavelmente cobre o clone, mas o caminho canônico atual é `HarnessMD/munder-difflin`.

## Exemplos de uso

O README descreve fluxos, não scripts de API:

- Contratar um agente escolhendo CLI, modelo e nível de autonomia, atribuindo uma mesa, e importar um papel pronto da Agent Gallery.
- Mandar uma tarefa pelo Slack ou webhook; Michael pode criar um worker efêmero, responder na thread e destruí-lo.
- Abrir um segundo "andar" para outro projeto, com board e memória próprios, mantendo uma licença para todos.
- Exportar um agente como arquivo (Pro) com o que deve ir — sem chaves, tokens ou valores de segredos — e reutilizar um dos 36 templates.
- Ditar em qualquer aplicativo (Option no Mac; Control+Alt+Space em Windows/Linux X11) e enviar a transcrição para um agente.

## Quando usar (e quando não usar)

- **Use quando:** você já usa assinaturas de CLIs de código e quer orquestrar vários em paralelo com memória, mensageria e supervisão visível; quer acompanhar o trabalho de perto e intervir em qualquer terminal; valoriza rodar localmente com os próprios logins.
- **Evite quando:** você precisa de software estável e previsível (o projeto se declara **pre-release**); não pode pagar ou não quer o modelo Pro; precisa de paridade de recursos entre sistemas operacionais; ou quer uma solução leve de linha de comando. Para um processo de engenharia mais estruturado em um único harness, compare com [affaan-m/ECC](../affaan-m/ecc.md) ou [garrytan/gstack](../garrytan/gstack.md).

## Limitações e cuidados

- **Pré-release.** O próprio README marca status `pre-release` e a versão 0.5.6. Há recursos anunciados como próximos (Telegram, mais engines, cobertura de avatares, histórico de layout).
- **Modelo comercial.** O código é MIT, mas o app tem uma edição Pro: Capabilities, agent files, Stapler, Teams e a sidebar nova. O README diz que o Pro é gratuito até 24 de outubro de 2026 e depois custa US$ 150/ano, com ajuste por poder de compra (até US$ 100/ano). A fronteira real entre grátis e Pro não foi verificada no código.
- **Licença de assets separada.** O código-fonte é MIT, mas os tilesets de pixel art são licenciados à parte pela LimeZu (Modern Interiors, Complete Version) e exigem atribuição; `LICENSE-ASSETS` faz o carve-out. O projeto é uma paródia e não tem afiliação com a NBC.
- **Muitas integrações e credenciais.** CLIs de terceiros, chaves BYOK, Slack, webhooks, servidores MCP e modelos locais ampliam a superfície de ataque e a complexidade operacional. O README descreve gates humanos e circuit breaker, mas a aplicação real dessas políticas não foi verificada.
- **Telemetria.** Builds oficiais enviam eventos anônimos de uso (app aberto, agente iniciado, recurso usado) e, segundo o README, nunca prompts, código, caminhos ou output. Há opt-out por Settings, `DO_NOT_TRACK`, ou build a partir do código (forks não enviam nada).
- **Alegações de desempenho.** "A camada de memória mais rápida do mundo" e o ganho de ~37% em tokens são afirmações do projeto; o próprio README ressalva que a medição de tokens foi uma *replay*, não uma medição ao vivo.
- **README defasado.** Links para `chaitanyagiri/munder-difflin`, download, mídias e issues ainda apontam para o owner anterior; não foram verificados redirecionamentos de todos os endpoints.
- **Escopo do que foi lido.** Apenas o README foi consultado. `HIVE.md`, `SPEC.md`, `DESIGN.md`, `docs/ARCHITECTURE.md`, `TELEMETRY.md`, `CONTRIBUTING.md` e o código não foram lidos.

## Estado e adoção

- Versão citada: **0.5.6**; status declarado: **pre-release**. A 0.5.3 trouxe ditado e transcrição, múltiplos andares e tickets com chave; a 0.5.6 acrescentou Capabilities, Integrations, Teams, agent files e limites de tokens por período.
- Observado em 2026-10-19: ~8.905 stars, ~1.232 forks, ~252 issues abertas; último push em 2026-10-19; criado em 2026-05-31.
- Licença: MIT para o código; assets sob licença própria da LimeZu.
- Linguagem principal na API: TypeScript.

## Relações

- Mantido por: [HarnessMD](../../../entities/harnessmd.md)
- Conceitos: [Agent harness](../../../concepts/agent-harness.md), [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md)
- Relacionado: [affaan-m/ECC](../affaan-m/ecc.md) e [garrytan/gstack](../garrytan/gstack.md) — também instalam processo e especialistas sobre CLIs existentes, mas sem a metáfora de escritório nem o modelo de hive; [SynkraAI/aiox-core](../../../repos/github.com/synkraai/aiox-core.md) — orquestração multiagente por artefatos; [croffasia/itsaplan](../../../repos/github.com/croffasia/itsaplan.md) — outra proposta de agentes trabalhando em um board compartilhado.
- Projetos citados: [HarnessMD/awesome-agent-capabilities](https://github.com/HarnessMD/awesome-agent-capabilities), Agent Gallery, [LimeZu](https://limezu.itch.io/).

## Perguntas abertas

- Como o hive evita perda de mensagens e como o committer único escala com muitos agentes?
- Como as aprovações humanas e o circuit breaker são aplicados tecnicamente — hooks, intercepção do PTY ou configuração do CLI?
- A memória semântica funciona igual em macOS, Windows e Linux, e qual é o custo de indexação?
- Qual é a divisão exata entre o app gratuito e o Pro, e como a licença é verificada?
- Os 12 CLIs têm o mesmo nível de suporte (hooks, retomada de sessão, instalação interna)?
- Como o app isola credenciais e segredos entre agentes e entre andares?
- O que muda quando o repositório canônico é `HarnessMD` mas os links apontam para `chaitanyagiri`?

## Fontes

- README: https://raw.githubusercontent.com/HarnessMD/munder-difflin/436d65a74a69d347c57641fbace4eb822bf98600/README.md (commit `436d65a74a69d347c57641fbace4eb822bf98600`, consultado em 2026-10-19). Somente o README foi lido; `HIVE.md`, `SPEC.md`, `DESIGN.md`, `docs/`, código e demais arquivos não foram consultados.
- Metadados: API do GitHub (`/repos/HarnessMD/munder-difflin`) em 2026-10-19.
