---
type: skill
name: Ink
slug: ink
url: https://www.skills.sh/google-labs-code/design.md/ink
source_url: https://github.com/google-labs-code/design.md
source_path: .agents/skills/ink/SKILL.md
author: google-labs-code
version: desconhecida
license: Apache-2.0
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [terminal, ui, ink, json-render, react, typescript, agent-skills]
---

# Ink

> Skill que ensina o agente a renderizar interfaces de terminal a partir de uma especificação JSON, usando o pacote `@json-render/ink` e um catálogo de componentes tipado.

## O que é

Ink é uma [agent skill](../../../../concepts/agent-skills.md) publicada por [google-labs-code](../../../../entities/google-labs-code.md) no repositório `google-labs-code/design.md` e distribuída pelo catálogo skills.sh. Ela documenta o `@json-render/ink`, um renderer de terminal que converte **specs JSON** em árvores de componentes interativas, com componentes padrão, data binding, visibilidade condicional, ações e props dinâmicas.

Diferente das skills de texto, esta é essencialmente uma **referência de biblioteca**: ensina o agente a montar catálogo, registry, providers e spec, e a respeitar diretrizes de design para uma superfície de terminal de ~80–120 colunas. O valor está em permitir que o agente produza UI de terminal declarativamente — emitindo JSON, não código imperativo de layout.

O conteúdo desta página vem do `SKILL.md` renderizado na página do skills.sh. O arquivo cru no repositório não foi buscado e o repositório não foi clonado. O README de `design.md` não menciona essa skill; o diretório correspondente é `.agents/skills/ink/`.

## Como funciona

O uso começa por um catálogo e um registry tipados:

```ts
import { defineCatalog } from "@json-render/core";
import { schema } from "@json-render/ink/schema";
import {
  standardComponentDefinitions,
  standardActionDefinitions,
} from "@json-render/ink/catalog";
import { defineRegistry, Renderer, type Components } from "@json-render/ink";
```

O catálogo combina os componentes padrão com componentes customizados descritos por props Zod. O registry registra apenas os componentes customizados; os padrão são embutidos. O `Renderer` recebe o spec e o registry.

O spec é um **mapa plano de elementos** com uma raiz:

```json
{
  "root": "main",
  "elements": {
    "main": { "type": "Box", "props": { "flexDirection": "column", "padding": 1 }, "children": ["heading", "content"] },
    "heading": { "type": "Heading", "props": { "text": "Dashboard", "level": "h1" }, "children": [] },
    "content": { "type": "Text", "props": { "text": "Hello from the terminal!" }, "children": [] }
  }
}
```

O modelo de dados e eventos inclui:

| Mecanismo | Uso |
| --- | --- |
| `visible` | Condições com `$state`, `eq`, `not`, `$and` e `$or`. |
| Expressões | `$state` (leitura), `$bindState` (duas vias), `$bindItem`, `$cond`/`$then`/`$else` e `$template`. |
| Eventos | Componentes emitem eventos; o campo `on` do elemento mapeia evento → ação. |
| Ações embutidas | `setState`, `pushState` e `removeState`. |
| `repeat` | Listas dinâmicas a partir de um array de estado, com `$item` e `$index`. |
| Streaming | `useUIStream` renderiza specs progressivamente a partir de streams JSONL. |
| Stores | `StateStore` externo para modo controlado, ignorando estado inicial e callback. |

O catálogo traz componentes de layout (`Box`, `Text`, `Newline`, `Spacer`), conteúdo (`Heading`, `Divider`, `Badge`, `Spinner`, `ProgressBar`, `Sparkline`, `BarChart`, `Table`, `List`, `ListItem`, `Card`, `KeyValue`, `Link`, `StatusLine`, `Markdown`) e interação (`TextInput`, `Select`, `MultiSelect`, `ConfirmInput`, `Tabs`). Para construir do zero, `createRenderer` embute os providers de estado, visibilidade, ações e foco.

As diretrizes de design recomendam layout vertical como estrutura principal, largura de ~80–120 colunas, `borderStyle` para agrupar, cores de terminal nomeadas, `Heading` e `Divider` para hierarquia, `Tabs` com visibilidade condicional e `Sparkline`/`BarChart` para séries.

## Instalação e uso

Comando publicado na página de origem:

```bash
npx skills add https://github.com/google-labs-code/design.md --skill ink
```

A página também oferece invocação sem instalação permanente, via `npx skills use`. O projeto consumidor precisa instalar as dependências `@json-render/core`, `@json-render/ink` e `zod` conforme o quick start.

## Exemplos de uso

Os prompts abaixo são **exemplos derivados da descrição publicada**, não instruções oficiais da skill.

