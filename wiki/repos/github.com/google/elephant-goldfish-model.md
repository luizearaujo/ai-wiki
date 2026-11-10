---
type: repo
url: https://github.com/google/elephant-goldfish-model
host: github.com
owner: google
repo: elephant-goldfish-model
commit: bdcfe8cdaee99699c4b2cb7ad4e3b2c1a6b56a31
license: Apache-2.0
language: Python
status: active
created: 2026-11-10
ingested: 2026-11-10
updated: 2026-11-10
tags: [agentes, design, spec, revisao, orquestracao, skills, spec-driven]
---

> Plugin open-source para design e revisão de software com agentes: um "Elephant" com contexto profundo rascunha a especificação; um "Goldfish" com contexto limpo expõe suposições e riscos.

## Propósito

O Elephant-Goldfish Model (EGM) estrutura o processo de design de software como uma colaboração entre dois perfis de agente e o usuário:

| Papel | Contexto | Responsabilidade |
|-------|----------|-----------------|
| **Elephant** | Projeto completo, requisitos, decisões anteriores | Explorar o problema e rascunhar a especificação |
| **Goldfish** | Apenas o documento + código referenciado (sem conversa anterior) | Identificar suposições faltantes e riscos |
| **Usuário** | Objetivos e restrições | Resolver trade-offs e aprovar o design |

A revisão Goldfish exige subagentes com contexto limpo. Se o agente não conseguir criá-los, o EGM interrompe a revisão — essa é a garantia de que a perspectiva fresca é genuína, não contaminada pelo histórico da sessão.

O projeto foi publicado pela Google com aviso explícito de que **não é um produto Google oficialmente suportado**.

## Skills disponíveis

O plugin expõe sete skills:

| Skill | Propósito |
|-------|-----------|
| `egm-brainstorm` | Explorar ideia e escrever breve conceitual (`concepts_brief.md`) |
| `egm-draft` | Converter breve em documento de design (`design_draft.md`) |
| `egm-review` | Revisão em cinco estágios com leitores Goldfish |
| `egm-review-loop` | Executar grupo configurado de revisores |
| `egm-resolve` | Trabalhar achados de revisão |
| `egm-bootstrap` | Criar ou atualizar documentação de base de código existente |
| `egm-drift-report` | Comparar documentos de design com o código-fonte atual |

## Instalação

**Claude Code:**
```bash
claude plugin marketplace add google/elephant-goldfish-model
claude plugin install egm@egm
```

**Antigravity CLI:**
```bash
agy plugin install https://github.com/google/elephant-goldfish-model
```

**Codex CLI:**
```bash
codex plugin marketplace add google/elephant-goldfish-model
codex plugin add egm@egm
```

No Claude Code e Antigravity, as skills são invocadas com o prefixo `/egm:` (ex.: `/egm:egm-brainstorm`). Uma nova sessão é necessária após a instalação.

## Exemplo de uso

Adicionar webhook delivery a um sistema existente:

1. `/egm:egm-brainstorm` — discutir requisitos e salvar em `concepts_brief.md`
2. `/egm:egm-draft` — transformar o breve em `design_draft.md`
3. `/egm:egm-review design_draft.md` — revisores Goldfish avaliam clareza, suposições e plano de implementação

As especificações aprovadas são salvas em `docs/designs/`.

## Pré-requisitos

- Agente compatível com plugins: Claude Code, Codex CLI, Antigravity ou ChatGPT Desktop.
- Capacidade de criar subagentes com contexto limpo (obrigatório para a fase de revisão Goldfish).

## Limitações

- Revisão não substitui testes automatizados nem julgamento humano.
- O plugin ChatGPT/Codex Desktop funciona apenas no app desktop.
- Suporte e comportamento variam entre harnesses (documentado em `docs/setup`).

**A verificar:** versão atual, número de estrelas e forks; comportamento específico por harness; relação com o `Google Labs Code` ou equipes internas da Google.

## Fontes

- README.md do repositório (`bdcfe8cdaee99699c4b2cb7ad4e3b2c1a6b56a31`), lido em 2026-11-10.
- Metadados via API do GitHub (linguagem, licença, tópicos), consultados em 2026-11-10.
- Apenas o `README.md` foi lido.
