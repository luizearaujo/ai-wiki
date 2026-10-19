---
type: repo
url: https://github.com/vastsa/PI-Desktop
host: github.com
owner: vastsa
repo: pi-desktop
commit: 87a48b953e8bada43a7a63f8922846198b9efb61
license: LGPL-3.0
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, desktop, local-first, plugins, orquestracao, harness, electron, rust, mcp]
---

# vastsa/PI-Desktop

> Workspace desktop modular para agentes de IA, que reúne projetos, sessões, modelos, plugins e workflows em um ambiente local-first, sem depender de IDE ou terminal.

## O que é

O README posiciona o PI-Desktop como uma terceira camada, depois dos agentes de terminal (fortes em execução) e dos agentes de IDE (fortes dentro do editor): um **workspace desktop próprio do agente**, persistente e extensível. A promessa é que projetos, sessões, revisões, previews e agentes vivam em um ambiente independente, e não como abas descartáveis.

O produto é declarado como **local-first**, **model-agnostic** e **plugin-powered**, com builds para macOS, Windows e Linux. A linha de release atual é **0.21.x (Early Preview)**.

A descrição do repositório na API do GitHub resume a stack como “Electron + Rust host core + pi Agent Harness + user-installable plugins”. O README confirma o host core em Rust (`cargo build -p host-core`) e o runtime `pi`, mas não nomeia o Electron nem detalha a divisão entre as camadas.

## Como funciona

### Quatro pilares

| Pilar | O que o README promete |
|---|---|
| **Workspace independente** | Sem dependência de IDE ou terminal; projetos, sessões, revisões, previews e agentes no mesmo workspace. |
| **Plugins** | Extensões que adicionam painéis, views, widgets, ferramentas, servidores MCP, temas e serviços em background. |
| **Orquestração** | Subagentes em background ou Worker Sessions completas coordenadas por uma sessão principal. |
| **Liberdade de modelo** | Modelos em nuvem, locais, gateways próprios e APIs compatíveis, trocáveis sem refazer o workflow. |

### Plugins como parte do produto

O Core é mantido pequeno, e o workflow real é montado por extensões em três camadas:

- **Agente:** Agent Tools, Skills, Completion e pi Extensions.
- **Workspace:** Commands, Panels, Work Panel Views, Floating Widgets e Themes.
- **Plataforma:** MCP Servers, Resident Services e Plugin Message Bus.

Uma extensão pode ser um produto inteiro — o README cita como exemplos um agente de voz (widget flutuante + serviço de fala + agent tool + comandos), um workspace de GitHub (painel + MCP + tools + serviço) e analytics de sessão (dashboard + comandos + view). Plugins são distribuídos como pacotes `.piplug` ou pelo marketplace.

### Modos de trabalho e delegação

Há três modos: **Agent** (executa a tarefa), **Plan** (estuda o projeto e produz um plano antes da execução) e **Goal** (objetivo e critérios de aceitação são fixados, e o agente conduz a execução). Operações privilegiadas passam pela camada de permissão independentemente do modo.

Para trabalho paralelo, existem dois níveis:

- **Subagentes:** trabalho independente em background (exploração de código, implementação, análise de testes, pesquisa, revisão), cada um com contexto próprio e resultado devolvido ao agente pai.
- **Session Orchestrator:** delegação para **Worker Sessions** completas, com contexto e execução independentes, inspecionáveis, reutilizáveis e com transcript integral.

### Sessões persistentes

A organização é **Project → Session → Agent → Work**, não em torno de chats descartáveis. O README lista sessões que continuam entre execuções do app, pin/archive/branch/search, fila de prompts enquanto o agente trabalha, referência a arquivos com `@`, slash commands, revisão de diffs, inspeção de saída de comandos, Work Panel à direita, checkpoints de streaming e recuperação de trabalho interrompido quando possível.

O app também importa sessões locais de **Claude Code, Codex, OpenCode e Pi**.

### Modelos e permissões

Cada modelo é configurado com provider, model ID, context window, output limit, reasoning/thinking, temperatura, OAuth, API key e endpoint. Sessões diferentes podem usar modelos diferentes, e a mesma sessão pode trocar de modelo a qualquer momento — o README exemplifica planejamento, código, revisão e tarefa privada com modelos distintos.

