---
type: repo
url: https://github.com/cloudflare/skills
host: github.com
owner: cloudflare
repo: skills
commit: 86505e44f87d801aa1864a3c4109e9a8ae5c409f
license: Apache-2.0
language: Shell
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agent-skills, cloudflare, mcp, workers, agents-sdk]
---

# cloudflare/skills

> Skills oficiais da Cloudflare para construir sobre Workers, o Agents SDK, Durable Objects, Sandbox e o restante da plataforma de desenvolvedor, empacotadas junto com o servidor MCP principal da Cloudflare.

## O que é

O repositório reúne 18 Agent Skills contextuais — carregadas automaticamente quando a conversa aciona seus gatilhos — cobrindo o desenvolvimento na Cloudflare Developer Platform: do roteamento inicial entre produtos até tópicos específicos como Durable Objects, Sandbox, e-mail, Turnstile e migração de outras plataformas de segurança (Cloudflare One).

## Como funciona

Dezoito skills, descobertas por gatilho de conversa:

| Skill | Útil para |
|---|---|
| `cloudflare` | Ajuda o agente a descobrir qual produto Cloudflare atende a necessidade, e então localizar as skills e docs certas. |
| `basin` | Workflows de analytics com Basin Pipelines, Basin Catalog e Basin SQL. |
| `k2` | Streams duráveis K2 com produtores HTTP/Worker e consumidores de assinatura. |
| `nextjs-on-cloudflare` | Next.js em Workers com vinext. |
| `agents-sdk` | Agentes de IA com estado, agendamento, RPC, servidores MCP, e-mail e streaming de chat. |
| `durable-objects` | Coordenação com estado (salas de chat, jogos, reservas), RPC, SQLite, alarms, WebSockets. |
| `sandbox-next` / `sandbox-stable` / `sandbox-migrate-to-next` | Sandbox na versão preview 1.0 ou estável, e migração entre elas. |
| `cf-cli` / `wrangler` | Comandos da CLI `cf` vs. Wrangler; deploy e gestão de Workers, KV, R2, D1, Vectorize, Queues, Workflows. |
| `workers-best-practices` / `workers-profiling` | Boas práticas de produção e profiling de CPU/alocação em Workers e Durable Objects. |
| `cloudflare-email-service` | Email Sending, Email Routing e configuração de entrega. |
| `turnstile-spin` | Setup, reparo ou migração do Turnstile (verificação de bot), incluindo Siteverify server-side. |
| `web-perf` | Auditoria de Core Web Vitals (FCP, LCP, TBT, CLS) e cadeias de rede. |
| `cloudflare-one` / `cloudflare-one-migrations` | Design e troubleshooting de Access, Gateway, WARP, Tunnel, Magic WAN, DLP, CASB, postura e identidade; avaliação de migração desde Zscaler, Palo Alto, VPN legado e SASE. |
| `gateway-workers` | Workers invocados pela ação Forward em políticas HTTP do Gateway. |

**Servidor MCP incluído:** o pacote de instalação traz o MCP server remoto principal da Cloudflare, que dá acesso à API da Cloudflare e à documentação atual via Code Mode MCP. A Cloudflare publica outros servidores MCP específicos por produto, mas o README é explícito: este plugin empacota apenas o servidor `cloudflare` principal.

## Instalação e uso rápido

Codex (marketplace de plugins):

```sh
codex plugin marketplace add cloudflare/skills
codex plugin add cloudflare@cloudflare
```

Claude Code (marketplace de plugins):

```
/plugin marketplace add cloudflare/skills
/plugin install cloudflare@cloudflare
```

VS Code/GitHub Copilot: habilitar `chat.plugins.enabled`, abrir a Command Palette → **Chat: Install Plugin From Source** → informar `https://github.com/cloudflare/skills`.

Cursor: via Cursor Marketplace, ou manualmente em Settings → Rules → Add Rule → Remote Rule (GitHub) com `cloudflare/skills`.

`npx skills`:

```
npx skills add https://github.com/cloudflare/skills
```

Clone/cópia manual por agente (diretórios citados no README): Claude Code (`~/.claude/skills/`), Cursor (`~/.cursor/skills/`), OpenCode (`~/.config/opencode/skills/`), OpenAI Codex (`~/.codex/skills/`), Pi (`~/.pi/agent/skills/`).

## Exemplos de uso

O README não publica prompts de exemplo; as skills são contextuais e carregam automaticamente quando a conversa menciona o produto ou a tarefa correspondente — por exemplo, perguntar sobre Durable Objects aciona a skill `durable-objects`, e pedir para "revisar um Worker de produção" aciona `workers-best-practices`.

## Quando usar (e quando não usar)

- **Use quando:** o projeto é construído sobre Cloudflare (Workers, Durable Objects, Agents SDK, Sandbox, D1, R2, Vectorize etc.) e o time quer que o agente siga as práticas e a documentação atuais da plataforma.
- **Use quando:** precisa migrar de Zscaler, Palo Alto, VPN legado ou outra SASE para Cloudflare One, e quer orientação estruturada de avaliação e rollout.
- **Evite quando:** o projeto não usa a plataforma Cloudflare — as 18 skills são específicas dela.
- **Evite quando:** só é necessário o servidor MCP, sem as skills de orientação — nesse caso, instalar diretamente o MCP server principal da Cloudflare pode ser suficiente.

## Limitações e cuidados

- **Somente o README foi lido.** O conteúdo de cada `SKILL.md` e do servidor MCP empacotado não foi inspecionado.
- O README não detalha o critério exato de gatilho por skill além da tabela "Useful for" — a precisão da descoberta automática não foi verificada.
- O plugin bundla apenas o servidor MCP principal; servidores específicos por produto (citados mas não listados) exigem instalação separada.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~3,1 mil estrelas, 317 forks; criado em 2025-12-10, último push em 2026-10-15.
- **Licença:** Apache-2.0.
- **Linguagem principal:** Shell.

## Relações

- **Mantido por:** [Cloudflare](../../../entities/cloudflare.md) — mesma organização de [cloudflare/agentic-inbox](../cloudflare/agentic-inbox.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — skills oficiais de fornecedor, mesmo padrão de `anthropics/skills`, `vercel-labs/agent-skills` e `remotion-dev/skills`; [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — o pacote inclui o servidor MCP principal da Cloudflare.
- **Relacionado a:** [cloudflare/agentic-inbox](../cloudflare/agentic-inbox.md) — outro produto Cloudflare já documentado nesta wiki, também com servidor MCP próprio.

## Perguntas abertas

- Como a descoberta automática por gatilho de conversa decide entre skills com escopo próximo (ex.: `sandbox-next` vs. `sandbox-stable`)?
- Quais servidores MCP específicos por produto a Cloudflare publica fora deste plugin, e como se relacionam com o servidor principal aqui incluído?
- As skills de migração (`cloudflare-one-migrations`) incluem algum critério de avaliação verificável, ou são apenas orientação qualitativa?

## Fontes

- README: https://github.com/cloudflare/skills (commit `86505e44f87d801aa1864a3c4109e9a8ae5c409f`, consultado em 2026-10-19). Somente o README foi lido; os `SKILL.md` individuais e a implementação do servidor MCP não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19); perfil da organização já registrado em [entities/cloudflare.md](../../../entities/cloudflare.md).
