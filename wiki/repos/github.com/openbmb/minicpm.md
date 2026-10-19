---
type: repo
url: https://github.com/OpenBMB/MiniCPM
host: github.com
owner: openbmb
repo: minicpm
commit: 316cfb1cea39f39cfa16b4f5703b77495c2340be
license: Apache-2.0
language: Jupyter Notebook
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [llm, on-device, modelos-compactos, inferencia, edge, openbmb, quantizacao, atencao-esparsa, contexto-longo, agent-skills]
---

# OpenBMB/MiniCPM

> Família de LLMs compactos da OpenBMB para dispositivos e ambientes com recursos limitados, com a geração MiniCPM5 (1B e 2B densos), a arquitetura híbrida SALA para contexto de milhões de tokens e a linhagem MiniCPM4/4.1 com atenção esparsa treinável.

## O que é

MiniCPM é uma família de modelos de linguagem de pequeno porte publicada pela OpenBMB, mantida em um repositório que funciona como **hub de releases, cookbooks e skills**: os pesos ficam no HuggingFace e no ModelScope, e o GitHub concentra instruções de implantação, ajuste fino e avaliação.

A release corrente é a **MiniCPM5**, com dois checkpoints densos:

| Modelo | Foco | Arquitetura e escala |
|---|---|---|
| **MiniCPM5-2B** | assistentes locais, agentes de código, tool use e raciocínio | `LlamaForCausalLM` denso, 2.516.756.480 parâmetros (1.981.982.720 sem embeddings), 42 camadas, GQA 16 Q / 2 KV, contexto de 131.072 tokens |
| **MiniCPM5-1B** | mesmo caso de uso com footprint menor | Transformer denso de 1B, com modos Think e No Think no mesmo checkpoint e contexto longo nativo |

O README declara **SOTA open-source na classe de 2B** para o MiniCPM5-2B, com média de 53,9 em um conjunto de comparação que inclui LFM2.5-2.6B, Qwen3.5-2B e Gemma-4-E2B-it, além de modelos maiores listados como referência (o maior teria 51,1). Para o MiniCPM5-1B, a alegação é SOTA na classe de 1B, com vantagem em tool use, geração de código e raciocínio difícil. São afirmações do projeto dentro de um conjunto escolhido por ele, não um ranking independente.

O repositório também documenta gerações anteriores:

- **MiniCPM-SALA** (9B): atenção híbrida esparsa + linear para contexto de milhões de tokens.
- **MiniCPM4 / 4.1** (8B e 0.5B): atenção esparsa treinável, quantização ternária, raciocínio híbrido e runtime CUDA próprio.
- **MiniCPM3-4B e modelos de 2024** (2B, 1B, MoE 8x2B, 128k, MiniCPM-S-1B): linhagem histórica, mantida em tabelas de downloads.

## Como funciona

### MiniCPM5: arquitetura padrão e receita de treino

O MiniCPM5-2B usa a arquitetura **`LlamaForCausalLM` padrão**, sem kernels customizados nem fork do código do modelo — a mesma escolha vale para o 1B. Isso permite que vLLM, SGLang, llama.cpp, Transformers, Ollama, LM Studio, MLX, LiteRT-LM e ArcLight carreguem o checkpoint diretamente. A compatibilidade com o ecossistema é parte da tese: o diferencial está nos dados e no treino, não em um runtime proprietário.

A receita de treino segue três estágios:

```text
base training -> mid-training -> post-training (SFT -> RL -> OPD)
```

No pós-treino do 2B, o projeto usa **400B tokens de SFT de deep-thinking**, treina **professores de RL** especializados (matemática, código, tarefas agênticas, escrita e domínios relacionados) e aplica **On-Policy Distillation (OPD)** para consolidar **16 modelos especialistas**, incluindo cinco de tarefas agênticas, em um único checkpoint. O OPD calcula a divergência KL reversa de vocabulário completo entre aluno e professor em cada posição da resposta, em vez do advantage baseado em verificação. O README atribui ao par RL + OPD um ganho médio de **+10,96 pontos** em raciocínio e capacidades gerais e **+6,96 pontos** em capacidades agênticas.

O 1B usa a mesma estrutura com **200B tokens de SFT deep-thinking e 200B de SFT hybrid-thinking**; o projeto reporta **+16 pontos** em matemática, código e instrução e **−29 pontos percentuais** na fração de respostas que atingem o limite de tokens.

Os dados de treino são publicados como parte da família **UltraData**: Ultra-FineWeb, UltraX, UltraData-Code, UltraData-Math, UltraData-SFT-2605, UltraData-SFT-Agent-2609 e UltraData-RL-2609.