O agente pode ler arquivos, editar código, executar comandos, chamar ferramentas, usar extensões e delegar. A camada de permissão decide **Allow / Ask / Deny** por operação, e o usuário define o grau de autonomia de cada sessão.

### Local-first

| Dado | Comportamento padrão |
|---|---|
| Projetos, sessões, configurações e logs | Local |
| Credenciais de API | OS Keychain |
| Telemetria do PI-Desktop | Nenhuma |
| Requisições a modelos | Enviadas diretamente ao provider configurado |

Não há conta obrigatória nem relay obrigatório do PI-Desktop. Em modelos remotos, o contexto necessário é enviado diretamente ao provider.

### Base técnica

O runtime é construído sobre o ecossistema [pi](https://github.com/badlogic/pi-mono), usando `pi-ai`, `pi-agent-core` e `pi-coding-agent`. O README é explícito: o Pi fornece o engine do agente; o PI-Desktop adiciona o workspace persistente, sessões, permissões, plugins e orquestração. Do código-fonte, o build do host core é feito com `cargo build -p host-core`.

## Instalação e uso rápido

O caminho principal é baixar o instalador da [última release](https://github.com/vastsa/PI-Desktop/releases/latest):

| Plataforma | Arquitetura | Pacote |
|---|---|---|
| macOS | Apple Silicon / Intel | `.dmg` / `.zip` |
| Windows | x64 | Instalador / `.zip` |
| Linux | x64 / ARM64 | `.AppImage` / `.deb` / `.rpm` / `.asar` |

Releases de macOS são assinadas com Developer ID e notarizadas pela Apple. No Linux, os pacotes exigem **glibc 2.35+**; o README cita Ubuntu 22.04+, Debian 12+ e Fedora 36+.

Fluxo de onboarding: instalar, conectar um provider, abrir um projeto local e começar em Agent, Plan ou Goal.

Para rodar do código-fonte:

```bash
git clone https://github.com/vastsa/PI-Desktop.git
cd PI-Desktop
pnpm install
cargo build -p host-core
pnpm build:js
pnpm dev
```

Requisitos: Node.js `>=22.19`, pnpm `>=10` e toolchain Rust estável. Validação: `pnpm typecheck`, `pnpm lint` e `pnpm test`.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Desenvolvimento diário:** abrir o repositório, usar o modo Agent para ler/editar/testar e revisar diffs no Work Panel.
- **Refatoração de risco:** usar o modo Plan para receber um plano antes de permitir a execução.
- **Trabalho longo:** fixar objetivo e critérios no modo Goal, com sessão persistente entre execuções do app.
- **Trabalho paralelo:** delegar exploração e revisão a subagentes, ou dividir frontend, backend, testes e revisão entre Worker Sessions.
- **Mistura de modelos:** planejar com um modelo, implementar com outro, revisar com um terceiro e tratar tarefas privadas com um modelo local.
- **Extensão do workspace:** instalar um plugin de voz, de GitHub ou de analytics, ou criar um a partir dos templates `panel-basic`, `agent-tool-basic`, `skill-pack` e `full-demo`.

## Quando usar (e quando não usar)

- **Use quando:** você quer um workspace de agente independente do IDE e do terminal, com sessões persistentes, orquestração de workers, troca de modelo e extensibilidade por plugins.
- **Use quando:** o time precisa empacotar um fluxo de agente como produto desktop — painéis, widgets, MCP e serviços — mantendo o Core pequeno.
- **Evite quando:** um CLI ou uma extensão de IDE já cobre o fluxo e a equipe não quer manter mais um runtime desktop; ou quando a política da organização exige um harness auditado e de código aberto com histórico estável, já que o projeto está em Early Preview.
- **Alternativas documentadas:** [HarnessMD/munder-difflin](../harnessmd/munder-difflin.md) também é um app desktop multiagente, mas embrulha CLIs de terminal em PTYs em vez de embarcar um runtime próprio; [affaan-m/ECC](../affaan-m/ecc.md) e [garrytan/gstack](../garrytan/gstack.md) operam sobre CLIs existentes.

## Limitações e cuidados

- **Somente o README foi lido.** Não foram verificados código, arquitetura interna, sandbox de plugins, curadoria do marketplace nem a implementação da camada de permissão.
- **Early Preview:** a linha 0.21.x é declarada como prévia; APIs de plugin e formato `.piplug` podem mudar.
- **Plugins são superfície de confiança:** o README lista Message Bus, serviços residentes e MCP, mas não descreve isolamento, revisão de código ou assinatura de pacotes do marketplace. É a mesma questão de supply chain de outras extensões de agente.
- **Electron e Rust não são detalhados no README:** a descrição da API cita Electron, e o README cita o host core em Rust; a divisão de responsabilidades e o modelo de segurança entre processos **A verificar**.
- **Dependência do ecossistema `pi`:** a evolução do `pi-agent-core` e do `pi-coding-agent` afeta diretamente o produto; o README não fixa versões nem política de atualização.
- **Local-first não significa ausência de rede:** com modelos remotos, o contexto é enviado ao provider. Privacidade depende de qual provider e modelo são configurados.
- **Licença LGPL-3.0:** diferente de MIT/Apache de vários harnesses da wiki; integração e redistribuição exigem atenção às obrigações da licença.
- **Importação de sessões** de Claude Code, Codex, OpenCode e Pi é anunciada, mas o README não detalha formatos suportados, perda de informação ou limites.

## Estado e adoção

- **Release citada:** linha 0.21.x (Early Preview).
- **Atividade e popularidade observadas em 2026-10-19:** ~7,0 mil estrelas, 677 forks, 211 issues abertas; último push em 2026-10-19; repositório criado em 2023-03-22.
- **Licença:** GNU Lesser General Public License v3.0 (LGPL-3.0).
- **Linguagem principal (API):** TypeScript.
- **Documentação:** [pi-docs.aiuo.net](https://pi-docs.aiuo.net/), com links para arquitetura, especificação, desenvolvimento de plugins, plano de testes E2E e runbook de release.
- **Desenvolvimento declarado:** mais de 27 bilhões de tokens usados em desenvolvimento, refatoração, revisão, design e depuração.

## Relações

- **Mantido por:** [vastsa](../../../entities/vastsa.md).
- **Conceitos:** [Agent harness](../../../concepts/agent-harness.md) — o PI-Desktop embarca um engine de agente e adiciona o workspace; [Plugins de agente](../../../concepts/plugins-de-agente.md) — o mecanismo central de extensão; [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — subagentes e Worker Sessions; [Memória de agente](../../../concepts/memoria-de-agente.md) — sessões persistentes e retomada; [Model Context Protocol](../../../concepts/model-context-protocol.md) — plugins podem expor servidores MCP.
- **Alternativas:** [HarnessMD/munder-difflin](../harnessmd/munder-difflin.md) — escritório desktop sobre CLIs; [affaan-m/ECC](../affaan-m/ecc.md) e [garrytan/gstack](../garrytan/gstack.md) — harnesses sobre CLIs existentes.
- **Depende de:** [pi (badlogic/pi-mono)](https://github.com/badlogic/pi-mono) — runtime `pi-ai`, `pi-agent-core` e `pi-coding-agent`; não documentado na wiki.

## Perguntas abertas

- O core em Rust e o app Electron trocam quais dados, e onde ficam os limites de confiança?
- Como o marketplace de plugins revisa, assina e versiona pacotes `.piplug`?
- A camada de permissão Allow/Ask/Deny é imposta no host core, no runtime `pi` ou na interface?
- Como as Worker Sessions isolam filesystem, git e credenciais entre si?
- Que informação é preservada e perdida ao importar sessões de Claude Code, Codex, OpenCode e Pi?
- O formato de plugin e o runtime `pi` têm compatibilidade garantida entre versões?
- Como o produto se compara, na prática, a um CLI + IDE + worktrees para o mesmo fluxo?

## Fontes

- README: https://github.com/vastsa/PI-Desktop/blob/main/README.md (commit `87a48b953e8bada43a7a63f8922846198b9efb61`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório e do perfil `vastsa` via API do GitHub (consultados em 2026-10-19).
