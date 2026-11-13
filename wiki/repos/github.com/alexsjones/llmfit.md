---
type: repo
url: https://github.com/AlexsJones/llmfit
host: github.com
owner: AlexsJones
repo: llmfit
commit: 700cfc818c63e98f61200b8b00401f4c76d265bc
license: MIT
language: Rust
status: active
created: 2026-11-13
ingested: 2026-11-13
updated: 2026-11-13
tags: [inferencia-local, hardware, gguf, mlx, cli, benchmark, rust]
---

> CLI/TUI em Rust que inspeciona CPU, RAM, GPU e VRAM e recomenda, por scoring multidimensional, quais modelos open-source rodam bem no hardware detectado.

## Propósito

llmfit responde à pergunta "quais modelos cabem na minha máquina?" sem exigir que o usuário converta especificações de hardware em tamanhos de quantização manualmente. A ferramenta detecta o hardware, pontua cada modelo em quatro dimensões (adequação de memória, velocidade estimada, qualidade e contexto) e retorna uma lista ordenada de recomendações com as quantizações compatíveis.

## Instalação

```bash
# macOS/Linux
brew install llmfit

# Windows (WinGet)
winget install AlexsJones.llmfit

# Script
curl -fsSL https://github.com/AlexsJones/llmfit/releases/latest/download/install.sh | sh

# Python
uv tool install llmfit  # ou: pip install llmfit
```

Também disponível via Scoop, MacPorts, binários no GitHub Releases e Docker (`ghcr.io/alexsjones/llmfit`).

## Comandos

| Comando | Propósito |
|---------|-----------|
| `llmfit` | Interface TUI interativa |
| `llmfit recommend` | Saída JSON de recomendações |
| `llmfit fit` | Tabela de modelos por adequação |
| `llmfit bench` | Medir tokens/segundo reais no hardware |
| `llmfit serve` | API web + dashboard na porta local |

## Detecção de hardware

Detecta automaticamente: núcleos de CPU, RAM total, GPUs discretas e integradas, VRAM e tipo de acelerador. Arquiteturas suportadas: NVIDIA CUDA, Apple Silicon (Metal), AMD ROCm, Intel OneAPI.

## Formatos e provedores

**Quantizações suportadas:** GGUF, AWQ, GPTQ, EXL2.

**Provedores suportados:** Ollama, llama.cpp, MLX, Docker Model Runner, LM Studio.

## Como calcula a recomendação

Estimativas de velocidade combinam um modelo de largura de banda de memória baseado em amostragem de tempo de execução com benchmarks comunitários reais (`llmfit bench`). O resultado é um score composto por: adequação de memória, velocidade estimada, qualidade do modelo e comprimento de contexto suportado.

## Outros modos

- **API REST:** endpoints `/api/v1/system` (specs detectadas) e `/api/v1/models` (lista com scores) para integração com scripts.
- **Cluster:** modo Ray para múltiplos nós em preview; suporte a múltiplas GPUs e modelos MoE.
- **Benchmarks comunitários:** medições reais enviadas pela comunidade complementam as estimativas do modelo de largura de banda.

## Limitações

- Modo cluster em preview — pode ter instabilidades.
- Recomendações são estimativas; `llmfit bench` verifica o throughput real.
- Suporte a modelos MoE declarado, sem detalhe de como lida com roteamento.

## Fontes

- README.md do repositório (`700cfc818c63e98f61200b8b00401f4c76d265bc`), lido em 2026-11-13.
- Metadados via API do GitHub (linguagem, licença, tópicos), consultados em 2026-11-13.
- Apenas o `README.md` foi lido.
