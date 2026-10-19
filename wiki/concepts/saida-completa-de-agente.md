---
type: concept
aliases: [full output, completude de saída, anti-truncamento, output enforcement]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [engenharia-de-agentes, completude, truncamento, output]
---

# Saída completa de agente

> Política de comportamento que trata toda entrega como crítica de produção: nada de placeholders ou elipses no lugar de conteúdo, contagem explícita de entregáveis e um protocolo de pausa e retomada quando o limite de tokens é atingido.

## Definição

Modelos de linguagem tendem a economizar saída: substituir trechos por `// ...`, dizer "o restante segue o mesmo padrão", entregar um esqueleto quando o pedido era implementação completa ou encerrar com "let me know if you want me to continue". A "saída completa de agente" é a política que proíbe esses atalhos e exige que cada item pedido seja entregue por inteiro.

Na wiki, o conceito é documentado pela skill [Full-Output Enforcement](../skills/github.com/leonxlnx/taste-skill/full-output-enforcement.md), publicada no mesmo catálogo das skills de design.

## Como funciona

A política tem três componentes:

1. **Escopo contado** — ler o pedido e contar os entregáveis distintos (arquivos, funções, seções, respostas). Esse número é o contrato.
2. **Construção completa** — gerar cada entregável por inteiro, sem rascunho parcial nem "você pode estender depois".
3. **Conferência antes de responder** — reler o pedido, comparar a contagem entregue com a do escopo e acrescentar o que faltar.

Padrões banidos:

| Categoria | Exemplos |
| --- | --- |
| **Código** | `// ...`, `// rest of code`, `// implement here`, `// TODO`, `/* ... */`, reticências soltas. |
| **Prosa** | "for brevity", "the rest follows the same pattern", "and so on" no lugar de conteúdo real. |
| **Estrutura** | Esqueleto no lugar de implementação, primeira e última seção sem o meio, um exemplo no lugar de lógica repetida, descrição no lugar de código. |

Para saídas longas, a política define um ponto de corte limpo (fim de função, arquivo ou seção) e um marcador explícito de progresso — `[PAUSED — X of Y complete. Send "continue" to resume from: <seção>]`. Ao receber "continue", o agente retoma exatamente de onde parou, sem recapitular.

## Onde aparece

- [Full-Output Enforcement](../skills/github.com/leonxlnx/taste-skill/full-output-enforcement.md) — a formulação direta da política, sem dependência de domínio.
- [Design Taste Frontend](../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) — aplica o mesmo princípio à copy deck e à construção de seções completas.
- [Impeccable](../skills/github.com/pbakaus/impeccable/impeccable.md) — exige código de produção e verifica o resultado renderizado, o que pressupõe entrega integral.

## Trade-offs

- **Vantagens:** entregas previsíveis, menos retrabalho por conteúdo omitido, contrato claro entre usuário e agente, pausa explícita em vez de truncamento silencioso.
- **Limitações:** conflita com instruções de concisão; pode inflar respostas quando o usuário pediu um recorte; não controla o limite real do harness; o marcador de pausa depende de reconhecimento pelo host.

## Relações

- Relacionado a: [Agent skills](agent-skills.md), [Agent harness](agent-harness.md), [TDD para agentes](tdd-para-agentes.md), [Evidência e proveniência](evidencia-e-proveniencia.md).
- Contrasta com: respostas resumidas ou elididas para economizar tokens.
- Pré-requisito para: geração confiável de múltiplos arquivos e migrações completas.

## Perguntas abertas

- O marcador de pausa é reconhecido automaticamente por algum harness?
- A política reduz mensuravelmente a taxa de truncamento?
- Como conciliar completude com janelas de contexto pequenas?
- O usuário deve poder desativar a política por tarefa?

## Fontes

- https://www.skills.sh/leonxlnx/taste-skill/full-output-enforcement — `SKILL.md` renderizado, consultado em 2026-10-19.
- https://www.skills.sh/leonxlnx/taste-skill — catálogo consultado em 2026-10-19.
