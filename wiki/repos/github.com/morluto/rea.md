---
type: repo
url: https://github.com/morluto/rea
host: github.com
owner: morluto
repo: rea
commit: 09de00b4108a5d738ebe56903e0110ef63820aca
license: MIT
language: TypeScript
status: active
created: 2026-10-17
ingested: 2026-10-17
updated: 2026-10-17
tags: [agentes, engenharia-reversa, mcp, analise-binaria, cli, local-first]
---

# morluto/rea

> CLI e servidor MCP local que dá a agentes de IA ferramentas para investigar binários nativos, aplicações JavaScript/Electron, assemblies .NET, Android, firmware, websites e comportamento em execução.

## O que é

REA (Reverse Engineer Anything) é uma ferramenta de engenharia reversa assistida por agentes. Em vez de ser um modelo ou um agente, ela é a **camada de ferramentas**: um servidor [MCP](../../../concepts/model-context-protocol.md) e uma CLI que compartilham os mesmos workflows de análise. O usuário descreve um aplicativo ou uma feature que quer entender; o agente chama as ferramentas do REA para inspecionar o alvo, seguir referências, comparar versões e reunir evidências.

A análise roda localmente. O REA retorna observações, código, referências, limitações e incertezas, e o agente usa esse material para explicar o comportamento ou reconstruir uma implementação. O projeto se posiciona para pesquisa lícita, educação, interoperabilidade, preservação de software e análise de software que o usuário possui ou está autorizado a examinar.

## Como funciona

1. `npx rea-agents setup` registra o servidor MCP nos clientes escolhidos e instala a skill de investigação correspondente. O setup mostra o plano, faz backup das configurações e pede aprovação antes de escrever.
2. O agente escolhe a ferramenta a partir do tipo de alvo (binário nativo, ASAR/JavaScript, APK, assembly .NET, captura de rede etc.).
3. O REA seleciona um provider local, executa a análise e normaliza o resultado em um registro de [evidência](../../../concepts/evidencia-e-proveniencia.md).
4. O agente recebe o resultado normalizado, a cobertura observada, as limitações e os pontos desconhecidos; pode pedir mais detalhes, paginar a evidência retida ou comparar dois resultados.
5. A CLI expõe os mesmos workflows para uso direto em scripts e terminal.

O modo de investigação é iterativo: o agente alterna entre análise estática e observação de runtime, e usa a evidência para decidir o próximo passo. A skill do repositório orienta explicitamente a não usar o REA para análise de arquitetura de um repositório-fonte comum — ele é para artefatos entregues, binários e comportamento observado.

## Arquitetura e componentes

A arquitetura segue dependências para dentro: domínio e contratos → providers → workflows de aplicação → adaptadores CLI/MCP.

- **Entry points:** `scripts/rea.mjs` (dispatcher), `src/cli.ts` (CLI one-shot) e `src/main.ts` (servidor MCP via stdio).
- **Composição:** `src/composition/` cria factories tipadas de providers e sessões, com carregamento opcional e seleção determinística.
- **Aplicação:** `src/application/` contém os workflows compartilhados, o roteamento de providers (`SessionProviderRouter`), o `AnalysisProviderRegistry` e a reconstrução de artefatos JavaScript. Sessões de binário são imutáveis por alvo.
- **Evidência:** `src/application/investigation/` concentra `InvestigationRecords`, o `EvidenceLedger` e a propriedade explícita de desconhecidos; snapshots e cache ficam em componentes próprios.
- **Providers:** `src/hopper`, `src/ghidra`, `src/ida`, `src/kuna`, `src/android`, `src/dotnet`, `src/javascript`, `src/browser`, `src/inspector`, `src/frida`, `src/native`, `src/wasm`, `src/evm`, `src/firmware`, `src/pcap`, `src/signals`, `src/sqlite`, `src/objdump`, `src/rizin`, `src/gdb` e `src/cutter`.
- **Bridges:** `bridge/hopper_bridge.py` roda dentro do Hopper; `bridge/ghidra/ReaGhidraBridge.java` implementa o script headless do Ghidra.
- **Fundação de processos:** `src/process/` supervisiona grupos de processos, deadlines e limpeza; `src/windows/` e `native/windows/src/` tratam o boundary do Windows (Node-API, jobs e DACLs).
- **Contratos e domínio:** `src/contracts/` define os schemas visíveis ao chamador; `src/domain/` é puro e sem efeitos colaterais; `src/config/` valida ambiente com Zod.
- **Superfícies:** CLI e MCP compartilham a camada de aplicação. A documentação fica em `docs/` (VitePress) e o site em `website/`.
- **Submódulos:** `third_party/jadx-headless-mcp`, `binwalk`, `unblob`, `ghidra-nativeaot` e `wakaru`.
- **Build e testes:** TypeScript, npm, Turbo, Vitest, oxlint/oxfmt, Stryker (mutation testing) e lanes de verificação com ferramentas reais.

