---
type: repo
url: https://github.com/cloudflare/agentic-inbox
host: github.com
owner: cloudflare
repo: agentic-inbox
commit: 48039bb6785af34e592c2966f87cde2b255c4c80
license: Apache-2.0
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [email, agentes, cloudflare, workers, mcp, self-hosted, typescript]
---

# cloudflare/agentic-inbox

> Cliente de e-mail self-hosted com um agente de IA embutido, rodando inteiramente em Cloudflare Workers, com isolamento por mailbox em Durable Objects e servidor MCP em `/mcp`.

## O que é

Agentic Inbox permite enviar, receber e gerenciar e-mails por uma interface web moderna, usando a própria conta Cloudflare do usuário. E-mails recebidos chegam via [Cloudflare Email Routing](https://developers.cloudflare.com/email-routing/); cada mailbox fica isolado em um [Durable Object](https://developers.cloudflare.com/durable-objects/) com banco SQLite; anexos são armazenados em [R2](https://developers.cloudflare.com/r2/).

O diferencial é o **AI Email Agent**: um painel lateral construído com o Cloudflare Agents SDK e Workers AI que lê a caixa de entrada, busca conversas e redige respostas. O projeto é uma aplicação de referência da Cloudflare para a ideia de "email for agents", anunciada no blog da empresa.

O público é desenvolvedor ou equipe pequena que quer um cliente de e-mail próprio, sem servidor de e-mail dedicado, e que aceita a dependência da plataforma Cloudflare.

## Como funciona

A arquitetura publicada no README:

```
Browser (React SPA + Agent Panel)
   │  WebSocket
   ▼
Hono Worker (API + SSR)
   ├──> MailboxDO (SQLite + R2)
   ├──> EmailAgent DO (AIChatAgent, 9 email tools)
   │        └──> Workers AI
   └──> /mcp  (servidor MCP)
```

- **Frontend:** React 19, React Router v7, Tailwind CSS, Zustand, TipTap e `@cloudflare/kumo`.
- **Backend:** Hono, Workers, Durable Objects com SQLite, R2 e Email Routing.
- **Agente:** Cloudflare Agents SDK (`AIChatAgent`), AI SDK v6, Workers AI com `@cf/moonshotai/kimi-k2.5`, `react-markdown` e `remark-gfm`.
- **Autenticação:** validação de JWT do Cloudflare Access, obrigatória fora do desenvolvimento local.

Cada mailbox é uma unidade isolada de armazenamento. O agente tem nove ferramentas de e-mail — leitura, busca, rascunho e envio — e pode gerar rascunhos automaticamente para mensagens recebidas, sempre exigindo confirmação explícita antes de enviar.

## Instalação e uso rápido

Pré-requisitos: conta Cloudflare com domínio, Email Routing para receber, Email Service para enviar, Workers AI habilitado e Cloudflare Access configurado em produção.

Deploy pelo botão "Deploy to Cloudflare" ou localmente:

```bash
npm install
npm run dev
```

Configuração mínima: definir o domínio em `wrangler.jsonc` e criar o bucket R2.

```bash
wrangler r2 bucket create agentic-inbox
npm run deploy
```

Depois do deploy, o README exige passos adicionais: configurar Cloudflare Access e definir os secrets `POLICY_AUD` e `TEAM_DOMAIN`; criar uma regra catch-all de Email Routing apontando para o Worker; habilitar o binding `send_email`; e criar um mailbox pela interface.

## Exemplos de uso

O README não publica exemplos de conversa com o agente nem chamadas ao MCP. Os fluxos que ele descreve são: ler e buscar e-mails no painel, pedir um rascunho de resposta, organizar pastas e anexos. Qualquer prompt de exemplo seria inventado.

## Quando usar (e quando não usar)

- **Use quando:** você quer um cliente de e-mail próprio, com agente e MCP, sem operar servidor de e-mail.
- **Use quando:** já usa Cloudflare e quer aproveitar Email Routing, Workers, R2 e Workers AI na mesma conta.
- **Use quando:** o caso é pessoal ou de equipe pequena e uma política única de Cloudflare Access é um limite aceitável.
- **Evite quando:** você precisa de autorização por mailbox ou por usuário. O README afirma explicitamente que qualquer usuário que passe na política compartilhada acessa todos os mailboxes, inclusive pelo MCP.
- **Evite quando:** precisa de portabilidade. O produto depende de componentes proprietários da Cloudflare (Durable Objects, Email Routing, Workers AI) e não descreve exportação.
- **Evite quando:** a conta Cloudflare não pode expor e-mail e anexos a um serviço de terceiros, mesmo que seja a própria plataforma de hospedagem.

## Limitações e cuidados

- **Somente o README foi lido.** Código, `wrangler.jsonc`, testes, frontend e implementação das nove ferramentas não foram consultados. As capacidades são afirmações do projeto.
- **Fronteira de confiança única.** O README declara que não há autorização por mailbox: a política do Cloudflare Access é o único limite, e ferramentas externas via MCP podem operar em qualquer mailbox passando `mailboxId`. Em ambiente compartilhado, isso significa acesso total por qualquer pessoa autorizada.
- **Dependência de plataforma.** E-mail recebido, enviado, armazenado e processado por IA passa por serviços Cloudflare; não há descrição de uso de outro provedor.
- **Modelo de IA fixo no README.** O agente usa `@cf/moonshotai/kimi-k2.5` via Workers AI; a possibilidade de trocar de modelo não é documentada.
- **Custo não detalhado.** Workers, Durable Objects, R2, Workers AI e Email Routing têm cobrança própria; o README não estima consumo por mailbox.
- **Setup em várias etapas.** O próprio README avisa que o botão de deploy é só parte do processo e aponta para um comentário de issue com o guia completo — sinal de que a configuração é propensa a erro.
- **Produção exige Access.** A aplicação se recusa a rodar sem Cloudflare Access fora do desenvolvimento local, por design.
- **Envio exige confirmação.** Rascunhos automáticos não são enviados sem confirmação explícita; **A verificar** como isso é imposto no código e se o MCP respeita a mesma regra.

## Estado e adoção

- **Atividade e popularidade observadas em 2026-10-19:** ~8,4 mil estrelas, ~1,1 mil forks, 55 issues abertas; criado em 2026-04-10 e último push em 2026-04-23.
- **Licença:** Apache-2.0.
- **Linguagem principal:** TypeScript.
- **Commit de referência:** `48039bb6785af34e592c2966f87cde2b255c4c80`.

## Relações

- **Mantido por:** [Cloudflare](../../../entities/cloudflare.md).
- **Conceitos:** [Email para agentes](../../../concepts/email-para-agentes.md) — cliente de e-mail com agente e MCP; [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — servidor em `/mcp`; [Memória de agente](../../../concepts/memoria-de-agente.md) — histórico de chat persistente por mailbox; [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md).
- **Stack:** Cloudflare Workers, Durable Objects, R2, Email Routing, Email Service, Workers AI, Agents SDK.
- **Alternativas:** não há outro cliente de e-mail documentado na wiki. Projetos de agentes que consomem MCP podem usar este inbox como fonte de contexto.

## Perguntas abertas

- Como impor autorização por mailbox sem quebrar o modelo de Durable Objects e o servidor MCP?
- O agente pode enviar sem confirmação em algum caminho, por exemplo via MCP ou chamada direta à API?
- Qual é o custo mensal de uma conta Cloudflare com um mailbox ativo e uso moderado do agente?
- Como anexos são escaneados contra malware antes de chegar ao modelo?
- É possível trocar o modelo de Workers AI por outro provedor?
- Como exportar e-mails e anexos, e o que acontece se o Worker for removido?
- Qual é a política de retenção de histórico de chat e de dados no SQLite?

## Fontes

- README: https://github.com/cloudflare/agentic-inbox/blob/main/README.md (commit `48039bb6785af34e592c2966f87cde2b255c4c80`, consultado em 2026-10-19). Somente o README foi lido; código, configuração e demais arquivos do repositório não foram consultados.
- Metadados do repositório e da organização: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues e datas).
- Post citado pelo projeto: https://blog.cloudflare.com/email-for-agents/ (não consultado diretamente nesta ingestão).
