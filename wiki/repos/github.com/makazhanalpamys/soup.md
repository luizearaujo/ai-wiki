---
type: repo
url: https://github.com/MakazhanAlpamys/Soup
host: github.com
owner: MakazhanAlpamys
repo: Soup
commit: 26ffea17461d0d14a0d3641b93435343b54c29e1
license: Apache-2.0
language: Python
status: active
created: 2026-11-10
ingested: 2026-11-10
updated: 2026-11-10
tags: [fine-tuning, lora, qlora, llm, treinamento, consumer-gpu, layer-streaming, cli]
---

> CLI Python que fine-tuna qualquer modelo do HuggingFace a partir de um único arquivo YAML, com layer streaming para treinar modelos 8B em GPUs laptop de 4 GB de VRAM.

## Propósito

Soup reduz o fine-tuning de LLMs a dois passos: escrever um `soup.yaml` e rodar `soup train`. O projeto elimina o setup manual de scripts de treinamento, configuração de quantização e orquestração de PEFT. A inovação técnica central é o **layer streaming**: as camadas congeladas da base do modelo ficam na RAM e são enviadas para a GPU uma de cada vez, mantendo apenas a camada ativa em VRAM. Isso permite treinar modelos 8B em GPUs laptop com apenas 4 GB.

O layer streaming está publicado como pesquisa acadêmica com DOI próprio (Zenodo 10.5281/zenodo.21918325).

## Instalação

```bash
# CLI + ferramentas de dados
pipx install soup-cli

# Com stack de treinamento
pipx install "soup-cli[train]"

# Completo (UI + treinamento + exportação)
pipx install "soup-cli[all]"
```

Requer Python 3.11–3.13. Python 3.14+ ainda não suportado.

## Fluxo de trabalho típico

```bash
soup init --template chat          # Gera soup.yaml de exemplo
soup train --config soup.yaml      # Executa o treinamento
soup chat --model ./output         # Teste interativo
soup merge --adapter ./output      # Combina LoRA com a base
soup export --model ./output --format gguf  # Exporta para Ollama/GGUF
```

## Exemplo de configuração

```yaml
base: meta-llama/Llama-3.1-8B-Instruct
task: sft
data:
  train: ./data/train.jsonl
  format: alpaca
  val_split: 0.1
training:
  epochs: 3
  lr: 2e-5
  batch_size: auto
  lora:
    r: 64
    alpha: 16
  quantization: 4bit
output: ./output
```

## Técnicas suportadas

**Tipos de tarefa:** SFT, DPO, GRPO, PPO, KTO, ORPO, SimPO; treinamento de modelos de visão e áudio.

**PEFT:** LoRA, DoRA, VeRA, PiSSA, ReLoRA, GaLore.

**Quantização:** QLoRA, NF4, FP8, NVFP4, QAT.

**Backends:** PyTorch (padrão), MLX (Apple Silicon), Unsloth (2–5× aceleração declarada).

**Distribuído:** DeepSpeed, FSDP.

**Formatos de dados:** Alpaca, ShareGPT, ChatML, pares de preferência, visão, áudio.

**Exportação:** GGUF, ONNX, TensorRT.

## Desempenho medido

RTX 3050 Laptop: 208,6 tok/s com pico de 2,40 GB de VRAM usando layer streaming.

| VRAM disponível | Modelos viáveis com QLoRA |
|-----------------|--------------------------|
| 4 GB | 8B (layer streaming BETA) |
| 8 GB | ~7B |
| 16 GB | ~14B |
| 24 GB | ~34B |
| 48 GB | ~70B |

## Modelos suportados

Qualquer modelo HuggingFace que suporte `AutoModelForCausalLM`. Mais de 100 receitas pré-configuradas incluindo Llama 3.x/4, Qwen 2.5/3, Gemma 3, Mistral e DeepSeek.

## Outros comandos relevantes

| Comando | Propósito |
|---------|-----------|
| `soup serve` | Servidor de API compatível com OpenAI |
| `soup eval` | Benchmarking e avaliação |
| `soup doctor` | Diagnóstico de ambiente |
| `soup profile` | Estima requisitos de memória sem YAML |
| `soup data inspect` | Análise de dataset |
| `soup recipes list` | Receitas pré-configuradas |
| `soup ui` | Dashboard web para gerenciar experimentos |

## Limitações

- Layer streaming em BETA — pode ter instabilidades.
- CPU training experimental e muito lento.
- Python 3.14+ não suportado.
- Funcionalidades dependentes de hardware exigem multi-GPU ou Apple Silicon.

## Fontes

- README.md do repositório (`26ffea17461d0d14a0d3641b93435343b54c29e1`), lido em 2026-11-10.
- Metadados via API do GitHub (linguagem, licença, tópicos), consultados em 2026-11-10.
- Apenas o `README.md` foi lido.
