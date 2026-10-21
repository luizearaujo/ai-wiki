---
type: concept
aliases: [System 1 para agentes, Modelo de decisão não generativo, Jev, TypeSafe AI, decisão calibrada sem geração]
status: draft
created: 2026-10-21
updated: 2026-10-21
tags: [agentes, roteamento, guardrails, inferencia, calibracao]
---

# Decisão não generativa para agentes (System 1)

> Modelo treinado para responder perguntas tipadas (escolha, nota, sim/não) com confiança calibrada em uma única passada paralela, sem gerar texto token a token — trocando o "raciocínio" caro de um LLM generativo por roteamento, guardrail e triagem de baixa latência.

## Definição

A analogia usada pelos próprios fornecedores é a de Kahneman: um LLM generativo e autorregressivo (GPT, Claude, etc.) age como **System 2** — deliberativo, caro, lento, bom em prosa e raciocínio aberto. Para decisões rotineiras dentro de um loop de agente — "para qual fila isso vai?", "isso é uma tentativa de prompt injection?", "qual a urgência deste ticket?" — essa deliberação é desperdício: 1,5–3,5s de latência e custo de API por passo, mais risco de a saída cair fora do schema esperado (alucinação de JSON).

Um modelo **System 1** resolve isso invertendo o problema: em vez de gerar uma resposta livre, ele recebe um `state` não estruturado e um conjunto de **perguntas tipadas** — escolha categórica, nota ordinal, sim/não — e devolve, em uma única passada paralela (ordem de 70–150ms), a opção escolhida mais uma probabilidade calibrada por opção. Nada é gerado: a saída nunca cai fora da lista permitida, porque a lista é o próprio espaço de saída do modelo.

## Como funciona

- **Primitivas tipadas** (nomenclatura observada no SDK da TypeSafe AI, usada pelo Jev): `Choice` (classificação categórica com critérios por opção), `Score` (nota ordinal contínua) e `Noul` (decisão binária sim/não com probabilidade calibrada).
- **Uma passada, várias perguntas**: um `state` (ex.: o texto de um ticket) é avaliado contra várias perguntas tipadas ao mesmo tempo — roteamento de departamento, urgência, detecção de ataque adversarial, elegibilidade para resolução automática — em vez de uma chamada de LLM por pergunta.
- **Calibração via RLCD** (Reinforcement Learning for Calibrated Decisions, nome usado pela TypeSafe): a confiança retornada é treinada para refletir a probabilidade real de acerto, não só um score relativo — o que permite usá-la como gatilho de decisão (ex.: só agir automaticamente acima de um limiar).
- **Roteamento por limiar de confiança**: um padrão comum observado é usar a saída do System 1 como *firewall* — bloquear se a pontuação adversarial (`Noul`) passar de um limiar; agir automaticamente se confiança e uma política permitirem; e só então escalar para um LLM generativo (**System 2**) nos casos de baixa confiança ou alta urgência.
- **Compatibilidade de API como superfície comum**: pelo menos um motor de inferência local (colibri) declara compatibilidade com a API do Jev/TypeSafe, bastando trocar a base URL — sugerindo que esse padrão de "perguntas tipadas + confiança calibrada" está virando uma interface, não só um produto fechado.

## Onde aparece

- [JustVugg/colibri](../repos/github.com/justvugg/colibri.md) — o motor de inferência em C expõe um modo **System One** nativo: a resposta traz a opção escolhida, uma probabilidade por opção permitida e uma confiança; nada é gerado. O README declara compatibilidade com a API do Jev (TypeSafe), permitindo trocar apenas a base URL.
- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) (pasta `src/jev-system-one-model-python-demo`) — demo hands-on do Jev da TypeSafe AI: um dispatcher de triagem de tickets de suporte avalia `department` (`Choice`), `urgency` (`Score`), `is_adversarial` e `can_auto_resolve` (`Noul`) em uma única chamada por ticket, com branching explícito para firewall, ação automática ou escalação a um LLM generativo.

## Trade-offs

- **Vantagens:** latência de ordem de 100ms em vez de segundos; custo por chamada muito menor que um LLM generativo; saída sempre dentro do schema (sem alucinação de formato); confiança calibrada permite automação segura acima de um limiar.
- **Limitações:** só funciona para decisões que cabem em perguntas tipadas definidas de antemão — não substitui raciocínio aberto, geração de texto ou tarefas sem um espaço de resposta fechado; depende de um modelo/provedor especializado (TypeSafe/Jev é o único exemplo hospedado observado na wiki); a qualidade da calibração depende do treinamento (RLCD) do fornecedor, não é algo que se audita facilmente de fora.
- **Quando não usar:** tarefas que exigem geração de texto, raciocínio multi-passo ou síntese — aí o padrão é escalar para um LLM generativo (System 2), não forçar o System 1.

## Relações

- Relacionado a: [Streaming de experts em MoE](streaming-de-experts-em-moe.md) — outro padrão de inferência especializada em [JustVugg/colibri](../repos/github.com/justvugg/colibri.md), mas para um problema diferente (rodar modelos generativos grandes, não decisão tipada); [Orquestração multiagente](orquestracao-multiagente.md) — System 1 é frequentemente o componente de roteamento/guardrail dentro de um loop maior.
- Contrasta com: LLMs generativos autorregressivos (System 2) usados para raciocínio aberto e geração de texto.
- Pré-requisito para: automação segura de roteamento e guardrails em agentes de produção com latência e custo previsíveis.

## Perguntas abertas

- Que outros fornecedores, além da TypeSafe AI (Jev), oferecem esse padrão de decisão tipada e calibrada hospedada?
- Como a calibração (RLCD) é auditada ou validada de fora, sem acesso ao treinamento do fornecedor?
- Esse padrão vai padronizar como uma API comum (como MCP fez para ferramentas), ou cada fornecedor mantém seu próprio schema de perguntas tipadas?

## Fontes

- [JustVugg/colibri](../repos/github.com/justvugg/colibri.md) — README no commit já registrado na página do repositório (consultado em 2026-10-19).
- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) — `src/jev-system-one-model-python-demo/README.md` e `demo.py`, no commit `555467c365e6750278efba09349369109f62f65f` (clone local, consultado em 2026-10-21).
