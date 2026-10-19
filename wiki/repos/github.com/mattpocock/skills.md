---
type: repo
url: https://github.com/mattpocock/skills
host: github.com
owner: mattpocock
repo: skills
commit: 5beb35b040e3de97e54fa9e386d7e42d15c295c2
license: MIT
language: Shell
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, skills, engenharia-de-software, tdd, dominio, produtividade, claude-code, codex]
---

# mattpocock/skills

> Coleção de skills pequenas e compostas para engenharia de software real com agentes de código, organizadas em torno de alinhamento, linguagem compartilhada, loops de feedback e design de código.

## O que é

O README apresenta as skills como o que Matt Pocock usa diariamente para “fazer engenharia real, não vibe coding”. O posicionamento é explícito contra abordagens que assumem o processo inteiro — GSD, BMAD e Spec-Kit — porque, ao controlar o fluxo, elas tiram o controle do desenvolvedor e tornam falhas de processo difíceis de diagnosticar.

As skills são descritas como **pequenas, fáceis de adaptar e compostas**, compatíveis com qualquer modelo. A ideia é que o engenheiro continue no comando e use as skills como práticas reutilizáveis, não como um framework que dita o workflow.

## Como funciona

### Quatro falhas que as skills atacam

| Falha | Diagnóstico do README | Skills associadas |
|---|---|---|
| O agente não fez o que o usuário queria | Lacuna de comunicação; a correção é uma **sessão de grilling** com perguntas detalhadas antes de começar. | `/grill-me`, `/grill-with-docs` |
| O agente é prolixo demais | Falta uma **linguagem compartilhada**; um glossário do domínio encurta nomes, variáveis, arquivos e o próprio raciocínio do agente. | `domain-modeling`, `/grill-with-docs` |
| O código não funciona | Faltam **loops de feedback**: tipos estáticos, acesso ao navegador e testes automatizados em red-green-refactor. | `/tdd`, `/diagnosing-bugs` |
| A base virou um “ball of mud” | Agentes aceleram a entropia; é preciso investir no **design de módulos profundos** continuamente. | `/to-spec`, `/improve-codebase-architecture`, `codebase-design` |

### Duas categorias de skill

O README separa as skills por **quem pode invocá-las**:

- **User-invoked:** só são acionadas quando o usuário digita o comando (por exemplo `/grill-me`); servem para orquestrar. Uma skill user-invoked pode chamar model-invoked, mas nunca outra user-invoked.
- **Model-invoked:** podem ser acionadas pelo usuário ou escolhidas automaticamente pelo agente quando a tarefa se encaixa; concentram a disciplina reutilizável.

### Engineering (uso diário em código)

- **User-invoked:** `ask-matt` (roteador entre as skills), `grill-with-docs` (grilling + modelo de domínio, `GLOSSARY.md` e ADRs), `triage` (máquina de estados de triagem de issues), `improve-codebase-architecture` (relatório HTML de oportunidades de aprofundamento seguido de grilling), `setup-matt-pocock-skills` (configuração por repositório), `to-spec` (converte a conversa em spec publicada no issue tracker), `to-tickets` (divide plano em tickets com arestas de bloqueio), `implement` (executa spec/tickets dirigindo `/tdd` e fechando com `/code-review`), `implement-spec` (spec inteira em branch de integração, com subagentes na fronteira pronta), `wayfinder` (mapa de tickets de decisão para trabalho maior que uma sessão) e `retro` (melhorias no ambiente do agente após a sessão).
- **Model-invoked:** `prototype`, `diagnosing-bugs`, `research` (fontes primárias com citações, em background), `tdd`, `domain-modeling`, `codebase-design`, `code-review` (revisão em dois eixos, Standards e Spec, com subagentes paralelos), `pr` (formato do corpo do pull request com evidência antes/depois) e `wizard` (assistente bash interativo para passos humanos).

### Productivity (fluxo geral)

- **User-invoked:** `grill-me` (entrevista implacável sobre plano ou design), `handoff` (compacta a conversa para outro agente continuar), `teach` (ensino multi-sessão usando o diretório como workspace), `to-questionnaire` (transforma uma decisão em questionário assíncrono) e `wait-what` (reapresenta uma mensagem que não ficou clara).
- **Model-invoked:** `grilling` (primitiva de entrevista por trás de `grill-me`, `grill-with-docs`, `triage`, `wayfinder` e `improve-codebase-architecture`) e `writing-for-agents` (como escrever skills, `AGENTS.md`/`CLAUDE.md` e documentos alcançados por ponteiro).

## Instalação e uso rápido

A instalação é por agente, e o README alerta: **escolha um caminho por agente**, porque instalar dois duplica todas as skills. Plugins se atualizam sozinhos; a instalação via `skills.sh` copia arquivos editáveis que o usuário atualiza à mão.

| Agente | Comando | Atualização |
|---|---|---|
| Claude Code | `claude plugin install mattpocock-skills@claude-plugins-official` | automática por padrão |
| Codex | `codex plugin marketplace add mattpocock/skills` + `codex plugin add mattpocock-skills@mattpocock` | automática no startup |
| GitHub Copilot (CLI/VS Code) | `copilot plugin marketplace add ...` + `copilot plugin install ...`; no VS Code, **Chat: Install Plugin From Source** | diária; requer `extraKnownMarketplaces` em `~/.copilot/settings.json` |
| Gemini CLI | `gemini skills install ... --path skills/engineering` e `--path skills/productivity` | manual: repetir os dois comandos |
| Qualquer outro agente | `npx skills@latest add mattpocock/skills -a <agent>` (cursor, opencode, devin, windsurf, amp, pi) | manual: `npx skills@latest update` |

