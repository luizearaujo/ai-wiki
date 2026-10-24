---
type: repo
url: https://github.com/bytedance/deer-flow
host: github.com
owner: bytedance
repo: deer-flow
commit: fee0cd0c180874325305e995197db99f03fa6a6f
license: MIT
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, harness, super-agente, subagentes, sandbox, memoria, langgraph]
---

# bytedance/deer-flow

> Super agent harness open-source que orquestra subagentes, memória, sandboxes e skills extensíveis para tarefas longas de pesquisa, código e criação — reescrito do zero na versão 2.0.

## O que é

O DeerFlow (Deep Exploration and Efficient Research Flow) começou como framework de *deep research* e foi reconstruído como um **super agent harness**. A tese do README é que a comunidade usou o projeto para muito além de pesquisa — pipelines de dados, decks, dashboards, automação de conteúdo — e que o valor real estava em ser um runtime com infraestrutura para o agente trabalhar.

A versão 2.0 não compartilha código com a 1.x; o framework original de deep research permanece na branch `main-1.x`. O projeto é construído sobre LangGraph e LangChain e vem com filesystem, memória, skills, execução em sandbox e capacidade de planejar e gerar subagentes.

O README é notavelmente detalhado: documenta configuração, migrações, políticas de memória, limites de sandbox, papéis de mensagem, teardown e dezenas de decisões de engenharia. Esta página resume o que o README publica; a implementação não foi lida.

## Como funciona

O runtime roda dentro do **Gateway**, com uma interface web (Next.js) e uma TUI. O agente líder decompõe a tarefa e pode despachar subagentes com contexto, ferramentas e condições de término próprios.

### Componentes principais

| Componente | O que faz |
|---|---|
| **Skills** | Módulos Markdown (`SKILL.md`) com workflow, boas práticas e referências. Carregamento progressivo: só entram no contexto quando a tarefa precisa. Podem ser ativadas por `/skill-name` em um turno. |
| **Tools e MCP** | Catálogo no Capability Center; plugins incluem servidores MCP e integração Lark/Feishu. Skills podem declarar `allowed-tools`, aplicado após ativação explícita. |
| **Subagentes** | `task` com contexto isolado (padrão) ou snapshot do histórico do pai; o líder verifica e sintetiza resultados. Subagentes são otimização, não resposta padrão a qualquer tarefa complexa. |
| **Sandbox** | Execução isolada em Docker/AIO, hostPath, E2B ou provisioner; filesystem compartilhado por thread; projeção de skills habilitadas em `/mnt/skills`. |
| **Memória de longo prazo** | DeerMem é o backend local padrão, com fatos por usuário/agente em Markdown, índice FTS5/BM25 e gate determinístico de escopo/durabilidade. Backends opcionais: mem0, Honcho, [OpenViking](../volcengine/openviking.md). |
| **Context engineering** | Isolamento de subagentes, sumarização, offload de resultados para arquivos, compactação manual (`/compact`), metas de sessão (`/goal`) e orçamento de saída de ferramentas. |
| **Browser agêntico** | Grupo opcional com Playwright: navega, lê elementos interativos, clica, digita e envia formulários; cada ação devolve um snapshot com referências estáveis. |
| **Conhecimento privado** | Providers read-only como RAGFlow, LightRAG e WeKnora, com citações atribuíveis (provedor, documento, trecho). |
| **Canais e automação** | Telegram, Slack, Feishu/Lark, WeChat, WeCom e DingTalk; tarefas agendadas por cron; projetos com instruções e estante de documentos; cliente Python embutido. |

### Fluxo de uma execução

```text
pedido -> agente líder -> planejamento -> (subagentes em paralelo | ferramentas)
       -> sandbox/filesystem -> verificação e síntese -> resposta + artefatos
```

O Gateway registra checkpoints, uso de tokens, eventos de execução e recibos de entrega. A compactação substitui histórico antigo por resumo e mantém a requisição atual; subagentes longos também compactam e reinjetam o resumo como contexto durável.

### Segurança

O README trata o DeerFlow como software de alto privilégio: executa comandos, opera arquivos e chama lógica de negócio. O padrão é rodar em ambiente local confiável, acessível apenas por loopback. A pilha Docker publica a porta em `127.0.0.1`; para expor na rede é preciso definir `BIND_HOST` e implementar controles adicionais (allowlist de IP, autenticação forte, VLAN isolada).

O README também alerta que **admin do Gateway equivale a execução de código** (servidores MCP stdio rodam comandos no contêiner), que mensagens `system`/`developer` enviadas por clientes são rejeitadas e que a correção não reescreve checkpoints antigos.

## Instalação e uso rápido

Pré-requisitos: Docker + Docker Compose v2.24+ (caminho recomendado) ou Python 3.12+, Node.js 22+, pnpm, uv e nginx para desenvolvimento local.

**Docker (recomendado):**

```bash
make docker-init    # baixa a imagem de sandbox
make docker-start   # sobe os serviços
make docker-logs
```

**Desenvolvimento local:**

```bash
make check          # verifica Node 22+, pnpm, uv, nginx
make install        # dependências de backend e frontend
make setup-sandbox  # opcional: pré-baixa a imagem de sandbox
make dev
```

