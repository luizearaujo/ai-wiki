---
type: repo
url: https://github.com/duixcom/Duix-Avatar
host: github.com
owner: duixcom
repo: Duix-Avatar
commit: 1328feb5871448c8fa3d0e45b3bbc87e7c1d458a
license: licença própria (ver nota)
language: C
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [avatar-digital, clonagem-de-voz, geracao-de-video]
---

# duixcom/Duix-Avatar

> Ferramenta de síntese de vídeo totalmente offline que clona aparência e voz de uma pessoa para gerar vídeos de um avatar digital a partir de texto ou fala.

## O que é

Duix.Avatar resolve o problema de criar vídeos com "humano digital" sem o custo de pipelines 3D tradicionais: clona rosto e voz de uma pessoa real a partir de dados de vídeo, e deixa o usuário gerar novos vídeos digitando texto ou falando, sem conexão à internet. O README situa o projeto como a versão aberta e gratuita da tecnologia comercial da Duix.com, que já teria produzido mais de 500 mil avatares personalizados para empresas.

## Como funciona

Três camadas técnicas, segundo o README: clonagem de voz (geração de voz similar a partir de amostra, com controle de contexto, intonação e velocidade), reconhecimento automático de fala (ASR) e visão computacional para sincronização labial entre áudio e vídeo. O app roda via três serviços Docker (`guiji2025/fun-asr` para ASR, `guiji2025/fish-speech-ziming` para TTS, `guiji2025/duix.avatar` para o core) orquestrados por `docker-compose`, com um cliente desktop separado (Windows `.exe` ou Linux `.AppImage`). Expõe APIs HTTP locais para treino de modelo, síntese de áudio e síntese de vídeo, documentadas no próprio README com exemplos de requisição.

## Instalação e uso rápido

- **Pré-requisitos**: Node.js 18, Docker, e (fortemente recomendado) GPU NVIDIA com driver instalado.
- **Windows**: WSL + Docker Desktop; `docker-compose up -d` no diretório `/deploy` (ou `docker-compose-lite.yml` para a versão leve com um único serviço); cliente via instalador oficial.
- **Ubuntu 22.04**: `docker.io` + `docker-compose` + NVIDIA Container Toolkit; `docker-compose -f docker-compose-linux.yml up -d`; cliente via `.AppImage`.
- Requisitos de hardware citados: CPU i5-13400F, 32GB RAM, GPU RTX 4070, disco D com 30GB livres e disco C com 100GB livres (para as imagens de serviço); suporte específico para GPUs da série 50 da NVIDIA.

## Exemplos de uso

- Separar um vídeo em vídeo mudo + áudio, treinar um modelo de voz a partir do áudio e then gerar novas falas por texto — fluxo descrito na seção "Model Training" do README.
- Chamar `http://127.0.0.1:8383/easy/submit` com um áudio e um vídeo de referência para sintetizar um novo vídeo com lip-sync — exemplo do README.

## Quando usar (e quando não usar)

- **Use quando:** precisa gerar vídeos de um avatar digital clonado totalmente offline, com controle total do pipeline e sem custo de API comercial, e tem uma GPU NVIDIA disponível.
- **Evite quando:** precisa de qualidade "estonteante" e suporte dedicado sem manter infraestrutura própria — o próprio README recomenda, nesse caso, o serviço comercial de API da Duix.com; ou quando não há GPU NVIDIA disponível, já que os três serviços não iniciam sem ela.

## Limitações e cuidados

- Licenciamento não é um SPDX simples: o README remete ao arquivo `LICENSE` do repositório, mas a tabela de comparação do próprio README afirma suporte a "uso comercial global gratuito", com a ressalva de que empresas com mais de 100 mil usuários ou receita anual acima de US$ 10 milhões precisam assinar um acordo de licença comercial separado. **A verificar**: o texto completo do `LICENSE` não foi lido.
- O README não detalha o que acontece com os dados de voz/rosto processados localmente, nem oferece benchmarks formais de qualidade do lip-sync.
- Suporte a distribuições Linux além do Ubuntu 22.04 é declarado "teórico", não testado.
- Apenas o README foi lido; código-fonte (`src/main/service/*`), imagens Docker e os três repositórios de serviço (`fun-asr`, `fish-speech-ziming`) não foram consultados.

## Estado e adoção

- Versão/releases citadas no README: builds oficiais em [Releases](https://github.com/duixcom/Duix.Avatar/releases); última release no GitHub, `v1.0.6` (2025-09-28).
- Atividade e popularidade observadas em 2026-10-23: 16.022 estrelas, 2.736 forks (GitHub API); push em 2026-04-21.
- Licença: não detectada pela API do GitHub (`NOASSERTION`); README remete ao arquivo `LICENSE` com condições de uso comercial descritas na tabela comparativa.

## Relações

- Mantido por: [Duix](../../../entities/duixcom.md).
- Conceitos: [Clonagem de voz](../../../concepts/clonagem-de-voz.md), [Geração de imagem e vídeo com modelos de difusão](../../../concepts/geracao-de-imagem-e-video-com-difusao.md).
- Alternativas: [debpalash/VoiceStudio](../debpalash/voicestudio.md) — cobre apenas a parte de voz (clonagem, design, dublagem), sem geração de vídeo/avatar visual.

## Perguntas abertas

- Qual é a taxa real de sucesso do lip-sync em condições de áudio/vídeo variadas, fora dos exemplos de demonstração?
- O que exatamente o acordo de licença comercial exige além dos limiares de usuários/receita citados na tabela?

## Fontes

- README: https://raw.githubusercontent.com/duixcom/Duix-Avatar/1328feb5871448c8fa3d0e45b3bbc87e7c1d458a/README.md (commit `1328feb5871448c8fa3d0e45b3bbc87e7c1d458a`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
