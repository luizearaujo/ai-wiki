---
type: repo
url: https://github.com/dietrichgebert/ponytail
host: github.com
owner: dietrichgebert
repo: ponytail
commit: 09c434ab73ca43761c5d8b0c5d341926c2fba710
license: MIT
language: JavaScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, skills, yagni, minimalismo, codigo, claude-code, codex, revisao-de-codigo]
---

# dietrichgebert/ponytail

> Skill e plugin que faz o agente de código escrever só o que a tarefa exige — menos código, menos custo e mais testes — sem cortar validação, segurança ou acessibilidade.

## O que é

O README apresenta o Ponytail como a personificação do "dev sênior mais preguiçoso da sala": lê o código, diz pouco e troca cinquenta linhas por uma. A promessa é instalar esse comportamento em agentes de código, com uma regra explícita: **escrever apenas o que a tarefa precisa**.

O projeto rejeita a leitura de que o objetivo é "menos tokens". Segundo o README, código menor é consequência de necessidade, não de golfe de tokens, e economia de custo e latência é efeito colateral. A versão atual anunciada é a linha **5.x**, com o recurso **5.3 "the band"**.

O núcleo é um único prompt — [`skills/ponytail/SKILL.md`](https://github.com/DietrichGebert/ponytail/blob/main/skills/ponytail/SKILL.md) — e o restante do repositório são adaptadores que carregam esse prompt em diferentes agentes.

## Como funciona

### A escada

Antes de escrever código, o agente para no primeiro degrau que resolve o problema:

| Degrau | Pergunta |
|---|---|
| 1 | Isso precisa existir? |
| 2 | Já existe neste código? |
| 3 | A biblioteca padrão resolve? |
| 4 | Há recurso nativo da plataforma? |
| 5 | Uma dependência já instalada resolve? |
| 6 | Dá para ser uma linha? |
| 7 | Só então: o mínimo que funciona, com um teste pequeno se houver lógica. |

A escada roda **depois** de entender o problema: o agente lê o código tocado pela mudança e traça o fluxo real antes de escolher o degrau. O README resume a postura como "preguiçoso na solução, nunca na leitura".

### O que nunca é cortado

Validação em fronteira de confiança, tratamento de perda de dados, segurança e acessibilidade não entram na tesoura. Lógica com branch, loop, parser, dinheiro ou segurança deixa um teste pequeno. Toda resposta termina declarando o que foi omitido, o que não foi verificado e o risco envolvido.

### Comandos e modos

- **Modos:** `/ponytail [lite | full | ultra | off]`; sem argumento, liga no padrão ou informa o nível atual. O nível aparece no texto de inicialização e de troca de modo.
- **`/ponytail-review`:** revisa o diff como o sênior que é acionado quando algo quebra — lê o código tocado, não apenas o diff, e cobre bugs, segurança, carga real, testes ausentes, caminhos lentos e o que cortar. Cada achado diz o que o código faz, o que dá errado, como corrigir e o que acontece se nada for feito. Aceita alvos como `uncommitted`, `staged`, `branch` ou link de PR.
- **`/ponytail-audit`:** aplica as mesmas verificações ao repositório inteiro, mapeia pontos de entrada e fluxo de dados e ranqueia o que corrigir primeiro.
- **`/ponytail-debt`:** colhe comentários `shortcut:` adiados em um registro, para que "depois" não vire "nunca".
- **`/ponytail-gain`:** mostra o placar medido no benchmark.
- **`/ponytail-help`:** referência rápida.

### The band (5.3, só Claude Code)

Em Claude Code, uma faixa acima do prompt mostra custo da tarefa, tokens, tempo do agente, taxa de reutilização de código existente e se os testes passaram após a última mudança. Os botões acionam `/ponytail-review`, `/ponytail-audit`, copiam a tarefa em Markdown ou recolhem a faixa. Requer Claude Code 2.1.290 ou superior, em terminal ou app desktop; não aparece no painel de chat do VS Code, em sessões cloud nem em `claude -p`.

O **board** abre uma página local (`~/.config/ponytail/band/` por padrão) com custo, tempo de agente, tokens, sessões e testes ao longo do tempo; `/ponytail band import` adiciona sessões antigas do Claude Code.

## Instalação e uso rápido

**Claude Code:**

```
/plugin marketplace add DietrichGebert/ponytail
/plugin install ponytail@ponytail
```

**Codex:**

```bash
codex plugin marketplace add DietrichGebert/ponytail
codex plugin add ponytail@ponytail
```

Depois, abrir `/hooks` no Codex, confiar nos dois hooks de ciclo de vida e iniciar uma nova thread.

**Qualquer outro agente:** copiar o `AGENTS.md` para o projeto ou pedir ao agente que instale `skills/ponytail/SKILL.md` como skill. Instruções específicas para Copilot, Cursor, OpenCode, Gemini e outros estão no `INSTALL.md`.

Não há arquivo de configuração obrigatório; um `~/.config/ponytail/config.json` ou a variável `PONYTAIL_DEFAULT_MODE` podem definir o nível padrão.

O README alerta para instalar somente a partir de `DietrichGebert/ponytail` no GitHub ou de `@dietrichgebert/ponytail` no npm: o projeto nunca distribui `.exe` ou `.dll`, e uma cópia que distribua não é do autor.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Seletor de data:** sem o Ponytail, o agente instala uma biblioteca ou constrói um calendário à mão (335 linhas no exemplo); com ele, reutiliza o componente `Input` existente com `type="date"` e deixa o calendário para o navegador (10 linhas).
- **Revisão de mudança:** rodar `/ponytail-review branch` antes de abrir o PR para pegar problemas fora do diff, como um arquivo não tocado que passa a quebrar.
- **Dívida acumulada:** rodar `/ponytail-debt` para transformar comentários `shortcut:` em um registro acionável.
- **Medição:** `/ponytail-gain` para ver o placar do benchmark declarado.
- **Acompanhamento:** manter a *band* ligada no Claude Code para observar custo, tokens e testes por tarefa.

## Quando usar (e quando não usar)

- **Use quando:** o agente tende a inflar soluções, instalar dependências desnecessárias, construir componentes nativos à mão ou revisar apenas o diff.
- **Use quando:** o time quer uma política explícita de YAGNI e de "menor código que funciona", com testes preservados para lógica de risco.
- **Evite quando:** a tarefa exige deliberadamente uma solução robusta de longo prazo que o YAGNI classificaria como prematura, ou quando o agente já opera sob regras de engenharia mais específicas do projeto. O README não discute composição com outros conjuntos de regras além de permitir trocar a palavra `shortcut:` via `CLAUDE.md`/`AGENTS.md`.

## Limitações e cuidados

- **Somente o README foi lido.** Não foram verificados o prompt real, os adaptadores, a implementação da *band* nem os scripts do benchmark.
- **Resultados são auto-relatados:** o README cita 39 tarefas em Claude Code com Opus 5.5 e 5 execuções por configuração; método, tabelas e limites estariam em `benchmarks/results/2026-10-07-agentic.md`, não consultado.
- **Escopo de host:** comandos exigem host com suporte a skills; adaptadores somente de instrução (regra do Cursor, Windsurf, Cline, Copilot, Kiro) carregam as regras sempre ligadas sem os comandos.
- **A *band* depende do Claude Code 2.1.290+** e não funciona em todos os modos do produto, segundo o próprio README.
- **Supply chain:** o README alerta sobre cópias que distribuem binários; a verificação de integridade de pacotes npm/plugin **A verificar**.
- **Licença MIT**, compatível com uso e redistribuição, sem garantias.

## Estado e adoção

- **Versão/releases citadas no README:** linha 5.x; recurso 5.3; comparações com a versão 4.13.
- **Atividade e popularidade observadas em 2026-10-19:** 167.764 estrelas, 9.115 forks, 34 issues abertas; repositório criado em 2026-06-12; último push em 2026-10-18.
- **Licença:** MIT.
- **Linguagem principal (API):** JavaScript.
- **Site:** [ponytail.dev](https://ponytail.dev), com página de histórias de uso e waitlist.

## Relações

- **Mantido por:** [dietrichgebert](../../../entities/dietrichgebert.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — o produto é distribuído como skill/plugin para múltiplos agentes; [TDD para agentes](../../../concepts/tdd-para-agentes.md) — lógica de risco deixa um teste pequeno; [CLAUDE.md](../../../concepts/claude-md.md) — o README permite ajustar termos via regras do projeto; [CLI agent-first](../../../concepts/cli-agent-first.md) — os comandos operam no terminal.
- **Relacionado:** [addyosmani/agent-skills](../addyosmani/agent-skills.md) — também empacota práticas de engenharia como skills; [mattpocock/skills](../mattpocock/skills.md) — coleção de skills de engenharia.
- **Alternativas:** não há alternativa equivalente citada no README.

## Perguntas abertas

- Como o prompt lida com composição de regras de projeto que pedem explicitamente uma solução mais extensa?
- Os números de −53% de código, −41% de tempo, −26% de custo e −45% de tokens se sustentam fora do benchmark do autor?
- A *band* mede custo e tokens corretamente em diferentes providers e planos?
- Quais hooks de ciclo de vida o Codex executa, e que permissões eles recebem?
- O comportamento "ultra" tem limites documentados ou é apenas intensidade retórica?

## Fontes

- README: https://github.com/DietrichGebert/ponytail/blob/main/README.md (commit `09c434ab73ca43761c5d8b0c5d341926c2fba710`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19).
