---
type: concept
aliases: [UX audit, Auditoria de experiência do usuário, Avaliação heurística de UX]
status: draft
created: 2026-10-17
updated: 2026-10-17
tags: [ux, design, avaliacao, auditoria]
---

# Auditoria de UX

> Avaliação estruturada da experiência de um produto contra um conjunto explícito de critérios, para identificar problemas, lacunas e oportunidades de redesign.

## Definição

Uma auditoria de UX examina um produto — app, site, fluxo ou interface — a partir de critérios declarados e produz um diagnóstico: o que funciona, o que falha em cada dimensão, quais lacunas existem e o que mudar. É uma análise conduzida por especialista (humano ou agente), distinta de pesquisa com usuários: não observa comportamento real em escala nem substitui testes de usabilidade.

O valor está na **estrutura**: sem um framework, a avaliação vira uma lista de opiniões. Com um framework, cada achado pode ser atribuído a uma dimensão e comparado entre versões ou produtos.

## Como funciona

Um roteiro comum:

1. **Escolher o framework** adequado à pergunta (produto inteiro, usabilidade, acessibilidade).
2. **Reunir evidência**: telas, fluxos, texto, feedback de usuários e, quando possível, o comportamento em uso.
3. **Avaliar cada dimensão**, atribuindo achados e, se o método permitir, uma classificação.
4. **Fazer análise de lacunas** entre o que o produto promete e o que entrega.
5. **Priorizar recomendações** de redesign por impacto e esforço.

Frameworks citados na página da skill [UX Audit Rethink](../skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md):

| Framework | Dimensões |
| --- | --- |
| Honeycomb de Morville | útil, usável, encontrável, crível, desejável, acessível, valioso |
| Características de usabilidade (ISO) | efetividade, eficiência, engajamento, tolerância a erros, facilidade de aprendizado |
| Dimensões de interaction design | palavras, visuais, espaço físico, tempo, comportamento |

Frameworks especializados cobrem recortes: heurísticas de Nielsen para problemas de usabilidade e WCAG para acessibilidade. Uma auditoria ampla pode usá-los como complemento, não como substitutos.

## Onde aparece

- [UX Audit Rethink](../skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — skill que operacionaliza os três frameworks para agentes e inclui guardas contra prompt injection em material de entrada.

## Trade-offs

- **Vantagens:** diagnóstico estruturado e comparável; cobertura ampla sem depender de uma única lente; recomendações priorizáveis.
- **Limitações:** julgamento qualitativo e sujeito a viés; critérios como "desejável" e "crível" dependem de público e cultura; sem acesso ao produto ou a evidências, o resultado é especulação; não mede uso real.

## Relações

- **Relacionado a:** [Agent skills](../concepts/agent-skills.md) — formato que permite distribuir um método de auditoria como instruções reutilizáveis.
- **Contrasta com:** pesquisa com usuários e analytics de produto, que observam comportamento em vez de julgar critérios.
- **Complementa:** auditorias especializadas de acessibilidade (WCAG) e de usabilidade (heurísticas de Nielsen).

## Perguntas abertas

- Como comparar auditorias feitas por agentes diferentes com o mesmo framework?
- Que evidência mínima é necessária para que uma auditoria não seja opinião?
- Como medir o impacto real das recomendações de redesign?

## Fontes

- [UX Audit Rethink](../skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — descrição dos três frameworks e do tipo de saída (consultada em 2026-10-17).
- https://claudemarketplaces.com/skills/mastepanoski/claude-skills/ux-audit-rethink — página de origem da skill (consultada em 2026-10-17).
