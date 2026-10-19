---
type: skill
name: TDD Red-Green-Refactor
slug: tdd-red-green-refactor
url: https://www.skills.sh/google-labs-code/design.md/tdd-red-green-refactor
source_url: https://github.com/google-labs-code/design.md
source_path: .agents/skills/tdd/SKILL.md
author: google-labs-code
version: desconhecida
license: Apache-2.0
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [tdd, testes, typescript, vitest, agentes, verificacao, agent-skills]
---

# TDD Red-Green-Refactor

> Skill que impõe ao agente o ciclo vermelho-verde-refatorar em TypeScript, com um teste por vez, para que cada linha gerada tenha uma falha observada e uma verificação correspondente.

## O que é

TDD Red-Green-Refactor é uma [agent skill](../../../../concepts/agent-skills.md) publicada por [google-labs-code](../../../../entities/google-labs-code.md) no repositório `google-labs-code/design.md` e distribuída pelo catálogo skills.sh. Ela implementa um framework estrutural para programação assistida por IA: o código só avança quando um teste prova que a funcionalidade ainda não existe e, depois, prova que a implementação mínima passou.

O alvo é um comportamento frequente em agentes de código: escrever muitas linhas e muitos testes de uma vez, "adivinhar" a solução e ajustar o teste até ele passar. A skill troca esse padrão por um loop incremental verificável, no qual a transição de falha para sucesso é tratada como **Proof of Work**.

O conteúdo desta página vem do `SKILL.md` renderizado na página do skills.sh. O arquivo cru no repositório não foi buscado e o repositório não foi clonado. O diretório da skill no repositório é `.agents/skills/tdd/`, diferente do slug publicado `tdd-red-green-refactor`.

## Como funciona

O ciclo tem três fases:

| Fase | Objetivo | Ações exigidas |
| --- | --- | --- |
| **Red** | Estabelecer a falha. | Escrever **um** teste para o próximo comportamento; executar; confirmar que falha pelo motivo certo — por exemplo, `ReferenceError: add is not defined`, não um erro de configuração. |
| **Green** | Passar com o mínimo. | Escrever a implementação mais simples que satisfaz o teste atual, sem construir para o futuro; rodar a suíte e confirmar que tudo está verde. |
| **Refactor** | Limpar sem quebrar. | Melhorar nomes, remover duplicação e otimizar o código da fase Green; rodar os testes após cada mudança e reverter imediatamente qualquer alteração que os torne vermelhos. |

Três regras operacionais sustentam o ciclo:

1. **Sem "horizontal splurging".** É proibido escrever vários testes de uma vez. O loop é `1 teste → ver falhar → 1 correção → ver passar`, repetido para cada subfuncionalidade.
2. **Backpressure.** Asserções automatizadas e tipagem forte em TypeScript servem de contrapressão contra soluções "chutadas" ou código de baixa qualidade. A verificação limita o que o agente pode fazer sem evidência.
3. **Integridade dos testes.** Nunca alterar um teste existente para fazer uma implementação falha passar. Um teste só muda quando o requisito muda — não porque o código é difícil de escrever.

O exemplo publicado usa Vitest: um teste de `add(2, 2)` que falha porque a função não existe, uma implementação que retorna `4` para passar, e então a versão refatorada que soma os dois parâmetros com tipos explícitos.

## Instalação e uso

Comando publicado na página de origem:

```bash
npx skills add https://github.com/google-labs-code/design.md --skill tdd-red-green-refactor
```

A página também oferece invocação sem instalação permanente, via `npx skills use`. A skill pressupõe um projeto TypeScript com Vitest ou Jest; o teste e a execução da suíte ficam a cargo do agente no ambiente do projeto.

## Exemplos de uso

Os prompts abaixo são **exemplos derivados da descrição publicada**, não instruções oficiais da skill.

- **Nova função:** "Implemente `parseDuration` seguindo red-green-refactor: um teste de cada vez, mostre a falha antes da implementação."
- **Correção de bug:** "Reproduza o bug com um teste que falha, faça a correção mínima e só depois refatore."
- **Revisão de código gerado:** "Verifique se cada comportamento novo tem um teste que falhou antes da implementação; não aceite testes escritos depois do código."

## Saídas esperadas

- uma sequência observável de testes que falham pelo motivo esperado;
- implementações mínimas que fazem cada teste passar;
- refatorações que mantêm a suíte verde;
- histórico em que cada comportamento tem um teste correspondente, sem testes ajustados retroativamente.

