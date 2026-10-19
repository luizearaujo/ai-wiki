---
type: repo
url: https://github.com/myshell-ai/OpenVoice
host: github.com
owner: myshell-ai
repo: openvoice
commit: 74a1d147b17a8c3092dd5430504bd83ef6c7eb23
license: MIT
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [tts, voz, clonagem-de-voz, audio, mit]
---

# myshell-ai/OpenVoice

> Modelo de clonagem instantânea de voz: a partir de uma amostra curta de áudio, reproduz o timbre do locutor em qualquer idioma suportado, com controle granular de estilo, sem precisar daquele locutor ou daquele idioma no treino.

## O que é

OpenVoice é um modelo de text-to-speech com foco em clonagem de timbre (tone color). O README resume três vantagens centrais: clonagem precisa do timbre de referência; controle flexível de estilo de voz (emoção, acento, ritmo, pausas, entonação); e clonagem de voz zero-shot cross-lingual — nem o idioma gerado nem o idioma da referência precisam estar no conjunto de treino multi-locutor e multilíngue do modelo.

O modelo já operava em produção: alimentou a clonagem de voz instantânea do myshell.ai desde maio de 2023, usado "dezenas de milhões de vezes" até novembro de 2023, segundo o README.

## Como funciona

O README não detalha a arquitetura interna (ela está no paper, não no texto do repositório). Publica duas gerações:

- **OpenVoice V1:** clonagem de timbre, controle de estilo e clonagem zero-shot cross-lingual, conforme o paper original (arXiv:2312.01479).
- **OpenVoice V2 (abril de 2024):** mantém as três capacidades do V1 e adiciona (1) melhor qualidade de áudio, por uma estratégia de treino diferente; (2) suporte nativo a seis idiomas — inglês, espanhol, francês, chinês, japonês e coreano; (3) uso comercial livre, com V1 e V2 relicenciadas sob MIT a partir de abril de 2024.

A implementação é baseada em três projetos de terceiros citados no README: TTS (Coqui), VITS e VITS2.

## Instalação e uso rápido

O README não publica comandos de instalação ou inferência diretamente; remete a `docs/USAGE.md` para instruções detalhadas e a `docs/QA.md` para perguntas frequentes — nenhum dos dois foi lido nesta ingestão.

## Exemplos de uso

Não há exemplos de código no README; o uso prático está documentado em `docs/USAGE.md` (não consultado). O README aponta um vídeo de demonstração e o site do projeto (research.myshell.ai/open-voice) como referências visuais.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é clonar o timbre de um locutor a partir de pouco áudio de referência, com controle de estilo e/ou geração cross-lingual, em um projeto que aceite MIT (uso comercial liberado desde abril de 2024).
- **Evite quando:** a aplicação precisa de qualidade state-of-the-art atual — o README não publica benchmark objetivo de qualidade (MOS, similaridade de locutor) nem comparação com sistemas mais recentes; ou quando o uso envolve risco de impersonação de voz sem consentimento, tema que o README não aborda.

## Limitações e cuidados

- **Somente o README foi lido.** `docs/USAGE.md`, `docs/QA.md`, o código do modelo e os pesos não foram inspecionados.
- O README não detalha a arquitetura do conversor de timbre nem publica métricas de qualidade objetivas nesta página — a descrição de capacidades é a do paper, citado mas não lido.
- Não há discussão, no README, de salvaguardas contra uso indevido (deepfake de voz, impersonação) — tema relevante para qualquer tecnologia de clonagem de voz.
- **Atividade recente baixa:** o último push observado na API do GitHub é de 2025-04-19, cerca de um ano e meio antes desta ingestão; o projeto parece estável/pouco mantido, não necessariamente abandonado.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~38,0 mil estrelas, ~4,3 mil forks, 314 issues abertas; criado em 2023-11-29, último push em 2025-04-19.
- **Licença:** MIT para V1 e V2 desde abril de 2024 (antes disso, V1 tinha licença mais restritiva, segundo o README).
- **Linguagem principal:** Python.

## Relações

- **Mantido por:** [MyShell (myshell-ai)](../../../entities/myshell-ai.md), com contribuição de pesquisadores do MIT e da Tsinghua University citados no README.
- **Conceitos:** [Clonagem de voz](../../../concepts/clonagem-de-voz.md) — página criada a partir desta ingestão para descrever a técnica.
- **Relacionado a:** TTS (Coqui), VITS e VITS2 — projetos de terceiros cuja implementação o OpenVoice adapta, segundo os agradecimentos do README.

## Perguntas abertas

- Qual é a arquitetura exata do extrator e do conversor de timbre, e como ela se compara em qualidade objetiva (MOS, similaridade de locutor) com sistemas mais recentes?
- O baixo ritmo de atividade recente reflete estabilização do projeto ou abandono?
- Que salvaguardas, se alguma, o projeto ou o myshell.ai aplicam contra uso indevido da clonagem de voz?

## Fontes

- README: https://github.com/myshell-ai/OpenVoice (commit `74a1d147b17a8c3092dd5430504bd83ef6c7eb23`, consultado em 2026-10-19). Somente o README foi lido; `docs/USAGE.md`, `docs/QA.md`, código e pesos não foram consultados.
- Metadados do repositório: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas).
- Perfil da organização: API do GitHub (`orgs/myshell-ai`) em 2026-10-19.
