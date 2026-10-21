---
type: repo
url: https://github.com/every-app/open-seo
host: github.com
owner: every-app
repo: open-seo
commit: c5f8db19c7ca9e750836b6ed5c8a6491d4f967f4
license: MIT
language: TypeScript
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [mcp, agent-skills, seo, cloudflare]
---

# every-app/open-seo

> Stack de SEO self-hosted (alternativa a Semrush/Ahrefs) desenhado para ser operado tanto por uma pessoa quanto por um agente de IA: servidor MCP próprio, Agent Skills para pesquisa de palavra-chave, rastreamento de posição e auditoria de site, e cobrança só do que a chave DataForSEO consumir.

## O que é

OpenSEO cobre pesquisa de palavra-chave, pesquisa de domínio, backlinks, rastreamento de posição, auditoria de site e integração com o Google Search Console. É um app web em TypeScript, pensado para Cloudflare Workers, com interface em React. O usuário traz a própria chave da API [DataForSEO](https://dataforseo.com) para os dados brutos de SEO, pagando só pelo uso — a versão hospedada da Every App cobra 28% a mais por requisição à DataForSEO como seu modelo de receita.

## Como funciona

- **Servidor MCP**: expõe os dados de SEO como ferramentas que agentes como Claude Code, OpenClaw ou Hermes podem chamar diretamente.
- **Agent Skills**: workflows reutilizáveis pré-construídos que guiam o agente por uma tarefa de SEO usando o MCP por baixo — o usuário também pode escrever as próprias.
- **Contexto persistente entre sessões**: os agentes usam o Cloudflare Agents SDK para manter contexto de conversa.
- Workflows principais: pesquisa de palavra-chave, rastreamento de posição, insights de concorrentes, backlinks, auditorias de site e visibilidade em buscadores de IA.

## Instalação e uso rápido

Duas rotas de self-hosting:

- **Docker** — simples, para testar localmente. Ver `docs/SELF_HOSTING_DOCKER.md`.
- **Cloudflare** — recomendada para uso voltado à internet, entre dispositivos ou com um time; funciona no plano gratuito. Ver `docs/SELF_HOSTING_CLOUDFLARE.md`.

Em qualquer rota, é necessária uma chave da API DataForSEO (`docs/DATAFORSEO_API_KEY.md`). Setup de agentes: ChatGPT web/desktop, Codex, servidor MCP e Agent Skills têm guias próprios em openseo.so/docs.

```bash
npx skills add every-app/open-seo --skill simple-issue-description
```

## Quando usar (e quando não usar)

- **Use quando:** quer ferramentas de SEO operáveis por um agente (via MCP e skills), sem assinatura mensal de uma suíte fechada, e já tem ou aceita pagar por uma chave DataForSEO.
- **Evite quando:** prefere a versão hospedada sem lidar com infraestrutura própria — nesse caso o produto pago em openseo.so é a rota mais simples, com a mesma superfície de recursos.

## Limitações e cuidados

- O custo real dos dados de SEO vem da DataForSEO, não do OpenSEO — o README é explícito que o próprio projeto não embute dados de SEO, só os consulta.
- Self-hosting "simples" (Docker) é recomendado só para uso pessoal; para deploy voltado à internet ou multiusuário, o README recomenda Cloudflare em vez de Railway, Coolify ou Dokploy, com planos de simplificar essas outras rotas "nos próximos meses".
- Não foram lidos os guias de self-hosting, a documentação do servidor MCP nem a lista completa de Agent Skills — só o README raiz.

## Estado e adoção

- 24.394 estrelas, 3.295 forks, 212 issues abertas — observado em 2026-10-21.
- Repositório criado em 2026-02-27, com push mais recente em 2026-10-20 — observado em 2026-10-21.
- Modelo de preço da versão hospedada: a partir de US$ 10/mês (ver openseo.so/pricing); self-hosted paga só a DataForSEO direto.
- Licença: MIT.

## Relações

- Mantido por: [Every App (every-app)](../../../entities/every-app.md)
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Agent skills](../../../concepts/agent-skills.md).
- Projetos relacionados da mesma organização, citados no README: SAM (servidor de inferência de LLM), o Every-App SDK e um repositório de skills de agente — nenhum documentado nesta wiki.

## Perguntas abertas

- Quais ferramentas exatas o servidor MCP expõe, e como elas mapeiam para os endpoints da DataForSEO?

## Fontes

- README: https://raw.githubusercontent.com/every-app/open-seo/c5f8db19c7ca9e750836b6ed5c8a6491d4f967f4/README.md (commit `c5f8db19c7ca9e750836b6ed5c8a6491d4f967f4`, consultado em 2026-10-21). Somente o README foi lido; a documentação em `docs/` não foi consultada.
- Metadados: API do GitHub (`api.github.com/repos/every-app/open-seo`), consultada em 2026-10-21.
