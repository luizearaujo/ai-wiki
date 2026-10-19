---
type: skill
name: Typed Service Contracts
slug: typed-service-contracts
url: https://www.skills.sh/google-labs-code/design.md/typed-service-contracts
source_url: https://github.com/google-labs-code/design.md
source_path: .agents/skills/typed-service-contracts/SKILL.md
author: google-labs-code
version: desconhecida
license: Apache-2.0
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [arquitetura, contratos, zod, typescript, testes, cli, agent-skills]
---

# Typed Service Contracts

> Skill que ensina o agente a construir cada unidade de lógica como um contrato tipado — entrada, saída e erros declarados em Zod — mais um handler que nunca lança exceção, para que CLIs e bibliotecas tenham fronteiras previsíveis.

## O que é

Typed Service Contracts é uma [agent skill](../../../../concepts/agent-skills.md) publicada por [google-labs-code](../../../../entities/google-labs-code.md) no repositório `google-labs-code/design.md` e distribuída pelo catálogo skills.sh. Ela empacota um padrão de arquitetura para código TypeScript assistido por agentes: **Vertical Slice Architecture** com **Design by Contract (DbC)** e **Result Pattern**.

O problema que resolve é a fronteira entre entrada crua e lógica de negócio. Em vez de validar dados em vários pontos e lançar exceções em outros, a skill separa um *spec* — que descreve o contrato — de um *handler* — que executa os efeitos colaterais. A entrada é **parseada**, não apenas validada: o schema transforma o dado bruto em um DTO utilizável, e falhas viram valores de retorno explícitos.

