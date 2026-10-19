---
type: entity
kind: org
url: https://github.com/OpenBMB
created: 2026-10-19
updated: 2026-10-19
tags: [organizacao, llm, on-device, modelos-compactos, pesquisa, china, open-source, minicpm]
---

# OpenBMB

> Organização de pesquisa e engenharia que publica a família MiniCPM de modelos compactos para dispositivos, além de datasets, runtimes e ferramentas de implantação.

## O que é

**OpenBMB** (Open Lab for Big Model Base) se descreve como um laboratório dedicado a construir modelos de fundação e sistemas rumo à AGI. A conta no GitHub foi criada em 2021-09-01, declara 91 repositórios públicos e cerca de 7,4 mil seguidores observados em 2026-10-19; o site é `openbmb.cn` e o perfil aponta para `@OpenBMB` no Twitter/X.

O README do MiniCPM credita o desenvolvimento a três instituições: **ModelBest Inc.**, **THUNLP** (Tsinghua Natural Language Processing Lab) e a **Gaoling School of Artificial Intelligence da RUC**.

## Repositórios e projetos

- [openbmb/minicpm](../repos/github.com/openbmb/minicpm.md) — família MiniCPM5 (1B/2B densos), SALA (atenção híbrida para 1M+ tokens) e MiniCPM4/4.1 (atenção esparsa treinável), com cookbooks e Agent Skills de deploy e fine-tune.
- **openbmb/MiniCPM-V** — modelos visuais da família, citados no README como repositório separado; não ingerido nesta wiki.
- **openbmb/cpm.cu** — framework CUDA de inferência citado como runtime da linhagem MiniCPM4.
- **openbmb/ArcLight** — runtime local GGUF também listado entre os backends suportados.
- **openbmb/MiniCPM-Desk-Pet** — pet de desktop local movido pelo MiniCPM5-1B, com sidecar `llama-server` e troca de persona por LoRA.
- **UltraData** — família de datasets de pré-treino, SFT e RL publicada junto com os modelos.

## Relevância no ecossistema

A OpenBMB ocupa uma posição específica: em vez de competir apenas por escala, publica **modelos pequenos com receita de treino e dados abertos**. O MiniCPM5 adota arquitetura Transformer padrão para maximizar compatibilidade com runtimes, enquanto o SALA e o MiniCPM4 apostam em **eficiência arquitetural** — atenção esparsa, atenção linear, quantização ternária e kernels próprios.

Essa combinação ajuda a definir três padrões:

- **Abertura do pipeline**: pesos, datasets (UltraData, Ultra-FineWeb), relatórios técnicos e cookbooks no mesmo ecossistema.
- **Otimização para borda**: modelos e runtimes pensados para Jetson, GPUs de consumidor, Apple Silicon, Android/iOS e IoT.
- **Distribuição para agentes**: cookbooks de implantação e ajuste fino empacotados como Agent Skills, seguindo o formato que já circula em Cursor e Claude Code.

**A verificar:** a relação institucional exata entre OpenBMB, ModelBest e as universidades, e quais projetos do repositório são mantidos por cada grupo.

## Relações

- **Associado a:** ModelBest Inc., THUNLP e Gaoling School of AI (RUC), segundo o README do MiniCPM.
- **Publica:** [MiniCPM](../repos/github.com/openbmb/minicpm.md); MiniCPM-V, CPM.cu, ArcLight e MiniCPM-Desk-Pet são citados no README, mas não têm página própria.
- **Conceitos:** [LLMs compactos on-device](../concepts/llms-compactos-on-device.md) e [Atenção esparsa para contexto longo](../concepts/atencao-esparsa-para-contexto-longo.md).
- **Concorre com:** outras famílias de modelos compactos (Phi, Gemma, Qwen small, Llama small), não documentadas na wiki.

## Fontes

- https://github.com/OpenBMB — perfil, bio, data de criação, repositórios públicos e seguidores via API do GitHub em 2026-10-19.
- [openbmb/minicpm](../repos/github.com/openbmb/minicpm.md) — README no commit `316cfb1cea39f39cfa16b4f5703b77495c2340be` (consultado em 2026-10-19), incluindo a seção de instituições e os links para projetos relacionados.
