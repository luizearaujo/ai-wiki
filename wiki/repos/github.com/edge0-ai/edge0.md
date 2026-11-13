---
type: repo
url: https://github.com/Edge0-AI/Edge0
host: github.com
owner: Edge0-AI
repo: Edge0
commit: da9cc526747759227714ddde0728763d95306c04
license: Apache-2.0
language: C++
status: active
created: 2026-11-13
ingested: 2026-11-13
updated: 2026-11-13
tags: [inferencia-local, moe, edge, on-device, llm, streaming, cpp, foundation-model, latent-moe]
---

> Framework de inferência MoE em streaming e família de modelos fundação com até 145B parâmetros para rodar em laptops e celulares, via Latent MoE, offload de especialistas no SSD e router preditivo baseado em n-gramas.

## Propósito

Edge0 combina dois componentes: um motor de inferência (`edge0-infer`, baseado em GGML) e uma família de modelos fundação projetados e treinados especificamente para hardware de consumo. A aposta é diferente de outros projetos de inferência local como llama.cpp ou colibri: em vez de quantizar modelos existentes, a Edge0-AI treinou modelos do zero com uma arquitetura própria ([Latent MoE](../concepts/moe-latente.md)) e os otimizou para streaming de pesos do SSD com roteamento preditivo.

## Arquitetura: Latent MoE

A inovação central é o **[Latent MoE](../concepts/moe-latente.md)**: a representação do token é projetada para um espaço latente comprimido antes de ser enviada aos especialistas. A atenção permanece em largura completa; apenas os especialistas operam na dimensão reduzida. Isso resulta em pesos menores e roteamento em espaço mais denso.

| Modelo | Parâmetros totais | Ativos/token | Especialistas | Largura latente | Contexto |
|--------|------------------|-------------|---------------|-----------------|---------|
| Edge0 145B | 145B | 10,12B | 512 roteados + 1 compartilhado | 1792 | 256K (32K residente em KV int8) |
| Edge0 120B | 120B | 8,64B | 512 roteados + 1 compartilhado | 1280 | 256K (32K residente) |

Ambos têm 48 camadas com atenção híbrida (linear + indexada a cada 4 camadas) e uma tabela PLE (*Position-wise Linear Embedding*) de 51,2B parâmetros em fp8, usada para predição de roteamento baseada em n-gramas.

**Treinamento nativo em 4 bits:** os modelos Edge0 foram treinados diretamente em 4 bits (Q3_K e NVFP4), não quantizados em pós-treino. Derivados de Qwen3.8-Flash-Next como base de pesos.

## Streaming de pesos e router preditivo

- **`--mmap-experts`**: carrega especialistas não-cacheados diretamente do SSD sob demanda, permitindo rodar o modelo 145B com menos VRAM do que o tamanho total dos pesos.
- **Router preditivo (PLE table)**: prevê quais especialistas serão necessários um passo à frente usando n-gramas, reduzindo latência de carregamento do SSD.
- Offload configurável entre GPU, RAM e SSD.

## Plataformas e estado

| Plataforma | Modelos | Estado |
|------------|---------|--------|
| Linux/Windows (NVIDIA CUDA 13) | 145B, 120B | Oficial/lançado |
| macOS Apple Silicon (Metal) | 145B/120B | Medições existem; não lançado oficialmente |
| iOS/Android | 35B, 8B | Versões anteriores |

## Desempenho

**Edge0 145B Q3_K, RTX 5090 D (24 GB):**

| Cenário | Throughput |
|---------|-----------|
| Decode (modo agente) | ~121 tok/s |
| Prefill 4K | ~2.170 tok/s |
| Prefill 16K | ~3.555 tok/s |

**Edge0 120B Q3_K, RTX 5090 D:**

| Cenário | Throughput |
|---------|-----------|
| Decode (modo agente) | ~145 tok/s |
| Prefill 4K | ~3.237 tok/s |

## Benchmarks de qualidade (Edge0 145B)

| Benchmark | Score |
|-----------|-------|
| DeepSWE 1.1 | 64,6 |
| Terminal-Bench 2.1 | 86,5 |
| GPQA-Diamond | 90,4 |
| HLE | — |
| IFBench | — |
| AA-LCR | — |

## Instalação e uso

```bash
git clone https://github.com/Edge0-AI/Edge0
# compilar edge0-strata e edge0-infer
build/cpu/bin/edge0-infer serve --model /path/to/Edge0-145B-q3k
```

Expõe endpoints compatíveis com OpenAI e Anthropic na porta 8000.

## Quantizações disponíveis

| Variante | 145B | 120B |
|----------|------|------|
| Q3_K | 40,81 GiB | 27,98 GiB |
| NVFP4 | 47,79 GiB | 32,96 GiB |

## Licença

- **Framework (edge0-infer):** Apache-2.0.
- **Modelos Edge0:** Edge0 Community Model License 1.0 — permite uso pessoal, pesquisa e comercialização de saídas geradas; **não** permite serviços de modelo pago ou assistentes de IA comerciais sem autorização separada da Edge0-AI.

## Limitações

- Requer NVIDIA CUDA 13 em Linux/Windows; macOS e iOS/Android não estão oficialmente lançados para os modelos 145B/120B.
- Dados de treinamento, vocabulário exato e fine-tuning não estão documentados no README nem no card do modelo.

## Fontes

- README.md do repositório (`da9cc526747759227714ddde0728763d95306c04`), lido em 2026-11-13.
- `docs/models/edge0-145b.md` no mesmo commit, lido em 2026-11-13 com autorização explícita do usuário.
- Metadados via API do GitHub (linguagem, licença, tópicos), consultados em 2026-11-13.
