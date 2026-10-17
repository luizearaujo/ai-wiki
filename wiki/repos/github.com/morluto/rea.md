---
type: repo
url: https://github.com/morluto/rea
host: github.com
owner: morluto
repo: rea
commit: 9e372c6bc914b15e2f778f969da4fd3e11483d78
license: MIT
language: TypeScript
status: active
created: 2026-10-17
ingested: 2026-10-17
updated: 2026-10-17
tags: [agentes, engenharia-reversa, mcp, analise-binaria, cli, local-first]
---

# morluto/rea

> Servidor MCP e CLI local que dá a agentes de IA ferramentas para inspecionar binários nativos, apps JavaScript/Electron, assemblies .NET, websites e comportamento em execução, devolvendo as evidências e limitações de cada conclusão.

## O que é

REA (Reverse Engineer Anything) conecta um agente a ferramentas de inspeção de software entregue: binários nativos, aplicações JavaScript/Electron, assemblies .NET e websites. O README descreve o caso de uso central: você vê uma feature em um app que quer no seu produto, pede ao agente para investigá-la, e o REA permite inspecionar o app sem código-fonte, explicar como a feature funciona, mostrar a evidência e construir uma versão para o seu projeto.

A análise roda localmente e os resultados incluem a evidência e as limitações por trás de cada conclusão. As mesmas ferramentas podem ser usadas pelo terminal, não só pelo agente. O README reforça que a distribuição oficial vem de `morluto/rea`, `rea.tools` ou do pacote npm `rea-agents`; nomes parecidos ou READMEs copiados não estabelecem uma distribuição oficial.

## Como funciona

1. `npx rea-agents setup` registra o servidor MCP no agente escolhido e instala instruções de workflow correspondentes, com backup da configuração existente e aprovação antes de escrever.
2. O agente chama o REA via MCP para inspecionar o alvo e rastrear o código relevante.
3. O REA devolve achados com evidência; o agente usa esse material para fazer perguntas de acompanhamento, explicar o comportamento ou escrever e testar uma implementação.
4. A CLI executa os mesmos workflows para uso direto no terminal.

A inspeção estática de JavaScript e .NET lê os arquivos fornecidos sem executar a aplicação. Captura de runtime executa ou interage com o alvo usando as permissões do usuário, e cada guia de runtime descreve os efeitos. O README também afirma que a análise é local: o agente recebe os resultados das ferramentas, e o provedor do modelo tem sua própria política de dados.

## O que você pode analisar

Resumo da tabela do README:

| Alvo | O que o REA retorna | Requisito principal |
| --- | --- | --- |
| Binários nativos | Pseudocódigo, assembly, strings, símbolos, chamadas e referências | Hopper, Ghidra ou IDA |
| Binários Go e Rust | Metadados embutidos de build, módulos e dependências | Inspeção estática embutida |
| JavaScript/Electron | Módulos, imports, source maps, rotas, IPC e add-ons nativos | Node.js/npm; `ps` compatível com procps no Linux |
| .NET | Metadados, instruções CIL, dependências nativas e comparação de builds | Nenhum (somente estático) |
| Android | APK, dispositivos, recursos e apps Flutter | JADX + JDK (APK); adb (dispositivos); Apktool (recursos); Flutter exige apenas leitura estática |
| Websites e capturas | Estrutura, scripts, requisições, HAR/SAZ e screenshots | Navegador Chrome-family; tshark para pacotes |
| Firmware | Regiões, extração e handoff para análise nativa | Binwalk/Unblob no Linux |
| Outros artefatos | WASM, EVM, SQLite, crashes, sinais e pacotes | Ferramentas específicas, em grande parte fornecidas pelo usuário |
| Comportamento de processo | Saída de terminal, interações, exit, observações de filesystem e comparação de execuções | PTY nativo em Linux/macOS |

O setup pode instalar o Hopper com aprovação; Ghidra e IDA usam instalações existentes. Requisito base: Node.js 22.x (>=22.19), 24.x (>=24.11) ou 26+, e npm.

## Instalação e uso rápido

```bash
# Registrar o MCP no agente e instalar as instruções de workflow
npx rea-agents setup

# Inspecionar um app JavaScript/Electron extraído ou ASAR
npx -y rea-agents@latest analyze-javascript-application /caminho/absoluto/para/app --json

# Instalar a CLI globalmente
npm install --global rea-agents
rea --help

# Atualizar
rea update
```

No setup, escolha os agentes, revise as mudanças propostas e aprove; reinicie o agente depois. O README lista Claude Code, Codex, Cursor, Gemini CLI, Grok Build e outros. Para atualizar um setup feito via `npx`, rode `npx rea-agents@latest setup` e reinicie o agente.

## Exemplos de uso