Acesso: `http://localhost:2026`.

**Produção com Docker:**

```bash
make up
make down
```

O README também publica um atalho para agentes de código: pedir que o agente clone o repositório e siga `Install.md` para fazer o bootstrap local.

## Exemplos de uso

Exemplos derivados do README:

- **Pesquisa longa:** pedir um relatório com pesquisa web, fontes citadas e geração de slides ou página web.
- **Delegação:** o agente líder cria subagentes para subtarefas independentes e sintetiza os relatórios.
- **Automação recorrente:** agendar uma tarefa por cron e receber o resultado em um canal de mensagem.
- **Meta persistente:** `/goal finish the implementation and make all tests pass` mantém a meta ativa entre turnos e compactações.
- **Conhecimento privado:** configurar RAGFlow ou LightRAG e pedir respostas com citações de documentos internos.
- **Navegador:** habilitar o grupo `browser` para operar um site JavaScript-heavy em vez de apenas ler o HTML.

## Quando usar (e quando não usar)

- **Use quando:** você quer um super agente self-hosted para tarefas longas e multietapa, com subagentes, memória, sandbox, skills e canais de mensagem; precisa de citações e conhecimento privado; quer um runtime em Python/LangGraph que possa ser estendido.
- **Evite quando:** você precisa de um agente leve de linha de comando; não quer operar Docker/sandbox; não pode garantir ambiente de rede confiável; ou busca um produto SaaS sem manutenção.

## Limitações e cuidados

- **Somente o README foi lido.** Código, `backend/docs/`, `docs/`, `Install.md` e configuração de exemplo não foram verificados.
- **Superfície de segurança alta.** Execução de comandos, filesystem, navegador e MCP significam que uma exposição de rede mal configurada é grave. O README recomenda loopback e controles adicionais.
- **Complexidade operacional.** Docker, sandbox, banco, memória, múltiplos workers, proxies e migrações exigem operação cuidadosa. O README dedica muitas seções a casos de borda e recuperação.
- **Modelo e custo.** O projeto é model-agnostic via API OpenAI-compatible, mas desempenho depende de contexto longo, raciocínio, multimodalidade e bom tool use; tarefas longas podem consumir muitos tokens.
- **Memória é contexto não confiável.** O README descreve gates e isolamento por usuário/agente, mas memória continua sendo dado que pode envelhecer, conflitar ou ser envenenado.
- **Alegações de adoção.** Stars, forks e posição em trending são observações datadas, não evidência de qualidade.
- **Licença MIT**, mas dependências, modelos e serviços externos têm licenças e custos próprios.

## Estado e adoção

- Versão citada: **2.0**, reescrita sem código compartilhado com a 1.x. A branch `main-1.x` mantém o framework original.
- Observado em 2026-10-19: ~84.130 stars, ~11.741 forks, ~952 issues abertas; criado em 2025-05-07; último push em 2026-10-19.
- Licença: MIT.
- Linguagem principal na API: Python (frontend em TypeScript/Next.js).
- Site oficial: [deerflow.tech](https://deerflow.tech).

## Relações

- Mantido por: [bytedance](../../../entities/bytedance.md)
- Conceitos: [Agent harness](../../../concepts/agent-harness.md), [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md), [Memória de agente](../../../concepts/memoria-de-agente.md), [Agent skills](../../../concepts/agent-skills.md), [Model Context Protocol](../../../concepts/model-context-protocol.md)
- Relacionado: [HarnessMD/munder-difflin](../harnessmd/munder-difflin.md) — harness desktop que também orquestra agentes com memória e mensageria; [garrytan/gstack](../garrytan/gstack.md) e [affaan-m/ECC](../affaan-m/ecc.md) — processos e catálogos sobre CLIs existentes; [SynkraAI/aiox-core](../synkraai/aiox-core.md) — orquestração por artefatos.
- Projetos citados: LangGraph, LangChain, AIO Sandbox, E2B, Playwright, RAGFlow, LightRAG, WeKnora, DeerMem, mem0, Honcho, [OpenViking](../volcengine/openviking.md).

## Perguntas abertas

- Como o agente líder decide quando vale a pena criar subagentes, e como mede o ganho?
- Qual é a latência e o custo de tokens de uma tarefa longa com memória, sandbox e compactação?
- Como o DeerMem evita memória envenenada e vazamento entre usuários e agentes na prática?
- Qual é o nível real de isolamento do sandbox em cada backend (Docker, AIO, E2B, provisioner)?
- Como o projeto lida com atualizações de esquema e migrações em produção?
- Que partes do README são políticas implementadas e quais são recomendações operacionais?
- Como se compara a um harness de engenharia como ECC ou gstack em tarefas de código?

## Fontes

- README: https://raw.githubusercontent.com/bytedance/deer-flow/fee0cd0c180874325305e995197db99f03fa6a6f/README.md (commit `fee0cd0c180874325305e995197db99f03fa6a6f`, consultado em 2026-10-19). Somente o README foi lido; `backend/docs/`, `docs/`, código e demais arquivos não foram consultados.
- Metadados: API do GitHub (`/repos/bytedance/deer-flow`) em 2026-10-19.
