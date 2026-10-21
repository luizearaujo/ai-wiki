---
type: repo
url: https://github.com/ayghri/i-have-adhd
host: github.com
owner: ayghri
repo: i-have-adhd
commit: 1ecea1993b7fce257ffbd686c070948b5e07eda6
license: MIT
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, claude-code, produtividade]
---

# ayghri/i-have-adhd

> Skill de dez regras que impede um agente de código de "enterrar" a resposta sob rodeios — ação primeiro, passos numerados, sem "Hope this helps!" — adaptada de um livro sobre TDAH para como um LLM deve responder, não como uma pessoa deve organizar o dia.

## O que é

O repositório empacota uma única skill (`i-have-adhd`) que reformula o estilo de saída de um agente de código: em vez de explicar o raciocínio antes da ação, ele lidera com o próximo passo concreto. O README mostra o contraste lado a lado — uma resposta "antes" cheia de contexto e cortesias versus uma "depois" com três passos numerados e uma pergunta de acompanhamento objetiva.

## Como funciona

As dez regras, descritas no `SKILL.md`:

1. Liderar com a próxima ação.
2. Numerar tarefas de várias etapas.
3. Terminar com um próximo passo concreto.
4. Suprimir tangentes.
5. Reafirmar o estado a cada turno.
6. Estimativas de tempo específicas (minutos, não "um pouco").
7. Tornar vitórias visíveis.
8. Erros objetivos, sem rodeio.
9. Limitar listas a 5 itens.
10. Sem preâmbulo, sem recapitulação, sem fechos.

A skill é instalada como plugin do Claude Code; para customizar, o README recomenda fazer fork, editar o próprio `skills/i-have-adhd/SKILL.md` e trocar a instalação (desinstalar a cópia upstream, remover o marketplace antigo, adicionar o fork como novo marketplace).

## Instalação e uso

```text
Install the i-have-adhd skill/plugin from https://github.com/ayghri/i-have-adhd, refer to the repo's AGENTS.md for instructions.
```

Para ajustar:

```bash
claude plugin uninstall i-have-adhd
claude plugin marketplace remove i-have-adhd
claude plugin marketplace add <seu-usuario>/i-have-adhd
claude plugin install i-have-adhd@i-have-adhd
```

Reiniciar o agente e invocar `/i-have-adhd` de novo.

## Quando usar (e quando não usar)

- **Use quando:** quer que o agente responda com ação direta e passos numerados, especialmente em sessões rápidas de depuração ou correção, sem precisar pedir isso em cada prompt.
- **Evite quando:** a tarefa exige explicação deliberada do raciocínio para quem vai revisar depois (ex.: documentação de decisão) — a skill suprime justamente o contexto que esse caso pede.

## Limitações e cuidados

- Convenção de opinião, não configurável por parâmetro: para mudar o comportamento, é preciso editar o `SKILL.md` diretamente e manter o próprio fork.
- README disponível em dez traduções, mas o conteúdo técnico (as dez regras) não foi verificado linha a linha nesta ingestão além do que o README em inglês resume.

## Estado e adoção

- 58.109 estrelas, 3.370 forks, 83 issues abertas — observado em 2026-10-21.
- Repositório criado em 2026-05-13, com push mais recente em 2026-10-19 — observado em 2026-10-21.
- Licença: MIT.

## Relações

- Conceitos: [Agent skills](../../../concepts/agent-skills.md).
- Créditos do autor: inspirado em *The Adult ADHD Tool Kit*, de J. Russell Ramsay e Anthony L. Rostain — adaptado para como um LLM deve responder, segundo o próprio README.

## Perguntas abertas

- As dez regras têm algum mecanismo de verificação automática (lint, eval), ou dependem só de o modelo seguir o `SKILL.md`?

## Fontes

- README: https://raw.githubusercontent.com/ayghri/i-have-adhd/1ecea1993b7fce257ffbd686c070948b5e07eda6/README.md (commit `1ecea1993b7fce257ffbd686c070948b5e07eda6`, consultado em 2026-10-21). Somente o README foi lido; o `SKILL.md` e os demais arquivos não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/ayghri/i-have-adhd`), consultada em 2026-10-21.
