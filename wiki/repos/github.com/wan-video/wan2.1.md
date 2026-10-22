---
type: repo
url: https://github.com/Wan-Video/Wan2.1
host: github.com
owner: Wan-Video
repo: Wan2.1
commit: 9737cba9c1c3c4d04b33fcad41c111989865d315
license: Apache-2.0
language: Python
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [geracao-de-video, modelo-aberto, difusao]
---

# Wan-Video/Wan2.1

> Suíte aberta de modelos de base para geração de vídeo e imagem — texto-para-vídeo, imagem-para-vídeo, edição de vídeo e texto-para-imagem — da Alibaba, com pesos abertos em Apache-2.0.

## O que é

Wan2.1 resolve o problema de gerar vídeo (e imagem) a partir de texto ou imagem com um modelo aberto competitivo com soluções fechadas, incluindo suporte a GPUs de consumo. O README reivindica desempenho SOTA entre modelos abertos, geração de texto visual em chinês e inglês dentro do próprio vídeo, e um VAE de vídeo (Wan-VAE) capaz de codificar/decodificar vídeos 1080P de qualquer duração preservando informação temporal.

## Como funciona

Arquitetura de Diffusion Transformer sobre o paradigma Flow Matching, com um T5 Encoder multilíngue e cross-attention em cada bloco do transformer para incorporar o texto; um MLP compartilhado entre blocos prediz seis parâmetros de modulação por timestep, com biases distintos por bloco. O Wan-VAE é um VAE 3D causal próprio, desenhado para compressão espaço-temporal eficiente e causalidade temporal. O repositório oferece múltiplos checkpoints (T2V-14B, T2V-1.3B, I2V-14B em 480P/720P, FLF2V-14B, VACE-1.3B/14B) e integra-se a ComfyUI, Diffusers e Gradio.

## Instalação e uso rápido

- **Dependências**: `git clone` + `pip install -r requirements.txt` (torch ≥2.4.0).
- **Download de pesos**: via `huggingface-cli` ou `modelscope` (modelos hospedados no Hugging Face e ModelScope, não neste repositório).
- **Inferência single-GPU**: `python generate.py --task t2v-14B --size 1280*720 --ckpt_dir ./Wan2.1-T2V-14B --prompt "..."`. O modelo 1.3B roda em GPUs de consumo (8,19 GB VRAM) com `--offload_model True --t5_cpu`.
- **Multi-GPU**: FSDP + xDiT USP (estratégias Ulysses ou Ring) via `torchrun`.
- **Extensão de prompt**: via API Dashscope ou modelo Qwen local, melhora a riqueza de detalhes do vídeo gerado.
- Também disponível via `diffusers` (`WanPipeline`, `WanImageToVideoPipeline`) e Gradio local.

## Exemplos de uso

- Gerar um vídeo 720P de 5 segundos a partir de um prompt de texto em uma única GPU — exemplo do próprio README.
- Animar uma imagem estática (image-to-video) com um prompt descritivo, usando o checkpoint I2V-14B-720P — exemplo do README.
- Usar VACE para edição de vídeo condicionada por vídeo, máscara e imagens de referência.

## Quando usar (e quando não usar)

- **Use quando:** precisa de um modelo de vídeo aberto e competitivo, com pesos Apache-2.0, que roda tanto em GPUs de consumo (1.3B) quanto em clusters multi-GPU (14B), e quer integrá-lo a ComfyUI ou Diffusers.
- **Evite quando:** quer uma interface pronta sem lidar com checkpoints e scripts de inferência — nesse caso, [Comfy-Org/ComfyUI](../comfy-org/comfyui.md) (que já integra Wan2.1 como nó) é o caminho mais direto.

## Limitações e cuidados

- Comparações de desempenho (SOTA, avaliação manual) são do próprio projeto, com conjunto de prompts e pesos de avaliação definidos internamente — tratadas como afirmações datadas, não benchmark independente.
- O modelo 1.3B é instável em 720P segundo o próprio README, que recomenda 480P para esse checkpoint.
- O README não detalha mitigação de uso indevido alem da cláusula de licença (ver abaixo); não há filtro de conteúdo documentado no próprio repositório.
- Apenas o README foi lido; código de treino, scripts de avaliação e pesos (hospedados externamente) não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: sem tags de release no GitHub; checkpoints versionados no Hugging Face/ModelScope (T2V-14B/1.3B, I2V-14B-480P/720P, FLF2V-14B, VACE-1.3B/14B).
- Atividade e popularidade observadas em 2026-10-23: 17.272 estrelas, 3.880 forks (GitHub API); push em 2026-03-05.
- Licença: Apache-2.0 para os modelos deste repositório; o README isenta os mantenedores de responsabilidade sobre o conteúdo gerado pelo usuário, que deve respeitar leis aplicáveis.

## Relações

- Mantido por: [Wan](../../../entities/wan-video.md) (Alibaba Cloud).
- Conceitos: [Geração de imagem e vídeo com modelos de difusão](../../../concepts/geracao-de-imagem-e-video-com-difusao.md).
- Alternativas: integra-se, não concorre, com [Comfy-Org/ComfyUI](../comfy-org/comfyui.md), que executa Wan2.1 como um dos motores de geração de vídeo suportados.

## Perguntas abertas

- Como o desempenho do Wan2.1 se compara a modelos fechados mais recentes fora do conjunto de 1.035 prompts internos usado na avaliação do próprio projeto?
- Que garantias de proveniência (watermarking, metadados) o projeto oferece para conteúdo gerado, se alguma?

## Fontes

- README: https://raw.githubusercontent.com/Wan-Video/Wan2.1/9737cba9c1c3c4d04b33fcad41c111989865d315/README.md (commit `9737cba9c1c3c4d04b33fcad41c111989865d315`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
