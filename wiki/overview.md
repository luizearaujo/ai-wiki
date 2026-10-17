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
- **Agent skills como formato de distribuição:** instruções especializadas empacotadas em `SKILL.md`, versionadas em repositórios e instaladas por CLI em vários agentes.
- **Auditoria de UX assistida por agentes:** frameworks de avaliação de produto operacionalizados como instruções reutilizáveis, com métodos e limitações próprios.

## Mapa por área

| Área | Repositórios | Observações |
| --- | --- | --- |
| Engenharia reversa e análise de software | [morluto/rea](repos/github.com/morluto/rea.md) | CLI + MCP local; binários nativos, apps JavaScript/Electron, .NET, Android, firmware e runtime; providers bring-your-own. |
| Protocolos para agentes | — | MCP aparece como infraestrutura transversal; primeira página em [Model Context Protocol](concepts/model-context-protocol.md). |
| Skills para agentes | — | Primeira página em [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md); formato descrito em [Agent skills](concepts/agent-skills.md). |
| Avaliação de UX | — | Primeira síntese em [Auditoria de UX](concepts/auditoria-de-ux.md); aplicação documentada na skill UX Audit Rethink. |

## Tendências e observações

- Ferramentas para agentes estão migrando de plugins específicos para **servidores MCP locais com CLI compartilhada**, o que permite o mesmo workflow em vários clientes.
- O modelo **bring-your-own provider** (Hopper, Ghidra, IDA, JADX etc.) reduz o escopo do projeto, mas transfere ao usuário a responsabilidade por licenças e pela verificação real de cada plataforma.
- **Evidência estruturada** — cobertura, limitações e desconhecidos — é o que torna a análise por agentes auditável; sem isso, a explicação do agente não é distinguível de uma inferência plausível.
- Catálogos MCP grandes podem custar muito contexto; respostas com views, paginação e exportação preservam a evidência completa sem enviá-la inteira ao modelo.
- O REA é um caso de adoção expressiva (o README celebra 300 mil estrelas) e o próprio README avisa que o projeto muda rápido e recebe correções com frequência; registrar a versão e o commit usados continua essencial.
- **Skills e MCP são camadas complementares:** skills empacotam instruções e métodos; MCP expõe ferramentas e dados em runtime. Um agente pode usar as duas ao mesmo tempo.
- Catálogos de skills expõem métricas voláteis (instalações, estrelas) e, às vezes, não publicam a versão da skill; a fonte canônica continua sendo o repositório-fonte.
- A distribuição de skills por CLI cria uma **superfície de supply chain**: instruções de terceiros passam a fazer parte do comportamento do agente. Guardas contra prompt injection dentro de uma skill são um sinal do risco, não uma garantia.

## Lacunas e próximos passos

- [ ] Ingerir uma alternativa ou competidor: outro servidor MCP de engenharia reversa, ou um fluxo Ghidra/IDA + agente.
- [ ] Ler a documentação oficial do REA (com autorização) para aprofundar o `EvidenceLedger` e o roteamento de providers.
- [ ] Comparar o REA com fluxos manuais (Ghidra/IDA) e medir custo/tempo/tokens.
- [ ] Ler `docs/testing.md` (com autorização) para verificar quais providers e plataformas têm lanes de teste com ferramentas reais.
- [ ] Mapear outros repositórios do autor e do ecossistema MCP de análise.
- [ ] Ler o `SKILL.md` de UX Audit Rethink (com autorização) para documentar método, escala e formato de saída.
- [ ] Ingerir outras skills do ecossistema e comparar formatos/distribuição.
- [ ] Comparar auditoria de UX conduzida por agente com avaliação heurística tradicional.

## Fontes

- [morluto/rea](repos/github.com/morluto/rea.md) — README no commit `9e372c6bc914b15e2f778f969da4fd3e11483d78`; metadados do GitHub observados em 2026-10-17.
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — https://claudemarketplaces.com/skills/mastepanoski/claude-skills/ux-audit-rethink (consultada em 2026-10-17).
- https://github.com/mastepanoski/claude-skills — metadados e árvore via API do GitHub em 2026-10-17 (commit `b6457af10e586d394056aae9555e78d74a372225`).