## Alvos suportados

| Alvo | O que o REA retorna | Dependência |
| --- | --- | --- |
| Binários nativos | Pseudocódigo, assembly, strings, símbolos, chamadas e referências | Hopper, Ghidra, IDA ou Kuna (bring-your-own) |
| Go e Rust | Metadados embutidos de build, módulos e dependências | Inspeção estática embutida |
| JavaScript/Electron | Módulos, imports, source maps, rotas, IPC e add-ons nativos | Node.js; CDP/Playwright/Inspector para runtime |
| .NET | Metadados, instruções CIL e comparação de builds | Inspeção estática embutida |
| Android | Manifesto, classes, métodos, recursos, dispositivos e logs | JADX, adb e Apktool (bring-your-own) |
| Firmware | Regiões, extração e handoff para análise nativa | Binwalk/Unblob |
| Websites e capturas | Estrutura, scripts, requisições, HAR/SAZ e pcap | Navegador Chrome-family, tshark |
| WASM, EVM, SQLite, sinais e crashes | Inspeção validada e evidência com cobertura explícita | WABT, EVMole, Node/SQLite, sigrok, pwntools |
| Comportamento de processo | Saída de terminal, interações, exit e observações de filesystem | PTY nativo em Linux/macOS |

As dependências são, em grande parte, fornecidas pelo usuário. O setup não instala nem atualiza Node.js, npm, Homebrew, Java, Ghidra, IDA, JADX, Kuna, Binwalk ou Unblob; a exceção é o Hopper, que pode ser instalado com aprovação explícita.

## Principais conceitos

