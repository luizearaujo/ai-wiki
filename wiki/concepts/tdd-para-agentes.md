---
type: concept
aliases: [TDD para agentes, Test-driven development com agentes, TDD assistido por IA, Red-green-refactor para agentes]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [tdd, testes, verificacao, agentes, engenharia-de-software, backpressure]
---

# TDD para agentes

> Uso do ciclo red-green-refactor como mecanismo de contrapressão sobre código gerado por agentes: cada comportamento nasce de um teste que falha por um motivo observável, e o teste não pode ser ajustado para acomodar a implementação.

## Definição

TDD para agentes é a aplicação do test-driven development a fluxos em que um modelo escreve código. O problema não é novo — TDD existe para humanos —, mas o modo de falha muda: agentes tendem a produzir grandes blocos de código e testes de uma vez, inferir a solução em vez de derivá-la do requisito e alterar o teste quando a implementação não passa. O ciclo é usado como **estrutura de verificação**, não apenas como preferência de estilo.

A unidade de progresso é pequena: **um teste, uma falha, uma correção mínima, uma passagem**. A transição de vermelho para verde é a evidência de que o código faz algo verificável.

Não se confunde com:

- **escrever testes depois do código** — cobertura pode existir sem que o teste tenha orientado a implementação;
- **geração de testes por LLM** — produzir testes não garante que eles falhem antes nem que sejam independentes;
- **avaliação de código por revisão** — revisão olha o resultado; TDD olha a sequência.

## Como funciona

O ciclo tem três fases e três regras operacionais:

| Fase | Objetivo | Evidência exigida |
| --- | --- | --- |
| **Red** | Provar que o comportamento não existe. | Um teste novo falha pelo motivo esperado — não por erro de configuração, import ou ambiente. |
| **Green** | Fazer o teste passar com o mínimo. | Implementação mais simples possível; nenhuma construção especulativa para requisitos futuros. |
| **Refactor** | Melhorar a estrutura sem quebrar. | Suíte continua verde após cada mudança; qualquer alteração que a torne vermelha é revertida. |

As regras que impedem o agente de burlar o ciclo:

1. **Sem "horizontal splurging".** Um teste por vez. Escrever vários testes antes de qualquer implementação torna a falha ambígua e permite que o agente ajuste o conjunto até ele passar.
2. **Backpressure.** Asserções automatizadas e tipagem forte limitam o que o agente pode afirmar sem evidência. Em TypeScript, o compilador e o runner são parte do mecanismo, não detalhes de ferramenta.
3. **Integridade dos testes.** Um teste existente só muda quando o requisito muda. Alterar o teste para acomodar uma implementação difícil inverte a direção da verificação.

Quando o projeto separa contrato e lógica, o ciclo se desdobra em duas camadas: **contract tests** exercitam schemas com dados inválidos, e **logic tests** mockam dependências e verificam o objeto de resultado. A separação evita que um teste de lógica mascare uma fronteira de entrada mal definida.

## Onde aparece

- [TDD Red-Green-Refactor](../skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md) — operacionaliza o ciclo em TypeScript com Vitest/Jest, incluindo a proibição de splurging e a regra de integridade dos testes.
- [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — combina o ciclo com contratos tipados e separa testes de schema de testes de lógica.
- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — trata TDD como parte do processo de engenharia do harness: o workflow exige evidência RED antes da implementação e usa revisão em contexto novo.
- [Agent DX CLI Scale](../skills/github.com/google-labs-code/design.md/agent-dx-cli-scale.md) — verificação e `--dry-run` aparecem como trilhos de segurança para agentes que operam CLIs.
- [obra/superpowers](../repos/github.com/obra/superpowers.md) — red-green-refactor como skill obrigatória (`test-driven-development`), incluindo apagar código escrito antes do teste correspondente.

## Trade-offs

- **Vantagens:** cada comportamento tem evidência observável; reduz regressões silenciosas; limita a tendência do agente a "adivinhar" a solução; deixa um histórico auditável da ordem código/teste.
- **Limitações:** exige ambiente executável e suíte rápida; testes ruins podem dar falsa segurança; o ciclo é caro para tarefas exploratórias e para código de integração; não cobre desempenho, segurança ou requisitos ambíguos; a disciplina depende de o agente realmente mostrar a falha.
- **Critério prático:** vale quando há comportamento verificável, feedback barato e custo alto de regressão. Para spikes, protótipos descartáveis ou ambientes sem runner, um ciclo maior de testes de integração pode ser mais adequado.

## Relações

- **Relacionado a:** [Contratos tipados de serviço](contratos-tipados-de-servico.md) — contratos fornecem a fronteira que os testes exercitam; [Agent harness](agent-harness.md) — harnesses como ECC empacotam TDD como workflow; [CLI agent-first](cli-agent-first.md) — `--dry-run` e saída estruturada tornam a verificação possível.
- **Contrasta com:** geração de código seguida de testes retrospectivos; revisão apenas por leitura.
- **Pré-requisito para:** confiança em mudanças incrementais geradas por agentes e para refatoração segura.

## Perguntas abertas

- Basta o agente afirmar que o teste falhou, ou a saída do runner deve ser registrada como evidência?
- Como aplicar o ciclo em bases com testes legados frágeis sem incentivar o agente a "consertar" testes?
- Qual é a granularidade mínima viável quando cada execução da suíte custa minutos?
- O método reduz regressões em código gerado por LLM de forma mensurável, ou apenas muda a aparência do processo?
- Como lidar com requisitos ambíguos, em que o primeiro teste codifica a interpretação errada?

## Fontes

- [TDD Red-Green-Refactor](../skills/github.com/google-labs-code/design.md/tdd-red-green-refactor.md) — `SKILL.md` renderizado na página do skills.sh (consultada em 2026-10-19).
- [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — `SKILL.md` renderizado na página do skills.sh (consultada em 2026-10-19).
- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — README no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34` (consultado em 2026-10-19).
- https://github.com/google-labs-code/design.md — metadados e árvore via API do GitHub em 2026-10-19 (commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`); o repositório não foi clonado.
