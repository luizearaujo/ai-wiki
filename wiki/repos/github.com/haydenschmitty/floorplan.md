---
type: repo
url: https://github.com/haydenschmitty/floorplan
host: github.com
owner: haydenschmitty
repo: floorplan
commit: cec107540da3910c6d7a5fa6400fc9851bf4c15e
license: MIT
language: JavaScript
status: active
created: 2026-11-01
ingested: 2026-11-01
updated: 2026-11-01
tags: [visualizacao-de-arquitetura, plugin-de-agente, claude-code, codex, saude-de-seguranca]
---

# haydenschmitty/floorplan

> Plugin para Claude Code e Codex que lê a base de código do usuário e desenha um mapa interativo e navegável, em inglês simples, de suas partes, arquivos e requisições web.

## O que é

Floorplan ataca o problema de "construí com ajuda de IA e funciona, mas não sei como se encaixa": gera o diagrama que ninguém desenhou. É voltado a quem constrói com IA e não lê código (entendimento sem ler o código), a equipes (onboarding) e a quem trabalha com agentes (ver exatamente o que uma IA tocou e por quê, a cada mudança).

O README posiciona o projeto explicitamente contra dois concorrentes, com uma tabela comparativa própria: [tt-a1i/archify](../tt-a1i/archify.md) (diagramas polidos para explicar algo a alguém, não para auditoria) e [Egonex-AI/Understand-Anything](../egonex-ai/understand-anything.md) (grafo de conhecimento de desenvolvedor, função a função, para bases de código grandes). A posição que o próprio README reivindica é "entender e checar um app que você já construiu", com três diferenciais que diz serem exclusivos: Health check, "Recent work" (o que a IA acabou de mudar) e blueprints a partir de PRD.

## Como funciona

Pipeline descrito no README: `scan` (varre arquivos, imports, rotas e requisições em um ou vários repositórios, inclusive frontend e backend separados) → Claude ou Codex nomeia as partes e descreve cada arquivo em inglês simples → `build` (monta mapa, health, screens e recent work) → abre `floorplan/index.html` no navegador. Pedir "update the floorplan" relê somente o que mudou, e um mapa já aberto recarrega a si mesmo.

Segundo o README, os scripts que fazem o trabalho mecânico — achar repositórios, parsear código em uma dúzia de linguagens, casar cada requisição do frontend com o endpoint que responde (inclusive entre repositórios separados), montar o layout do mapa — são Node puro, sem dependências; a parte que só quem lê pode fazer (decidir o que cada parte da aplicação *é*, e dizer isso com clareza) fica com o agente.

Linguagens de código citadas: TypeScript, JavaScript, Python, Go, Rust, Java, Kotlin, Scala, mais arquivos Vue, Svelte e Astro, com suporte mais leve a outras. Frameworks de endpoint: Express, Koa, Hono, Next.js, Firebase Cloud Functions, Flask, FastAPI, Django, `net/http` do Go, Gin, Echo e chi, Actix, Axum, Spring. Frameworks de tela: Next.js, React Router, Vue, SvelteKit, Remix, Nuxt, Astro, Expo, Angular, TanStack.

## Instalação e uso rápido

Requer Node.js 18+ e Claude Code ou Codex; roda no plano já pago do usuário, sem chaves de API.

- **Claude Code:** `claude plugin marketplace add haydenschmitty/floorplan` seguido de `claude plugin install floorplan@floorplan`.
- **Codex:** `codex plugin marketplace add haydenschmitty/floorplan` seguido de `codex plugin add floorplan@floorplan`, ou pela UI em Plugins → "Add a marketplace" com a fonte `haydenschmitty/floorplan`.

Uso: pedir "Make me a floorplan of this app" (ou digitar `$floorplan` no Codex); depois, "Update the floorplan" para atualizações incrementais. O README aponta documentação própria mais detalhada — `docs/getting-started.md`, `docs/codex.md`, `docs/how-it-works.md` — que não foi lida nesta ingestão.

## Exemplos de uso

Exemplos citados no próprio README como prompts de exemplo, não como lista exaustiva:

