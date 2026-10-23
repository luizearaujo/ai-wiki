---
type: repo
url: https://github.com/open-gsd/gsd-core
host: github.com
owner: open-gsd
repo: gsd-core
commit: 6ddd0cef9cb26673bd8321c5480c0814a92d54cb
license: MIT
language: JavaScript
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [agent-harness, spec-driven-development, context-engineering, meta-prompting, claude-code]
---

# open-gsd/gsd-core (GSD)

> "Git. Ship. Done." — framework leve de engenharia de contexto e desenvolvimento orientado a spec que conduz agentes de código por um loop disciplinado de cinco fases, com subagentes de contexto limpo a cada etapa.

## O que é

GSD Core resolve o que o README chama de "context rot": a degradação de qualidade que se acumula conforme o contexto de um agente de código enche. Em vez de deixar toda pesquisa, planejamento e execução acontecer na mesma sessão, o framework roda esse trabalho pesado em subagentes de contexto novo, mantendo a sessão principal enxuta. Funciona sobre Claude Code, OpenCode, Antigravity CLI, Kimi CLI, Kilo, Codex, Copilot, Cursor, Windsurf e outros.

**Nota de proveniência:** este repositório é o sucessor direto de `glittercowboy/get-shit-done` (GSD / "GSD 2"). O repositório original está arquivado e seu README, no commit referenciado nesta wiki, é só um aviso de redirecionamento para `open-gsd/gsd-core` como "o novo lar ativo" do projeto — por isso a ingestão documenta este repositório, e não o antigo. A API do GitHub reporta o `full_name` atual do antigo repositório como `gsd-build/get-shit-done`, indicando também uma transferência de dono antes do arquivamento.

## Como funciona

Cada milestone repete o mesmo loop de cinco passos, uma fase por vez:

1. **Discuss** — captura decisões de implementação antes de qualquer plano.
2. **Plan** — pesquisa, decompõe e verifica que o plano cabe em uma janela de contexto nova.
3. **Execute** — roda os planos em ondas paralelas; cada executor começa com um contexto limpo de 200 mil tokens.
4. **Verify** — percorre o que foi construído, diagnostica e corrige antes de declarar a fase concluída.
5. **Ship** — cria o PR, arquiva a fase e repete para a próxima.

Artefatos estruturados como `STATE.md` e `CONTEXT.md` sobrevivem às fronteiras de sessão, substituindo memória implícita por estado explícito versionado. O README atribui a essa combinação — subagentes de contexto limpo, artefatos persistentes e um passo de verificação obrigatório — a resiliência contra os três modos de falha que aponta em setups de IA para código: degradação de contexto, ausência de memória compartilhada entre sessões e falta de verificação de que o código funciona.

## Instalação e uso rápido

```bash
npx @opengsd/gsd-core@latest
```

O instalador pergunta o runtime (Claude Code, OpenCode, Antigravity CLI, Kimi CLI, Kilo, Codex, Copilot, Cursor, Windsurf, entre outros) e se a instalação é global ou local; o README orienta a não copiar arquivos de `agents/` ou `commands/` diretamente, pois o instalador é necessário para compatibilidade entre runtimes.

Depois de instalado:

```bash
/gsd-new-project   # projeto novo
/gsd-onboard       # onboarding de um repositório existente
```

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- Iniciar um projeto do zero com `/gsd-new-project` e seguir o tutorial "Your first project" do install ao primeiro shipped phase.
- Fazer onboarding de um codebase existente com `/gsd-onboard`, seguindo "Onboarding an existing codebase".
- Consultar `docs/COMMANDS.md` e `docs/CONFIGURATION.md` como referência autoritativa de comandos e configuração.

## Quando usar (e quando não usar)

- **Use quando:** o projeto é grande ou multi-sessão e o objetivo é manter o agente de código em foco por várias etapas, com histórico de decisões e verificação formal antes de declarar algo pronto.
- **Evite quando:** a tarefa é um script ou correção pontual de sessão única — o próprio ecossistema do projeto reconhece a sobrecarga do processo nesses casos.
- **Alternativas documentadas na wiki:** [obra/superpowers](../../../repos/github.com/obra/superpowers.md) para skills compostas que disparam automaticamente sobre vários harnesses; [garrytan/gstack](../../../repos/github.com/garrytan/gstack.md) para um sprint de produto com especialistas fixos.

## Limitações e cuidados

- **Somente o README foi lido.** Os comandos reais (`agents/`, `commands/`), a implementação do instalador e os documentos de referência linkados (`docs/`) não foram inspecionados.
- **Histórico fragmentado:** o projeto já teve pelo menos três identidades de repositório observadas (`glittercowboy/get-shit-done` → `gsd-build/get-shit-done`, arquivado → `open-gsd/gsd-core`, ativo). Issues, releases e histórico de estrelas anteriores à mudança não foram conciliados.
- Existe um port comunitário para OpenCode (`rokicool/gsd-opencode`), citado no próprio README como "Original OpenCode port" — não ingerido nesta wiki.
- **A verificar:** cobertura funcional equivalente entre os runtimes suportados; o README não detalha diferenças por ferramenta.

## Estado e adoção

- Versão: changelog "What's new in 1.7.0" citado no README (`docs/whats-new-1.7.0.md`); número de versão exato não publicado no corpo do README.
- Atividade observada em 2026-10-23: 10.793 estrelas, 765 forks, 275 issues abertas; repositório criado em 2026-05-22, último push em 2026-10-23.
- Licença: MIT.
- Linguagem principal (API): JavaScript.
- Topics declarados: `claude-code`, `context-engineering`, `meta-prompting`, `spec-driven-development`.

## Relações

- Mantido por: [Open GSD (open-gsd)](../../../entities/open-gsd.md).
- Predecessor: `glittercowboy/get-shit-done` (arquivado; API reporta `full_name` atual `gsd-build/get-shit-done`) — não documentado com página própria por ter README insuficiente (apenas aviso de redirecionamento) no commit consultado.
- Conceitos: [Agent harness](../../../concepts/agent-harness.md) — loop de cinco fases que estrutura contexto e execução sobre vários runtimes; [Memória de agente](../../../concepts/memoria-de-agente.md) — `STATE.md`/`CONTEXT.md` como estado persistente entre sessões; [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — execução em ondas paralelas de subagentes na fase Execute.

## Perguntas abertas

- Qual é o custo real de contexto do próprio framework (comandos, templates, `STATE.md`/`CONTEXT.md`) por fase?
- Como o histórico de estrelas e issues do projeto se relaciona entre as três identidades de repositório observadas?
- O "Discuss" captura decisões de forma auditável o suficiente para substituir review humano em equipes grandes?

## Fontes

- README: https://github.com/open-gsd/gsd-core/blob/main/README.md (commit `6ddd0cef9cb26673bd8321c5480c0814a92d54cb`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-23).
- README de `glittercowboy/get-shit-done` no commit `bdcaab2c752d9a33a1a1ca9acf3a3c81fb991815` (consultado em 2026-10-23) — aviso de redirecionamento, usado só para registrar a proveniência.