### MiniCPM-SALA: atenção híbrida para 1M+ tokens

SALA combina **25% de atenção esparsa InfLLM-V2** com **75% de Lightning Attention** (linear). A parte esparsa preserva foco local; a linear mantém o custo global baixo. O modelo usa **HyPE (Hybrid Positional Embedding)** para generalização de comprimento e **HALO**, uma receita de destilação que transfere capacidades de atenção densa para a arquitetura híbrida.

O README afirma **até 3,5× a velocidade de inferência do Qwen3-8B com 256K tokens em uma A6000D**, menor overhead de KV cache que baselines densos, **até 2,5× de speedup em TTFT contra o Qwen3-8B em A6000D e RTX 5090** e contexto de **1M de tokens em uma única RTX 5090**, onde o Qwen3-8B comparado sofre OOM. A conversão de Transformer para híbrido por treino continuado custaria cerca de **25% do orçamento** de treinar um modelo comparável do zero.

### MiniCPM4 / 4.1: esparsidade treinável e runtime próprio

A linhagem 4.x aposta em eficiência de ponta a ponta:

| Componente | Papel declarado |
|---|---|
| **InfLLM-V2** | atenção esparsa treinável; cada token interage com menos de 5% dos tokens em 128K |
| **BitCPM** | quantização ternária, com três valores e ~90% de redução de bit-width |
| **CPM.cu** | framework CUDA leve para prefill/decode com atenção esparsa, quantização e amostragem especulativa |
| **ArkInfer** | implantação multiplataforma em diferentes backends |
| **Model Wind Tunnel 2.0** | scaling previsível para escolher configurações de treino |
| **UltraClean / UltraChat v2** | filtragem e geração de dados de pré-treino e SFT |

O README reporta **~7× de melhora de decode** contra Qwen3-8B em Jetson AGX Orin e **3× em decodificação de raciocínio** no MiniCPM4.1. Uma restrição importante: vLLM e SGLang só suportam o modo de **atenção densa**; para atenção esparsa é preciso usar Transformers ou CPM.cu. O 4.1 também oferece raciocínio híbrido via `enable_thinking` e o sufixo `/no_think`.

## Instalação e uso rápido

O caminho mais curto para o MiniCPM5-2B é um servidor compatível com OpenAI:

```bash
pip install "vllm>=0.21"
vllm serve openbmb/MiniCPM5-2B --port 8000
```

Alternativa com SGLang, recomendada para tool calling:

```bash
pip install "sglang[srt]>=0.5.16"
python -m sglang.launch_server --model-path openbmb/MiniCPM5-2B --port 30000 \
    --tool-call-parser minicpm5
```

Para inferência local em CPU/GPU, o README publica um exemplo com `transformers>=5.6` e `AutoModelForCausalLM`. Para GGUF, o comando é `llama-server -m MiniCPM5-2B-F16.gguf -ngl 99 -c 8192 --jinja`. Também há caminhos para Ollama, LM Studio, MLX (Apple Silicon), LiteRT-LM (Android/iOS/desktop/IoT), ArcLight e FlagOS multi-chip.

Parâmetros de amostragem recomendados para o 2B: `temperature=1.0, top_p=0.95, min_p=0.0`. No llama.cpp, o `min_p` padrão de 0,05 pode causar repetição; o README recomenda zerá-lo.

## Exemplos de uso

Exemplos derivados do README:

```bash
# servidor OpenAI-compatible com vLLM
vllm serve openbmb/MiniCPM5-1B --port 8000

# tool calling com o parser nativo do SGLang
python -m sglang.launch_server --model-path openbmb/MiniCPM5-1B --port 30000 \
    --tool-call-parser minicpm5

# decodificação especulativa com o draft DSpark do 2B
python -m sglang.launch_server --model-path openbmb/MiniCPM5-2B \
    --speculative-algorithm DSPARK \
    --speculative-draft-model-path openbmb/MiniCPM5-2B-DSpark \
    --speculative-dspark-block-size 7
```

O repositório distribui **Agent Skills** para agentes de código: `minicpm5-deploy` roteia entre backends de inferência e `minicpm5-finetune` entre frameworks de ajuste fino; cada rota tem cookbook e sub-skill próprios. O README mostra o uso em Cursor/Claude Code como `@minicpm5-deploy   serve openbmb/MiniCPM5-1B with vLLM on port 8000`.