- "Fix the important issues from the floorplan's Health check" — corrige a partir dos achados do Health check.
- "Add a flow showing how a new user signs up" — pede um fluxo guiado novo.
- "Here's my PRD. Make me a floorplan of what we'd need to build." — gera um blueprint (mapa de um sistema planejado, cards tracejados, ainda sem código) a partir de uma especificação.

## Quando usar (e quando não usar)

- **Use quando:** você (ou sua equipe) construiu uma aplicação majoritariamente com ajuda de IA e quer visualizar como as partes se conectam, checar riscos comuns de apps "vibe-coded" (chaves expostas ao navegador, tabelas Supabase ou regras Firebase abertas, webhooks Stripe falsificáveis, endpoints sem autenticação) ou acompanhar o que um agente alterou e por quê.
- **Evite quando:** o objetivo é um diagrama polido para uma apresentação, um documento ou uma ideia que não é código — o próprio README recomenda [tt-a1i/archify](../tt-a1i/archify.md) para isso; ou quando o objetivo é um grafo de conhecimento função a função de uma base de código grande — o README recomenda [Egonex-AI/Understand-Anything](../egonex-ai/understand-anything.md).

## Limitações e cuidados

- O README não detalha o formato interno de `floorplan/architecture.json` nem dos arquivos em `floorplan/descriptions/`; aponta para `docs/project-files.md`, não lido nesta ingestão.
- As regras exatas do Health check (por exemplo, como distingue uma chave pública "por design" de uma exposta por engano) não são detalhadas além dos exemplos do changelog da release 0.6.0.
- As afirmações de "zero dependências", execução inteiramente local e nenhuma telemetria são do próprio README; o README cita um teste e um fingerprint por release que verificariam isso (`docs/is-it-safe.md`), mas esse arquivo não foi lido aqui.
- **A verificar:** conteúdo de `docs/getting-started.md`, `docs/how-it-works.md`, `docs/project-files.md`, `docs/privacy-and-security.md`, `docs/is-it-safe.md`, `docs/troubleshooting.md`, `docs/development.md` e `CONTRIBUTING.md` — nenhum foi lido; somente o `README.md` foi consultado.

## Estado e adoção

- Versão citada no README/badge: 0.6.0 (tag `floorplan--v0.6.0`, publicada em 2026-10-31); badge de testes via GitHub Actions.
- Repositório criado em 2026-10-27, com push mais recente em 2026-10-31.
- Observado em 2026-11-01 via API do GitHub: 1.114 estrelas, 77 forks, 11 issues abertas — métricas datadas, não fatos estáveis.
- Licença: MIT (© 2026 Hayden Smith).

## Relações

- **Mantido por:** [Hayden Smith (haydenschmitty)](../../../entities/haydenschmitty.md).
- **Conceitos:** [Grafo de conhecimento de código](../../../concepts/grafo-de-conhecimento-de-codigo.md) — representação persistente e consultável ("Ask the map"), mas organizada em cards descritos em inglês simples, não em grafo de símbolos; [Plugins de agente](../../../concepts/plugins-de-agente.md) e [Agent skills](../../../concepts/agent-skills.md) — distribuído como plugin de marketplace para Claude Code e Codex, sem dependências e sem servidor MCP próprio.
- **Alternativas (citadas pelo próprio README):** [tt-a1i/archify](../tt-a1i/archify.md) — diagramas polidos para comunicação, não para auditoria contínua; [Egonex-AI/Understand-Anything](../egonex-ai/understand-anything.md) — grafo de conhecimento função a função para bases de código grandes.

## Perguntas abertas

- Como o Health check determina, na prática, se uma política do Supabase ou uma regra do Firebase está realmente aberta (o README menciona "replay" das migrations, mas não detalha o algoritmo)?
- Qual é o formato exato de `floorplan/architecture.json` e como edições manuais do usuário sobrevivem a um "update"?
- Existe qualquer envio de dados além do e-mail opcional da waitlist do "Floorplan Cloud"?

## Fontes

- README: https://raw.githubusercontent.com/haydenschmitty/floorplan/cec107540da3910c6d7a5fa6400fc9851bf4c15e/README.md (commit `cec107540da3910c6d7a5fa6400fc9851bf4c15e`, consultado em 2026-11-01). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/haydenschmitty/floorplan` e `.../releases/latest`), consultada em 2026-11-01.
