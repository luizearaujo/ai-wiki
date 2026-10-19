---
type: repo
url: https://github.com/twentyhq/twenty
host: github.com
owner: twentyhq
repo: twenty
commit: 31d95e98a2217e187d6f7d51f7ab69bb048e22bc
license: desconhecida
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [crm, agentes, agent-skills, objetos-como-codigo, open-source]
---

# twentyhq/twenty

> CRM open source "desenhado para IA": objetos, campos, views, workflows e agentes definidos como código versionável, com uma CLI própria e skills oficiais para agentes de código como Claude Code, Codex e Cursor.

## O que é

Twenty é um CRM que trata a modelagem de dados e a lógica de negócio como artefatos de desenvolvimento — definidos em TypeScript, publicados e versionados como qualquer outro pacote — em vez de configuração feita só pela interface. O README posiciona o projeto como alternativa ao Salesforce "desenhada para IA", com objetos, views e agentes como blocos de construção que um time técnico estende.

## Como funciona

- **Apps como código:** a CLI `create-twenty-app` cria um scaffold; objetos são definidos com `defineObject`/`FieldType` do `twenty-sdk/define`, e o app é publicado no workspace com `twenty app:publish`.
- **Skills oficiais para agentes:** o pacote `packages/twenty-agent-skills` é instalável via `npx skills add https://github.com/twentyhq/twenty/tree/agent-skills --list` e funciona em Claude Code, Codex, Cursor, Pi e qualquer harness suportado pela CLI `skills`. A branch `agent-skills` é gerada automaticamente pelo primeiro publish bem-sucedido a partir de `main`; até isso ocorrer, o README indica construir localmente. Um arquivo `SKILLS.md` na raiz descreve outras famílias de skills do repositório.
- **Hospedagem:** cloud (`twenty.com`, workspace pronto em minutos) ou self-hosted via Docker Compose.
- **Arquitetura:** monorepo Nx; backend NestJS com BullMQ (filas), PostgreSQL e Redis; frontend React com Jotai (estado), Linaria (CSS-in-JS) e Lingui (i18n).
- **Recursos de produto:** objetos e campos customizáveis, views, workflows, agentes e chats de IA integrados ao CRM (feature de produto, não documentada em detalhe no README raiz).

### Licenciamento (misto)

O arquivo `LICENSE` do repositório declara um esquema de três regimes, não um único SPDX:

1. A maior parte do projeto é **AGPLv3**, com uma permissão adicional da Seção 7 ("Twenty Application Exception").
2. Arquivos com o comentário `/* @license Enterprise */` no topo são licenciados sob termos comerciais definidos no próprio arquivo `LICENSE`.
3. Pacotes específicos usam **MIT** conforme o `license` do `package.json` de cada um: a CLI `twenty`, `twenty-sdk`, `twenty-client-sdk`, `create-twenty-app`, a biblioteca de componentes `twenty-ui` e as aplicações em `packages/twenty-apps`.

A API do GitHub reporta a licença como `NOASSERTION`/"Other" por não conseguir mapear esse esquema a um único SPDX.

## Instalação e uso rápido

Cloud (mais rápido):

```text
Cadastro em twenty.com -> workspace pronto em minutos
```

Scaffold de app com a CLI:

```bash
npx create-twenty-app my-app
```

```ts
import { defineObject, FieldType } from 'twenty-sdk/define';

export default defineObject({
  nameSingular: 'deal',
  namePlural: 'deals',
  labelSingular: 'Deal',
  labelPlural: 'Deals',
  fields: [
    { name: 'name', label: 'Name', type: FieldType.TEXT },
    { name: 'amount', label: 'Amount', type: FieldType.CURRENCY },
    { name: 'closeDate', label: 'Close Date', type: FieldType.DATE_TIME },
  ],
});
```

```bash
npx twenty app:publish --private
```

Skills oficiais para agentes de código:

```bash
npx skills add https://github.com/twentyhq/twenty/tree/agent-skills --list
```

Self-hosting: Docker Compose (ver documentação em docs.twenty.com).

## Exemplos de uso

Exemplos derivados do README: criar um objeto `deal` com campos de nome, valor e data de fechamento e publicá-lo no workspace privado do time; instalar as skills oficiais do Twenty num agente de código para que ele desenvolva apps sobre o CRM seguindo o guia publicado de extensão (objetos, views, agentes e funções de lógica).

## Quando usar (e quando não usar)

- **Use quando:** o time quer um CRM que modela e versiona objetos/campos/workflows como código, com opção de self-hosting e integração nativa com agentes de código via skills oficiais.
- **Evite quando:** o requisito é um CRM de configuração puramente visual sem equipe técnica para manter definições como código; ou quando o regime de licença misto (AGPLv3 + Enterprise + MIT por pacote) precisa de clareza jurídica antes do uso comercial — vale revisar o `LICENSE` por arquivo, não só o badge do README.

## Limitações e cuidados

- **Somente o README foi lido.** `SKILLS.md`, o pacote `twenty-agent-skills`, o backend NestJS, o frontend React e a documentação completa em docs.twenty.com não foram consultados.
- A branch `agent-skills` só existe após o primeiro publish bem-sucedido a partir de `main`; o README não garante que ela já exista no momento da leitura.
- A licença é mista por arquivo e por pacote — tratar o repositório como "um" regime de licença é impreciso; o módulo Enterprise é comercial dentro do mesmo código AGPLv3.
- Os recursos de "agentes e chats de IA" dentro do próprio produto CRM são citados no tour de funcionalidades, mas não detalhados no README raiz.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~58,5 mil estrelas, ~9,6 mil forks, 122 issues abertas; criado em 2022-12-01, último push em 2026-10-19.
- **Licença:** mista — AGPLv3 (com exceção de aplicação) + módulos comerciais Enterprise + pacotes MIT (CLI/SDK/UI), conforme o arquivo `LICENSE`; API do GitHub reporta `NOASSERTION`.
- **Linguagem principal:** TypeScript.

## Relações

- **Mantido por:** [twentyhq](../../../entities/twentyhq.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — skills oficiais instaláveis via CLI `skills` em múltiplos agentes de código.
- **Relacionado a:** [croffasia/itsaplan](../croffasia/itsaplan.md) — outra ferramenta de trabalho (issue tracker) onde agentes e pessoas compartilham o mesmo fluxo; o Twenty aplica uma lógica semelhante a objetos de CRM em vez de issues.

## Perguntas abertas

- O que exatamente os "agentes e chats de IA" embutidos no produto fazem, e como se relacionam com as skills de agente de código distribuídas no repositório?
- Como o regime de licença misto (AGPLv3 + Enterprise + MIT por pacote) se aplica na prática a um fork ou a um app de terceiro publicado no workspace?
- Qual a cobertura real do guia de "apps como código" para casos além dos exemplos do README?

## Fontes

- README: https://github.com/twentyhq/twenty (commit `31d95e98a2217e187d6f7d51f7ab69bb048e22bc`, consultado em 2026-10-19). Somente o README e o arquivo `LICENSE` (citado pela API de licença do GitHub) foram lidos; código-fonte, `SKILLS.md` e a documentação completa não foram consultados.
- Metadados do repositório: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas); endpoint `repos/twentyhq/twenty/license` e `raw.githubusercontent.com/twentyhq/twenty/main/LICENSE` consultados em 2026-10-19 para o detalhe do regime de licença.
- Perfil da organização: API do GitHub (`orgs/twentyhq`) em 2026-10-19.
