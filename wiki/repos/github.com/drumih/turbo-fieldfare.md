---
type: repo
url: https://github.com/Drumih/turbo-fieldfare
host: github.com
owner: drumih
repo: turbo-fieldfare
commit: 2e9ea50e8c35a65d9170e3bff9d1063be8931ec0
license: Apache-2.0
language: Swift
status: active
created: 2026-10-25
ingested: 2026-10-25
updated: 2026-10-25
tags: [inferencia, moe, metal, apple-silicon, gemma, on-device, swift, streaming-experts]
---

# Drumih/turbo-fieldfare

> Runtime Swift + Metal para rodar Gemma 4 26B-A4B em ~2 GB de RAM em qualquer Mac Apple Silicon: mantém o core denso residente e lê do SSD apenas os experts roteados por token, com um cache LFU de 16 slots por camada.

## O que é

TurboFieldfare é um motor de inferência model-specific em Swift e Metal para o Gemma 4 26B-A4B (modelo mixture-of-experts de 26B parâmetros, ~3,88B ativos por token). O projeto responde a uma restrição concreta: como rodar um modelo de 14,3 GB em um MacBook com 8 GB de RAM.

A solução é manter apenas o core compartilhado (~1,35 GB) e o KV cache FP16 em memória e **transmitir do SSD só os experts necessários para cada token**, assistido por um cache LFU de 16 slots por camada. O restante — kernels Metal, instalador, CLI, servidor e app nativo — é escrito do zero em Swift, sem depender de MLX ou llama.cpp.

O autor, Andrey Mikhaylov, é engenheiro iOS/Metal e documentou 103 experimentos medidos que fundamentam as decisões de design — um registro raro de metodologia explícita em projetos de inferência local.

> **Não é afiliado à Google** e os pesos não estão incluídos (baixados separadamente do Hugging Face pelos termos de licença do modelo).

## Como funciona

### Pipeline por camada (decode)

```
route  → Metal calcula atenção e router a partir de pesos residentes
plan   → CPU usa os top-8 expert IDs contra o cache LFU de 16 slots
fill   → pread paralelo e limitado para os experts ausentes → buffers Metal
compute → Metal computa o shared-expert enquanto os reads rodam (overlap)
combine → Metal une saídas shared e routed
```

O gargalo é a banda e a latência do SSD, não os FLOPs. O cache LFU por camada evita releituras de experts frequentes.

### Prefill

Prefill em chunks de até 128 tokens: um expert baixado serve múltiplas linhas. Necessário para imagens (sempre chunked) e recomendado para prompts longos.

### KV cache

- 25 camadas de sliding-window attention: armazenamento circular (FP16).
- 5 camadas de full attention: armazenamento linear (FP16).

### Instalador por streaming

O `TurboFieldfareRepack` baixa apenas os byte ranges necessários do Hugging Face e os repacks diretamente no formato `.gturbo` — sem materializar o checkpoint completo em disco. A instalação finaliza com validação de manifest e hashes de arquivo. O resultado ocupa ~14,3 GB.

## Produtos

| Produto | Tipo | Função |
|---------|------|--------|
| `TurboFieldfare` | Biblioteca Swift | Runtime e kernels Metal |
| `TurboFieldfareMac` | App nativo macOS | Instalação, geração, histórico de conversas |
| `TurboFieldfareDecodeService` | Executable | Proprietário do modelo e do Metal, usado pelo app |
| `TurboFieldfareCLI` | CLI | Chat por instrução e completions raw |
| `TurboFieldfareServer` | Servidor | Loopback OpenAI-compatible em `127.0.0.1:8080/v1` |
| `TurboFieldfareRepack` | CLI | Instalador de streaming e verificador de instalação |

O servidor loopback suporta Chat Completions, streaming e function tools — mas o cliente é quem executa as chamadas de tool; o modelo apenas gera a chamada.

## Suporte a imagens

Pack opcional (~1,1 GB) com vision tower para M2 ou superior. Instala ao lado do modelo de texto (`gemma4.gturbo` + `gemma4.vision.gturbo`). Requer ao menos 16 slots de expert cache porque prompts com imagem sempre usam prefill chunked. Texto continua disponível em M1 sem o pack.

