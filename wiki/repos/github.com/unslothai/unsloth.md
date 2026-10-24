---
type: repo
url: https://github.com/unslothai/unsloth
host: github.com
owner: unslothai
repo: unsloth
commit: 0edb8f511efd32654487af5c2f57a921c7dd63ef
license: Apache-2.0
language: Python
status: active
created: 2026-10-24
ingested: 2026-10-24
updated: 2026-10-24
tags: [llms-compactos-on-device, agent-skills, mcp]
---

# unslothai/unsloth

> Unsloth se descreve como "o primeiro app desktop para rodar e treinar modelos", cobrindo LLMs, diffusion, embedding e áudio localmente, com fine-tuning anunciado como 2× mais rápido e 70% menos VRAM.

## O que é

Unsloth resolve o problema de treinar e servir modelos localmente sem montar manualmente uma stack de fine-tuning: oferece três superfícies — **Unsloth Desktop** (app nativo), **Unsloth Studio** (UI web, incluída no Desktop ou standalone via Docker/instalador) e **Unsloth Core** (biblioteca Python). Cobre texto, imagem/vídeo (diffusion), embedding e áudio, com suporte declarado a Windows, Linux, WSL, macOS, múltiplas GPUs (NVIDIA, AMD, Intel) e backend Vulkan.

## Como funciona

O app roda e treina modelos (Qwen3.8, GLM-5.3-Flash, Kimi K3, Qwen-Image-2.1, MiniMax-H3, DeepSeek-V4, Gemma 4, entre outros), serve uma API compatível com OpenAI, permite acesso remoto via LAN ou Cloudflare HTTPS, e se conecta a agentes (Claude Code, Codex, MCP) com tool calling e execução de código. **Unsloth Start** liga agentes a modelos locais com um comando (`unsloth start claude`, `unsloth start codex` etc.). Para treino, oferece LoRA, QLoRA, full fine-tuning, pretraining, RL (GRPO, DPO) e FP8, com exportação para GGUF, NVFP4, FP8 e outros formatos; "Data Recipes" constrói datasets a partir de PDFs, CSVs e DOCX.

## Instalação e uso rápido

```bash
# macOS, Linux, WSL
curl -fsSL https://unsloth.ai/install.sh | sh
# Windows (PowerShell)
irm https://unsloth.ai/install.ps1 | iex
```

Também disponível via Docker (`unsloth/unsloth`, com tag `:core` só para notebooks, e `unsloth/unsloth-rocm` para AMD), Homebrew (`brew install --cask unsloth`) e Winget. Lançar a Studio: `unsloth studio` (ou `unsloth studio --secure` para HTTPS via Cloudflare). Unsloth Core (biblioteca) instala via `uv pip install unsloth --torch-backend=auto` em ambiente Python 3.13.

## Exemplos de uso

```bash
unsloth start claude --model unsloth/Qwen3.8-27B-GGUF:UD-Q4_K_XL
```

Notebooks gratuitos no Colab para modelos como Gemma 4 (E2B), Qwen3.5 (4B), gpt-oss (20B) com GRPO, Llama 3.1/3.2 e Orpheus-TTS, cobrindo fine-tuning, GRPO/GSPO e embeddings.

## Quando usar (e quando não usar)

- **Use quando:** quiser treinar ou servir LLMs/diffusion/embedding/áudio localmente com economia declarada de VRAM, ou plugar modelos locais em agentes de código via um único comando.
- **Evite quando:** precisar de orquestração de treino em escala de cluster/cloud — o produto é desenhado para uma máquina (desktop/servidor único), não para MLOps distribuído.

## Limitações e cuidados

- Licenciamento dual: o pacote core Unsloth é Apache 2.0, mas a UI do Unsloth Studio é AGPL-3.0 — a página da API do GitHub resolve o repositório como Apache-2.0, mas isso não cobre o componente Studio.
- Os números de performance ("2× mais rápido", "70% menos VRAM", "sem perda de acurácia") são alegações do próprio projeto; não há benchmark independente no README.
- No Windows, a documentação recomenda instalar `torchao` antes do Unsloth Core porque `--torch-backend=auto` só busca no índice do PyTorch, que não tem build recente para Windows.
- Expor a Studio fora de loopback (`--secure`, `--cloudflare`, `-H` não-loopback) liga ferramentas server-side por padrão; o README avisa para proteger a senha de admin.
- **A verificar:** maturidade relativa do suporte a AMD/Intel/Vulkan frente a NVIDIA/CUDA — o README linka guias próprios para cada um, mas não compara.

## Estado e adoção

- Observado em 2026-10-24: ~78.500 stars, 7.282 forks, 382 issues abertas, push mais recente em 2026-10-24.
- Licença: Apache-2.0 (core) + AGPL-3.0 (UI do Studio).

## Relações

- Mantido por: [unslothai](../../../entities/unslothai.md) (Daniel Han, Michael Han e equipe).
- Conceitos: [LLMs compactos on-device](../../../concepts/llms-compactos-on-device.md) (quantização e runtimes locais relacionados, embora Unsloth também treine/sirva modelos de tamanho completo), [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) (Unsloth Start conecta modelos locais a agentes via MCP).
- Alternativas: runtimes de inferência local como llama.cpp (citado como dependência/agradecimento no README) e ferramentas de fine-tuning hospedadas em nuvem (fora do escopo desta ingestão).

## Perguntas abertas

- As alegações de velocidade/memória têm benchmark reproduzível publicado fora do blog do próprio projeto?
- Qual a paridade de recursos entre Unsloth Desktop, Studio e Core para um mesmo workflow de fine-tuning?
- Como o licenciamento dual (Apache 2.0 + AGPL-3.0 para a UI) afeta quem empacota o Desktop app comercialmente?

## Fontes

- README: https://raw.githubusercontent.com/unslothai/unsloth/0edb8f511efd32654487af5c2f57a921c7dd63ef/README.md (commit `0edb8f511efd32654487af5c2f57a921c7dd63ef`, consultado em 2026-10-24). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados da API do GitHub, consultados em 2026-10-24.
