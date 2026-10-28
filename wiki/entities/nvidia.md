---
type: entity
kind: org
url: https://github.com/NVIDIA-NeMo
created: 2026-10-28
updated: 2026-10-28
tags: [llm, moe, nemotron, agentic-ai]
---

# NVIDIA

> Nesta wiki, documentada pela organização GitHub `NVIDIA-NeMo`, mantenedora do `Nemotron`, hub de receitas de treinamento e cookbooks de uso para a família aberta de modelos Nemotron.

## O que é

NVIDIA mantém várias organizações no GitHub; nesta wiki o escopo documentado se restringe ao que o README do `Nemotron` publica: a organização `NVIDIA-NeMo` concentra o ecossistema NeMo (treinamento, RL, avaliação, curadoria de dados) usado para construir os modelos Nemotron, incluindo repositórios irmãos citados como dependências (`Megatron-Bridge`, `Automodel`, `RL`, `Evaluator`, `DataDesigner`) que não foram ingeridos nesta wiki.

## Repositórios e projetos

- [NVIDIA-NeMo/Nemotron](../repos/github.com/nvidia-nemo/nemotron.md) — receitas de treinamento (pré-treino → SFT → RL), cookbooks de uso e exemplos de ponta a ponta para a família Nemotron, incluindo o Nemotron 3 Ultra (550B/55B); Apache-2.0.

## Relevância no ecossistema

A família Nemotron é um dos conjuntos mais extensos de modelos abertos "agent-first" documentados nesta wiki: cobre desde modelos de borda (Nano) até modelos multi-GPU de datacenter (Ultra, 550B/55B), com arquitetura híbrida Mamba-Attention, Mixture-of-Experts e contexto de até 1M de tokens, além de um catálogo próprio de datasets abertos para cada estágio de treinamento (pré-treino, SFT, RL, segurança, multimodal). O repositório também embute um plugin de Claude Code (`nemotron-customize`) para compor pipelines de treino — um exemplo de fornecedor de modelo distribuindo tooling de agente junto com as receitas.

## Relações

- Mantém: [NVIDIA-NeMo/Nemotron](../repos/github.com/nvidia-nemo/nemotron.md).
- Fonte que motivou a documentação: página de pesquisa do [Nemotron 3 Ultra](https://research.nvidia.com/labs/nemotron/Nemotron-3-Ultra/), do laboratório de pesquisa NVIDIA (`research.nvidia.com`), distinta da organização GitHub `NVIDIA-NeMo`.

## Fontes

- README de [NVIDIA-NeMo/Nemotron](../repos/github.com/nvidia-nemo/nemotron.md), commit `a8900c8dc4df1aecb07a6855e0f0f0dc0cc7e625` (consultado em 2026-10-28).
- Metadados da API do GitHub (`api.github.com/orgs/NVIDIA-NeMo`), consultados em 2026-10-28.
