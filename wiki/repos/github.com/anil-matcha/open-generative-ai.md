---
type: repo
url: https://github.com/Anil-matcha/Open-Generative-AI
host: github.com
owner: Anil-matcha
repo: Open-Generative-AI
commit: 2579652f1507f392520425f8ec484b739582f0b1
license: MIT
language: JavaScript
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [geracao-de-midia, modelos-locais, self-hosted]
---

# Anil-matcha/Open-Generative-AI

> Estúdio self-hosted de geração de imagem e vídeo por IA sobre 600+ modelos (Flux, Midjourney, Kling, Sora, Veo e outros) via a API da MuAPI, sem filtro de conteúdo, com app desktop Electron que também roda dois motores de inferência local (sd.cpp e Wan2GP).

## O que é

Posiciona-se como alternativa aberta a plataformas de vídeo por IA fechadas, com o diferencial explícito de não ter filtro de conteúdo nem bloqueio de prompt. É tanto uma versão hospedada (gratuita, sign-up) quanto um app desktop para macOS, Windows e Linux. O README dedica bastante espaço a um programa de white-label da MuAPI (a partir de US$ 49/mês) para quem quer revender o estúdio com marca própria — a receita de assinatura dos usuários finais fica com quem revende.

## Como funciona

- **Estúdios por modalidade**: Image (texto-para-imagem e imagem-para-imagem, trocando automaticamente o conjunto de modelos conforme há imagem de referência), Video (texto-para-vídeo e imagem-para-vídeo), Audio, AI Clipping, Vibe Motion, Lip Sync (9 modelos, retrato+áudio ou vídeo+áudio), Body Swap, Cinema (controles de lente/distância focal/abertura), Marketing, Workflow (pipelines visuais encadeando modelos), Agent Studio (agente criativo conversacional que planeja e executa gerações) e Design Agent Studio (agente de design em canvas).
- **Entrada multi-imagem**: até 14 imagens de referência em modelos compatíveis (Nano Banana 2 Edit), com seletor de múltipla seleção, upload em lote e numeração de ordem de envio.
- **Inferência local, só no app desktop**: dois motores independentes — **sd.cpp** (C++, bundled, roda em Mac/Windows/Linux via Metal/CUDA/Vulkan/ROCm, modelos SD 1.5/SDXL/Z-Image, sem chave de API) e **Wan2GP** (instalação própria do usuário, pasta local ou servidor MCP remoto, para Flux, Qwen-Image e modelos de vídeo em GPU CUDA/ROCm — a versão web hospedada sempre usa APIs na nuvem).
- Chaves de API ficam no `localStorage` do navegador, nunca em servidor próprio além da MuAPI, segundo o README.

## Instalação e uso rápido

- **Hospedado**: criar conta gratuita em muapi.ai/open-generative-ai.
- **Desktop**: instaladores de um clique para macOS (Apple Silicon/Intel), Windows e Linux (AppImage/.deb) em `github.com/Anil-matcha/Open-Generative-AI/releases`. macOS e Windows exigem destravar o Gatekeeper/SmartScreen manualmente por não serem assinados; Linux em Ubuntu 24.04+ pode precisar desativar uma restrição de AppArmor para o sandbox do Chromium (ou preferir o `.deb`, que já inclui o perfil necessário).
- **Build Linux local**: `npm run electron:build:linux`.

## Quando usar (e quando não usar)

- **Use quando:** quer uma interface única sobre centenas de modelos de geração de imagem/vídeo de vários provedores, com opção de rodar alguns modelos localmente no desktop.
- **Evite quando:** precisa de garantias de moderação de conteúdo ou de um produto com filtros — o próprio README anuncia "sem filtros, sem guardrails" como recurso, o que é uma responsabilidade adicional de uso para quem opera ou revende o estúdio.

## Limitações e cuidados

- README é fortemente promocional (upsell de white-label, tabela de preços de concorrentes) — o conteúdo técnico verificável está nas seções de inferência local e lista de features, não nas seções de marketing.
- A inferência local do app desktop depende de hardware específico: Z-Image em Mac com 8 GB de RAM é descrito como capaz de travar o sistema; Wan2GP exige GPU CUDA/ROCm, sem caminho MPS/Apple Silicon.
- Autenticidade do "sem filtros, sem guardrails" não foi verificada nesta ingestão — é a descrição do próprio projeto, a ser confirmada por quem for operá-lo.

## Estado e adoção

- 31.126 estrelas, 5.750 forks, 43 issues abertas — observado em 2026-10-21.
- Repositório criado em 2023-05-09 — mais antigo que a maioria dos outros repositórios desta ingestão, possivelmente reaproveitado/renomeado; push mais recente em 2026-10-21 — observado em 2026-10-21.
- Última release listada no README: `v2.0.0` (instaladores desktop).
- Licença: MIT.

## Relações

- Mantido por: [Anil Chandra Naidu Matcha (Anil-matcha)](../../../entities/anil-matcha.md)
- Projetos relacionados do mesmo autor, citados no README (nenhum documentado nesta wiki): `awesome-generative-ai-apps`, `awesome-vibecoded-saas`, `awesome-ai-video-models`, `awesome-ai-image-models`, `Open-AI-Design-Agent`.

## Perguntas abertas

- O "Agent Studio" (agente criativo conversacional) usa qual modelo/framework de orquestração por baixo? Não detalhado no README.

## Fontes

- README: https://raw.githubusercontent.com/Anil-matcha/Open-Generative-AI/2579652f1507f392520425f8ec484b739582f0b1/README.md (commit `2579652f1507f392520425f8ec484b739582f0b1`, consultado em 2026-10-21). Somente o README foi lido; o restante do repositório não foi consultado.
- Metadados: API do GitHub (`api.github.com/repos/Anil-matcha/Open-Generative-AI`), consultada em 2026-10-21.