## Benchmarks medidos

| Hardware | Velocidade de decode |
|----------|---------------------|
| 8 GB M2 MacBook Air | 5,1 – 6,3 tok/s |
| 24 GB M5 Pro | 31 – 35 tok/s |

Resultados influenciados por comprimento de prompt, comprimento gerado, estado do page cache e hardware. Resultados da comunidade em `docs/COMMUNITY_BENCHMARKS.md`.

O projeto mantém um inventário de 103 experimentos medidos (`docs/experiments/EXPERIMENT_INVENTORY.md`), cobrindo kernels, caching, I/O, prefill e decode — incluindo resultados que pareciam bons e reverteram sob validação mais forte.

## Uso rápido

```bash
git clone https://github.com/drumih/turbo-fieldfare.git
cd turbo-fieldfare
swift build -c release
.build/release/TurboFieldfareMac
# Na primeira execução: Download Model (~15 GB), depois Load Model e Generate
```

**Requisitos:** Apple Silicon Mac · 8 GB RAM · ~14,3 GB de armazenamento livre · macOS 26 · Metal 4 · Swift 6.2+.

## Quando usar (e quando não usar)

- **Use quando:** quiser rodar Gemma 4 26B-A4B localmente em um Mac com 8 GB de RAM, sem depender de API; quando precisar de um servidor OpenAI-compatible local para ferramentas que usam esse protocolo.
- **Evite quando:** o hardware não for Apple Silicon; precisar de outros modelos (escopo fixo em Gemma 4 26B-A4B); macOS 26 / Metal 4 ainda não estiverem disponíveis no seu dispositivo; precisar de áudio ou vídeo (fora de escopo).

## Limitações e cuidados

- **Model-specific:** só roda Gemma 4 26B-A4B. Não é um runtime genérico.
- **macOS 26 + Metal 4** são requisitos — versões anteriores não suportadas.
- Throughput limitado pela banda do SSD; SSDs NVMe rápidos fazem diferença.
- O servidor loopback não tem autenticação nem TLS — não exponha além do localhost.
- Pesos não incluídos: ~15 GB de download na primeira instalação; termos do modelo Gemma se aplicam.
- Não lidos: `docs/SYSTEM_DESIGN.md`, `docs/OPTIMIZATION_JOURNEY.md`, `docs/experiments/`, código-fonte dos kernels Metal.

## Estado e adoção

- Último push: 2026-10-15.
- Observado em 2026-10-25: ~7.035 stars, ~454 forks, ~55 issues abertas.
- Licença: Apache-2.0 (código e documentação); pesos do modelo sob termos do Gemma.

## Relações

- Mantido por: [Drumih](../../../entities/drumih.md)
- Conceitos: [Streaming de experts em MoE](../../../concepts/streaming-de-experts-em-moe.md), [LLMs compactos on-device](../../../concepts/llms-compactos-on-device.md)
- Relacionado: [JustVugg/colibri](../justvugg/colibri.md) — runtime genérico de streaming de experts (C puro, múltiplos modelos MoE, múltiplas GPUs); contrasta com o foco model-specific e Metal-nativo do TurboFieldfare.

## Perguntas abertas

- Qual é o impacto de um SSD mais lento vs. NVMe no throughput de decode, especialmente no M2 base?
- Como o cache LFU evolui ao longo de uma conversa longa — o hit rate aumenta?
- A validação de manifest e hashes do `.gturbo` é reproduzível o suficiente para verificar a integridade após corrupção parcial?
- Planos para suporte a outros modelos MoE (Mixtral, DeepSeek) ou o escopo permanece Gemma 4?

## Fontes

- README: https://raw.githubusercontent.com/Drumih/turbo-fieldfare/2e9ea50e8c35a65d9170e3bff9d1063be8931ec0/README.md (commit `2e9ea50e8c35a65d9170e3bff9d1063be8931ec0`, consultado em 2026-10-25). Somente o README foi lido.
- Metadados: API do GitHub em 2026-10-25.
