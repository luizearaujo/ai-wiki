---
type: concept
aliases: [Evidence, evidence ledger, proveniência, rastreabilidade de análise]
status: draft
created: 2026-10-17
updated: 2026-10-17
tags: [evidencia, proveniencia, agentes, analise]
---

# Evidência e proveniência

> Modelo em que cada resultado de análise é um registro canônico e rastreável, com resultado normalizado, cobertura observada, limitações e desconhecidos explícitos.

## Definição

Em ferramentas de análise usadas por agentes, "evidência" não é apenas a resposta textual: é o registro estruturado que sustenta uma conclusão. Um bom registro responde: qual alvo foi analisado, qual provider e perfil produziram o resultado, o que foi efetivamente observado, o que ficou fora da cobertura e o que permanece desconhecido.

Proveniência é a ligação entre a conclusão do agente e esse registro. Sem ela, uma explicação plausível é indistinguível de uma alucinação.

## Como funciona

No REA, o contrato MCP distingue:

- `structuredContent.normalized_result` — o resultado canônico da operação;
- `structuredContent.evidence_id` — a identidade da evidência;
- `raw_result` — a representação original do provider, quando existe;
- `analysis_profile` — o perfil de análise, sempre presente (objeto concreto ou `null`) e parte da identidade semântica.

A cobertura é declarada pelo produtor: `coverage.scope` (`root` ou `container-entries`) e `coverage.status` (`complete` ou `unknown`). Comparações exigem escopos compatíveis e cobertura completa antes de concluir igualdade; ausência de cobertura é **desconhecido**, não ausência de fato.

O REA também mantém um ledger de desconhecidos, permite reter evidência por sessão, paginar views, exportar bundles e devolver `resource_constraint` com uma referência à evidência completa quando o resultado não cabe no limite de transporte MCP.

## Onde aparece

- [morluto/rea](../repos/github.com/morluto/rea.md) — implementa o modelo em `docs/mcp-contracts.md`, `docs/tool-design.md` e `src/application/investigation/` (`InvestigationRecords`, `EvidenceLedger` e propriedade explícita de desconhecidos).
- O padrão aparece no fluxo de investigação: o agente recebe evidência, pode compará-la com outra evidência compatível e pode arquivar/exportar o bundle completo.

## Trade-offs

- **Vantagens:** auditoria e reprodutibilidade; preservação de resultados parciais; comparações honestas; conclusões que distinguem observado, derivado e inferido; menos espaço para o agente "preencher lacunas" com invenção.
- **Limitações:** evidências completas podem ser enormes (centenas de megabytes em aplicações reais); exigem views, paginação e exportação; aumentam a complexidade dos contratos; o custo de contexto depende de quanto o agente pede; retenção e expiração precisam de política.
- **Risco:** um registro com cobertura `unknown` ainda pode ser lido como completo se o consumidor ignorar os campos de cobertura. O produtor e o consumidor precisam tratar os metadados como parte do contrato.

## Relações

- **Relacionado a:** [Model Context Protocol (MCP)](model-context-protocol.md), [engenharia reversa agêntica](engenharia-reversa-agentica.md), observabilidade e linhagem de dados.
- **Contrasta com:** saídas de ferramentas sem metadados de cobertura, em que o agente não consegue distinguir "não há" de "não foi observado".
- **Pré-requisito para:** comparações confiáveis entre versões, providers ou camadas de uma aplicação.

## Perguntas abertas

- Como projetar resumos e views sem perder a proveniência necessária para auditoria?
- Como comparar evidências produzidas por providers diferentes sem tratar diferenças de capacidade como contradições?
- Qual política de retenção e expiração faz sentido para sessões longas?
- Como sinalizar, de forma difícil de ignorar, que uma cobertura é desconhecida?

## Fontes

- [morluto/rea](../repos/github.com/morluto/rea.md) — `README.md`, `AGENTS.md`, `docs/mcp-contracts.md`, `docs/tool-design.md` e `docs/architecture.mermaid` (commit `09de00b4108a5d738ebe56903e0110ef63820aca`, consultado em 2026-10-17).
