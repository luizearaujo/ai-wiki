---
type: concept
aliases: [YAGNI, Escada de reuso, Lazy senior dev, Minimal code guidance, Código que você não escreveu]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [yagni, engenharia-de-software, agentes, minimalismo, reuso, revisao]
---

# YAGNI para agentes

> Diretriz que obriga o agente a parar no primeiro recurso suficiente — biblioteca padrão, plataforma, dependência já instalada — antes de escrever código novo.

## Definição

**YAGNI** ("You Aren't Gonna Need It") é o princípio de não implementar o que ainda não é necessário. Aplicado a agentes de código, vira uma instrução operacional: antes de gerar código, o agente percorre uma escada de alternativas e só desce para a implementação própria quando nenhuma opção anterior resolve.

O objetivo não é minimizar tokens, e sim **escrever apenas o que a tarefa exige**. Código menor, menos custo e menos latência são consequências, não a regra.

## Como funciona

### A escada de reuso

A formulação mais explícita observada na wiki, do `ponytail`:

| Degrau | Pergunta |
|---|---|
| 1 | Isso precisa existir? |
| 2 | Já existe neste código? |
| 3 | A biblioteca padrão resolve? |
| 4 | Há um recurso nativo da plataforma? |
| 5 | Uma dependência já instalada resolve? |
| 6 | Cabe em uma linha? |
| 7 | Só então: o mínimo que funciona, com um teste pequeno se houver lógica. |

A escada roda **depois** de entender o problema: o agente lê o código afetado e traça o fluxo real antes de escolher o degrau. A preguiça é sobre a solução, não sobre a leitura.

### Carve-outs de segurança

YAGNI não autoriza cortar o que protege o sistema. As fontes preservam explicitamente:

- validação em fronteiras de confiança;
- tratamento de perda de dados;
- segurança;
- acessibilidade;
- um teste pequeno para lógica com ramificação, loop, parser, dinheiro ou segurança.

O README do `ponytail` é explícito: "lazy, not negligent". Cada resposta termina dizendo o que foi pulado, o que não foi verificado e qual risco existe.

### Efeito medido

O `ponytail` publica um benchmark de 39 tarefas, incluindo um repositório real FastAPI + React, com cinco execuções por configuração:

| Métrica | Com a skill | Sem a skill |
|---|---|---|
| Código | −53% | linha de base |
| Tempo | −41% | linha de base |
| Custo | −26% | linha de base |
| Tokens | −45% | linha de base |
| Lógica arriscada com teste | 98% | 68% |
| Bugs injetados capturados pelos testes do agente | 66% | 46% |
| Problemas plantados encontrados na revisão | 100% | 87% |

Os números são **declarados pelo README** e não foram reproduzidos por esta wiki.

## Onde aparece

- [dietrichgebert/ponytail](../repos/github.com/dietrichgebert/ponytail.md) — implementação central: skill, comandos de revisão e auditoria, medidor de custo e a escada de reuso.
- [juliusbrussee/caveman](../repos/github.com/juliusbrussee/caveman.md) — compartilha a meta de reduzir trabalho e tokens, mas atua na linguagem e no contexto, não na decisão de escrever código.
- [addyosmani/agent-skills](../repos/github.com/addyosmani/agent-skills.md) — coleção de práticas de engenharia que inclui disciplina de mudança e testes, em tensão produtiva com YAGNI.

## Trade-offs

- **Vantagens:** menos código para manter, menor superfície de bugs, mais reuso, sessões mais curtas e menor custo; força o agente a compreender o código existente antes de gerar.
- **Limitações:** pode inibir abstrações que seriam necessárias em breve; a avaliação de "o que a tarefa exige" fica a cargo do agente; benchmarks são publicados pela própria ferramenta; sem revisão, o minimalismo pode virar solução frágil.
- **Critério prático:** aplicar a escada a código de aplicação, mantendo intactos validação, segurança, acessibilidade e testes de lógica arriscada.

## Relações

- **Relacionado a:** [TDD para agentes](tdd-para-agentes.md) — o teste pequeno obrigatório ancora o minimalismo; [Economia de tokens em agentes](economia-de-tokens-em-agentes.md) — menos código e menos sessões reduzem custo; [Saída completa de agente](saida-completa-de-agente.md) — ambas as diretrizes tentam limitar o comportamento do agente, mas em direções opostas.
- **Contrasta com:** diretrizes que exigem entregáveis completos, cobertura ampla e ausência de placeholders.
- **Pré-requisito para:** reduzir dívida gerada por agentes que criam abstrações e dependências desnecessárias.

## Perguntas abertas

- Como distinguir minimalismo saudável de subengenharia em projetos que crescerão?
- Os ganhos se mantêm em tarefas de refatoração e migração, não apenas em features novas?
- O efeito depende do modelo e do nível de esforço configurado?
- Como medir reuso de código existente de forma objetiva ao longo do tempo?
- A escada de reuso conflita com instruções de "saída completa" no mesmo projeto?

## Fontes

- README de [dietrichgebert/ponytail](../repos/github.com/dietrichgebert/ponytail.md) no commit `09c434ab73ca43761c5d8b0c5d341926c2fba710` (consultado em 2026-10-19). Somente o README foi lido.
- README de [juliusbrussee/caveman](../repos/github.com/juliusbrussee/caveman.md) no commit `bad48a0e1df55e05e3f52249afa35ecc1909ee76` (consultado em 2026-10-19), para o contraste com economia de tokens.