## Quando usar (e quando não usar)

- **Use quando:** o agente vai escrever lógica de aplicação em TypeScript e existe suíte executável no projeto.
- **Use quando:** o custo de uma regressão é alto e você quer evidência de comportamento, não apenas código que parece correto.
- **Use quando:** o agente tende a gerar grandes blocos de código e testes de uma vez; o loop força granularidade.
- **Evite quando:** o projeto não tem infraestrutura de testes ou o feedback é caro demais para cada micro-passo; nesse caso, um ciclo maior com testes de integração pode ser mais adequado.
- **Evite quando:** a tarefa é exploratória, como um spike descartável, em que o objetivo é aprender e não manter o código.
- **Evite quando:** a linguagem ou o framework não se beneficia do estilo TypeScript/Vitest; o método é portável, os exemplos não.

## Limitações e cuidados

- **Pressupõe testes bons.** Um teste que apenas espelha a implementação passa sem provar comportamento; o ciclo não corrige especificações ruins.
- **Custo de tempo.** Um teste por vez reduz o escopo de cada iteração, mas multiplica execuções; em suítes lentas, o atrito pode levar o agente a burlar o processo.
- **Backpressure depende do ambiente.** Se o agente não puder rodar testes — sandbox sem dependências, sem runtime — a fase Red não é observável e a skill perde o mecanismo central.
- **Não cobre integração ou performance.** O foco é comportamento unitário; testes de contrato entre serviços, desempenho e segurança exigem outras camadas.
- **Especificidade de ferramentas.** Os exemplos usam Vitest/Jest e TypeScript; a skill não publica adaptadores para outras linguagens.
- **Superfície de supply chain.** Instalar a skill adiciona instruções de terceiros ao agente; revise o `SKILL.md` antes de usar em contexto sensível.
- **Contexto do repositório.** O README de `design.md` não menciona as skills; a fonte canônica é o `SKILL.md` em `.agents/skills/tdd/`.

## Estado e adoção

- **Versão da skill:** não publicada na página de origem (observado em 2026-10-19).
- **Catálogo:** 647 instalações, primeira aparição em 2026-04-22 (observado em 2026-10-19).
- **Auditorias de terceiros:** Gen Agent Trust Hub, Socket e Snyk com resultado "Pass" (observado em 2026-10-19); critérios não verificados nesta wiki.
- **Repositório-fonte:** Apache-2.0, TypeScript, ~28,4 mil estrelas e ~2,3 mil forks na API do GitHub; último push em 2026-10-16, no commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`. A licença é do repositório; a página da skill não declara licença própria.
- **Preço:** gratuito.

## Relações

- **Autor:** [google-labs-code](../../../../entities/google-labs-code.md) — organização Google Labs Code.
- **Repositório-fonte:** [google-labs-code/design.md](https://github.com/google-labs-code/design.md) — especificação DESIGN.md e CLI; esta skill fica em `.agents/skills/tdd/`.
- **Conceitos:** [TDD para agentes](../../../../concepts/tdd-para-agentes.md) — método que a skill operacionaliza; [Contratos tipados de serviço](../../../../concepts/contratos-tipados-de-servico.md) — separação entre testes de schema e de lógica; [CLI agent-first](../../../../concepts/cli-agent-first.md) — contexto de ferramentas verificáveis por agentes.
- **Skills irmãs:** [Typed Service Contracts](typed-service-contracts.md), [Ink](ink.md) e [Agent DX CLI Scale](agent-dx-cli-scale.md).

## Perguntas abertas

- A skill exige que o agente mostre a saída do teste falhando, ou basta afirmar que falhou?
- Como lidar com testes que são caros demais para rodar a cada micro-mudança?
- O loop continua útil em bases com testes legados frágeis, ou o agente tende a "consertar" testes existentes?
- Existe alguma avaliação de quanto o método reduz regressões em código gerado por LLM?
- O que acontece quando o requisito é ambíguo e o primeiro teste codifica a interpretação errada?

## Fontes

- Página de origem: https://www.skills.sh/google-labs-code/design.md/tdd-red-green-refactor (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/google-labs-code/design.md (metadados e árvore consultados via API do GitHub em 2026-10-19; commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`). O repositório não foi clonado; o `SKILL.md` foi lido conforme renderizado na página do skills.sh, não como arquivo cru no repositório.
