---
type: repo
url: https://github.com/sandbox-quantum/switch
host: github.com
owner: sandbox-quantum
repo: switch
commit: 233649fff5d58a8ed550eeff28f74f738aba79b0
license: Apache-2.0 + Commons Clause
language: Python
status: active
created: 2026-11-09
ingested: 2026-11-09
updated: 2026-11-09
tags: [agentes, mensageria, chatops, mcp, orquestracao, slack, discord, teams]
---

> Plataforma open-source que transforma canais de Slack, Teams, Discord e outros apps de mensageria em espaços de colaboração com agentes de IA, onde pessoas e agentes compartilham contexto persistente.

## Propósito

Switch resolve um problema de integração: agentes de IA como Claude Code, Codex e Antigravity vivem em CLIs ou IDEs, fora dos fluxos de comunicação de equipes. A plataforma conecta esses agentes a canais de mensageria existentes, tornando a colaboração com IA parte do fluxo de trabalho — não uma ferramenta separada.

A metáfora central do projeto: "each channel becomes a room for people and agents."

## Como funciona

Switch opera em quatro níveis de sofisticação crescente:

| Nível | Escopo |
|-------|--------|
| 1 | Agentes em canais existentes para colaboração diária |
| 2 | Automação de fluxos (triagem, abertura de chamados) |
| 3 | Processos completos (bug → correção → deploy) |
| 4 | Operação em escala corporativa |

O ponto central é o **Switch Console**, um app desktop que atua como hub: o usuário fala com um agente chamado `switch-buddy` e configura servidores, agentes e canais. O Switch não substitui apps de mensageria; ele se conecta a eles.

## Instalação

Switch Console está disponível como binário pré-compilado:

| Sistema | Formatos |
|---------|----------|
| macOS | DMG (Apple Silicon e Intel) |
| Windows | EXE |
| Linux x64 | AppImage, DEB |
| Linux ARM64 | AppImage, DEB |

Após instalar o console, o usuário escolhe entre **Switch Cloud** (em desenvolvimento) ou servidor próprio.

## Agentes e integrações suportados

**Agentes:** Claude Code, Codex, Antigravity, Cursor, OpenCode.

**Plataformas de mensageria:** Slack, Microsoft Teams, Discord, Telegram, Mattermost.

**Integrações de ferramentas:** Google Workspace, Atlassian, GitHub, Datadog, Airtable.

**Protocolos e frameworks:** MCP (Model Context Protocol), LangChain, ADK.

A integração com Claude Code ocorre via `claude mcp add` usando o endpoint de documentação.

## Exemplos de uso

- Agente detecta falha de checkout, abre canal de incidente e analisa taxa de erro em tempo real.
- Agente triador processa requisições em um canal, faz perguntas de esclarecimento e abre tickets no sistema de tracking.
- Pipeline completo sem intervenção humana: bug relatado → reproduzido → corrigido → revisado → deployado.

## Telemetria

- **Switch Console:** opt-out (ativada por padrão). Coleta: eventos anônimos (versão, SO, provedor de agente, erros). Nunca coleta código-fonte, prompts, credenciais, nomes de repositórios, IPs ou dados pessoais.
- **Switch Core Server:** desativada por padrão; quando ativada, reporta apenas métricas agregadas.

## Licença e limitações

**Apache 2.0 + Commons Clause:** uso comercial permitido, mas proibida a venda do Switch como serviço concorrente. Não é uma licença open source pela definição OSI.

Limitações declaradas:
- Switch Cloud ainda está em desenvolvimento (não disponível na ingestão desta página).
- Não fornece modelos ou agentes próprios — requer conexão com agentes externos.
- Contexto limitado aos canais aos quais o agente tem acesso.

**A verificar:** detalhes do protocolo de comunicação Switch Core ↔ agentes; autenticação de identidade do agente nos canais; preço e disponibilidade do Switch Cloud.

## Fontes

- README.md do repositório (`233649fff5d58a8ed550eeff28f74f738aba79b0`), lido em 2026-11-09.
- Metadados via API do GitHub (linguagem, status, tópicos), consultados em 2026-11-09.
- Apenas o `README.md` foi lido.
