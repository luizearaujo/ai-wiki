---
type: repo
url: https://github.com/openai/codex-plugin-cc
host: github.com
owner: openai
repo: codex-plugin-cc
commit: db52e28f4d9ded852ab3942cea316258ae4ef346
license: Apache-2.0
language: JavaScript
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [plugin, claude-code, codex, revisao-de-codigo, interoperabilidade]
---

# openai/codex-plugin-cc

> Plugin oficial da OpenAI para usar o Codex de dentro do Claude Code — review de código e delegação de tarefas sem sair do fluxo de trabalho existente.

## O que é

`codex-plugin-cc` é um plugin de Claude Code publicado pela própria OpenAI que expõe o Codex (CLI e app server da OpenAI) como um conjunto de slash commands dentro do Claude Code. O README o descreve como voltado a quem já usa Claude Code e quer uma forma simples de também usar o Codex, sem trocar de ferramenta — uma ponte entre os dois ecossistemas de agentes de código em vez de um runtime próprio.

## Como funciona

O plugin não traz runtime de Codex embutido: ele chama o binário `@openai/codex` já instalado localmente e o Codex app server, reaproveitando a autenticação existente em `~/.codex`. Isso significa que usa a mesma instalação, o mesmo login e o mesmo checkout de repositório que o Codex usaria se chamado diretamente.

Comandos (`/codex:*`):

| Comando | Função |
|---|---|
| `/codex:review` | Review de código somente leitura, sobre mudanças não commitadas ou comparando com uma branch base (`--base`); suporta `--wait`/`--background`. |
| `/codex:adversarial-review` | Review **esteirável** que desafia decisões e trade-offs; aceita texto de foco extra além das mesmas flags do `review`. |
| `/codex:rescue` | Delega investigação ou correção ao Codex via o subagente `codex:codex-rescue`; suporta `--background`, `--wait`, `--resume`, `--fresh` e seleção de modelo/esforço. |
| `/codex:transfer` | Cria uma thread persistente no Codex a partir da sessão atual do Claude Code e devolve um comando `codex resume <session-id>`. |
| `/codex:status` / `/codex:result` / `/codex:cancel` | Checam, mostram o resultado final ou cancelam um job do Codex em segundo plano. |
| `/codex:setup` | Verifica se o Codex está instalado/autenticado; oferece instalar via npm; gerencia o "review gate" opcional. |

O "review gate" opcional usa um hook `Stop` do Claude Code para rodar uma revisão direcionada do Codex a cada resposta do Claude e bloquear o fim da sessão se a revisão encontrar problemas — o README adverte que isso pode criar um loop longo entre Claude e Codex e consumir limite de uso rapidamente, recomendando ativá-lo só sob supervisão ativa.

## Instalação e uso rápido

Requisitos: assinatura do ChatGPT (incluindo o plano gratuito) ou chave de API da OpenAI; Node.js 18.18+.

```bash
/plugin marketplace add openai/codex-plugin-cc
/plugin install codex@openai-codex
/reload-plugins
/codex:setup
```

Se o Codex não estiver instalado e o npm estiver disponível, `/codex:setup` oferece instalá-lo (`npm install -g @openai/codex`); se estiver instalado mas sem login, `!codex login` resolve. Primeiro uso sugerido no README:

```bash
/codex:review --background
/codex:status
/codex:result
```

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- Revisar a branch atual contra `main` antes de abrir um PR: `/codex:review --base main`.
- Desafiar uma decisão de cache e retry específica: `/codex:adversarial-review --base main challenge whether this was the right caching and retry design`.
- Delegar a investigação de um teste instável: `/codex:rescue --background investigate the flaky integration test`.
- Pedir em linguagem natural, sem comando: "Ask Codex to redesign the database connection to be more resilient."

## Quando usar (e quando não usar)

- **Use quando:** já se trabalha em Claude Code e se quer uma segunda opinião de review (incluindo um review adversarial) ou delegar uma tarefa pontual ao Codex, sem sair da sessão.
- **Evite quando:** não se tem conta/chave da OpenAI configurada, ou quando o "review gate" automático não é desejável por consumir uso rapidamente em loops Claude↔Codex.
- **Alternativa:** usar o Codex diretamente, fora do Claude Code, quando não há necessidade de permanecer no fluxo do Claude Code.

## Limitações e cuidados

- **Somente o README foi lido.** A implementação dos comandos, do subagente `codex:codex-rescue` e do hook `Stop` do review gate não foi inspecionada.
- Uso do plugin conta para os limites de uso do Codex do usuário (não é uma camada gratuita adicional).
- O "review gate" é declarado explicitamente como arriscado para consumo de limite de uso sem supervisão.
- `/codex:transfer` exige que a origem esteja sob `~/.claude/projects` e uma versão do Codex que exponha importação de sessão externa; versões antigas precisam ser atualizadas.
- Fontes externas (não o README) discordam sobre a contagem exata de comandos (seis vs. três, segundo diferentes resenhas) e sobre a data exata de lançamento (30 ou 31 de março de 2026) — **a verificar** diretamente no histórico do repositório se necessário.

## Estado e adoção

- Versão: não publicada no corpo do README; fontes externas (não verificadas aqui) citam 1.0.5.
- Atividade observada em 2026-10-23: 34.515 estrelas, 2.382 forks, 537 issues abertas; repositório criado em 2026-03-30, último push em 2026-07-08.
- Licença: Apache-2.0.
- Linguagem principal (API): JavaScript.

## Relações

- Mantido por: [OpenAI (openai)](../../../entities/openai.md).
- Integra-se com: Codex CLI e Codex app server da própria OpenAI (`@openai/codex`), via autenticação local compartilhada.
- Conceitos: [Plugins de agente](../../../concepts/plugins-de-agente.md) — unidade de extensão que adiciona comandos e um subagente ao Claude Code sem alterar seu núcleo; [TDD para agentes](../../../concepts/tdd-para-agentes.md) — o review gate como contrapressão automática sobre o que o Claude produz, embora não seja TDD propriamente.

## Perguntas abertas

- Qual é o comportamento exato do hook `Stop` do review gate quando o Codex e o Claude discordam repetidamente?
- Como o plugin se comporta em monorepos ou workspaces com múltiplos `config.toml` de Codex em conflito?
- Existe alguma telemetria enviada pelo plugin além do uso normal de API do Codex?

## Fontes

- README: https://github.com/openai/codex-plugin-cc/blob/main/README.md (commit `db52e28f4d9ded852ab3942cea316258ae4ef346`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-23).
