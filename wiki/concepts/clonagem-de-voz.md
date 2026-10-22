---
type: concept
aliases: [Voice cloning, Clonagem de voz, Zero-shot TTS, Clonagem de timbre]
status: draft
created: 2026-10-19
updated: 2026-10-23
tags: [audio, tts, voz, modelos]
---

# Clonagem de voz

> Técnica de text-to-speech que reproduz o timbre de um locutor a partir de uma amostra curta de áudio de referência, podendo gerar fala em outro idioma ou estilo sem que esse locutor ou idioma tenha aparecido no treino do modelo.

## Definição

Clonagem de voz zero-shot separa duas coisas que um TTS tradicional funde: o **conteúdo** da fala (o texto) e o **timbre** do locutor (tone color). Um modelo zero-shot extrai o timbre de uma amostra de referência em tempo de inferência, sem precisar que esse locutor específico — ou mesmo o idioma da amostra — tenha sido visto durante o treino. Isso contrasta com abordagens que exigem fine-tuning por locutor.

A dimensão "cross-lingual" é uma consequência direta disso: nem o idioma da amostra de referência nem o idioma do texto gerado precisam estar no mesmo par visto no treino multi-locutor e multilíngue do modelo.

## Como funciona

O padrão observado no [myshell-ai/OpenVoice](../repos/github.com/myshell-ai/openvoice.md), descrito apenas em nível de capacidades pelo README (a arquitetura detalhada está no paper, não no texto do repositório):

- **Clonagem de timbre:** uma amostra de referência fornece o timbre; o modelo gera fala nova com esse timbre.
- **Controle de estilo:** parâmetros de emoção, acento, ritmo, pausas e entonação podem ser ajustados independentemente do timbre clonado.
- **Zero-shot cross-lingual:** nem o idioma de saída nem o idioma da referência precisam estar no conjunto de treino multi-locutor e multilíngue.

## Onde aparece

- [myshell-ai/OpenVoice](../repos/github.com/myshell-ai/openvoice.md) — V1 com as três capacidades acima; V2 (abril de 2024) com melhor qualidade de áudio, suporte nativo a seis idiomas (inglês, espanhol, francês, chinês, japonês, coreano) e uso comercial livre sob MIT.
- [debpalash/VoiceStudio](../repos/github.com/debpalash/voicestudio.md) — empacota clonagem e design de voz junto com dublagem de vídeo, dictation, transcrição e audiobook em 646 idiomas, com API/MCP local; "Model Manager" versiona avisos de licença por modelo de voz, embora o próprio README diga que isso não certifica uso comercial.
- [duixcom/Duix-Avatar](../repos/github.com/duixcom/duix-avatar.md) — combina clonagem de voz com clonagem de aparência e lip-sync para gerar vídeo de avatar digital; ver [Geração de imagem e vídeo com modelos de difusão](geracao-de-imagem-e-video-com-difusao.md) para a parte visual.

## Trade-offs

- **Vantagens:** clona com poucos segundos de áudio, sem re-treinar por locutor; separa conteúdo de timbre, permitindo controle de estilo independente; licenças permissivas (MIT, no caso do OpenVoice V2) viabilizam uso comercial.
- **Limitações:** qualidade objetiva (MOS, similaridade de locutor) depende do modelo e raramente é publicada de forma comparável entre projetos; a mesma capacidade que permite clonar uma voz legítima também permite impersonação sem consentimento. O VoiceStudio é o primeiro projeto desta wiki a tratar o problema explicitamente — recomenda clonar só com permissão e versiona avisos de licença por modelo —, mas o próprio README deixa claro que essa camada não enforça nem certifica a permissão; os demais projetos não discutem salvaguardas.
- **Questão de política:** diferente de scraping ou automação de browser, aqui o risco não é de acesso a dados, mas de uso da própria saída (uma voz sintética, ou um vídeo de avatar inteiro no caso do Duix-Avatar) para enganar terceiros. Nenhum dos projetos impõe watermarking por padrão.

## Relações

- **Relacionado a:** [LLMs compactos on-device](llms-compactos-on-device.md) — mesmo objetivo de eficiência e implantação ampla, em domínio de modelo diferente (áudio vs. texto); [Geração de imagem e vídeo com modelos de difusão](geracao-de-imagem-e-video-com-difusao.md) — o Duix-Avatar combina os dois domínios; [Model Context Protocol (MCP)](model-context-protocol.md) — VoiceStudio expõe a clonagem via MCP para agentes.
- **Contrasta com:** TTS tradicional por locutor único, que exige dados de treino daquele locutor específico; dublagem humana; transcrição pura (speech-to-text), como em [cjpais/Handy](../repos/github.com/cjpais/handy.md), que é o problema inverso (voz → texto, não texto → voz).
- **Distingue-se de:** detecção de deepfake de voz — um problema de verificação, não de geração, e que não é tratado pelas fontes lidas nesta wiki.

## Perguntas abertas

- Qual a qualidade objetiva (MOS, similaridade de locutor) do OpenVoice em comparação com sistemas comerciais mais recentes?
- Que salvaguardas — técnicas (watermarking) ou de política — existem ou deveriam existir para clonagem de voz zero-shot?
- Como a comunidade de pesquisa mede "zero-shot cross-lingual" de forma comparável entre projetos?
- O "reviewed-file preview" do Model Manager do VoiceStudio reduz na prática o uso sem consentimento, ou é apenas um registro informativo?

## Fontes

- [myshell-ai/OpenVoice](../repos/github.com/myshell-ai/openvoice.md) — README no commit `74a1d147b17a8c3092dd5430504bd83ef6c7eb23` (consultado em 2026-10-19). Somente o README foi lido; o paper (arXiv:2312.01479) e o código não foram consultados.
- [debpalash/VoiceStudio](../repos/github.com/debpalash/voicestudio.md) — README no commit `37996099869fdc18b8b1138ccbf6f2997de1fe73` (consultado em 2026-10-23).
- [duixcom/Duix-Avatar](../repos/github.com/duixcom/duix-avatar.md) — README no commit `1328feb5871448c8fa3d0e45b3bbc87e7c1d458a` (consultado em 2026-10-23).
