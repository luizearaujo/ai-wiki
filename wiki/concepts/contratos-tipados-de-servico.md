---
type: concept
aliases: [Contratos tipados de serviço, Typed service contracts, Spec & handler, Design by Contract, Result Pattern]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [arquitetura, contratos, design-by-contract, result-pattern, zod, cli, agentes]
---

# Contratos tipados de serviço

> Padrão que separa a definição de uma capacidade — entrada, saída e erros em schemas tipados — da sua implementação, que trata falhas como valores de retorno em vez de exceções.

## Definição

Contrato tipado de serviço é a aplicação de **Design by Contract** a uma unidade de aplicação: um *spec* declara o que a capacidade aceita, o que devolve e como falha; um *handler* implementa o comportamento e concentra os efeitos colaterais. A entrada é **parseada** — transformada em um tipo válido — e não apenas validada; a saída é um `Result` discriminado entre sucesso e falha.

O padrão é apresentado pela skill [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md) no contexto de **Vertical Slice Architecture**: cada capacidade reúne contrato, implementação e testes no mesmo slice, em vez de espalhar validação, lógica e tratamento de erro por camadas horizontais.

Não se confunde com:

- **validação de formulário** — o contrato define a fronteira de uma capacidade, não apenas campos de UI;
- **tipos de TypeScript** — tipos desaparecem em runtime; o contrato inclui schema executável;
- **tratamento de exceções** — o Result Pattern devolve falhas como dados, sem depender de `try/catch` no consumidor.

## Como funciona

| Componente | Responsabilidade | Conteúdo |
| --- | --- | --- |
| **Spec** | Define o *quê*: contrato ou porta. | Schema de entrada, schema de saída, união discriminada de erros, tipo `Result` (sucesso \| falha) e interface da capacidade. |
| **Handler** | Define o *como*: implementação ou adaptador. | Implementa a interface, executa efeitos colaterais e **nunca lança**: captura erros e os mapeia para o `Result`. |

O fluxo tem três momentos:

1. **Parse, don't validate.** O schema de entrada aceita o dado bruto e produz um DTO utilizável. Refinamentos reutilizáveis — como rejeitar `..` em caminhos — ficam no contrato, não espalhados pelo handler.
2. **Erros exaustivos como dados.** Em vez de strings soltas, um enum de códigos (`FILE_NOT_FOUND`, `PERMISSION_DENIED`, `UNKNOWN_ERROR`) e um payload com mensagem, sugestão opcional e indicador de recuperabilidade. O consumidor decide o que fazer sem interpretar texto.
3. **Testes em duas camadas.** *Contract tests* alimentam o schema com casos inválidos em estilo tabela; *logic tests* mockam dependências e verificam o objeto `Result`. A fronteira é testada separadamente da lógica.

O benefício central para agentes é a **previsibilidade**: um agente que chama a capacidade recebe sempre a mesma forma de resposta, consegue distinguir falha esperada de bug e não precisa capturar exceções para continuar. É a versão em código do que a [CLI agent-first](cli-agent-first.md) busca na saída de processos.

## Onde aparece

- [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — define o padrão, os templates de `spec.ts` e `handler.ts` e a estratégia de testes.
- [CLI agent-first](cli-agent-first.md) — saída estruturada, erros como JSON e contrato estável entre chamadas.
- [TDD para agentes](tdd-para-agentes.md) — separação entre testes de contrato e de lógica como parte do ciclo de verificação.
- [Model Context Protocol](model-context-protocol.md) — em MCP, a descrição tipada de ferramentas cumpre papel análogo ao spec, mas no nível do protocolo.

## Trade-offs

- **Vantagens:** fronteiras explícitas; erros consumíveis por outro agente; testes de schema separados de testes de lógica; menos exceções não tratadas; contrato serve de documentação executável.
- **Limitações:** boilerplate por capacidade; acoplamento a TypeScript e Zod nos exemplos publicados; "nunca lançar" exige disciplina e cobertura de todas as chamadas; falhas de programação ainda podem produzir sucesso incorreto; o overhead pode dominar em scripts pequenos.
- **Critério prático:** vale quando a capacidade é chamada por outro sistema ou agente e falhas precisam ser tratadas programaticamente. Para um script descartável, o custo de dois arquivos e vários schemas pode não se pagar.

## Relações

- **Relacionado a:** [CLI agent-first](cli-agent-first.md) — contrato de entrada/saída na fronteira do processo; [TDD para agentes](tdd-para-agentes.md) — verificação do contrato e da lógica; [Agent skills](agent-skills.md) — formato que distribui o padrão como instrução.
- **Contrasta com:** validação ad hoc, exceções como fluxo de controle e tratamento de erro disperso.
- **Pré-requisito para:** integração confiável entre agentes e ferramentas, e para testes que distinguem entrada inválida de lógica incorreta.

## Perguntas abertas

- O padrão é viável em linguagens sem tipos estruturais e schemas em runtime, como Go ou Rust?
- Como representar cancelamento, timeout e efeitos parciais dentro de um `Result`?
- O Result Pattern substitui exceções por completo, ou apenas nas fronteiras?
- Há evidência de que o padrão reduz falhas reais em código gerado por agentes?
- Como versionar um contrato sem quebrar consumidores existentes?

## Fontes

- [Typed Service Contracts](../skills/github.com/google-labs-code/design.md/typed-service-contracts.md) — `SKILL.md` renderizado na página do skills.sh (consultada em 2026-10-19).
- https://github.com/google-labs-code/design.md — metadados e árvore via API do GitHub em 2026-10-19 (commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`); o repositório não foi clonado.
- [CLI agent-first](cli-agent-first.md) e [TDD para agentes](tdd-para-agentes.md) — sínteses construídas a partir das skills acima (2026-10-19).
