---
type: entity
kind: org
url: https://github.com/PrismML-Eng
created: 2026-10-24
updated: 2026-10-24
tags: [llms-compactos-on-device]
---

# PrismML

> Empresa criadora da família Bonsai: modelos quantizados em ternário/1-bit que encolhem LLMs de ~27B para rodar em laptop, desktop e, segundo material de marketing do produto, até em celular.

## O que é

PrismML publica o código do demo sob a organização GitHub `PrismML-Eng`, com os pesos dos modelos hospedados no Hugging Face sob o org `prism-ml`. A aposta central é quantização extrema (pesos ternários {−1, 0, +1}, ~1,75 bit/peso) sobre modelos Qwen, mantendo a maior parte da capacidade original.

## Repositórios e projetos

- [PrismML-Eng/Bonsai-demo](../repos/github.com/prismml-eng/bonsai-demo.md) — demo oficial para rodar Bonsai 2 (2B, 4B, 9B, 27B) localmente via llama.cpp (fork próprio) ou MLX, com visão, tool calling e cliente MCP; Apache-2.0.
- `PrismML-Eng/llama.cpp` — fork do llama.cpp necessário para os empacotamentos `PQ2_0`/`PTQ1_0`, citado como dependência do Bonsai-demo.

## Relevância no ecossistema

Representa a aposta mais agressiva de quantização documentada nesta wiki até agora: enquanto o MiniCPM (OpenBMB) aposta em modelos densos pequenos (1B–8B) com arquitetura padrão, a PrismML comprime um modelo de 27B para pesos ternários, mantendo (segundo a própria empresa) 98,2% do desempenho do FP16.

## Relações

- Colabora com: comunidade llama.cpp (upstream já incorpora parte do suporte a `Q2_0`); Hugging Face (hospedagem dos pesos).
- Associado a: modelos-base Qwen (Qwen3.5, Qwen3.8), segundo a documentação oficial consultada fora do README.
- Concorre com: outras estratégias de compressão/execução local de LLMs, como o MiniCPM (OpenBMB) e o colibri (JustVugg).

## Fontes

- README de [PrismML-Eng/Bonsai-demo](../repos/github.com/prismml-eng/bonsai-demo.md), commit `ee6ee05ae01ed7483178a14d81530c5b4c4fa36f` (consultado em 2026-10-24).
- https://docs.prismml.com/models/bonsai-27b (consultado em 2026-10-24) — documentação oficial complementar, fora do README, usada para confirmar modelo-base e licença.
- Metadados da API do GitHub, consultados em 2026-10-24.