Há também o **MiniCPM-Desk-Pet**, um pet de desktop local movido pelo MiniCPM5-1B via sidecar `llama-server` e interface Electron, com troca de persona por LoRA.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é rodar um modelo capaz em hardware local ou de borda, com contexto longo, tool calling e formatos GGUF/MLX/GPTQ; ou quando se quer um checkpoint com arquitetura padrão que dispensa kernels customizados e um caminho de ajuste fino documentado.
- **Evite quando:** a tarefa exige o teto de capacidade de modelos de fronteira, avaliação independente ou garantias de qualidade fora dos benchmarks do projeto. Para contexto de milhões de tokens com throughput alto, o SALA é a aposta da própria família; para modelos MoE muito maiores em hardware modesto, o problema é outro (ver [colibri](../justvugg/colibri.md)).

## Limitações e cuidados

- **Somente o README foi lido.** Pesos, código de treino, datasets, cookbooks, skills e avaliações não foram inspecionados; todos os números são afirmações do projeto.
- **"SOTA" é relativo ao conjunto de comparação.** O README escolhe os baselines e apresenta médias agregadas; não há avaliação cega ou ranking independente nesta página.
- **A família mistura gerações com requisitos diferentes.** O MiniCPM5 usa arquitetura padrão e roda em qualquer backend; o MiniCPM4.x depende de kernels e modos de atenção próprios, e vLLM/SGLang só cobrem o modo denso.
- **Skills executam comandos.** As Agent Skills indicam backends, instalam dependências e rodam serviços; são instruções de terceiros no mesmo padrão de superfície já discutido em [Agent skills](../../../concepts/agent-skills.md).
- **Licença Apache-2.0 para o repositório e para os modelos, segundo o README.** Componentes externos mantêm suas licenças — por exemplo, a UI do Desk Pet é forkada de um projeto AGPL-3.0.
- **Dados e pesos de terceiros.** Os datasets UltraData e os runtimes de implantação têm termos próprios, não verificados aqui.
- **A linguagem principal da API é "Jupyter Notebook".** Isso descreve o conteúdo do repositório (notebooks e docs), não o runtime dos modelos.

## Estado e adoção

- **Release corrente:** MiniCPM5-2B em 2026-09-07; MiniCPM5-1B em 2026-05-19; SALA em 2026-02-11; MiniCPM4.1 em 2025-09-05.
- **Atividade e popularidade observadas em 2026-10-19:** ~11,6 mil estrelas, 809 forks, 22 issues abertas, criado em 2024-01-29 e último push em 2026-09-21; branch padrão `main`.
- **Licença:** Apache-2.0, conforme o README e a API do GitHub.
- **Formatos publicados:** BF16, GGUF, MLX, GPTQ e variantes de ajuste (SFT, Base, Midtrain, DSpark).

## Relações

- **Mantido por:** [OpenBMB](../../../entities/openbmb.md).
- **Conceitos:** [LLMs compactos on-device](../../../concepts/llms-compactos-on-device.md) — a tese central da geração 5; [Atenção esparsa para contexto longo](../../../concepts/atencao-esparsa-para-contexto-longo.md) — mecanismo do SALA e da linhagem 4.x; [Agent skills](../../../concepts/agent-skills.md) — cookbooks distribuídos como skills.
- **Relacionado a:** [OpenBMB/MiniCPM-V](https://github.com/OpenBMB/MiniCPM-V) — modelos visuais da mesma família, repositório separado e não ingerido; [JustVugg/colibri](../justvugg/colibri.md) — runtime de inferência local que aposta em MoE com experts no disco, uma estratégia oposta à de modelos densos pequenos.
- **Runtimes citados:** vLLM, SGLang, llama.cpp, Transformers, Ollama, LM Studio, MLX, LiteRT-LM, ArcLight, CPM.cu, FlagOS.

## Perguntas abertas

- Como o MiniCPM5-2B se compara a modelos da mesma classe em avaliação independente, fora do conjunto escolhido pelo projeto?
- O ganho de RL + OPD se mantém em domínios fora dos professores treinados?
- Qual é o custo real de memória e latência do SALA em 1M tokens fora das GPUs citadas?
- A conversão Transformer → híbrido por treino continuado preserva capacidades gerais de forma consistente?
- Como as Agent Skills de deploy/finetune se comportam em agentes além de Cursor e Claude Code?
- Quais termos se aplicam aos datasets UltraData e aos checkpoints derivados?
- A arquitetura padrão do MiniCPM5 reduz o atrito de implantação o suficiente para compensar a ausência de otimizações específicas de borda?

## Fontes

- README: https://github.com/OpenBMB/MiniCPM (commit `316cfb1cea39f39cfa16b4f5703b77495c2340be`, consultado em 2026-10-19). Somente o README foi lido; `docs/`, `skills/`, código, notebooks, testes e checkpoints não foram consultados.
- Metadados do repositório e da organização: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas, branch e descrição).
