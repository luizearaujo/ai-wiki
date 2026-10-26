---
type: concept
aliases: [agentic reverse engineering, reverse engineering with agents, RE agêntica]
status: draft
created: 2026-10-17
updated: 2026-10-26
tags: [agentes, engenharia-reversa, ferramentas]
---

# Engenharia reversa agêntica

> Uso de agentes de IA com acesso a ferramentas de análise para investigar software sem código-fonte, iterando entre observação estática e runtime até explicar ou reconstruir um comportamento.

## Definição

Engenharia reversa agêntica é a combinação de um agente de LLM com ferramentas especializadas — descompiladores, disassemblers, analisadores de artefatos, instrumentação e captura de execução — para conduzir uma investigação que tradicionalmente seria feita manualmente por um analista. O agente não "adivinha" o binário: ele planeja, chama ferramentas, lê os resultados, levanta hipóteses e pede verificações.

A diferença em relação a um chatbot com acesso a código é o ciclo fechado: a ferramenta produz fatos observáveis (assembly, pseudocódigo, referências, comportamento capturado), o agente decide o que investigar em seguida e o resultado final pode ser testado contra o alvo.

## Como funciona

1. **Roteamento pelo alvo.** O tipo de artefato determina o primeiro conjunto de ferramentas: binário nativo, aplicação JavaScript/Electron, assembly .NET, APK, firmware, website ou captura de rede.
2. **Coleta estática.** O agente decompila funções, busca strings, segue referências, monta grafos de chamadas e inventaria artefatos.
3. **Observação de runtime.** Quando o comportamento não é estabelecido pelo estático, o agente pode executar ou anexar ao alvo, capturar rede, inspecionar o browser ou instrumentar processos — dentro dos limites de autorização e das permissões do usuário.
4. **Reconciliação.** Achados estáticos e observações de runtime são comparados; divergências e lacunas permanecem explícitas.
5. **Reconstrução e teste.** O agente usa as evidências para explicar a feature, escrever uma implementação equivalente e validá-la contra casos observados.
6. **Proveniência.** Cada conclusão relevante deve apontar para a observação que a sustenta, incluindo cobertura e limitações.

## Onde aparece

- [morluto/rea](../repos/github.com/morluto/rea.md) — implementa esse padrão como um servidor MCP + CLI para binários e aplicações (estático + runtime). Exemplos publicados incluem a reconstrução de um cálculo de áudio do DX-Ball, o rastreamento da ponte de clipboard do Electron no Notion e a recuperação de um cálculo de bullet-ring do TH04 em DOS. O REA também documenta o lado epistemológico do padrão: ferramentas retornam cobertura, limitações e desconhecidos.
- [kalil0321/reverse-api-engineer](../repos/github.com/kalil0321/reverse-api-engineer.md) — aplica o padrão especificamente à camada de rede de websites: um agente (ou o usuário) navega no site, o tráfego HTTP é capturado em HAR, e um LLM gera um cliente tipado em até 10 linguagens. Distingue-se do REA por focar em APIs web (não binários), por produzir código de cliente (não apenas análise), e por integrar diretamente com Claude Code, Codex, Cursor e OpenCode.
- [littledivy/mimic](../repos/github.com/littledivy/mimic.md) — abordagem anterior ao mesmo problema, mas voltada a apps iOS/web via mitmproxy: captura sessões autenticadas e usa Claude para gerar um cliente Python chamável como biblioteca. Menos modos de operação, mas cobre interceptação de HTTPS em apps móveis que não têm DevTools acessível.

## Trade-offs

- **Vantagens:** reduz a barreira de entrada para investigações complexas; cruza camadas (binário → app → runtime) sem trocar de contexto; torna o processo reproduzível quando a evidência é preservada; permite que um único agente conduza ida e volta entre hipótese e verificação.
- **Limitações:** o agente pode superinterpretar saída incompleta; a qualidade depende do provider e da cobertura observada; o custo de tokens pode crescer com catálogo, ferramentas e evidências; resultados são não determinísticos; análise de runtime usa permissões reais e pode alterar ou executar o alvo (instrumentação com Frida, por exemplo, não é read-only).
- **Requisitos:** autorização para examinar o software, providers configurados e disciplina para distinguir observação, derivação, inferência e desconhecido.

## Relações

- **Relacionado a:** [Model Context Protocol (MCP)](model-context-protocol.md), agent skills, análise estática, análise dinâmica e observabilidade.
- **Depende de:** ferramentas de engenharia reversa (descompiladores, disassemblers, analisadores de artefatos) e de um agente capaz de orquestrar chamadas.
- **Contrasta com:** engenharia reversa puramente manual e com "vibe analysis" sem evidência.

## Perguntas abertas

- Como avaliar a qualidade de uma investigação agêntica de forma objetiva, além de "a explicação parece boa"?
- Como medir e reduzir falsas conclusões quando a cobertura da ferramenta é parcial?
- Qual é o custo total (tokens, tempo, CPU) de uma investigação real comparado a um fluxo manual?
- Como preservar a proveniência quando o agente combina vários providers e observações de runtime?

## Fontes

- [morluto/rea](../repos/github.com/morluto/rea.md) — `README.md`, `AGENTS.md`, `docs/cli.md`, `docs/tool-design.md`, `docs/roadmap.md` e `.agents/skills/reverse-engineer-anything/SKILL.md` (commit `09de00b4108a5d738ebe56903e0110ef63820aca`, consultado em 2026-10-17).
