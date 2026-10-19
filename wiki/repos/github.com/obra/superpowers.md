---
type: repo
url: https://github.com/obra/superpowers
host: github.com
owner: obra
repo: superpowers
commit: bb92a77741419a4ab5f06e711a283343f1ada0c3
license: MIT
language: Shell
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agent-skills, metodologia, tdd, subagentes, claude-code]
---

# obra/superpowers

> Metodologia completa de desenvolvimento de software para agentes de código, empacotada como skills que disparam automaticamente — design, plano, execução por subagentes e revisão — sem comandos especiais.

## O que é

Superpowers combina skills compostas com instruções iniciais que fazem o agente usá-las sem que o usuário precise invocar comandos. A proposta, de Jesse Vincent (Prime Radiant), é tratar brainstorming, planejamento, TDD e revisão de código como "workflows obrigatórios, não sugestões" — a mesma disciplina em qualquer harness suportado.

## Como funciona

O README descreve o fluxo em três fases, cada uma mapeada a uma skill:

1. **Design:** antes de escrever código, o agente pergunta o que o usuário quer construir e apresenta um documento de design em seções curtas para aprovação (`brainstorming`).
2. **Planejamento:** após aprovação, o agente escreve um plano com tarefas de 2–5 minutos, caminhos de arquivo, código e passos de verificação (`writing-plans`), sob TDD, YAGNI e DRY.
3. **Execução:** o agente despacha subagentes por tarefa, revisando cada um antes de avançar (`subagent-driven-development` ou `executing-plans`, inline quando mais simples).

Skills citadas no fluxo básico: `using-git-worktrees` (branch e workspace isolados com baseline de testes limpo), `test-driven-development` (red-green-refactor, inclusive apagando código escrito antes do teste), `requesting-code-review`/`receiving-code-review` (achados críticos bloqueiam o avanço) e `finishing-a-development-branch` (verifica testes, oferece merge/PR/manter/descartar e limpa o ambiente). O README também cita `systematic-debugging`, `verification-before-completion`, `dispatching-parallel-agents` e `writing-skills`, sem detalhar cada uma.

Se uma sessão se comportar mal, pedir ao agente para "descobrir o que deu errado com o superpowers nesta sessão" aciona a skill `diagnosing-superpowers`, que lê a transcrição e relata evidência linha a linha, podendo empacotar um bundle depurado para relatório de bug.

## Instalação e uso rápido

Instalação é por harness (instalar separadamente se usar mais de um):

- **Claude Code:** `/plugin install superpowers@claude-plugins-official` ou via marketplace Superpowers.
- **Antigravity:** `agy plugin install https://github.com/obra/superpowers`
- **Codex App/CLI, Cursor, Devin CLI, Factory Droid, Gemini CLI, GitHub Copilot CLI, Grok Build CLI, Kimi Code, OpenCode, Pi, Qwen Code, Hermes Agent, Muse:** cada um com comando próprio documentado no README (ex.: `gemini extensions install https://github.com/obra/superpowers`, `pi install git:github.com/obra/superpowers`).

Atualização depende do harness; alguns têm comando próprio, outros são automáticos.

## Exemplos de uso

- Enviar "Let's make a react todo list" em sessão nova deve disparar `brainstorming` antes de qualquer código — exemplo de verificação citado pelo próprio README (testado no Muse).
- Diagnosticar uma sessão anterior citando o ID da sessão.

## Quando usar (e quando não usar)

- **Use quando:** quiser impor processo (design → plano → TDD → revisão) de forma consistente entre vários harnesses de agente, sem depender de comandos manuais.
- **Evite quando:** precisar de execução rápida e informal, sem gate de design/plano, ou quando o harness não estiver na lista suportada e não houver tempo para seguir o `INSTALL.md` específico (caso do OpenCode).

## Limitações e cuidados

- O projeto **geralmente não aceita novas contribuições de skills**; atualizações precisam funcionar em todos os agentes suportados.
- Hermes não tem hook pós-compactação: em sessões muito longas o bootstrap pode se perder, exigindo sessão nova.
- Skills podem não disparar ou disparar errado — por isso existe a skill de diagnóstico dedicada.
- Suporte enterprise, ferramentas e gestão de gastos são comerciais (contato via e-mail no README).
- Telemetria: o componente visual de `brainstorming` carrega um logo com a versão do Superpowers, sem enviar dados de projeto, prompt ou agente; pode ser desativada por variável de ambiente, e respeita os opt-outs de telemetria do Claude Code.

## Estado e adoção

- Licença: MIT.
- Linguagem principal (API do GitHub): Shell.
- Atividade observada em 2026-10-19: push mais recente em 2026-10-10.

## Relações

- Mantido por: [obra](../../../entities/obra.md) (Jesse Vincent, Prime Radiant).
- Conceitos: [TDD para agentes](../../../concepts/tdd-para-agentes.md), [Agent skills](../../../concepts/agent-skills.md), [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md).
- Alternativas: outras coleções de skills de engenharia nesta wiki, como [addyosmani/agent-skills](../addyosmani/agent-skills.md) e [mattpocock/skills](../mattpocock/skills.md).

## Perguntas abertas

- Como a `writing-skills` orienta a criação de novas skills dentro do próprio framework? Não detalhado no README.
- Qual o conteúdo exato do harness de evals (`superpowers-evals`) citado para contribuição?

## Fontes

- README: https://raw.githubusercontent.com/obra/superpowers/bb92a77741419a4ab5f06e711a283343f1ada0c3/README.md (commit `bb92a77741419a4ab5f06e711a283343f1ada0c3`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Perfil do GitHub (`api.github.com/repos/obra/superpowers`, `api.github.com/users/obra`), consultado em 2026-10-19.
