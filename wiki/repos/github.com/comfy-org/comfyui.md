---
type: repo
url: https://github.com/Comfy-Org/ComfyUI
host: github.com
owner: Comfy-Org
repo: ComfyUI
commit: 1a82e6d01f395b43275c77acd289af1eb7090bb9
license: GPL-3.0
language: Python
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [difusao, geracao-de-imagem, geracao-de-video, inferencia-local]
---

# Comfy-Org/ComfyUI

> GUI, API e backend modular de nós para modelos de difusão — imagem, vídeo, 3D e áudio — otimizado para hardware de consumo local.

## O que é

ComfyUI resolve o problema de orquestrar modelos de difusão (checkpoints, VAEs, text encoders, LoRAs, ControlNets, upscalers) em um pipeline visual sem escrever código, com controle total sobre cada parâmetro. O README o descreve como o motor de inferência mais otimizado para difusão do mundo, com foco em hardware de consumo local, capaz de rodar os maiores modelos open source com apenas 4GB de VRAM + 8GB de RAM via "weight streaming" assíncrono.

## Como funciona

Interface de grafo de nós: cada etapa de um workflow (carregar modelo, codificar prompt, amostrar, decodificar, salvar) é um nó conectável, reutilizável como subgrafo ou template. Execução eficiente via fila assíncrona, re-execução parcial do grafo (só roda o que mudou desde a última execução) e gestão inteligente de VRAM/RAM com offloading de modelo. O README organiza o projeto em três repositórios interligados: **ComfyUI Core** (este, releases a cada ~2 semanas), **Comfy Desktop** (app nativo que empacota o core estável) e **ComfyUI Frontend** (atualizado a cada 2+ semanas e mesclado ao core). "App Mode" expõe workflows complexos como UI simples; "Partner nodes" dão acesso a modelos fechados (Nano Banana, Seedance, Hunyuan3D) via API paga opcional.

## Instalação e uso rápido

- **App desktop** (recomendado, Windows/macOS): [comfy.org/download](https://www.comfy.org/download).
- **Portable standalone** (Windows, NVIDIA/AMD/Intel): download direto do `.7z` nas releases.
- **`comfy-cli`**: `pip install comfy-cli && comfy install`.
- **Manual** (Windows/Linux): clonar o repositório, colocar checkpoints em `models/checkpoints`, instalar PyTorch (comando varia por GPU: NVIDIA/AMD ROCm/Intel XPU/Ascend NPU/Cambricon MLU/Iluvatar Corex) e `pip install -r requirements.txt`; rodar com `python main.py`.
- **Nuvem**: Comfy Cloud, oferta paga oficial para quem não tem hardware local.
- Flag `--offline` força todo o funcionamento embutido a ficar offline, desabilitando os nós pagos de parceiros; `--disable-partner-nodes` desabilita só esses nós.

## Exemplos de uso

- Montar um workflow de texto-para-imagem com Flux.1 ou SDXL a partir dos templates mantidos em comfy.org/workflows — exemplo do README.
- Rodar um modelo de vídeo (Wan 2.1/2.2, HunyuanVideo, LTX-Video) como um dos nós do grafo — citado na lista de modelos suportados do README.
- Expor um workflow pronto como API local para integrar a outra aplicação, via as "API endpoints" citadas no README.

## Quando usar (e quando não usar)

- **Use quando:** quer controle total sobre cada parâmetro de um pipeline de difusão (imagem, vídeo, 3D, áudio), rodando localmente em hardware limitado, com a maior cobertura de modelos open source do ecossistema.
- **Evite quando:** só precisa gerar uma imagem simples sem granularidade de pipeline — uma interface mais direta (ou a API de um provedor fechado) exige menos curva de aprendizado que o grafo de nós.

## Limitações e cuidados

- O repositório foi transferido do mantenedor original `comfyanonymous` para a organização `Comfy-Org`; a URL antiga redireciona para a atual, mas vários links e badges do próprio README ainda apontam para `comfyanonymous/ComfyUI` e `comfyanonymous.github.io`, não atualizados para o novo owner.
- O README não detalha o modelo de dados dos "Partner nodes" pagos (o que é enviado a terceiros) além de citar que usam a API paga do Comfy.
- Compatibilidade de hardware exótico (Ascend NPU, Cambricon MLU, Iluvatar Corex) é descrita, mas não testada de forma independente pela wiki.
- Apenas o README foi lido; código-fonte, `ComfyUI-Manager`, `ComfyUI_frontend` e os workflows de exemplo não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: ciclo semanal/quinzenal (meta é segunda-feira); última release no GitHub, `v0.42.1` (2026-10-19).
- Atividade e popularidade observadas em 2026-10-23: 141.874 estrelas, 16.729 forks (GitHub API); push em 2026-10-22.
- Licença: GPL-3.0 para o core; o frontend é publicado separadamente no PyPI como dependência.

## Relações

- Mantido por: [Comfy Org](../../../entities/comfy-org.md).
- Conceitos: [Geração de imagem e vídeo com modelos de difusão](../../../concepts/geracao-de-imagem-e-video-com-difusao.md); também relevante para [Streaming de experts em MoE](../../../concepts/streaming-de-experts-em-moe.md) pela técnica de weight streaming assíncrono que permite rodar grandes modelos com pouca VRAM — mesmo padrão de troca memória↔latência já visto no [JustVugg/colibri](../justvugg/colibri.md), aplicado a difusão em vez de MoE de texto.
- Alternativas: executa modelos como [Wan-Video/Wan2.1](../wan-video/wan2.1.md) como um dos motores suportados, em vez de concorrer com ele.

## Perguntas abertas

- Como o "weight streaming" assíncrono se compara, em throughput e latência, ao streaming de experts do colibri?
- Que garantias de privacidade e retenção de dados o Comfy API Nodes oferece para os "Partner nodes" fechados?

## Fontes

- README: https://raw.githubusercontent.com/Comfy-Org/ComfyUI/1a82e6d01f395b43275c77acd289af1eb7090bb9/README.md (commit `1a82e6d01f395b43275c77acd289af1eb7090bb9`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
