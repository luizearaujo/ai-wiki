---
type: repo
url: https://github.com/debpalash/VoiceStudio
host: github.com
owner: debpalash
repo: VoiceStudio
commit: 37996099869fdc18b8b1138ccbf6f2997de1fe73
license: AGPL-3.0
language: Python
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [clonagem-de-voz, tts, mcp, agent-skills]
---

# debpalash/VoiceStudio

> Alternativa open source e totalmente local ao ElevenLabs: clonagem e design de voz, dublagem de vídeo, dictation, transcrição e criação de audiobook em 646 idiomas.

## O que é

VoiceStudio resolve o problema de depender de um serviço de voz pago e fechado (ElevenLabs) ao empacotar clonagem de voz, design de voz (gerar uma voz nova a partir de descrição), dublagem de vídeo com fala sincronizada no tempo, dictation com widget flutuante e criação de audiobook/histórias em lote — tudo executável localmente, com serviços remotos opcionais. É um app Electron com motor padrão próprio (k2-fsa/OmniVoice), mas permite escolher outros motores de voz.

## Como funciona

Três frentes descritas no README: **Create** (clonar uma voz ou desenhar uma nova, dictation com widget flutuante), **Produce** (dublagem de vídeo com timing, histórias/audiobooks e jobs em lote) e **Connect** (API local e MCP para agentes, receitas reutilizáveis e watch folders). O app roda sobre hardware próprio: aceleração CUDA (NVIDIA), Metal/MPS (Apple Silicon) ou CPU puro (mais lento, ~5GB de disco para o build CPU do PyTorch); Windows on ARM é experimental e Mac Intel só roda a UI conectada a um backend remoto.

## Instalação e uso rápido

- **Instalador de uma linha** (macOS/Linux): `curl -fsSL https://voicestudio.sh/install | sh`; variantes para versão específica (`--version X.Y.Z`), build do `main` (`--main`) ou desinstalar preservando dados (`--uninstall`).
- **Windows**: `irm https://voicestudio.sh/install | iex` no PowerShell.
- **A partir do código-fonte**: `git clone` + `bun install` + `bun run setup:api` + `bun run dev`.
- **Instalação via agente**: colar um prompt que referencia `docs/install/agent.md`, ou `npx skills add debpalash/VoiceStudio` para agentes que suportam skills (duas skills: `voicestudio` para workflows de áudio, `voicestudio-maintainer` para manutenção do repositório).
- Nota importante: desde a versão 0.5.3 (última release Tauri), o Electron é o único app desktop e web UI suportado; usuários do shell Tauri antigo precisam migrar.

## Exemplos de uso

- Clonar uma voz a partir de uma gravação de referência limpa e gerar fala a partir de texto na workspace de clonagem — exemplo derivado do README.
- Dublar um vídeo com fala sincronizada no tempo, usando a workspace de dublagem — exemplo do README.
- Conectar um agente via MCP para disparar gerações de voz programaticamente — citado no README (`docs/mcp.md`).

## Quando usar (e quando não usar)

- **Use quando:** quer clonagem/design de voz, dublagem ou transcrição totalmente local, com API/MCP para integrar a agentes, sem depender de um serviço de voz pago.
- **Evite quando:** precisa apenas de transcrição/dictation simples sem as demais capacidades de voz — [cjpais/Handy](../cjpais/handy.md) é uma alternativa mais enxuta e focada só em speech-to-text.

## Limitações e cuidados

- Licença AGPL-3.0 cobre a aplicação, mas pesos de modelo, tokenizers, vozes e condições de saída gerada são tratados separadamente — uma licença paga do app não concede automaticamente direitos sobre esses artefatos, segundo o próprio README.
- O README recomenda clonar vozes apenas com permissão, e aponta um "Model Manager" com avisos de licença versionados por modelo, mas descreve a revisão de arquivos como não obrigatória nem uma certificação de uso comercial.
- Suporte a Windows on ARM é experimental; Mac Intel não executa o backend local.
- Apenas o README foi lido; `docs/`, código Electron/Python, scripts de instalação e o catálogo completo de motores (`docs/feature-catalog.md`) não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: última release no GitHub, `v0.5.6` (2026-09-23).
- Atividade e popularidade observadas em 2026-10-23: 81.121 estrelas, 8.950 forks (GitHub API); push em 2026-10-22, criado em 2026-04-09 — crescimento rápido em poucos meses.
- Licença: AGPL-3.0 para a aplicação; pesos/vozes/modelos sob licenciamento separado e não uniforme.

## Relações

- Mantido por: [Palash Debnath (debpalash)](../../../entities/debpalash.md).
- Conceitos: [Clonagem de voz](../../../concepts/clonagem-de-voz.md), [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Agent skills](../../../concepts/agent-skills.md).
- Alternativas: [myshell-ai/OpenVoice](../myshell-ai/openvoice.md) — modelo de clonagem isolado, sem app nem as camadas de dublagem/dictation/MCP do VoiceStudio; [cjpais/Handy](../cjpais/handy.md) — cobre só a parte de transcrição/dictation.

## Perguntas abertas

- Como o motor padrão (k2-fsa/OmniVoice) se compara, em qualidade e velocidade, às demais opções do catálogo de engines?
- O que exatamente o "reviewed-file preview" do Model Manager verifica, e por que o README é explícito que ele não certifica permissão de uso comercial?

## Fontes

- README: https://raw.githubusercontent.com/debpalash/VoiceStudio/37996099869fdc18b8b1138ccbf6f2997de1fe73/README.md (commit `37996099869fdc18b8b1138ccbf6f2997de1fe73`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
