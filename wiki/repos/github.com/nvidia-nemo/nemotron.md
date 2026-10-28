---
type: repo
url: https://github.com/NVIDIA-NeMo/Nemotron
host: github.com
owner: NVIDIA-NeMo
repo: Nemotron
commit: a8900c8dc4df1aecb07a6855e0f0f0dc0cc7e625
license: Apache-2.0
language: Jupyter Notebook
status: active
created: 2026-10-28
ingested: 2026-10-28
updated: 2026-10-28
tags: [llm, moe, mamba, mixture-of-experts, agentic-ai, pretraining, reinforcement-learning, nvidia, nemotron, plugins-de-agente, claude-code]
---

# NVIDIA-NeMo/Nemotron

> Developer Asset Hub da família NVIDIA Nemotron: receitas de treinamento completas (pré-treino → SFT → RL), cookbooks de uso e exemplos de ponta a ponta para os modelos abertos Nemotron, incluindo o Nemotron 3 Ultra (550B/55B).

## O que é

Repositório oficial da NVIDIA que reúne, para toda a família Nemotron (modelos abertos e eficientes voltados a IA agêntica), os blocos de construção de treinamento ("steps"), as receitas completas e reproduzíveis de treinamento, os guias de uso/implantação e exemplos de aplicação de ponta a ponta. Não é o repositório dos pesos dos modelos (esses ficam no Hugging Face); é o hub de como eles foram treinados e como usá-los.

A ingestão foi motivada pela página de pesquisa do **Nemotron 3 Ultra** (`research.nvidia.com/labs/nemotron/Nemotron-3-Ultra/`), que não é um repositório GitHub nem uma página de skill — por isso esta página documenta o repositório de desenvolvimento vinculado a ela, com destaque para esse modelo específico.

### Nemotron 3 Ultra, o modelo que motivou a ingestão

