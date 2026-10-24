---
type: repo
url: https://github.com/PrismML-Eng/Bonsai-demo
host: github.com
owner: prismml-eng
repo: bonsai-demo
commit: ee6ee05ae01ed7483178a14d81530c5b4c4fa36f
license: Apache-2.0
language: Shell
status: active
created: 2026-10-24
ingested: 2026-10-24
updated: 2026-10-24
tags: [llms-compactos-on-device, agent-skills, mcp]
---

# PrismML-Eng/Bonsai-demo

> Demo oficial para rodar localmente a família Bonsai 2 (2B–27B) da PrismML: modelos quantizados em ternário (~1,75 bit/peso) que retêm 98,2% da inteligência do FP16 em cerca de um nono do tamanho.

## O que é

Bonsai-demo resolve o problema de rodar um modelo de ~27B parâmetros inteiro no laptop ou desktop do usuário, com visão, chamada de ferramentas e um modo de raciocínio ("thinking"), sem depender de API em nuvem. O modelo-base é o Qwen3.8-27B (Qwen3.5 para os tamanhos menores), comprimido para pesos ternários {−1, 0, +1} — cerca de 1,75 bit por peso, em vez de 16.

## Como funciona

Dois empacotamentos de pesos, mesmo conteúdo, trade-off memória/velocidade diferente:

- **`PTQ1_0`:** menor arquivo.
- **`PQ2_0`:** +1,3 GB, processamento de prompt mais rápido; é o que o demo baixa por padrão.

`Q2_0` já roda no llama.cpp oficial upstream; `PQ2_0` e `PTQ1_0` ainda exigem o [fork da PrismML](https://github.com/PrismML-Eng/llama.cpp). No Apple Silicon, roda via MLX com carregador `mlx-vlm` nativo. Contexto de até 262.144 tokens, com cache KV dimensionado automaticamente pela RAM da máquina (ou fixado via `BONSAI_CTX`); cache KV em 4 bits (`BONSAI_KV4=1`) corta o uso de memória em ~3,5×.

Suporta chamada de ferramentas nativa estilo OpenAI e um cliente MCP embutido na UI de chat (Hugging Face e DeepWiki pré-configurados). O modo "thinking" vem ligado por padrão em esforço `xhigh`; pode ser ajustado por requisição (`reasoning_effort`) ou por orçamento de tokens na UI.

## Instalação e uso rápido

```bash
# macOS / Linux
git clone https://github.com/PrismML-Eng/Bonsai-demo.git
cd Bonsai-demo
./setup.sh
./scripts/start_llama_server.sh    # http://localhost:8080
```

`setup.sh` instala dependências de sistema, cria um venv Python via `uv`, baixa os pesos do Hugging Face e os binários pré-compilados do llama.cpp (fork PrismML), e opcionalmente instala Open WebUI e um interpretador de código Jupyter (`BONSAI_OPENWEBUI=0`/`BONSAI_CODE_INTERPRETER=0` para pular). No Windows, equivalente via `setup.ps1`.

Trocar de tamanho: `export BONSAI_MODEL=4B` (valores: `2B`, `4B`, `9B`, `27B`) antes de `./setup.sh`.

## Exemplos de uso

```bash
./scripts/run_llama.sh -p "What is the capital of France?"
./scripts/start_openwebui.sh   # UI completa com tools, code interpreter e banco de dados de demo, em http://localhost:9090
```

Parâmetros de geração recomendados para o 27B em modo thinking: `temperature=1.0`, `top_p=0.95`, `top_k=20`, `min_p=0.05`, limite de saída generoso (≥16384 tokens).

## Quando usar (e quando não usar)

- **Use quando:** quiser rodar um modelo multimodal de ~27B com ferramentas e MCP inteiramente local, em hardware de consumo (Mac com Metal, Linux/Windows com CUDA/Vulkan/ROCm, ou CPU).
- **Evite quando:** precisar da compatibilidade mais ampla de runtime possível — os empacotamentos `PQ2_0`/`PTQ1_0` ainda dependem do fork próprio do llama.cpp, não do upstream oficial.

## Limitações e cuidados

- Quantização ternária/1-bit é agressiva: o README reporta 98,2% de retenção de benchmark médio em relação ao FP16, mas é número do próprio projeto (model card), sem auditoria independente lida nesta ingestão.
- `Q2_0` funciona no llama.cpp upstream oficial; `PQ2_0`/`PTQ1_0` (os formatos padrão do demo) e alguns recursos experimentais (MTP/DFlash) continuam exigindo o fork da PrismML — risco de desalinhamento se o fork atrasar frente ao upstream.
- Expor o servidor fora de `127.0.0.1` (`BONSAI_HOST` não-loopback) abre a rede sem autenticação própria documentada no README além do aviso de segurança.
- **A verificar:** data de lançamento da geração Bonsai 2 e da geração anterior (Bonsai 1-bit/Ternary-Bonsai) — não publicada no README nem na documentação oficial consultada.

## Estado e adoção

- Observado em 2026-10-24: 3.437 stars, 391 forks, 26 issues abertas, push mais recente em 2026-10-24.
- Licença: Apache-2.0 (demo e pesos, segundo a documentação oficial consultada).
- Tamanhos disponíveis: Bonsai 2 2B, 4B, 9B e 27B (GGUF e MLX); gerações anteriores (1-bit e Ternary-Bonsai, 27B/8B/4B/1,7B) documentadas em `Bonsai1_README.md`.

## Relações

- Mantido por: PrismML (PrismML-Eng no GitHub; pesos publicados em `prism-ml` no Hugging Face).
- Conceitos: [LLMs compactos on-device](../../../concepts/llms-compactos-on-device.md) — quantização extrema (ternária/1-bit) como variante mais agressiva do padrão GGUF/MLX já documentado via MiniCPM; [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — cliente MCP embutido na UI de chat.
- Depende de: [open-webui/open-webui](../open-webui/open-webui.md) (integração opcional para a demo agêntica completa), fork próprio do llama.cpp (`PrismML-Eng/llama.cpp`).

## Perguntas abertas

- Quando os formatos `PQ2_0`/`PTQ1_0` devem fundir no llama.cpp upstream, eliminando a dependência do fork?
- Há benchmark de retenção (98,2%) auditado por terceiros, além do model card da própria PrismML?
- Qual o modelo de segurança recomendado para expor o servidor fora de loopback além do aviso genérico no README?

## Fontes

- README: https://raw.githubusercontent.com/PrismML-Eng/Bonsai-demo/ee6ee05ae01ed7483178a14d81530c5b4c4fa36f/README.md (commit `ee6ee05ae01ed7483178a14d81530c5b4c4fa36f`, consultado em 2026-10-24). Somente o README foi lido; os demais arquivos do repositório (scripts, `Bonsai1_README.md`, `TOOLS.md` etc.) não foram consultados.
- Metadados da API do GitHub, consultados em 2026-10-24.
- Documentação oficial complementar: https://docs.prismml.com/models/bonsai-27b (consultada em 2026-10-24, fora do README, para confirmar base model, licença e links oficiais).
