---
type: repo
url: https://github.com/camtrik/agent-trail
host: github.com
owner: camtrik
repo: agent-trail
commit: 6e53f21f292955974ac21a082edb4ac216e2ad92
license: MIT
language: TypeScript
status: active
created: 2026-10-25
ingested: 2026-10-25
updated: 2026-10-25
tags: [observabilidade, agentes, claude-code, codex, dashboard, sessoes, tokens, replay, subagentes]
---

# camtrik/agent-trail

> Dashboard local de observabilidade para agentes de código: agrega token usage, custo estimado, tool calls e árvores de subagentes de sessões JSONL/SQLite, com replay completo turno a turno.

## O que é

Agent Trail é uma ferramenta de observabilidade local-only que lê os arquivos de sessão que seus agentes já produzem (JSONL para Claude Code, OpenClaw e Codex; SQLite para OpenCode e Qoder) e os indexa em um banco SQLite local. Não modifica os agentes, não reexecuta tool calls, não envia dados para fora da máquina.

Instalado via npm como `@camtrik/agent-trail` e acessado pelo navegador em `localhost:3030`.

## Funcionalidades

### Dashboard de uso agregado

Centraliza consumo de tokens e custo estimado em USD para Claude Code, OpenClaw, Codex, OpenCode e Qoder — por sessão, projeto, modelo e janela temporal (hoje / semana / total). Inclui live activity feed à medida que novas sessões são gravadas em disco.

### Session replay com estrutura interna

Reproduz qualquer sessão turno a turno, expondo a estrutura interna de cada turno do assistente:

- **Tool calls**: expandir qualquer `Bash`, `Read`, `Edit`, `Write` ou ferramenta customizada para ver argumentos e saída completa recebida pelo modelo
- **Subagent trees**: quando Claude Code ou OpenClaw lança um subagente, renderiza a árvore aninhada — qual subtarefa foi delegada, quais instruções recebeu e o que retornou
- **Contexto injetado e eventos de sistema**: contexto oculto, prompts de permissão e mensagens sintéticas que normalmente ficam entre os turnos
- **Token accounting por turno**: input, output, cache-read, cache-write e reasoning tokens no nível do turno, não apenas da sessão

### Skill `local-session-search`

Skill bundled em `.agents/skills/local-session-search/SKILL.md` que ensina um agente de código (Claude Code, Codex etc.) a buscar sessões históricas via a API local de ingestão (`GET /api/v1/sessions/search`) sem precisar do session ID. Retorna `source`, `sessionId`, título, projeto, `updatedAt` e trecho para o agente localizar a sessão certa.

## Instalação

**npm (recomendado, Node.js 22+):**
```bash
npm install -g @camtrik/agent-trail
agent-trail
```

**Docker (imagem publicada):**
```bash
docker run --rm -p 127.0.0.1:3030:3030 \
  -v "$HOME/.claude/projects:/agents/claude:ro" \
  -e CLAUDE_PROJECTS_DIR=/agents/claude \
  ghcr.io/camtrik/agent-trail:latest
```

Montar diretórios adicionais com `-v` e a variável de ambiente correspondente (`OPENCLAW_DIR`, `CODEX_SESSIONS_DIR`, `OPENCODE_DB_PATH`).

## Agentes suportados

| Agente | Fonte |
|---|---|
| **Claude Code** | `~/.claude/projects/**/*.jsonl` |
| **OpenClaw** | `~/.openclaw/agents/*/sessions/*.jsonl` |
| **Codex** | `~/.codex/sessions/**/*.jsonl` |
| **OpenCode** | `~/.local/share/opencode/opencode.db` (SQLite) |
| **Qoder** | cache DB local (token counts; custo excluído dos rollups) |

## Arquitetura

- Dois serviços em desenvolvimento: Next.js (porta 3000) + ingest service (porta 8078)
- Dados indexados em SQLite local (`data/ingest.db`)
- Dashboard é read-only — nunca reexecuta tool calls
- Sem telemetria, sem dados saindo da máquina

## Posicionamento

Foco em **custo e rastreabilidade** (token accounting por turno, árvore de subagentes, contexto injetado), diferentemente de [sodiumsun/agenttrail](../sodiumsun/agenttrail.md), que foca em **progresso do projeto** (PLAN.md, mudanças de arquivo, metáfora culinária 3D). Os dois cobrem múltiplos agentes locais, mas com ângulos distintos.

**A verificar:** sem informações sobre roadmap, comparação com outras ferramentas de observabilidade ou suporte a outros runtimes além dos listados. Somente o README foi lido.

## Fontes

- README no commit `6e53f21f292955974ac21a082edb4ac216e2ad92` (consultado em 2026-10-25). Somente o README foi lido.
- Metadados: GitHub API — TypeScript, 40 estrelas (2026-10-25), licença não detectada pela API mas declarada MIT no README.
