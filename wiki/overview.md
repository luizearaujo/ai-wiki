---
type: overview
created: 2026-10-17
updated: 2026-10-18
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
- **Instruções persistentes para agentes:** arquivos como `CLAUDE.md` fixam convenções, comandos e critérios de comportamento entre sessões, em contraste com skills carregadas por tarefa.
- **Bibliotecas de personalidades de agente:** coleções de arquivos `.md` que definem especialidade, voz, regras críticas, entregáveis e métricas para agentes de IA, instaláveis em vários clientes; o Agency Agents é o maior exemplo documentado na wiki.
- **Grafo de conhecimento de código como camada de contexto para agentes:** indexar uma base de código em um grafo persistente permite que o agente responda perguntas estruturais (callers, rotas, dependências) em milissegundos e com ~10–120× menos tokens do que lendo arquivos; o CBM é o primeiro servidor MCP desse tipo documentado na wiki.

## Mapa por área

| Área | Repositórios | Observações |
| --- | --- | --- |
| Engenharia reversa e análise de software | [morluto/rea](repos/github.com/morluto/rea.md) | CLI + MCP local; binários nativos, apps JavaScript/Electron, .NET, Android, firmware e runtime; providers bring-your-own. |
| Protocolos para agentes | — | MCP aparece como infraestrutura transversal; primeira página em [Model Context Protocol](concepts/model-context-protocol.md). |
| Skills para agentes | — | Primeira página em [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md); formato descrito em [Agent skills](concepts/agent-skills.md). |
| Instruções e diretrizes para agentes | [multica-ai/andrej-karpathy-skills](repos/github.com/multica-ai/andrej-karpathy-skills.md) | Quatro princípios de comportamento em um `CLAUDE.md`; distribuição como arquivo ou plugin; variação para Cursor. Formato descrito em [CLAUDE.md](concepts/claude-md.md). |
| Personalidades de agente por especialidade | [msitarzewski/agency-agents](repos/github.com/msitarzewski/agency-agents.md) | 150+ arquivos `.md`, cada um com identidade, regras críticas, entregáveis e métricas; organizados em 16 divisões (Engenharia, Segurança, Marketing, GIS etc.); instaláveis via app ou script em Claude Code, Cursor, Codex e mais. |
| Grafo de conhecimento de código | [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) | Servidor MCP local em C puro; indexa 162 linguagens via tree-sitter + Hybrid LSP; 17 ferramentas MCP; SQLite persistente; CBM Lens Beta para visualização; ~120× menos tokens vs arquivo por arquivo (comparação do projeto); suporta 45 clientes. |
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
- O Agency Agents amplia essa superfície: 150+ arquivos de terceiros que moldam o comportamento do agente, instalados por script ou app nativo. Cada arquivo `.md` é uma instrução de sistema com personalidade e regras críticas; sem verificação de integridade documentada, a fonte importa.
- O CBM toma uma rota oposta: binário estático com SLSA 3, OpenSSF Scorecard e checksums SHA-256 por release; não faz nenhuma requisição de rede por conta própria. O custo é que atualizar exige rodar o install script manualmente ou via gerenciador de pacotes.
- **Grafo estático ≠ cobertura completa**: um grafo de código responde apenas ao que o parser indexou; chamadas dinâmicas, dispatch por reflexão e código gerado em runtime não aparecem. O README do CBM documenta explicitamente as lacunas de cobertura e disponibiliza um workspace "Coverage" no Lens.
- **Diretrizes e skills ocupam camadas diferentes:** um `CLAUDE.md` fornece contexto persistente do projeto; uma skill é acionada por tarefa. Os formatos podem coexistir, mas custo de contexto e precedência em conflitos ainda não são claros.
- A transferência de `andrej-karpathy-skills` de `forrestchang` para `multica-ai` ilustra como **links de instalação podem ficar defasados** mesmo quando o host redireciona o caminho antigo.

## Lacunas e próximos passos

- [ ] Ingerir uma alternativa ou competidor: outro servidor MCP de engenharia reversa, ou um fluxo Ghidra/IDA + agente.
- [ ] Ler a documentação oficial do REA (com autorização) para aprofundar o `EvidenceLedger` e o roteamento de providers.
- [ ] Comparar o REA com fluxos manuais (Ghidra/IDA) e medir custo/tempo/tokens.
- [ ] Ler `docs/testing.md` (com autorização) para verificar quais providers e plataformas têm lanes de teste com ferramentas reais.
- [ ] Mapear outros repositórios do autor e do ecossistema MCP de análise.
- [ ] Ler o `SKILL.md` de UX Audit Rethink (com autorização) para documentar método, escala e formato de saída.
- [ ] Ingerir outras skills do ecossistema e comparar formatos/distribuição.
- [ ] Comparar auditoria de UX conduzida por agente com avaliação heurística tradicional.
- [ ] Ler `CLAUDE.md`, `CURSOR.md` e `.cursor/rules/karpathy-guidelines.mdc` de `andrej-karpathy-skills` (com autorização) para verificar o texto real das diretrizes e a adaptação ao Cursor.
- [ ] Verificar se os comandos de instalação com `forrestchang/...` continuam funcionando após a transferência do repositório.
- [ ] Comparar `CLAUDE.md` e skills `SKILL.md` em custo de contexto, precedência e efeito observável no comportamento do agente.

## Fontes

- [morluto/rea](repos/github.com/morluto/rea.md) — README no commit `9e372c6bc914b15e2f778f969da4fd3e11483d78`; metadados do GitHub observados em 2026-10-17.
- [UX Audit Rethink](skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — https://claudemarketplaces.com/skills/mastepanoski/claude-skills/ux-audit-rethink (consultada em 2026-10-17).
- https://github.com/mastepanoski/claude-skills — metadados e árvore via API do GitHub em 2026-10-17 (commit `b6457af10e586d394056aae9555e78d74a372225`).
- [multica-ai/andrej-karpathy-skills](repos/github.com/multica-ai/andrej-karpathy-skills.md) — README no commit `2c606141936f1eeef17fa3043a72095b4765b9c2`; metadados da API do GitHub observados em 2026-10-17.
- [msitarzewski/agency-agents](repos/github.com/msitarzewski/agency-agents.md) — README no commit `652b2692f8d8ec2b1f1a38e559073e287dfdc469`; metadados da API do GitHub observados em 2026-10-18.
- [DeusData/codebase-memory-mcp](repos/github.com/deusdata/codebase-memory-mcp.md) — README no commit `354ccecbe612a9fdb624396a6738fa87f2617434`; metadados da API do GitHub observados em 2026-10-18.