Exemplos derivados do README — não são instruções oficiais além do que ele publica.

- **Pedir uma feature ao agente:** "Entenda como a busca funciona no app Notes, mostre a evidência e construa uma feature parecida para o meu projeto."
- **Reconstruir um cálculo:** o showcase DX-Ball segue uma chamada de som até o helper de posição→pan, inspeciona as instruções e transforma pseudocódigo incompleto em C; a reconstrução passa 3.205 casos x86 originais e reproduz os 63 bytes da função compilada.
- **Rastrear uma ponte Electron:** o showcase do Notion encontra a API de clipboard do renderer, segue por preload e IPC até o processo principal e inspeciona o formato de clipboard rico.
- **Recuperar código legado:** o showcase TH04 inspeciona instruções de 16 bits de um jogo PC-98 e compara o C++ reconstruído com a saída do compilador histórico.

## Quando usar (e quando não usar)

- **Use quando:** a resposta depende de um artefato entregue — binário, app empacotado, APK, assembly, firmware, website ou comportamento em execução — e você quer explicar uma feature, reconstruir uma implementação ou reunir evidências.
- **Use quando:** você quer cruzar análise estática com observação de runtime mantendo a proveniência do que foi observado.
- **Evite quando:** o alvo é um repositório-fonte e a leitura normal do código já responde; o foco do README é inspecionar artefatos entregues e comportamento.
- **Evite quando:** você não tem autorização para examinar o software ou não pode obter as licenças das ferramentas comerciais. O README declara que o REA é para pesquisa lícita, educação, interoperabilidade, preservação e análise de software que você possui ou está autorizado a examinar; IDA, Hopper e JEB exigem licença própria.

## Limitações e cuidados

- **Somente o README foi lido nesta ingestão.** Contratos de ferramentas, configuração de providers, comandos nativos, snapshots e detalhes de cada workflow estão na documentação oficial e não foram verificados aqui.
- **Runtime não é read-only.** Captura de runtime executa ou interage com o alvo com as permissões do usuário; os efeitos dependem do guia de cada modo.
- **Ferramentas comerciais.** O REA não fornece licenças, chaves ou ativação; o usuário precisa obter e estar autorizado a usar IDA, Hopper e JEB.
- **Análise local, política do provedor.** O README afirma que a análise é local, mas o provedor do modelo do agente tem política de dados própria.
- **Projeto em mudança rápida.** O README recomenda manter a instalação atualizada e atualizar antes de reportar bugs.
- **Distribuição.** Só as fontes oficiais citadas devem ser tratadas como distribuição legítima.

## Estado e adoção

- **Versão:** o README não fixa uma versão; a última release observada via API do GitHub em 2026-10-17 era `rea-agents-6.5.0` (2026-10-14).
- **Popularidade (observada em 2026-10-17):** ~305 mil estrelas, ~77 mil forks e ~1,2 mil issues abertas. O README celebra a marca de 300 mil estrelas. Números voláteis.
- **Atividade:** último push em 2026-10-17; repositório criado em 2026-04-14.
- **Licença:** MIT para o código do REA; materiais de terceiros mantêm suas licenças.

## Relações

- **Mantido por:** [morluto](../../../entities/morluto.md).
- **Conceitos:** [Model Context Protocol](../../../concepts/model-context-protocol.md) — protocolo usado para expor as ferramentas; [Engenharia reversa agêntica](../../../concepts/engenharia-reversa-agentica.md) — modelo de investigação iterativa; [Evidência e proveniência](../../../concepts/evidencia-e-proveniencia.md) — achados com evidência e limitações.
- **Skills:** o README menciona uma skill de investigação distribuída via skills.sh e instalada pelo setup; o formato é descrito em [Agent skills](../../../concepts/agent-skills.md).
- **Alternativas:** não comparadas nesta ingestão; candidatos naturais são fluxos manuais com Ghidra/IDA e outros servidores MCP de engenharia reversa.

## Perguntas abertas

- Quais são os contratos exatos das ferramentas MCP e o formato dos resultados? (não lidos nesta ingestão)
- Como funciona a seleção de provider e o que cada um suporta por plataforma?
- Qual é o custo real de tokens/contexto de uma investigação?
- Quais lanes de teste com ferramentas reais cobrem cada provider? O README cita `docs/testing.md`, não consultado.
- Como o REA se compara, na prática, a Ghidra/IDA + agentes?

## Fontes

- README: https://raw.githubusercontent.com/morluto/rea/9e372c6bc914b15e2f778f969da4fd3e11483d78/README.md (commit `9e372c6bc914b15e2f778f969da4fd3e11483d78`, consultado em 2026-10-17). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do GitHub API: repositório `morluto/rea` e última release, consultados em 2026-10-17.
