---
type: concept
aliases: [Geração de vídeo com difusão, Diffusion models, Text-to-video, Modelos de difusão de imagem e vídeo]
status: draft
created: 2026-10-23
updated: 2026-10-23
tags: [difusao, geracao-de-imagem, geracao-de-video, inferencia-local]
---

# Geração de imagem e vídeo com modelos de difusão

> Modelos de base e motores de execução que geram ou editam imagem, vídeo e avatares digitais a partir de texto, imagem ou voz, por difusão — localmente em hardware de consumo ou via grafo visual de nós.

## Definição

Este padrão cobre três papéis que se combinam na prática: o **modelo de base** (pesos treinados que fazem a geração em si), o **motor/GUI de execução** (que orquestra modelos, checkpoints e pós-processamento) e a **aplicação final** (que empacota um caso de uso específico, como um avatar digital). Os três projetos da wiki que ocupam esse espaço — [Wan-Video/Wan2.1](../repos/github.com/wan-video/wan2.1.md) (modelo), [Comfy-Org/ComfyUI](../repos/github.com/comfy-org/comfyui.md) (motor/GUI) e [duixcom/Duix-Avatar](../repos/github.com/duixcom/duix-avatar.md) (aplicação) — ilustram cada papel, e o próprio Wan2.1 roda como um nó dentro do ComfyUI.

A pressão comum é rodar modelos grandes em hardware limitado: VRAM de GPUs de consumo (4GB a 24GB) é ordens de magnitude menor que o necessário para manter um modelo de difusão inteiro residente, o que empurra os três projetos para técnicas de offloading, streaming ou quantização.

## Como funciona

| Componente | Papel | Exemplo |
|---|---|---|
| **Modelo de base** | Pesos treinados para a tarefa generativa | Wan2.1 (T2V, I2V, VACE), checkpoints citados pelo ComfyUI (SDXL, Flux.1, HunyuanVideo) |
| **VAE de domínio** | Comprime/descomprime o espaço latente preservando qualidade | Wan-VAE (3D causal, 1080P de qualquer duração) |
| **Motor de execução** | Orquestra modelos, memória e fila de trabalho | ComfyUI (grafo de nós, fila assíncrona, re-execução parcial) |
| **Gestão de VRAM** | Permite rodar modelos maiores que a memória disponível | Weight streaming assíncrono (ComfyUI), offload de modelo + T5 em CPU (Wan2.1) |
| **Extensão de prompt** | Enriquece o prompt do usuário antes da geração | Modelo Qwen local ou API Dashscope (Wan2.1) |
| **Aplicação final** | Empacota um caso de uso específico para o usuário final | Duix.Avatar (clonagem de aparência/voz + lip-sync) |
| **Paralelização multi-GPU** | Distribui a geração entre várias GPUs | FSDP + xDiT (estratégias Ulysses/Ring) no Wan2.1 |

A escolha estrutural central é **onde a memória é trocada por latência**: ComfyUI faz streaming assíncrono de pesos do disco/RAM para a GPU conforme necessário (mesmo princípio de troca memória↔latência do [JustVugg/colibri](../repos/github.com/justvugg/colibri.md) para MoE de texto); Wan2.1 oferece offloading explícito de partes do modelo para CPU; Duix-Avatar evita o problema delegando a três serviços Docker especializados, cada um otimizado para sua tarefa (ASR, TTS, síntese de vídeo).

## Onde aparece

- [Wan-Video/Wan2.1](../repos/github.com/wan-video/wan2.1.md) — suíte aberta de modelos de vídeo/imagem (Diffusion Transformer + Flow Matching), com checkpoints de 1.3B a 14B, Apache-2.0.
- [Comfy-Org/ComfyUI](../repos/github.com/comfy-org/comfyui.md) — GUI/backend de nós que executa modelos de difusão de terceiros, com weight streaming assíncrono para hardware limitado.
- [duixcom/Duix-Avatar](../repos/github.com/duixcom/duix-avatar.md) — aplicação offline que combina clonagem de voz e de aparência para gerar vídeos de avatar digital com lip-sync.

## Trade-offs

- **Vantagens:** permite gerar/editar mídia em hardware de consumo sem depender de API paga; a separação entre modelo, motor e aplicação permite reusar o mesmo modelo em diferentes interfaces (Wan2.1 roda tanto via CLI quanto dentro do ComfyUI).
- **Limitações:** qualidade e velocidade variam fortemente com o hardware disponível; benchmarks de "SOTA" costumam ser do próprio projeto, com conjunto de avaliação e pesos definidos internamente; aplicações que clonam voz/aparência (Duix-Avatar) levantam questões de consentimento e uso indevido não resolvidas pela ferramenta em si.
- **Critério prático:** para prototipar rápido com controle visual, prefira um motor de nós (ComfyUI); para integrar um modelo específico ao próprio pipeline, use a biblioteca do modelo direto (Wan2.1); para um caso de uso fechado e pronto, uma aplicação (Duix-Avatar) exige menos configuração mas menos flexibilidade.

## Relações

- **Relacionado a:** [Streaming de experts em MoE](streaming-de-experts-em-moe.md) — mesmo princípio de troca memória↔latência, aplicado a difusão em vez de MoE de texto; [Clonagem de voz](clonagem-de-voz.md) — Duix-Avatar combina esse domínio com geração visual; [LLMs compactos on-device](llms-compactos-on-device.md) — mesma pressão por rodar modelos grandes em hardware limitado, em domínio de texto.
- **Contrasta com:** geração de mídia por pipeline agêntico declarado (OpenMontage, HyperFrames), que compõe ativos já gerados em vez de treinar/rodar o modelo generativo em si.
- **Depende de:** GPU (ou fallback CPU/NPU mais lento), VAE de domínio e, para qualidade máxima, extensão de prompt por um segundo modelo.

## Perguntas abertas

- Como comparar de forma independente (fora dos benchmarks internos de cada projeto) a qualidade de geração entre Wan2.1 e concorrentes fechados?
- Que garantias de proveniência (watermarking, metadados C2PA) os três projetos oferecem para o conteúdo gerado, se alguma?
- Como a técnica de weight streaming do ComfyUI se compara, em throughput real, ao offloading explícito do Wan2.1 para o mesmo modelo?

## Fontes

- [Wan-Video/Wan2.1](../repos/github.com/wan-video/wan2.1.md) — README no commit `9737cba9c1c3c4d04b33fcad41c111989865d315` (consultado em 2026-10-23).
- [Comfy-Org/ComfyUI](../repos/github.com/comfy-org/comfyui.md) — README no commit `1a82e6d01f395b43275c77acd289af1eb7090bb9` (consultado em 2026-10-23).
- [duixcom/Duix-Avatar](../repos/github.com/duixcom/duix-avatar.md) — README no commit `1328feb5871448c8fa3d0e45b3bbc87e7c1d458a` (consultado em 2026-10-23).