- **Dashboard de terminal:** "Monte um spec com `Box` vertical, `Heading`, `KeyValue` e `StatusLine` para exibir o status de um serviço."
- **Seleção interativa:** "Crie uma `Tabs` com três visões e use `visible` para alternar o conteúdo."
- **Streaming:** "Mostre a resposta de `/api/generate` com `useUIStream`, renderizando o spec conforme os patches JSONL chegam."
- **Lista dinâmica:** "Use `repeat` sobre `/items` e renderize `ListItem` com `$item`."

## Saídas esperadas

- um catálogo tipado de componentes e ações;
- um registry com apenas os componentes customizados;
- um spec JSON plano com raiz e elementos;
- uma aplicação Ink que renderiza o spec, com providers corretos;
- uso de componentes padrão antes de criar customizações.

## Quando usar (e quando não usar)

- **Use quando:** o agente precisa gerar uma UI de terminal interativa e você quer uma representação declarativa, versionável e inspecionável.
- **Use quando:** um sistema externo ou modelo deve emitir JSON, e não código React/Ink, para montar a interface.
- **Use quando:** você precisa de streaming progressivo de UI a partir de um endpoint.
- **Evite quando:** a interface é simples e um script de terminal com texto puro resolve; o catálogo e o spec adicionam camadas.
- **Evite quando:** o alvo é uma UI web ou desktop; o pacote é específico para terminal.
- **Evite quando:** você não pode adicionar as dependências `@json-render/*` e `zod` ao projeto.

## Limitações e cuidados

- **Dependência de ecossistema externo.** A skill documenta `@json-render/ink`, mas a página não publica versão, licença ou repositório do pacote; compatibilidade e manutenção não foram verificadas.
- **Especificidade de terminal.** O layout é limitado por largura de colunas e capacidades de texto; gráficos são aproximações com caracteres Unicode.
- **Segurança de conteúdo.** Um spec pode renderizar `Link` e `Markdown`; se o JSON vier de uma fonte não confiável, trate-o como entrada não confiável e sanitize antes de renderizar.
- **Exemplo de quick start truncado na origem.** O trecho publicado omite o corpo do componente e do `return`; o código completo precisa ser consultado na documentação do pacote.
- **Sem benchmark de qualidade.** A skill não mede se o layout gerado é legível ou se respeita acessibilidade de terminal.
- **Superfície de supply chain.** Instalar a skill adiciona instruções de terceiros ao agente; revise o `SKILL.md` antes de usar em contexto sensível.

## Estado e adoção

- **Versão da skill:** não publicada na página de origem (observado em 2026-10-19).
- **Catálogo:** 169 instalações, primeira aparição em 2026-04-22 (observado em 2026-10-19).
- **Auditorias de terceiros:** Gen Agent Trust Hub, Socket e Snyk com resultado "Pass" (observado em 2026-10-19); critérios não verificados nesta wiki.
- **Repositório-fonte:** Apache-2.0, TypeScript, ~28,4 mil estrelas e ~2,3 mil forks na API do GitHub; último push em 2026-10-16, no commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`. A licença é do repositório; a página da skill não declara licença própria, e a licença do pacote `@json-render/ink` não foi verificada.
- **Preço:** gratuito.

## Relações

- **Autor:** [google-labs-code](../../../../entities/google-labs-code.md) — organização Google Labs Code.
- **Repositório-fonte:** [google-labs-code/design.md](https://github.com/google-labs-code/design.md) — esta skill fica em `.agents/skills/ink/`.
- **Conceitos:** [CLI agent-first](../../../../concepts/cli-agent-first.md) — superfície de terminal consumível por agentes; [Agent skills](../../../../concepts/agent-skills.md) — formato de distribuição; [Artefatos HTML autocontidos](../../../../concepts/artefatos-html-autocontidos.md) — contraste: artefato único para web vs. UI declarativa de terminal.
- **Skills irmãs:** [Typed Service Contracts](typed-service-contracts.md), [TDD Red-Green-Refactor](tdd-red-green-refactor.md) e [Agent DX CLI Scale](agent-dx-cli-scale.md).

## Perguntas abertas

- Qual é a versão atual de `@json-render/ink` e quem a mantém?
- O pacote continua ativo, ou a skill documenta uma integração específica do `design.md`?
- Como o streaming lida com specs inválidos no meio do stream?
- Há suporte a temas, acessibilidade de terminal e testes de snapshot?
- Qual é o custo de contexto de um catálogo grande de componentes?

## Fontes

- Página de origem: https://www.skills.sh/google-labs-code/design.md/ink (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/google-labs-code/design.md (metadados e árvore consultados via API do GitHub em 2026-10-19; commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`). O repositório não foi clonado; o `SKILL.md` foi lido conforme renderizado na página do skills.sh, não como arquivo cru no repositório. O pacote `@json-render/ink` não foi consultado diretamente.
