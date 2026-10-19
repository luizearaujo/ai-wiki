---
type: entity
kind: person
url: https://github.com/karpathy
created: 2026-10-19
updated: 2026-10-19
tags: [pessoa, pesquisa, aprendizado-profundo, wiki, conhecimento]
---

# Andrej Karpathy (karpathy)

> Pesquisador de aprendizado profundo cujo gist `llm-wiki` descreve o padrão de wiki pessoal mantida por LLM que esta wiki instancia.

## O que é

O perfil público no GitHub (`karpathy`) identifica **Andrej Karpathy**, localizado em Stanford, com a bio "I like to train Deep Neural Nets on large datasets". Em 2026-10-19, a API do GitHub reportava 63 repositórios públicos, 226.782 seguidores e 8 seguindo; a conta foi criada em 2010-04-10 e o perfil foi atualizado pela última vez em 2026-03-09.

A fonte desta página é o perfil no GitHub e o gist `llm-wiki`. A biografia profissional mais ampla não foi consultada e não é afirmada aqui.

## Repositórios e projetos

- **Gist `llm-wiki`** — documento de ideia, intencionalmente abstrato, que descreve o padrão: fontes brutas imutáveis, wiki em Markdown mantida pelo agente e schema que define as convenções. Não é um repositório de código; é um texto para ser entregue a um agente e instanciado com ele. Ver [Wiki pessoal com LLMs](../concepts/wiki-pessoal-com-llms.md).
- [multica-ai/andrej-karpathy-skills](../repos/github.com/multica-ai/andrej-karpathy-skills.md) — repositório mantido pela Multica, não por Karpathy, que empacota quatro princípios de comportamento para agentes de código derivados de suas observações sobre falhas recorrentes de LLMs.

## Relevância no ecossistema

O gist fornece o vocabulário operacional usado por wikis mantidas por agentes: três camadas (fontes, wiki, schema), três operações (ingest, query, lint), índice por conteúdo e log cronológico, e a tese de que o bookkeeping é a parte cara — não a leitura. A ideia é apresentada como relacionada ao Memex de Vannevar Bush, com o LLM assumindo a manutenção que a visão original não resolvia.

As diretrizes atribuídas a Karpathy sobre como agentes devem programar também circulam de forma independente, empacotadas por terceiros. Isso mostra que sua influência documentada neste corpus é mais conceitual — padrões de trabalho e de comportamento — do que um projeto de software específico.

## Relações

- **Associado a:** [multica-ai](../entities/multica-ai.md) — mantém o repositório de diretrizes atribuídas a Karpathy.
- **Autor de:** gist `llm-wiki`, a ideia original desta wiki.
- **Relacionado a:** [Wiki pessoal com LLMs](../concepts/wiki-pessoal-com-llms.md), [CLAUDE.md](../concepts/claude-md.md) e [Memória de agente](../concepts/memoria-de-agente.md).

## Fontes

- Perfil `karpathy` via API do GitHub: https://api.github.com/users/karpathy (metadados observados em 2026-10-19).
- Gist `llm-wiki`: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f (revisão `ac46de1ad27f92b28ac95459c782c07f6b8c964a`, consultada em 2026-10-19).
- [multica-ai/andrej-karpathy-skills](../repos/github.com/multica-ai/andrej-karpathy-skills.md) — página existente da wiki; README no commit `2c606141936f1eeef17fa3043a72095b4765b9c2`.
