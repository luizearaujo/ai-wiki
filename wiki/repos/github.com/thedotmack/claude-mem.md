---
type: repo
url: https://github.com/thedotmack/claude-mem
host: github.com
owner: thedotmack
repo: claude-mem
commit: 3fae1eb45ba1a7fbd4818527f48b439991a273da
license: Apache-2.0
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [memoria-de-agente, claude-code, busca-hibrida]
---

# thedotmack/claude-mem

> Sistema de memória persistente para Claude Code: captura observações de uso de ferramentas durante a sessão, comprime-as com IA e injeta contexto relevante em sessões futuras, com busca híbrida semântica e por palavra-chave.

## O que é

Claude-Mem resolve a perda de contexto entre sessões de um agente de código: observa o que o agente fez, gera resumos semânticos e os torna disponíveis depois que a sessão termina, para que o Claude mantenha o contexto do projeto.

## Como funciona

- **Hooks de ciclo de vida** (`SessionStart`, `UserPromptSubmit`, `PreToolUse`, `PostToolUse`, `Stop`, `SessionEnd`) executam `claude-mem hook claude-code <event>`.
- Um **worker service**, gerenciado pelo Bun, expõe uma API HTTP local e um visualizador web.
- Um **banco SQLite** armazena sessões, observações e resumos, com busca FTS5.
- Um **banco vetorial Chroma** fornece busca híbrida semântica e por palavra-chave.
- A skill `mem-search` suporta consultas em linguagem natural com *progressive disclosure*.
- Busca em **3 camadas**: `search` retorna um índice compacto, `timeline` dá contexto cronológico, e `get_observations` busca detalhes completos só para IDs selecionados — o README reivindica cerca de 10x de economia de tokens com essa filtragem.

## Instalação e uso rápido

- **Claude Code (recomendado):** `npx claude-mem install`. Oferece login no navegador para um observador hospedado com trial gratuito de 30 dias; pular login com `--provider`, `CLAUDE_MEM_ONLINE_OPTIN=false` ou shell não interativo.
- **Marketplace de plugins:** `/plugin marketplace add thedotmack/claude-mem`, depois `/plugin install claude-mem`, depois reiniciar o Claude Code.
- **Outros IDEs/harnesses:** OpenCode, T3 Code, Antigravity CLI, OMP, Pi, DeepSeek Harness, Grok Bot e gateways OpenClaw, cada um com opção `--ide` ou script próprio.
- O pacote npm instala apenas o SDK/biblioteca, não os hooks do plugin nem o worker — o README alerta contra depender só de `npm install -g`.
- Configuração em `~/.claude-mem/settings.json`; modos como `code`, `code--zh`, `code--ja` controlam workflow e idioma de saída (requer reiniciar o Claude Code).
- Pré-requisitos: Node.js ≥ 20.0.0, Claude Code com suporte a plugins, Bun e uv (auto-instalados se ausentes), SQLite 3 (embutido); no Windows, Node/npm no PATH (hooks não precisam de Git Bash).

## Exemplos de uso

```typescript
search(query="authentication bug", type="bugfix", limit=10)
get_observations(ids=[123, 456])
```
A primeira chamada retorna um índice; a segunda busca detalhes completos só para os IDs escolhidos.

- Envolver conteúdo em tags `<private>` o exclui do armazenamento.
- O visualizador web traz uma página "My Work" com memória, sessões e configurações; um workspace opcional "TeamBrain" suporta trabalho compartilhado em equipe.

## Quando usar (e quando não usar)

- **Use quando:** quiser contexto automático entre sessões do Claude Code (ou outros harnesses suportados) sem retomar manualmente o histórico do projeto.
- **Evite quando:** precisar de um pacote só-biblioteca via `npm install -g` (não funciona sozinho) ou quando o harness não tiver hooks nativos — caso do Grok Bot, que depende de observar arquivos de log de chat.

## Limitações e cuidados

- Hooks dependem de `claude-mem` estar no PATH; usuários Windows podem ver erros de "Executable not found" e precisar de `npx claude-mem doctor`.
- Integrações parciais: Grok Bot não tem hooks nativos de host.
- O observador hospedado é pago após o trial; sem assinatura, a memória volta a depender do plano Anthropic do usuário.
- Parte da página do README é promocional (patrocinadores, uma seção sobre um token "CMEM" descrito como de terceiros, link de comunidade) — conteúdo não verificável a partir do README isoladamente.

## Estado e adoção

- Licença: Apache-2.0 — o README indica a escolha como intencional, para facilitar a incorporação da camada de memória em outras ferramentas.
- Linguagem principal (API do GitHub): TypeScript.
- Atividade observada em 2026-10-19: push mais recente no mesmo dia.

## Relações

- Mantido por: [thedotmack](../../../entities/thedotmack.md) (Alex Newman).
- Conceitos: [Memória de agente](../../../concepts/memoria-de-agente.md), [Economia de tokens em agentes](../../../concepts/economia-de-tokens-em-agentes.md).
- Alternativas: outros formatos de memória citados na wiki em [Memória de agente](../../../concepts/memoria-de-agente.md); menções no próprio README a `mem0`, `openmemory` e `supermemory` como tópicos relacionados (não comparados diretamente no texto).

## Perguntas abertas

- Qual a precisão/custo real da compressão por IA das observações, fora as afirmações do próprio README?
- O que exatamente é o token "CMEM" e qual sua relação formal com o projeto?

## Fontes

- README: https://raw.githubusercontent.com/thedotmack/claude-mem/3fae1eb45ba1a7fbd4818527f48b439991a273da/README.md (commit `3fae1eb45ba1a7fbd4818527f48b439991a273da`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Perfil do GitHub (`api.github.com/repos/thedotmack/claude-mem`, `api.github.com/users/thedotmack`), consultado em 2026-10-19.
