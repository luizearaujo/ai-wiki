---
type: overview
created: 2026-10-17
updated: 2026-10-17
tags: []
---

# Panorama do ecossistema de IA

> Síntese em evolução do que a wiki cobre. Atualize quando uma ingestão mudar o quadro geral.

## Temas cobertos

- **Engenharia reversa agêntica:** agentes usando ferramentas locais para investigar artefatos sem código-fonte, cruzar análise estática com runtime e reconstruir comportamento.
- **MCP como camada de integração:** um servidor de ferramentas compartilhado por CLI e agentes, em vez de integrações específicas por cliente.
- **Evidência e proveniência:** resultados de análise com cobertura, limitações e desconhecidos explícitos, para que conclusões de agentes sejam auditáveis.

## Mapa por área

| Área | Repositórios | Observações |
| --- | --- | --- |
| Engenharia reversa e análise de software | [morluto/rea](repos/github.com/morluto/rea.md) | CLI + MCP local; binários nativos, apps JavaScript/Electron, .NET, Android, firmware e runtime; providers bring-your-own. |
| Protocolos para agentes | — | MCP aparece como infraestrutura transversal; primeira página em [Model Context Protocol](concepts/model-context-protocol.md). |

## Tendências e observações

- Ferramentas para agentes estão migrando de plugins específicos para **servidores MCP locais com CLI compartilhada**, o que permite o mesmo workflow em vários clientes.
- O modelo **bring-your-own provider** (Hopper, Ghidra, IDA, JADX etc.) reduz o escopo do projeto, mas transfere ao usuário a responsabilidade por licenças e pela verificação real de cada plataforma.
- **Evidência estruturada** — cobertura, limitações e desconhecidos — é o que torna a análise por agentes auditável; sem isso, a explicação do agente não é distinguível de uma inferência plausível.
- Catálogos MCP grandes podem custar muito contexto; respostas com views, paginação e exportação preservam a evidência completa sem enviá-la inteira ao modelo.
- O REA é um caso de adoção expressiva e cadência de releases muito rápida (~5 releases em 5 dias em outubro de 2026), o que aumenta a importância de registrar a versão e o commit usados em cada análise.

## Lacunas e próximos passos

- [ ] Ingerir uma alternativa ou competidor: outro servidor MCP de engenharia reversa, ou um fluxo Ghidra/IDA + agente.
- [ ] Aprofundar o `EvidenceLedger` e o roteamento determinístico de providers do REA.
- [ ] Comparar o REA com fluxos manuais (Ghidra/IDA) e medir custo/tempo/tokens.
- [ ] Verificar quais providers e plataformas têm lanes de teste com ferramentas reais.
- [ ] Mapear outros repositórios do autor e do ecossistema MCP de análise.

## Fontes

- [morluto/rea](repos/github.com/morluto/rea.md) — commit `09de00b4108a5d738ebe56903e0110ef63820aca`; metadados do GitHub observados em 2026-10-17.