- **Especificações** (README + página de pesquisa): 550B parâmetros totais / 55B ativos por token (MoE); arquitetura híbrida Mamba-Attention com LatentMoE e duas camadas de Multi-Token Prediction (MTP) de peso compartilhado; 20T tokens de pré-treino em NVFP4, currículo de dados em duas fases; contexto de até 1.048.576 tokens (1M).
- **Pipeline completo:** Pretrain → SFT → RLVR → MOPD (destilação multi-professor on-policy) → MTP Boosting. A receita publicada neste repositório cobre apenas **Pretrain → SFT**; o restante do pipeline usado no modelo lançado não está reproduzível a partir daqui.
- **Dados abertos usados na receita:** mistura de pré-treino em duas fases (Figura 4 do relatório técnico) sobre datasets Nemotron abertos; inclui os datasets novos `Nemotron-Pretraining-Specialized-v1.2` e `Nemotron-Pretraining-Legal-v1`.
- **Aviso do próprio README:** a receita treina exclusivamente no subconjunto open-source dos dados; os resultados divergem dos benchmarks do relatório técnico, que usou dados proprietários adicionais. É uma implementação de referência da metodologia, não uma reprodução do modelo lançado.
- **Benchmarks citados na página de pesquisa** (não verificados de forma independente, números do próprio divulgador): vazão de inferência (8k de entrada, 64k de saída) 5,9× maior que a do GLM-5.1, 4,8× maior que a do Kimi-K2.6 e 1,6× maior que a do Qwen-3.5; desempenho superior no RULER com 1M de contexto; precisão "comparável" a outros LLMs abertos de ponta.
- **Pesos:** [NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16) (pós-treinado), variantes `-NVFP4`, `-Base-BF16` e `-GenRM` na [coleção Nemotron v3](https://huggingface.co/collections/nvidia/nvidia-nemotron-v3).
- **Relatório técnico:** [NVIDIA-Nemotron-3-Ultra-Technical-Report.pdf](https://research.nvidia.com/labs/nemotron/files/NVIDIA-Nemotron-3-Ultra-Technical-Report.pdf).

## Como funciona

O repositório se organiza em quatro camadas, da mais granular à mais aplicada:

| Camada | Propósito | Formato | Local |
|---|---|---|---|
| **Nemotron Steps** | Blocos reutilizáveis de todo o ciclo (curadoria de dados, SDG, tradução, pré-treino, SFT, PEFT, RL, conversão, avaliação) | CLI `nemotron steps` + configs YAML | `src/nemotron/steps/` |
| **Training Recipes** | Pipelines completos e reproduzíveis, de dados brutos a modelo pronto para deploy | Pacotes Python com configs, scripts e avaliação | `src/nemotron/recipes/` |
| **Usage Cookbooks** | Deploy e uso de modelos já treinados | Notebooks Jupyter passo a passo | `usage-cookbook/` |
| **Use Case Examples** | Aplicações completas (RAG, agentes, tool use) | Notebooks e scripts | `use-case-examples/` |

As receitas de treinamento compõem os "steps" e dependem de outros repositórios da organização NVIDIA-NeMo: `DataDesigner` (geração sintética de dados), `NeMo-Curator` (curadoria em escala), `Megatron-Bridge` (treino de modelos Megatron) ou `Automodel` (modelos HuggingFace), `NeMo-RL` (RL) e `Evaluator` (avaliação em benchmarks padrão).

Além do Nemotron 3 Ultra, o repositório documenta receitas para: Nemotron 3 Super (120,6B/12,7B), Nemotron 3.5 Super (120B/12B, visão-linguagem), Nemotron 3 Nano (31,6B/3,6B), Nemotron 3.5 Lightning (30B/3B, licenciado sob OpenMDW-1.1), Nemotron 3 Nano Omni (30B/3B, multimodal texto/imagem/vídeo/áudio, licenciado sob NVIDIA Nemotron Open Model License), além de Nemotron Embed e Nemotron Rerank.

### Plugin de Claude Code embutido

O repositório inclui um plugin de Claude Code, `nemotron-customize`, que transforma o catálogo de steps em `src/nemotron/steps/` em um construtor de pipeline guiado:

```text
/plugin marketplace add NVIDIA-NeMo/Nemotron
/plugin install nemotron-customize@nvidia-nemotron
```

Deve ser invocado a partir da raiz do checkout do repositório (precisa de `pyproject.toml` e `src/nemotron/steps/` no diretório atual); roda a partir de subdiretório falha. O marketplace instala apenas esse plugin — as demais pastas em `skills/` (bases de conhecimento de modelo, skills de contribuidor) permanecem no disco apenas para navegação, sem carregar como plugin.

## Instalação e uso rápido

```bash
git clone https://github.com/NVIDIA-NeMo/Nemotron
```

Cada seção tem seu próprio ponto de entrada: `nemotron steps run <step>` para blocos isolados; guias de treinamento em `docs/nemotron/<modelo>/README.md` para receitas completas (ex.: `docs/nemotron/ultra3/README.md` para o Ultra); notebooks em `usage-cookbook/<Modelo>/` para deploy/uso; notebooks em `use-case-examples/` para aplicações. Documentação consolidada em `docs.nvidia.com/nemotron/latest/`.

## Exemplos de uso

- Reproduzir a metodologia de pré-treino + SFT do Nemotron 3 Ultra com dados abertos, para entender o currículo de dados em duas fases e a configuração de paralelismo (TP=2/PP=12/EP=32 no pré-treino, PP=6 no SFT).
- Rodar `nemotron steps run sdg/persona_mcq` para gerar dados sintéticos de múltipla escolha isoladamente, sem montar um pipeline completo.
- Usar os cookbooks de `usage-cookbook/Nemotron-3-Ultra/` para implantar o modelo já treinado em configuração multi-GPU.
- Instalar o plugin `nemotron-customize` no Claude Code para planejar e validar um pipeline de steps customizado dentro do próprio editor.

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é entender ou reproduzir *como* um modelo Nemotron foi treinado (dados, currículo, hiperparâmetros), implantar um modelo Nemotron já treinado, ou compor um pipeline de treino customizado a partir dos steps publicados.
- **Evite quando:** o objetivo é apenas obter os pesos do modelo para inferência — nesse caso, os cookbooks em `usage-cookbook/` bastam, sem precisar do restante do repositório; e não espere reproduzir os números do relatório técnico com as receitas aqui publicadas, já que elas usam apenas o subconjunto de dados aberto.

## Limitações e cuidados

- A receita do Nemotron 3 Ultra publicada cobre só **Pretrain → SFT** de um pipeline de cinco estágios (o programa completo inclui RLVR, MOPD e MTP Boosting); os pesos publicados no Hugging Face passaram pelo pipeline completo, não pelo que está reproduzível aqui.
- Toda receita marcada "Open-Source Data Only" produz resultados diferentes dos benchmarks do relatório técnico, que usaram dados proprietários adicionais — declarado explicitamente pelo README para Ultra, Super, Nano e 3.5 Lightning.
- Licenciamento não é uniforme dentro do mesmo repositório: o código é Apache-2.0 (confirmado pela API do GitHub), mas pesos/dados/receitas variam por modelo — Nemotron 3.5 Lightning usa OpenMDW-1.1, Nemotron 3 Nano Omni usa a NVIDIA Nemotron Open Model License, e os datasets individuais têm licenças próprias (CC-BY-4.0, ODC-BY-1.0, NVIDIA Data Agreement, entre outras) listadas na tabela de datasets do README.
- Os benchmarks de desempenho do Nemotron 3 Ultra citados na página de pesquisa (vazão vs. GLM-5.1/Kimi-K2.6/Qwen-3.5, RULER) vêm do próprio divulgador (NVIDIA) e não foram verificados de forma independente nesta ingestão.
- Nemotron 3.5 Super tem dados de SFT/RL ainda não publicados ("Pending Open-Source Release"), segundo o próprio README.
- Esta página documenta o `README.md` da raiz e a página de pesquisa do Nemotron 3 Ultra que motivou a ingestão; os guias individuais em `docs/nemotron/<modelo>/README.md`, o código em `src/`, e os demais arquivos do repositório não foram lidos.

## Estado e adoção

- Repositório criado em 2025-10-03; push mais recente em 2026-10-27, observado em 2026-10-28.
- 2.227 estrelas, 459 forks, 96 issues abertas, observado em 2026-10-28.
- Licença do código: Apache-2.0 (confirmada pela API do GitHub). Pesos, dados e algumas receitas têm licenças próprias por modelo/dataset (ver Limitações).
- Lançamentos recentes citados no README (com data de anúncio, não de push): Nemotron 3.5 Super e 3.5 Lightning, Nemotron 3 Ultra (anunciado na GTC San Jose 2026), Nemotron 3 Nano Omni.

## Relações

- Mantido por: [NVIDIA](../../../entities/nvidia.md).
- Fonte que motivou a ingestão: [página de pesquisa do Nemotron 3 Ultra](https://research.nvidia.com/labs/nemotron/Nemotron-3-Ultra/) (não é repositório nem skill; usada como fonte complementar de arquitetura e benchmarks).
- Repositórios irmãos citados como dependências (não ingeridos nesta wiki): `NVIDIA-NeMo/DataDesigner`, `NVIDIA-NeMo/Megatron-Bridge`, `NVIDIA-NeMo/Automodel`, `NVIDIA-NeMo/RL`, `NVIDIA-NeMo/Evaluator`, `NVIDIA/NeMo-Curator`.
- Conceitos: nenhum conceito dedicado nesta wiki cobre "arquitetura híbrida Mamba-Attention com MoE" ou "quantização NVFP4"; a página fica listada na categoria [Modelos abertos e treinamento de LLMs](../../../categorias.md#modelos-abertos-e-treinamento-de-llms).

## Perguntas abertas

- O que os guias de treinamento individuais (`docs/nemotron/ultra3/README.md` etc.) detalham além do resumo na tabela de receitas do README raiz?
- Como o plugin `nemotron-customize` se comporta na prática — o `SKILL.md` referenciado (`skills/nemotron-customize/SKILL.md`) não foi lido nesta ingestão.
- Quais números de benchmark do Nemotron 3 Ultra aparecem no relatório técnico (PDF), já que a página de pesquisa resume mas não detalha a metodologia de medição?

## Fontes

- README: https://raw.githubusercontent.com/NVIDIA-NeMo/Nemotron/a8900c8dc4df1aecb07a6855e0f0f0dc0cc7e625/README.md (commit `a8900c8dc4df1aecb07a6855e0f0f0dc0cc7e625`, consultado em 2026-10-28). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Página de pesquisa: https://research.nvidia.com/labs/nemotron/Nemotron-3-Ultra/ (consultada em 2026-10-28), usada como fonte complementar para arquitetura e benchmarks do Nemotron 3 Ultra não detalhados no README.
- Metadados: API do GitHub (`api.github.com/repos/NVIDIA-NeMo/Nemotron`), consultada em 2026-10-28.
