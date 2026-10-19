---
type: entity
kind: person
url: https://github.com/JustVugg
created: 2026-10-19
updated: 2026-10-19
tags: [pessoa, inferencia, moe, modelos-locais, colibri, open-source]
---

# Vincenzo Fornaro (JustVugg)

> Desenvolvedor italiano autor do colibri, motor de inferência em C que roda modelos MoE de centenas de bilhões de parâmetros em hardware doméstico.

## O que é

`JustVugg` é a conta de **Vincenzo Fornaro** no GitHub, descrita na bio como "Founder of Colibrì a tiny engine, immense model for affordable hardware". A conta foi criada em 2015-06-23, declara 121 repositórios públicos e cerca de 2 mil seguidores observados em 2026-10-19. O perfil aponta para `@justvugg` no Twitter/X e o README do colibri mantém site próprio, Discord e um link de doação (Buy Me a Coffee).

O README do colibri situa o projeto como obra de uma pessoa: começou em um laptop de 12 núcleos com 25 GB de RAM, e hoje os números vêm de uma comunidade de máquinas reais. A licença do repositório é Apache 2.0, Copyright 2026 Vincenzo Fornaro.

## Repositórios e projetos

- [justvugg/colibri](../repos/github.com/justvugg/colibri.md) — motor de inferência em C puro para MoE, com experts transmitidos do disco, tiers de GPU opcionais (Vulkan, CUDA, Metal), servidor compatível com OpenAI/Anthropic, modo de decisão System One e servidor MCP; ~42,8 mil estrelas em 2026-10-19.
- **Demais repositórios públicos** — 121 no total, não inventariados nesta ingestão.

## Relevância no ecossistema

O projeto é um caso de **engenharia de sistemas de inferência como bem público**: em vez de competir por aceleração proprietária, aposta em posicionamento de pesos e em medir tudo de ponta a ponta. O README institucionaliza essa postura com uma tabela de hipóteses, evidências e experimentos ainda necessários, e pede resultados negativos — um contraste com projetos que publicam apenas o melhor número.

Fornaro também representa uma linha de trabalho sobre **soberania de hardware**: rodar modelos de fronteira em CPUs, GPUs integradas e discos comuns, com a GPU como acelerador opcional e não como pré-requisito. A escolha de C, um arquivo por família de modelo e headers compartilhados prioriza auditabilidade e portabilidade sobre a conveniência de um framework Python.

**A verificar:** a relação entre os 121 repositórios públicos e o colibri, e se há contribuições relevantes fora deste projeto.

## Relações

- **Criou:** [colibri](../repos/github.com/justvugg/colibri.md).
- **Conceitos:** [Streaming de experts em MoE](../concepts/streaming-de-experts-em-moe.md), [Model Context Protocol (MCP)](../concepts/model-context-protocol.md).
- **Associado a:** Z.ai (GLM), Moonshot AI (Kimi), Alibaba Qwen, DeepSeek, Xiaomi (MiMo), Thinking Machines (Inkling), Allen AI (OLMoE), Convai Innovations (Laya), fastino (GLiNER2.5-Decide) e Cloudflare (Clef) — autores dos modelos que o colibri executa, segundo os agradecimentos do README.

## Fontes

- https://github.com/JustVugg — perfil, bio, data de criação, repositórios públicos e seguidores via API do GitHub em 2026-10-19.
- https://github.com/JustVugg/colibri — README no commit `e0db083cdc9e563e0766cc6fc661ef23c32298e0`; metadados do repositório observados em 2026-10-19.
