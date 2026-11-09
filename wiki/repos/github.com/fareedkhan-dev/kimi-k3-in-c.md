---
type: repo
url: https://github.com/FareedKhan-dev/kimi-k3-in-c
host: github.com
owner: FareedKhan-dev
repo: kimi-k3-in-c
commit: 81bb6c23ccee2154bc35cad922588ab66494a9a9
license: Apache-2.0
language: C
status: active
created: 2026-11-09
ingested: 2026-11-09
updated: 2026-11-09
tags: [inferencia, moe, c99, quantizacao, cpu, kimi-k3, streaming-de-experts]
---

> Runtime de inferência em C99 puro que executa o Kimi K3 (2,78 trilhões de parâmetros) com apenas 8 GB de RAM e sem GPU, via streaming de experts do disco e quantização MXFP4.

## Propósito

Kimi K3 in C demonstra que modelos de mistura de especialistas extremamente grandes podem rodar em CPUs de hardware de consumo sem sacrificar a fidelidade do output. A saída é byte-idêntica em qualquer configuração de memória — de um laptop com 8 GB a um servidor com 128 GB — trocando latência por disponibilidade de memória.

A inovação central é uma **redução de 675×** em requisitos de memória frente ao baseline bfloat16, resultado de quatro otimizações encadeadas:

| Técnica | Ganho |
|---------|-------|
| Pesos MXFP4 (0,53 bytes/peso) | ~3× frente a bfloat16 |
| KDA: estado recorrente de tamanho fixo | independente do comprimento de contexto |
| MLA: cache de latentes comprimidos (53× menor que heads expandidas) | 2,37 MB/posição vs. 125 MB padrão |
| Parte densa transmitida do disco (não residente) | elimina 113,5 GB residentes |

## Arquitetura do modelo

Kimi K3 tem 93 camadas no total:
- 69 usam **KDA** (Kimi Delta Attention): atenção recorrente com estado fixo de 96 cabeças × 128×128.
- 24 usam **MLA** (Gated Multi-head Latent Attention): projeta para latente de 576 dim em vez de cachear 96×320 heads por posição.
- 896 experts roteados por camada; apenas 16 ativos por token.
- 2 experts compartilhados ativos em todo token.
- Residual de atenção: a cada 12 camadas, snapshot e reset do residual acumulado.

## Requisitos e instalação

**Hardware mínimo:**
- 8 GB de RAM
- 1,7 TB de armazenamento livre (1,56 TB de checkpoint + 109 GB de trunk empacotado)
- x86-64 com AVX2+FMA (arm64 NEON suportado)

**Software:**
- C99 — GCC ≥9 ou Clang ≥10 (sem dependências externas; apenas libm e OpenMP)
- Python 3.9+ (somente para ferramentas auxiliares)

**Processo de seis passos:**
1. Clonar o repositório
2. Executar diagnóstico (`k3-doctor.sh`)
3. Compilar: `make -j`
4. Verificar: `make test`
5. Baixar checkpoint (1,56 TB via HuggingFace)
6. Empacotar trunk (gera arquivo único de 109 GB a partir de 93 camadas)

## Uso e presets

```bash
./bin/k3 <model_dir> --trunk <packed_dir> --preset <name> \
  --tok <model_dir> --prompt "text" --gen 8 --incremental
```

Modo chat: `--chat` implementa o protocolo XTML oficial com thinking blocks, histórico multi-turn e captura de raciocínio.

**Presets disponíveis:**

| Preset | Trunk (GB) | Experts cache (GB) | Tempo/token |
|--------|------------|-------------------|-------------|
| ultra | 2,5 | 0,31 | — (prova de vida, 8 GB) |
| laptop | 3,0 | 1,0 | 26,5 s |
| desktop | 16,0 | 10,0 | 24,2 s |
| workstation | 60,0 | 30,0 | 19,8 s |
| server | 110,0 | 13,0 | 5,6 s |
| max | 110,0 | 109,0 | — (pico de 224 GB) |

## Implementação técnica

**Experts roteados:** nunca dequantizados; multiplicados diretamente em nibbles empacotados no formato E2M1 (4 bits) com expoente compartilhado de 8 bits por 32 pesos. Cache LRU com planejamento de capacidade baseado em trace.

**Kernels:** 176 KB de binário implementando todas as operações sem BLAS. Contratos de ponto flutuante garantem saída bit-idêntica em caminhos scalar/AVX2/NEON.

**Formato de entrada:** safetensors (1,56 TB indexado sem carregamento completo); tokenizador tiktoken BPE.

## Validação

A saída é verificada token por token contra uma referência PyTorch — sem tolerância. Inclui testes de multiplicação MXFP4 sem dequantização e determinismo do tokenizador entre Linux e Windows.

## Limitações

- Sem caminhos de GPU: otimização exclusivamente para CPU.
- Sem dependências externas também significa sem aceleração de bibliotecas como cuBLAS.
- Largura de banda de armazenamento domina 80% do tempo de geração; NVMe local rápido é essencial.
- Limite de contexto determinado pelo cache KV do MLA (recusa inicialização se não houver RAM suficiente).
- Requer `--trunk` para streaming; sem ele, tenta carregar 113,5 GB residentes.

## Fontes

- README.md do repositório (`81bb6c23ccee2154bc35cad922588ab66494a9a9`), lido em 2026-11-09.
- Metadados via API do GitHub (linguagem, licença, tópicos), consultados em 2026-11-09.
- Apenas o `README.md` foi lido.