A skill integra o mesmo repositório que define o formato [DESIGN.md](https://github.com/google-labs-code/design.md), mas o README do projeto não descreve as skills; elas vivem em `.agents/skills/`. O conteúdo desta página vem do `SKILL.md` renderizado na página do skills.sh; o arquivo cru no repositório não foi buscado e o repositório não foi clonado.

## Como funciona

O padrão tem dois componentes obrigatórios:

| Componente | Papel | Conteúdo mínimo |
| --- | --- | --- |
| **Spec** (`spec.ts`) | Contrato ou porta — define o *quê*. | Schema de entrada, schema de saída, união discriminada de erros, tipo `Result` (sucesso \| falha) e a interface da capacidade. |
| **Handler** (`handler.ts`) | Implementação ou adaptador — define o *como*. | Implementa a interface, concentra efeitos colaterais (filesystem, API) e **nunca lança exceção**: captura erros internos e os mapeia para o `Result`. |

O fluxo de uso tem três passos:

1. **Definir o contrato.** Schemas Zod para entrada, erros e sucesso; uma interface como `MyTaskSpec`. Refinamentos reutilizáveis, como um `SafePathSchema` que rejeita `..`, ficam junto do contrato. Códigos de erro são um enum exaustivo (`FILE_NOT_FOUND`, `PERMISSION_DENIED`, `UNKNOWN_ERROR`), não strings livres.
2. **Implementar o handler.** A classe verifica o estado do mundo e devolve `{ success: false, error: { code, message, suggestion?, recoverable } }` em vez de lançar. Um `catch` de segurança converte erros desconhecidos em `UNKNOWN_ERROR`.
3. **Testar em duas camadas.** *Contract tests* exercitam o schema com dados inválidos em estilo tabela; *logic tests* mockam dependências e verificam o objeto `Result`. O objetivo é separar "o dado é aceitável?" de "a lógica está correta?".

A skill também define vocabulário: a entrada é tratada como um **Command**, o resultado como um **Monad** de sucesso/falha e o handler como um adaptador impuro. A arquitetura é vertical porque cada capacidade reúne seu contrato, implementação e testes no mesmo slice, em vez de espalhar camadas horizontais.

## Instalação e uso

Comando publicado na página de origem:

```bash
npx skills add https://github.com/google-labs-code/design.md --skill typed-service-contracts
```

A página também oferece invocação sem instalação permanente, via `npx skills use`. A instalação é por projeto e cross-platform; não há instruções separadas de escopo global.

## Exemplos de uso

Os prompts abaixo são **exemplos derivados da descrição publicada**, não instruções oficiais da skill.

- **Nova capacidade de CLI:** "Implemente `configure` como um slice: crie `spec.ts` com schemas Zod de entrada, saída e erros, e `handler.ts` que devolve `Result` e nunca lança."
- **Refatoração defensiva:** "Refatore este handler que lança exceções para o padrão spec/handler, com códigos de erro exaustivos e um catch de segurança."
- **Testes:** "Separe os testes em contract tests do schema e logic tests do handler com dependências mockadas."

## Saídas esperadas

- um par `spec.ts`/`handler.ts` por capacidade, com interface compartilhada;
- entrada parseada por schema, com refinamentos reutilizáveis;
- erros como valores discriminados, incluindo mensagem, código, sugestão opcional e indicador de recuperabilidade;
- testes de contrato orientados a dados e testes de lógica baseados no objeto `Result`.

## Quando usar (e quando não usar)

- **Use quando:** a fronteira entre entrada de usuário/agente e lógica de sistema precisa ser estrita — CLIs, bibliotecas, ferramentas expostas a agentes.
- **Use quando:** a validação envolve transformação (normalizar caminhos, impor limites) e não apenas aceitar/rejeitar.
- **Use quando:** erros precisam ser consumidos programaticamente por outro agente, e exceções não tratadas são inaceitáveis.
- **Use quando:** você quer separar testes de schema de testes de lógica.
- **Evite quando:** o projeto não usa TypeScript ou Zod; o padrão é portável em conceito, mas os exemplos e a implementação são específicos do ecossistema.
- **Evite quando:** um script descartável se beneficia mais de simplicidade do que de contratos e tipos de resultado; o custo de boilerplate não se paga.

## Limitações e cuidados

- **Acoplamento a TypeScript e Zod.** A ideia de spec/handler é geral, mas os templates dependem de Zod e de tipos TypeScript; adaptar para outra linguagem exige tradução explícita.
- **Boilerplate.** Cada capacidade ganha dois arquivos, schemas e um tipo de erro; em projetos pequenos, isso pode dominar o código de negócio.
- **"Nunca lançar" é uma disciplina, não uma garantia.** Dependências podem lançar antes do `catch`; o padrão só funciona se o handler envolver todas as chamadas relevantes.
- **Erros de programação continuam possíveis.** O Result Pattern trata falhas esperadas; bugs de lógica podem produzir sucesso incorreto, que os testes precisam cobrir.
- **Sem validação de runtime independente.** A skill não publica benchmarks nem verifica se os agentes aplicam o padrão corretamente; a auditoria cobre segurança do pacote, não qualidade arquitetural.
- **Superfície de supply chain.** Instalar a skill adiciona instruções de terceiros ao agente; revise o `SKILL.md` antes de usar em contexto sensível.
- **Contexto do repositório.** O README de `design.md` não menciona essas skills; a documentação canônica é o próprio `SKILL.md`, não a página principal do projeto.

## Estado e adoção

- **Versão da skill:** não publicada na página de origem (observado em 2026-10-19).
- **Catálogo:** 669 instalações, primeira aparição em 2026-04-22 (observado em 2026-10-19).
- **Auditorias de terceiros:** Gen Agent Trust Hub, Socket e Snyk com resultado "Pass" (observado em 2026-10-19); critérios não verificados nesta wiki.
- **Repositório-fonte:** Apache-2.0, TypeScript, ~28,4 mil estrelas e ~2,3 mil forks na API do GitHub; último push em 2026-10-16, no commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`. A licença é do repositório; a página da skill não declara licença própria.
- **Preço:** gratuito.

## Relações

- **Autor:** [google-labs-code](../../../../entities/google-labs-code.md) — organização Google Labs Code.
- **Repositório-fonte:** [google-labs-code/design.md](https://github.com/google-labs-code/design.md) — especificação DESIGN.md e CLI de lint/diff/export; esta skill fica em `.agents/skills/`.
- **Conceitos:** [Contratos tipados de serviço](../../../../concepts/contratos-tipados-de-servico.md) — padrão que a skill operacionaliza; [TDD para agentes](../../../../concepts/tdd-para-agentes.md) — separação entre testes de contrato e de lógica; [CLI agent-first](../../../../concepts/cli-agent-first.md) — saída estruturada e erros consumíveis por agentes.
- **Skills irmãs:** [TDD Red-Green-Refactor](tdd-red-green-refactor.md), [Ink](ink.md) e [Agent DX CLI Scale](agent-dx-cli-scale.md).

## Perguntas abertas

- O padrão funciona igualmente bem em Python, Go ou Rust, ou depende de recursos de tipos do TypeScript?
- Como a skill lida com efeitos colaterais parciais (arquivo gravado e erro posterior) sem transações?
- O Result Pattern cobre cancelamento e timeout, ou exige um código de erro adicional?
- Há medição de quanto o padrão reduz falhas reais em código gerado por agentes?
- Quais são os critérios exatos das auditorias "Pass" publicadas pelo skills.sh?

## Fontes

- Página de origem: https://www.skills.sh/google-labs-code/design.md/typed-service-contracts (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/google-labs-code/design.md (metadados e árvore consultados via API do GitHub em 2026-10-19; commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`). O repositório não foi clonado; o `SKILL.md` foi lido conforme renderizado na página do skills.sh, não como arquivo cru no repositório.
