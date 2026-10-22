---
type: repo
url: https://github.com/OpenHands/OpenHands
host: github.com
owner: OpenHands
repo: OpenHands
commit: c8a20662d5ddaa8b298b81a9ee6be90b5d86b2db
license: MIT
language: TypeScript
status: active
created: 2026-10-22
ingested: 2026-10-22
updated: 2026-10-22
tags: [agentes, harness, automacao]
---

# OpenHands/OpenHands

> Centro de controle self-hosted, chamado "Agent Canvas", que roda e automatiza agentes de codificação (OpenHands, Claude Code, Codex, Gemini, Pi, OpenCode ou qualquer agente compatível com ACP) sobre múltiplos backends locais, remotos ou em nuvem.

## O que é

O README atual descreve o repositório principal da organização (antes `All-Hands-AI`, hoje `OpenHands` — o GitHub redireciona a URL antiga para a nova) não como o agente autônomo de desenvolvimento em si, mas como **Agent Canvas**: um "developer control center" self-hosted para iniciar conversas com agentes de codificação e automatizar tarefas recorrentes, como gerar relatórios publicados no Slack ou decompor issues do GitHub em tarefas. É uma reestruturação relevante do projeto — ver "Perguntas abertas".

Agent Canvas roda localmente por padrão, mas conecta-se a múltiplos "agent backends": containers Docker, VMs ou infraestrutura da própria empresa, com a opção de usar a OpenHands Cloud ou Enterprise. O agente open source OpenHands roda prontamente, mas agentes de terceiros (Claude Code, Codex, Gemini CLI, Pi, OpenCode) também são suportados.

## Como funciona

Agent Canvas é o frontend; a lógica do agente vive em repositórios separados da mesma organização:

| Repositório | Responsabilidade |
|---|---|
| `OpenHands/OpenHands` (este) | Frontend Agent Canvas, seleção de backend, orquestração do stack local. |
| `OpenHands/software-agent-sdk` | SDK Python, Agent Server, agentes, ferramentas, conversas, workspaces e a API canônica do servidor. |
| `OpenHands/typescript-client` | Cliente TypeScript compatível com browser para a API do Agent Server. |
| `OpenHands/automation` | Definições de automação, agendamento, webhooks, histórico de execuções. |

O Agent Server (do SDK) expõe uma REST API para rodar múltiplos agentes em uma única máquina; o Canvas pode se conectar a vários Agent Servers e alternar entre eles. Um Automation Server opcional permite agentes acionados por agendamento ou evento.

## Instalação e uso rápido

- **Sem sandbox** (acesso total ao filesystem): `npm install -g @openhands/agent-canvas && agent-canvas` — requer Node.js 24+ e `uv`.
- **Com sandbox Docker**: `docker run -it --rm -p 127.0.0.1:8000:8000 ... ghcr.io/openhands/agent-canvas:1.30.1`, com `PROJECTS_PATH` montado.
- **Múltiplos sandboxes Docker**: `OH_CONVERSATION_RUNTIME=docker agent-canvas`, cada conversa isolada em seu próprio container.
- **A partir do código-fonte**: `git clone` + `npm install` + `npm run dev`.

UI acessível em `http://localhost:8000` (ou `/canvas` na imagem Docker). Variáveis como `AGENT_CANVAS_ALLOW_LAN_SESSION_KEY`, `OH_BIND_HOST` e `LOCAL_BACKEND_API_KEY` controlam exposição de rede e injeção de chave de sessão — o README recomenda cuidado ao publicar fora de `127.0.0.1`.

## Exemplos de uso

- Executar o agente OpenHands padrão localmente para conversas de desenvolvimento, exemplo derivado do README.
- Conectar o Canvas a um Agent Server compartilhado pela equipe para revisão de código e atualização de dependências, enquanto agentes pessoais rodam no laptop — exemplo citado no README.
- Automações agendadas ou por webhook integradas a Slack, GitHub, Linear e outros serviços de terceiros.

## Quando usar (e quando não usar)

- **Use quando:** quer um painel único para alternar entre vários agentes de codificação (próprios ou de terceiros) e vários backends, com automações recorrentes.
- **Evite quando:** só precisa de um agente de codificação simples sem múltiplos backends ou automações — um CLI de agente isolado (Claude Code, Codex) é mais direto. Rodar sem sandbox dá ao agente acesso total ao filesystem da máquina; o próprio README marca isso como aviso.

## Limitações e cuidados

- O README não detalha pricing do OpenHands Cloud/Enterprise, benchmarks de desempenho do agente OpenHands nem o roadmap do agente "clássico" anterior ao pivô para Agent Canvas.
- Badge do README marca o projeto como "status: beta".
- Segurança de hardening remete a `docs/SELF_HOSTING.md`, não detalhada no próprio README.
- Apenas o README foi lido; `docs/`, código-fonte e os demais repositórios da organização não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: imagem Docker `ghcr.io/openhands/agent-canvas:1.30.1`; última release no GitHub, `v1.30.1` (2026-10-22).
- Atividade e popularidade observadas em 2026-10-22: 91.548 estrelas, 12.152 forks (GitHub API); projeto com push no mesmo dia.
- Licença: MIT.

## Relações

- Mantido por: [OpenHands](../../../entities/openhands.md) (antes All-Hands-AI).
- Conceitos: [Agent harness](../../../concepts/agent-harness.md).
- Alternativas: não concorre diretamente com os agentes que orquestra (Claude Code, Codex, Gemini CLI, Pi, OpenCode) — ele os integra como backends via ACP.

## Perguntas abertas

- O que aconteceu com o agente OpenHands "clássico" (antigo OpenDevin, agente autônomo de desenvolvimento) agora que o README do repositório principal descreve um control center multi-backend? A lógica do agente parece ter migrado para `OpenHands/software-agent-sdk`.
- Como o Agent Canvas se diferencia, em uso prático, de simplesmente abrir vários terminais com CLIs de agente?

## Fontes

- README: https://raw.githubusercontent.com/OpenHands/OpenHands/c8a20662d5ddaa8b298b81a9ee6be90b5d86b2db/README.md (commit `c8a20662d5ddaa8b298b81a9ee6be90b5d86b2db`, consultado em 2026-10-22). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
