---
type: concept
aliases: [CLI agent-first, Agent-first CLI, Agent DX, DX para agentes]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [cli, agent-dx, design-de-ferramentas, agentes, seguranca]
---

# CLI agent-first

> Desenho de interfaces de linha de comando cujo consumidor principal é um agente: saída estruturada e estável, entrada sem tradução, introspecção de schema, proteção de contexto e defesa contra falhas típicas de modelos.

## Definição

CLI agent-first é uma CLI otimizada para **previsibilidade e defesa em profundidade**, não para descoberta e tolerância a erro. A distinção é apresentada pela skill [Agent DX CLI Scale](../skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md) como a diferença entre *human DX* e *agent DX*: um humano explora `--help`, tolera tabelas coloridas e corrige um caminho digitado errado; um agente precisa parsear a saída sem heurística, enviar payloads completos, descobrir o schema em runtime, limitar o que entra no contexto e não ser tratado como operador confiável.

Não se confunde com:

- **CLI amigável para humanos** — pode ter a mesma lógica por baixo, mas otimiza mensagens, cores e descoberta;
- **MCP** — protocolo de ferramentas; uma CLI agent-first pode expor MCP como uma das superfícies;
- **biblioteca/SDK** — contrato em código, sem a camada de processo, flags e streams.

A distinção é de **consumidor e contrato de saída**: a mesma ferramenta pode ter um modo humano e um modo agente, mas só o segundo é avaliado pelos critérios abaixo.

## Como funciona

A escala publicada organiza o desenho em sete eixos, cada um pontuado de 0 a 3:

| Eixo | O que mede | Sinal de maturidade |
| --- | --- | --- |
| **Saída legível por máquina** | Parseabilidade sem heurísticas. | JSON consistente em todos os comandos, inclusive erros; NDJSON e padrão fora de TTY no nível máximo. |
| **Entrada de payload cru** | Capacidade de enviar o payload da API sem tradução. | Payload cru é primeira classe ao lado de flags; o schema da API serve de documentação. |
| **Introspecção de schema** | Descoberta do que a CLI aceita em runtime. | Schemas resolvidos em runtime, com escopos, enums e tipos aninhados. |
| **Disciplina de contexto** | Controle do tamanho da resposta. | Field masks em todas as leituras, paginação por stream e orientação explícita. |
| **Endurecimento de entrada** | Defesa contra alucinação do agente. | Rejeição de `../`, `%2e`, `?` e `#`; sandbox de saída; postura "o agente não é confiável". |
| **Trilhos de segurança** | Validação antes da ação e sanitização da resposta. | `--dry-run` em todas as mutações e proteção contra prompt injection em dados. |
| **Empacotamento de conhecimento** | Conhecimento consumível no início da conversa. | Skills versionadas com guardrails, em vez de apenas `--help` e um site. |

O total vai de 0 a 21 e classifica a ferramenta em **human-only** (0–5), **agent-tolerant** (6–10), **agent-ready** (11–15) ou **agent-first** (16–21). Fora da pontuação, a skill pede uma observação de **prontidão multi-superfície**: MCP via stdio, instalação como extensão/plugin e autenticação headless por variáveis de ambiente.

Três padrões atravessam os eixos:

1. **Estrutura antes de ergonomia.** O agente precisa de um contrato estável de entrada e saída; mensagens bonitas são secundárias.
2. **Contexto é recurso escasso.** Field masks, paginação e streaming existem para que a resposta caiba na janela sem perder evidência.
3. **O agente não é confiável por padrão.** Validação de caminho, `--dry-run`, sandbox e sanitização tratam a entrada como potencialmente hostil ou alucinada.

## Onde aparece

- [Agent DX CLI Scale](../skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md) — instrumento de avaliação que define os sete eixos, as faixas e o bônus multi-superfície.
- [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — implementa no código a parte de entrada/saída estruturadas e erros como valores, em vez de exceções.
- [Ink](../skills/github.com/google-labs-code/design.md/ink.md) — mostra a superfície de saída de terminal como spec declarativa, com componentes e eventos definidos.
- [TDD Red-Green-Refactor](../skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md) — verificação como contrapressão ao comportamento do agente que opera a ferramenta.

## Trade-offs

- **Vantagens:** menos tokens gastos em parsing e tentativa e erro; menos alucinação de flags e payloads; auditoria e automação mais simples; a mesma superfície serve agentes e scripts.
- **Limitações:** mais trabalho de design e manutenção; JSON verboso pode custar contexto se não houver field masks; `--dry-run` e introspecção aumentam a superfície da CLI; a escala não mede qualidade da tarefa, só o desenho da interface.
- **Critério prático:** a CLI precisa ser agent-first quando agentes a operam em volume ou em ações com efeito colateral; para uso humano ocasional, o custo pode não se pagar.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — conhecimento empacotado que a CLI pode distribuir; [Contratos tipados de serviço](contratos-tipados-de-servico.md) — mesma disciplina de contrato, no nível do código; [Model Context Protocol](model-context-protocol.md) — superfície alternativa ou complementar para expor ferramentas.
- **Contrasta com:** human DX, que otimiza descoberta e perdão de erro.
- **Pré-requisito para:** automação confiável de agentes sobre ferramentas de linha de comando e para avaliação comparável entre CLIs.

## Perguntas abertas

- Os sete eixos têm o mesmo peso em todos os domínios, ou deveriam variar por risco e volume?
- Como medir na prática a redução de tokens e de erros atribuível a cada eixo?
- Vale a pena manter dois modos (humano e agente) ou um único modo estruturado?
- MCP torna flags e saída JSON obsoletos, ou as duas superfícies coexistem?
- Como validar "sanitização contra prompt injection" sem um benchmark comum?

## Fontes

- [Agent DX CLI Scale](../skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md) — `SKILL.md` renderizado na página do skills.sh (consultada em 2026-10-19).
- [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — `SKILL.md` renderizado na página do skills.sh (consultada em 2026-10-19).
- https://github.com/google-labs-code/design.md — metadados e árvore via API do GitHub em 2026-10-19 (commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`); o repositório não foi clonado.
