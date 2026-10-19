---
type: concept
aliases: [Auditoria de mídia paga, Paid media audit, Auditoria de anúncios, Ad account audit]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [marketing, publicidade, auditoria, evidencia, agentes]
---

# Auditoria de mídia paga

> Avaliação estruturada de contas de anúncios em que cada achado é vinculado a uma evidência, dados ausentes viram `unknown` em vez de suposição e recomendações ficam separadas das alterações efetivamente aplicadas.

## Definição

Auditoria de mídia paga é a verificação de uma conta de anúncios — configuração, tracking, estrutura de campanha, gasto, criativos e conformidade — contra um conjunto explícito de controles. Feita por agentes, o problema deixa de ser "gerar uma lista de dicas" e passa a ser **produzir um registro auditável**: o que passou, o que falhou, o que não pôde ser verificado e qual evidência sustenta cada item.

Isso a distingue de:

- **análise de performance** — mede resultado (CPA, ROAS, CTR) sem julgar configuração;
- **recomendação genérica** — boas práticas sem vínculo com os dados da conta;
- **automação de campanha** — aplica mudanças, com ou sem auditoria prévia.

## Como funciona

O padrão observado no [AgriciDaniel/claude-ads](../repos/github.com/agricidaniel/claude-ads.md):

```text
perfil da conta -> evidência (export, screenshot, resumo) -> controles por plataforma
        -> pass | fail | unknown | not_applicable -> cobertura -> relatório versionado
```

| Componente | Papel |
|---|---|
| **Perfil** | Modelo de negócio, objetivo, conversão principal, gasto, plataformas e aprovador |
| **Evidência** | Export CSV/JSON, screenshots ou resumo com período, moeda e fuso |
| **Controles** | Checklist por plataforma, com severidade e referência |
| **Estados** | `pass`, `fail`, `unknown`, `not_applicable`; `unknown` nunca é adivinhado |
| **Cobertura** | Proporção de controles verificáveis; abaixo de um limite, a auditoria é evidência insuficiente |
| **Agregação** | Conductor consolida workers; falha obrigatória marca a execução como parcial |
| **Escrita** | Capacidade, IDs explícitos, diff, aprovação, idempotência, rollback e verificação |

Duas separações sustentam a confiabilidade: **saúde da conta** não se confunde com **cobertura de evidência** (um dado ausente não piora o diagnóstico conhecido, só reduz a confiança), e **achado** não se confunde com **mudança** (rascunho é reversível; aplicar exige gates).

## Onde aparece

- [AgriciDaniel/claude-ads](../repos/github.com/agricidaniel/claude-ads.md) — skill em 12 plataformas: conductor + workers, JSON versionado, quatro estados, cobertura graduada, Cockpit opcional e escrita read-only por padrão. Os perfis de saúde estão desativados no estado atual do projeto.

## Trade-offs

- **Vantagens:** achados reproduzíveis e citáveis; separação entre o que se sabe e o que falta; recomendações não se disfarçam de fatos; permite comparar execuções e contas; gates de escrita reduzem risco de alteração indevida.
- **Limitações:** depende da qualidade e da completude da exportação; cobertura baixa pode tornar a auditoria inconclusiva; o custo de construir e manter controles por plataforma é alto e envelhece com mudanças de API e política; sem um score aprovado, a comparação entre contas fica mais difícil; validação "ao vivo" e leitura por API introduzem rate limits e permissões.
- **Critério prático:** vale quando o resultado precisa ser auditado por terceiros ou quando há várias contas/plataformas; para uma conta pequena e uma pergunta pontual, uma análise de performance direta pode ser suficiente.

## Relações

- **Relacionado a:** [Evidência e proveniência](evidencia-e-proveniencia.md) — o mesmo padrão de registro canônico com cobertura e incerteza; [Agent skills](agent-skills.md) — o método é distribuído como skill instalável; [CLI agent-first](cli-agent-first.md) — comandos e saídas estruturadas como interface do agente; [Saída completa de agente](saida-completa-de-agente.md) — execução parcial declarada em vez de relatório silenciosamente incompleto.
- **Contrasta com:** automação de campanha sem auditoria; listas de boas práticas sem vínculo com dados; dashboards de performance que não avaliam configuração.
- **Depende de:** acesso a exports ou APIs de cada plataforma; permissões e limites de leitura; um modelo de controles versionado.

## Perguntas abertas

- Qual é a cobertura mínima para uma auditoria ser considerada conclusiva na prática?
- Como manter controles atualizados quando a plataforma muda política ou API?
- Quem aprova uma escrita e como o limite por conta é representado de forma verificável?
- Como comparar auditorias de plataformas diferentes sem um score comum?
- Qual é o risco de o agente confundir `unknown` com `pass` por otimismo?
- Como tratar contas multi-moeda, multi-fuso e com histórico incompleto?

## Fontes

- [AgriciDaniel/claude-ads](../repos/github.com/agricidaniel/claude-ads.md) — README no commit `fc3908e786c318776df89a3a098333da377364be` (consultado em 2026-10-19). Somente o README foi lido.
