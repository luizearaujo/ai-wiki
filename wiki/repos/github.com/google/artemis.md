---
type: repo
url: https://github.com/google/artemis
host: github.com
owner: google
repo: artemis
commit: 351ca8422f7b5b54e80a9c1ce03a222e02415b6b
license: Apache-2.0
language: Python
status: active
created: 2026-10-24
ingested: 2026-10-24
updated: 2026-10-24
tags: [navegacao-web-agentica, mcp, agent-harness]
---

# google/artemis

> Agente que transforma instruções em linguagem natural em automação Android confiável em dispositivos reais ou emuladores, com 99%+ de conclusão de tarefas no benchmark AndroidWorld, segundo o projeto.

## O que é

ARTEMIS resolve o problema de automatizar testes e tarefas do dia a dia em Android a partir de instruções em português/inglês simples, em vez de scripts de UI frágeis. É criado pelo time **Pixel Test Engineering (PTE) Fusion** do Google. Executa workflows cross-app, localiza elementos por índice de acessibilidade com fallback visual/coordenadas para interfaces customizadas (Canvas, Compose, Flutter), e se integra como servidor MCP nativo a IDEs de IA (Antigravity, Claude Code, Codex, Windsurf, Cursor).

## Como funciona

Dois perfis de execução:

- **Flash (`--profile flash`):** loop reativo observar-e-agir, ~3–5s por passo, sem orquestração em grafo; histórico comprimido em resumos visuais e blocos pesquisáveis em vez de cortado por limite; sem plano de tarefa, rede de segurança pré-execução, checkpoint ou relatório final.
- **Pro (`--profile pro`):** workflow multiagente de planejamento e verificação (~15–40s por passo) — um **Planner** mantém um plano Markdown com marcos e itens de verificação/assert; o **Operator** executa com o toolset completo (grounding do Explorer em modo flash/pro/ultra configurado pelo usuário, nunca escolhido pelo agente); toda ação passa por uma **Safety Net** pré-execução (XML primeiro, fallback de pixel); um **Checker** somente leitura verifica checkpoints e faz revisão final contra o objetivo original.

A primeira tarefa em um dispositivo instala o **Artemis Accessibility Helper**, um serviço de acessibilidade que lê o layout de tela sem tomar a conexão UiAutomation; roda só no aparelho e não envia dados para fora, segundo o README. Pode ser pré-instalado, inspecionado ou removido via CLI, e o projeto cai para UIAutomator2 se o helper falhar.

## Instalação e uso rápido

```bash
# macOS/Linux
git clone https://github.com/google/artemis.git && cd artemis
./start.sh

# Windows PowerShell
git clone https://github.com/google/artemis.git
cd artemis
.\start.bat
```

O script de início único detecta e instala toolchains (ADB, scrcpy, FFmpeg, `uv`) e oferece montar configuração MCP global e o arquivo de regras comportamentais (`mcp_server/rules.md`) nas IDEs suportadas. Abre um console web em `http://localhost:8000` com wizard de conexão, espelhamento de tela e replay de execução. Uso direto via CLI: `uv run artemis run "<instrução>" --profile flash`.

Para MCP: `uv run artemis mcp --install all` (ou `--install claude`, `--install antigravity` etc.); configuração manual via `uv run artemis mcp --generate-config <client>`. Há também um SDK Python sem dependências de runtime (`artemis-client`) para integrar em frameworks de teste (pytest) ou CI/CD.

## Exemplos de uso

```python
from artemis_client import ArtemisClient

client = ArtemisClient("http://artemis-host:8000", default_profile="flash")
result = await client.run(
    "Open System Settings, go to 'Battery', verify battery percentage is displayed, "
    "and check for any crash dialogs."
)
```

No chat de uma IDE conectada via MCP: "Build the latest changes into an APK, install it on the connected device, open the login screen with a test account, verify if there are any unexpected popups after login, and return screenshots of the final page."

## Quando usar (e quando não usar)

- **Use quando:** quiser automatizar testes ou tarefas Android a partir de linguagem natural, com reprodução de bugs guiada por um agente de IDE via MCP, ou workflows de teste de longa duração com plano e verificação.
- **Evite quando:** precisar de automação iOS (fora do roadmap atual) ou de controle fino sobre UiAutomation sem a camada de acessibilidade do Helper.

## Limitações e cuidados

- README declara que código em `third_party/mobile_use` deriva do projeto `mobile-use` da Minitap, Inc. (Apache 2.0) — fontes de terceiros fora desta wiki descrevem uma disputa de atribuição não resolvida sobre a origem do projeto; esta ingestão não verificou essa disputa além do que o próprio README credita.
- O benchmark de 99%+ no AndroidWorld é resultado reportado pelo projeto, sem verificação independente nesta ingestão.
- Roadmap declarado inclui integração com Android Studio, expansão para iOS, VLMs leves on-device e interação de voz em duplex — nenhum desses itens está implementado ainda.
- **A verificar:** maturidade relativa do perfil Pro fora dos benchmarks do próprio projeto; comportamento em apps com proteções anti-automação.

## Estado e adoção

- Observado em 2026-10-24: ~14.344 stars, 1.532 forks, 146 issues abertas, push mais recente em 2026-10-01.
- Licença: Apache-2.0.

## Relações

- Mantido por: Google, time Pixel Test Engineering (PTE) Fusion.
- Conceitos: [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md) (mesmo padrão de observação→ação→nova observação, aplicado a UI mobile nativa em vez de browser), [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Agent harness](../../../concepts/agent-harness.md) (perfil Pro com Planner/Operator/Checker).
- Cita como origem parcial: `mobile-use` (Minitap, Inc.), em `third_party/mobile_use`.

## Perguntas abertas

- Qual o status da disputa de atribuição com a Minitap citada por fontes externas, além do crédito já presente em `third_party/`?
- O Helper de acessibilidade é auditável por terceiros, ou a garantia de "não envia dados para fora" depende apenas da declaração do README?
- Há diferença de robustez do perfil Flash versus Pro em apps com proteções anti-automação não documentadas?

## Fontes

- README: https://raw.githubusercontent.com/google/artemis/351ca8422f7b5b54e80a9c1ce03a222e02415b6b/README.md (commit `351ca8422f7b5b54e80a9c1ce03a222e02415b6b`, consultado em 2026-10-24). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados da API do GitHub, consultados em 2026-10-24.
