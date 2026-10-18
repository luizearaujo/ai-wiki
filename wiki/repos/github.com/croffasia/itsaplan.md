---
type: repo
url: https://github.com/croffasia/itsaplan
host: github.com
owner: croffasia
repo: itsaplan
commit: a54d8c3c4e88193777de0f75601d403c3b96bc1a
license: AGPL-3.0
language: TypeScript
status: active
created: 2026-10-18
ingested: 2026-10-18
updated: 2026-10-18
tags: [agentes, gerenciamento-de-projetos, mcp, self-hosted, multi-agente, linear-alternative]
---

# croffasia/itsaplan

> Alternativa self-hosted e open-source ao Linear/Jira/Trello onde agentes de IA trabalham como membros de equipe — com as mesmas permissões, o mesmo board e os mesmos issues que as pessoas.

## O que é

It's a Plan é um gerenciador de projetos e issue tracker completo, auto-hospedado, sem taxas por assento e sem lock-in. A diferença em relação a ferramentas similares é que agentes de IA podem ser adicionados como membros de projeto com papel, permissões e slot de atribuição — eles aparecem no mesmo Kanban que os humanos, recebem issues, e rodam quando são @mencionados, recebem uma tarefa ou têm um agendamento configurado.

Suporta qualquer tipo de trabalho: desenvolvimento, marketing, design, suporte, vendas, operações, pesquisa. Tem site em [itsaplan.dev](https://itsaplan.dev).

> **A verificar:** o projeto está em desenvolvimento ativo e pode ter breaking changes antes da primeira release estável.

## Como funciona

### Camadas principais

**Gerenciamento de produto** — issue tracker completo:
- Views: Kanban, tabela, timeline e calendário, cada uma salva como aba com filtros e agrupamento próprios.
- Ciclos (sprints), campos customizados, labels, estados e tipos de issue por projeto.
- Subtarefas, checklists, anexos e links entre issues (blocks, relates, duplicates).
- Docs: páginas Markdown em árvore com histórico de revisões, favoritos e links para issues.
- Dashboards: throughput, burnup com data projetada, breakdown, pulse.
- Iniciativas para agrupar trabalho relacionado; ações rápidas e auto-atribuição por estado.

**Agentes de IA** — dois modos:

| Modo | Onde roda | Como configurar |
|------|-----------|-----------------|
| **Interno** | Na instância | Modelo, prompt de sistema, ferramentas e skills inline ou importadas de repositório GitHub |
| **Externo** | Na máquina do usuário | `@itsaplan/runner` entrega cada tarefa para Claude Code, Codex, Antigravity CLI, GitHub Copilot CLI, opencode ou qualquer comando que leia stdin |

Gatilhos de execução: @menção em comentário, atribuição de issue, ou agendamento. Há chat direto com cada agente, com histórico de conversa por agente e sessão retomada no runner externo a cada mensagem.

Ferramentas disponíveis para agentes internos além do tracker: Notion, Telegram, Threads, Instagram, Jina, Firecrawl, Gitea.

**Plataforma:**
- REST API com referência OpenAPI e API keys.
- Servidor MCP — um assistente externo pode ler e alterar issues via MCP.
- Pull requests de GitHub, GitLab, Gitea, Forgejo e Bitbucket. "Fixes KEY-42" no título vincula o PR ao issue; o issue avança ao abrir e mergar o PR.
- Webhooks de saída com payloads assinados, retentativas e log de entrega.
- Auth: email/senha, passkey ou Google.
- Notificações por e-mail (SMTP ou Resend) e Telegram.
- Interface em 11 idiomas, incluindo português (Brasil).

### Stack técnico

| Camada | Tecnologia |
|--------|------------|
| Runtime | Bun + Turborepo |
| Backend | Elysia |
| Frontend | Next.js App Router (SSR) |
| UI | shadcn/ui + Tailwind v4 |
| Auth | better-auth |
| Banco de dados | Drizzle + PostgreSQL |
| Storage | S3-compatible (RustFS) |
| Agentes de IA | Mastra |

## Instalação e uso rápido

**Testar localmente** (requer Docker e Bun):

```bash
git clone https://github.com/croffasia/itsaplan.git
cd itsaplan
bun install
bun run setup   # escolher "Try it"
# abre http://localhost:3001
```

**Deploy em produção:**
- [Railway](https://railway.com/deploy/its-a-plan) — stack completo com um clique, sem servidor para manter.
- [Docker / self-hosting](https://github.com/croffasia/itsaplan/blob/main/docs/self-hosting.md) — setup completo com secrets e processo de atualização.
- [Coolify](https://github.com/croffasia/itsaplan/blob/main/docs/coolify.md) / [Kubernetes (Helm)](https://github.com/croffasia/itsaplan/blob/main/docs/helm.md).

**Configurar agente externo** (Claude Code, Codex etc.):

```bash
npm install -g @itsaplan/runner
# ver docs/runner.md para configuração por CLI
```

## Quando usar (e quando não usar)

- **Use quando:** quiser um issue tracker self-hosted onde agentes de IA podem receber e executar tarefas da mesma forma que membros humanos; quando precisar de rastreabilidade completa entre issues e PRs; quando AGPL-3.0 for compatível com seu contexto.
- **Evite quando:** a equipe já usa Linear ou Jira com integrações profundas difíceis de migrar; quando AGPL-3.0 conflitar com o uso comercial (licença comercial disponível mediante contato); quando o projeto ainda estiver pré-estável e breaking changes forem inaceitáveis.

## Limitações e cuidados

- **Pré-estável:** breaking changes são esperados antes da primeira release estável.
- **Licença AGPL-3.0:** exige que modificações distribuídas sejam abertas; `packages/runner` usa Apache-2.0. Licença comercial disponível.
- Agentes externos dependem de CLIs de terceiros (Claude Code, Codex etc.) instaladas e configuradas localmente — o runner não inclui o modelo.
- Skills de agentes internos importadas de GitHub exigem acesso ao repositório-fonte; detalhes de segurança não verificados (somente README lido).
- Não lidos: `docs/`, `CONTRIBUTING.md`, `SECURITY.md`, código-fonte, `packages/runner`.

## Estado e adoção

- Último push: 2026-10-18.
- Observado em 2026-10-18: ~1.292 stars, ~202 forks, ~49 issues abertas.
- Licença: AGPL-3.0 (runner: Apache-2.0). Copyright © 2026 Andrii Poluosmak.

## Relações

- Mantido por: [croffasia](../../../entities/croffasia.md)
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Agent skills](../../../concepts/agent-skills.md)
- Relacionado: [msitarzewski/agency-agents](../msitarzewski/agency-agents.md) — personalidades de agente instaláveis em clientes como Claude Code, que podem ser usadas como agentes externos no itsaplan.

## Perguntas abertas

- Como o Mastra gerencia o ciclo de vida dos agentes internos e isola execuções concorrentes?
- Qual é o mecanismo de segurança para skills importadas de repositórios GitHub externos?
- O servidor MCP expõe apenas leitura ou também permite mutações (criar/atualizar issues)?
- Existe um marketplace ou catálogo de skills compatíveis com agentes internos do itsaplan?

## Fontes

- README: https://raw.githubusercontent.com/croffasia/itsaplan/a54d8c3c4e88193777de0f75601d403c3b96bc1a/README.md (commit `a54d8c3c4e88193777de0f75601d403c3b96bc1a`, consultado em 2026-10-18). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub em 2026-10-18.