- [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — protocolo usado para expor as ferramentas ao agente.
- [Engenharia reversa agêntica](../../../concepts/engenharia-reversa-agentica.md) — o modelo de investigação iterativa com ferramentas e evidência.
- [Evidência e proveniência](../../../concepts/evidencia-e-proveniencia.md) — como o REA mantém cobertura, limitações e incertezas.

## Uso rápido

Requisitos: Node.js 22.19+, 24.11+ ou 26+, e npm. Alguns workflows no Linux exigem um `ps` compatível com procps.

```bash
# Registrar o MCP nos agentes e instalar a skill de workflow
npx rea-agents setup

# Analisar uma aplicação JavaScript/Electron extraída, sem engine nativa
npx -y rea-agents@latest analyze-javascript-application /caminho/para/app --json

# Instalar a CLI globalmente e usar um provider nativo
npm install --global rea-agents
rea analyze /caminho/para/binario --provider ghidra --json
rea decompile /caminho/para/binario 0x1000 --provider ghidra --json
rea xrefs /caminho/para/binario 0x1000 --provider ghidra --json
```

Clientes suportados incluem Claude Code, Codex, Cursor, Gemini CLI, Windsurf, OpenCode, Copilot CLI, VS Code e Grok Build, entre outros; a lista completa e a configuração manual estão em `docs/installation.md`.

## Quando usar (e quando não usar)

- **Use quando:** a resposta depende de um artefato entregue (binário, app empacotado, APK, assembly, firmware), de decompilação, de comportamento em runtime ou de comparação entre versões; você quer explicar uma feature, reconstruir uma implementação ou reunir evidências de interoperabilidade.
- **Use quando:** você precisa cruzar análise estática com observação de runtime e manter a proveniência do que foi observado.
- **Evite quando:** o alvo é um repositório-fonte completo e a análise normal de código já responde — a própria skill do REA recomenda não usá-lo nesse caso.
- **Evite quando:** você não tem autorização para examinar o software, ou não pode configurar o provider necessário. Ferramentas comerciais (IDA, Hopper, JEB) exigem licença própria; o projeto não fornece licenças.
- **Atenção:** captura de runtime usa as permissões do seu usuário; instrumentação com Frida executa código estrangeiro e não é read-only.

## Estado do projeto

- **Licença:** MIT para o código do REA; materiais de terceiros mantêm suas licenças.
- **Versão observada:** `rea-agents` 6.5.0, publicada em 2026-10-14.
- **Atividade:** último push em 2026-10-17; releases 6.1.0 a 6.5.0 entre 2026-10-09 e 2026-10-14, indicando cadência muito rápida.
- **Popularidade (observada em 2026-10-17):** ~305 mil estrelas, ~77 mil forks e ~1,2 mil issues abertas. Números voláteis; a API do GitHub é a fonte.
- **Criação do repositório:** 2026-04-14.
- **Distribuição:** npm (`rea-agents`), site oficial `rea.tools` e repositório `morluto/rea`. O README alerta que nomes parecidos ou READMEs copiados não estabelecem uma distribuição oficial.
- **Verificação:** o projeto mantém lanes de teste com ferramentas reais (Hopper, Ghidra, IDA, Kuna, JADX, binwalk, unblob, entre outras) e documenta explicitamente o que foi ou não verificado por plataforma.

## Relações

- **Mantido por:** [morluto](../../../entities/morluto.md).
- **Depende de:** Node.js, SDKs MCP, providers locais de análise e submódulos de terceiros.
- **Integra com:** agentes de código via MCP e com scripts/terminal via CLI.
- **Inspirado por:** não mapeado nesta ingestão.
- **Alternativas:** não comparadas nesta ingestão; candidatos naturais são fluxos manuais com Ghidra/IDA e outros servidores MCP de engenharia reversa.
- **Usado por:** não mapeado; o número de estrelas não estabelece uso.

## Perguntas abertas

- Como o `AnalysisProviderRegistry` decide entre providers e como o usuário seleciona um provider específico?
- Como o `EvidenceLedger` preserva identidade, cobertura e desconhecidos quando vários providers contribuem para a mesma sessão?
- Qual é o custo real de tokens/contexto de uma investigação, somando catálogo de tools, argumentos, retries e evidências?
- Quais lanes de verificação com ferramentas reais cobrem cada provider e cada plataforma? O que permanece não verificado?
- Como o projeto lida com a pressão de ~1.217 issues abertas mantendo releases quase diários?
- Como o REA se compara, na prática, a alternativas como Ghidra/IDA + bridges MCP e outras ferramentas de RE agêntica?

## Fontes

- Repositório: https://github.com/morluto/rea (commit `09de00b4108a5d738ebe56903e0110ef63820aca`, consultado em 2026-10-17).
- Arquivos lidos: `README.md`, `AGENTS.md`, `package.json`, `CHANGELOG.md`, `docs/architecture.mermaid`, `docs/cli.md`, `docs/mcp-contracts.md`, `docs/installation.md`, `docs/tool-design.md`, `docs/roadmap.md`, `docs/testing.md`, `.agents/skills/reverse-engineer-anything/SKILL.md`, `.agents/skills/rea-analysis-optimization/references/kuna-case-study.md` e `.gitmodules`.
- Metadados do GitHub API: repositório e usuário `morluto`, consultados em 2026-10-17.