Depois da instalação, rodar `/setup-matt-pocock-skills` **uma vez por repositório**. A skill pergunta qual issue tracker usar (GitHub, GitLab, arquivos locais ou outro), quais labels marcar durante a triagem (usadas por `/triage`) e onde salvar os documentos criados.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Antes de uma mudança:** `/grill-me` ou `/grill-with-docs` para alinhar o escopo; o segundo também atualiza glossário e ADRs.
- **Feature com testes:** `/implement`, que conduz `/tdd` nos seams combinados e fecha com `/code-review`.
- **Bug difícil:** `diagnosing-bugs`, com loop de feedback que fica vermelho, minimização, hipótese, instrumentação, correção e teste de regressão.
- **Trabalho grande:** `wayfinder` para mapear decisões em tickets ou `implement-spec` para processar a spec inteira em uma branch de integração.
- **Manutenção contínua:** `/improve-codebase-architecture` a cada poucos dias para receber candidatos de aprofundamento — o README ressalva que é um levantamento, não um resgate.
- **Troca de sessão:** `handoff` para compactar o contexto antes de outro agente continuar.

## Quando usar (e quando não usar)

- **Use quando:** você quer práticas de engenharia incrementais e editáveis sobre um agente de código, sem adotar um framework que controla o processo inteiro.
- **Use quando:** os problemas recorrentes são desalinhamento de escopo, verbosidade, falta de testes ou degradação arquitetural.
- **Evite quando:** o time precisa de um processo prescritivo e uniforme de ponta a ponta — o README reconhece que GSD, BMAD e Spec-Kit existem justamente para assumir o processo, ao custo de controle.
- **Evite quando:** o agente usado não tem suporte a skills/plugins e você não quer manter arquivos copiados à mão.

## Limitações e cuidados

- **Somente o README foi lido.** Não foram verificados o conteúdo dos `SKILL.md`, a qualidade dos prompts, os installers nem o comportamento real das skills.
- As skills são declaradamente opinativas e derivadas da experiência do autor; não há avaliação publicada de eficácia.
- A instalação manual via `skills.sh` **não se atualiza sozinha**; o README exige rerodar `update` e `add` para receber mudanças e skills novas.
- Instalar pelo plugin e por `skills.sh` no mesmo agente duplica as skills; a escolha é responsabilidade do usuário.
- A configuração por repositório (`/setup-matt-pocock-skills`) é pré-requisito das demais skills de engineering, mas o README não detalha o que acontece se ela for pulada.
- `/improve-codebase-architecture` é explicitamente um levantamento: em bases antigas ele encontra candidatos reais, mas não desembaraça o código sozinho.
- Compatibilidade declarada com “qualquer modelo”, mas os caminhos de instalação cobrem um conjunto específico de agentes; o suporte a outros depende de `skills.sh`. **A verificar.**
- O repositório não publica, no README, versionamento das skills nem política de compatibilidade entre versões.

## Estado e adoção

- **Atividade e popularidade observadas em 2026-10-19:** 297.161 estrelas, 24.949 forks e 196 issues abertas; último push em 2026-10-19; repositório criado em 2026-02-03.
- **Licença:** MIT.
- **Linguagem principal (API):** Shell.
- **Distribuição:** plugin oficial do Claude Code, marketplace próprio para Codex e Copilot, instalação via `skills.sh` e listagem em [skills.sh/mattpocock/skills](https://skills.sh/mattpocock/skills).
- **Divulgação:** newsletter do autor com cerca de 60 mil desenvolvedores, segundo o README.

## Relações

- **Mantido por:** [Matt Pocock](../../../entities/mattpocock.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — o repositório é uma coleção didática do formato; [TDD para agentes](../../../concepts/tdd-para-agentes.md) — `/tdd` e `/diagnosing-bugs` materializam o loop red-green-refactor; [CLAUDE.md](../../../concepts/claude-md.md) — a skill `writing-for-agents` trata de instruções persistentes.
- **Relacionado a:** [addyosmani/agent-skills](../addyosmani/agent-skills.md) — outra coleção de skills de engenharia para agentes; [ComposioHQ/awesome-claude-skills](../composiohq/awesome-claude-skills.md) — catálogo onde coleções como esta podem ser descobertas.
- **Contrasta com:** frameworks que assumem o processo de desenvolvimento (GSD, BMAD, Spec-Kit), citados no README como abordagens opostas em controle.

## Perguntas abertas

- As skills realmente melhoram a qualidade do código em comparação com um agente sem elas? Não há benchmark no README.
- Como as skills se comportam em modelos menores ou fora dos agentes com instalação suportada?
- Qual o custo de contexto de carregar todas as skills de engineering em uma sessão?
- Como o formato de plugin do Codex/Copilot evolui e o que quebra entre versões?
- O glossário e os ADRs produzidos por `/grill-with-docs` são suficientes para reduzir tokens de forma mensurável?

## Fontes

- README: https://github.com/mattpocock/skills/blob/main/README.md (commit `5beb35b040e3de97e54fa9e386d7e42d15c295c2`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19).
