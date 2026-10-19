---
type: repo
url: https://github.com/vercel-labs/agent-skills
host: github.com
owner: vercel-labs
repo: agent-skills
commit: 063bee94c3f4df8453406c830b0a7df0f2860278
license: MIT
language: JavaScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agent-skills, vercel, react, nextjs, performance, design, deploy]
---

# vercel-labs/agent-skills

> Coleção oficial da Vercel de Agent Skills para agentes de código: auditoria de custo e performance de projetos Vercel, boas práticas de React/Next.js, guidelines de design web e de escrita, React Native e deploy "claimable" direto do chat.

## O que é

O repositório empacota o conhecimento de engenharia da Vercel — performance, design, escrita e deploy — como skills no formato padrão Agent Skills (agentskills.io), para que agentes de código apliquem essas práticas automaticamente quando a tarefa se encaixa.

## Como funciona

Oito skills publicadas, cada uma como pasta própria com `SKILL.md`, `scripts/` (opcional) e `references/` (opcional):

| Skill | Função |
|---|---|
| `vercel-optimize` | Audita um projeto Vercel para custo, performance, confiabilidade, cache, uso de functions e oportunidades de billing; coleta métricas da Vercel primeiro e só investiga as rotas/arquivos que elas apontam. |
| `react-best-practices` | 40+ regras em 8 categorias (waterfalls, bundle size, performance server/client-side, re-render, renderização, micro-otimizações JS), priorizadas por impacto. |
| `web-design-guidelines` | Audita código de UI contra 100+ regras de acessibilidade, performance e UX (foco, formulários, animação, tipografia, imagens, dark mode, i18n). |
| `writing-guidelines` | Audita docs e prosa contra o manual de escrita da Vercel: 80+ regras de voz, estrutura, tipos de conteúdo, código, tipografia e fluxo de revisão com IA. |
| `react-native-guidelines` | 16 regras em 7 seções para apps React Native/Expo: performance, layout, animação, imagens, estado, arquitetura e padrões por plataforma. |
| `react-view-transitions` | Implementa animações com a View Transition API do React (`<ViewTransition>`, `addTransitionType`, integração com `next/link`). |
| `composition-patterns` | Padrões de composição React que evitam proliferação de props booleanas (compound components, lifting de estado, composição interna). |
| `vercel-deploy-claimable` | Deploy instantâneo para Vercel a partir de uma conversa no claude.ai/Claude Desktop, com URL de preview e URL de "claim" para o usuário transferir a posse do projeto. |

**Índice de descoberta:** toda mudança em uma skill na branch `main` publica uma release imutável do GitHub com um índice de descoberta Agent Skills e um artefato por skill; o mesmo processo pode ser reproduzido localmente com `node scripts/build-discovery-index.mjs`.

## Instalação e uso rápido

```bash
npx skills add vercel-labs/agent-skills
```

As skills ficam disponíveis automaticamente após a instalação; o agente as aciona quando detecta uma tarefa relevante (ex.: "Deploy my app", "Review this React component for performance issues").

## Exemplos de uso

Exemplos derivados do README:

```text
Deploy my app
Review this React component for performance issues
Help me optimize this Next.js page
```

A saída de `vercel-deploy-claimable` publicada no README:

```text
Deployment successful!

Preview URL: https://skill-deploy-abc123.vercel.app
Claim URL:   https://vercel.com/claim-deployment?code=...
```

## Quando usar (e quando não usar)

- **Use quando:** o time desenvolve com React/Next.js ou React Native e quer que o agente aplique automaticamente boas práticas de performance, acessibilidade e escrita já consolidadas pela Vercel.
- **Use quando:** quer auditar um projeto Vercel real quanto a custo e performance antes de otimizar manualmente.
- **Evite quando:** o projeto não usa Vercel, React ou Next.js — a maioria das skills é específica desse stack.
- **Evite quando:** o fluxo de deploy "claimable" (que expõe URLs públicas de preview) não é adequado ao modelo de segurança do time.

## Limitações e cuidados

- **Somente o README foi lido.** O conteúdo de cada `SKILL.md`, os scripts de automação e o índice de descoberta não foram inspecionados.
- `vercel-deploy-claimable` é descrita como projetada para uso com claude.ai e Claude Desktop — compatibilidade com outros clientes não é detalhada no README.
- `vercel-optimize` depende de acesso a métricas da Vercel; sem esse acesso, a auditoria não tem como começar pelo recorte de rotas/arquivos relevantes.
- As regras numéricas (40+, 100+, 80+, 16) são contagens do próprio projeto; não verificadas por esta wiki.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~32,6 mil estrelas, ~2,9 mil forks, 181 issues abertas; criado em 2025-12-08, último push em 2026-10-14.
- **Licença:** MIT.
- **Linguagem principal:** JavaScript.

## Relações

- **Mantido por:** [Vercel Labs (vercel-labs)](../../../entities/vercel-labs.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — coleção oficial de um fornecedor de plataforma, no mesmo padrão de `anthropics/skills`, `cloudflare/skills` e `remotion-dev/skills`.
- **Relacionado a:** [anthropics/skills](../anthropics/skills.md), [cloudflare/skills](../cloudflare/skills.md), [remotion-dev/skills](../remotion-dev/skills.md) e [firecrawl/cli](../firecrawl/cli.md) — skills oficiais publicadas por fornecedores de produto, no mesmo formato Agent Skills.

## Perguntas abertas

- O índice de descoberta publicado nas releases é consumido automaticamente por algum cliente, ou é só um artefato de build?
- Quais são as 40+, 100+, 80+ e 16 regras exatas de cada skill de guidelines?
- `vercel-deploy-claimable` funciona fora de claude.ai/Claude Desktop, ou depende de integração específica desses clientes?

## Fontes

- README: https://github.com/vercel-labs/agent-skills (commit `063bee94c3f4df8453406c830b0a7df0f2860278`, consultado em 2026-10-19). Somente o README foi lido; os `SKILL.md` individuais, scripts e o índice de descoberta não foram consultados.
- Metadados do repositório e do perfil `vercel-labs` via API do GitHub (consultados em 2026-10-19).
