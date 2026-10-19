---
type: repo
url: https://github.com/upstash/context7
host: github.com
owner: upstash
repo: context7
commit: c7f80ce5af1ff1403d167579b76784482cf7f3e2
license: MIT
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [mcp, documentacao, cli, llm]
---

# upstash/context7

> Servidor MCP e CLI que injetam documentação e exemplos de código atuais e específicos de versão no contexto de agentes, em vez de depender do conhecimento desatualizado ou genérico do modelo.

## O que é

Context7 ataca um problema concreto: LLMs treinados em dados antigos geram código com APIs inexistentes ou genéricas para versões antigas de pacotes. O repositório publica a parte cliente (servidor MCP) de uma plataforma cujo backend de API, engine de parsing e crawler são privados.

## Como funciona

Dois modos de uso, não mutuamente exclusivos:

- **CLI + Skills:** instala uma skill que orienta o agente a buscar documentação com comandos `ctx7`, sem precisar de MCP.
  - `ctx7 library <name> <query>`: busca bibliotecas e seus IDs.
  - `ctx7 docs <libraryId> <query>`: recupera documentação para um ID.
- **MCP:** registra um servidor MCP com duas ferramentas:
  - `resolve-library-id`: mapeia um nome de biblioteca para um ID Context7, ranqueando resultados pela query (`query`, `libraryName`).
  - `query-docs`: busca documentação por ID (`libraryId`, `query`, `language` opcional para priorizar exemplos nessa linguagem).

## Instalação e uso rápido

- `npx ctx7 setup` — autentica via OAuth, gera API key e instala a skill apropriada; permite escolher entre CLI+Skills ou MCP e mirar um agente específico (`--cursor`, `--claude`, `--opencode`).
- `npx ctx7 remove` remove a configuração; CLI instalada globalmente precisa de `npm uninstall -g ctx7` separado.
- Setup manual: apontar um cliente MCP para `https://mcp.context7.com/mcp` com API key no header `Authorization: Bearer`.
- Pré-requisitos: Node.js ≥ 22.13 para a CLI `ctx7`; agente com suporte a MCP ou skills (README cita Cursor, Claude Code, OpenCode); API key gratuita recomendada para limites de taxa maiores.

## Exemplos de uso

- Adicionar "use context7" ao final de um pedido para disparar a busca.
- Fixar biblioteca com sintaxe de barra, ex.: `/supabase/supabase`, para pular o matching.
- Fixar versão citando-a no prompt, ex.: "Next.js 16".
- Regra permanente em `CLAUDE.md` do tipo "Always use Context7 when I need library/API documentation" sem precisar pedir.
- Exemplos do README: proxy Next.js que valida JWT em cookies, Cloudflare Worker com cache de 5 minutos para respostas JSON, e API de auth do Supabase para sign-up por e-mail/senha sem a tag explícita "use context7".

## Quando usar (e quando não usar)

- **Use quando:** o agente precisa de exemplos e assinaturas de API corretos para uma versão específica de uma biblioteca, em vez de generalizar a partir do treinamento.
- **Evite quando:** a biblioteca não está no catálogo (comunitário) ou quando exatidão é crítica sem possibilidade de revisão humana — o README é explícito que não garante acurácia.

## Limitações e cuidados

- **Acurácia não garantida:** documentação é contribuída pela comunidade; há botão de "Report" por projeto para conteúdo problemático.
- **Código-fonte parcial:** este repositório é só o servidor MCP; backend de API, parsing e crawler são privados — não auditáveis.
- **Matching impreciso** sem ID ou versão explícitos no prompt.
- **Rate limits** sem API key.

## Estado e adoção

- Licença: MIT.
- Linguagem principal (API do GitHub): TypeScript.
- Atividade observada em 2026-10-19: push mais recente no mesmo dia (projeto com cadência de desenvolvimento ativa).

## Relações

- Mantido por: [upstash](../../../entities/upstash.md).
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md).
- Alternativas: pacotes adicionais citados no README para outros ambientes (SDK TypeScript, Vercel AI SDK tools, extensão pi.dev) e suporte a mais de 30 clientes MCP via setup manual.

## Perguntas abertas

- Qual o modelo de dados e atualização do backend privado que alimenta os resultados (não documentado no README)?
- Como o catálogo comunitário é curado ou moderado além do botão de "Report"?

## Fontes

- README: https://raw.githubusercontent.com/upstash/context7/c7f80ce5af1ff1403d167579b76784482cf7f3e2/README.md (commit `c7f80ce5af1ff1403d167579b76784482cf7f3e2`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Perfil do GitHub (`api.github.com/repos/upstash/context7`, `api.github.com/orgs/upstash`), consultado em 2026-10-19.
