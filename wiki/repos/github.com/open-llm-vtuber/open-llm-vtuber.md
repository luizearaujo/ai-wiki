---
type: repo
url: https://github.com/Open-LLM-VTuber/Open-LLM-VTuber
host: github.com
owner: open-llm-vtuber
repo: open-llm-vtuber
commit: 992309c0aa19845960228f880013d4685fde93b5
license: MIT
language: Python
status: maintenance
created: 2026-10-24
ingested: 2026-10-24
updated: 2026-10-24
tags: [clonagem-de-voz]
---

# Open-LLM-VTuber/Open-LLM-VTuber

> Companheiro de IA interativo por voz, com percepção visual e avatar Live2D, capaz de rodar inteiramente offline — alternativa open-source ao AI VTuber de código fechado neuro-sama.

## O que é

O objetivo declarado do projeto é recriar com soluções open-source, capazes de rodar offline em qualquer plataforma além do Windows, a proposta do VTuber de IA de código fechado `neuro-sama` — daí o nome "Open-LLM-VTuber" em vez de "Open-LLM-Companion" ou "Open-LLM-Waifu". Funciona como companheiro configurável (persona livre: "virtual girlfriend", "boyfriend", pet ou qualquer personagem), com conversa de voz em tempo real, visão (câmera, gravação de tela, screenshots) e um avatar Live2D animado, em modo web ou app desktop — incluindo um modo "pet de desktop" com fundo transparente e clique-através.

## Como funciona

Arquitetura modular trocável por arquivo de configuração, sem tocar em código:

- **LLM:** Ollama, qualquer API compatível com OpenAI, Gemini, Claude, Mistral, DeepSeek, Zhipu AI, GGUF, LM Studio, vLLM.
- **ASR (reconhecimento de fala):** sherpa-onnx, FunASR, Faster-Whisper, Whisper.cpp, Whisper, Groq Whisper, Azure ASR.
- **TTS (síntese de fala):** sherpa-onnx, pyttsx3, MeloTTS, Coqui-TTS, GPTSoVITS, Bark, CosyVoice, Edge TTS, Fish Audio, Azure TTS.
- **Agente plugável:** interface de Agent que pode ser implementada para integrar outras arquiteturas (HumeAI EVI, OpenAI Her, Mem0 citados como exemplos).

Recursos de interação: interrupção de voz sem fone (o sistema não "escuta" sua própria fala), feedback por toque/arraste, mapeamento de expressões Live2D, exibição dos "pensamentos internos" da IA sem que sejam falados, fala proativa da IA, persistência de histórico de chat, e tradução de TTS (ex.: conversar em chinês enquanto a IA responde em japonês).

## Instalação e uso rápido

O README não traz os passos de instalação — remete à [documentação oficial](https://open-llm-vtuber.github.io/docs/quick-start). Atualização para quem já tem v1.0.0+: `uv run update.py` (versões anteriores a v1.0.0 exigem reinstalação completa, por mudança incompatível em `conf.yaml`). Acesso remoto (servidor em uma máquina, uso em outra, como um celular) exige HTTPS via proxy reverso, porque o microfone só funciona em contexto seguro do navegador.

## Quando usar (e quando não usar)

- **Use quando:** quiser um companheiro de IA com voz, visão e avatar Live2D rodando localmente/offline, com liberdade de trocar LLM, ASR e TTS por configuração.
- **Evite quando:** precisar de memória de longo prazo — o README diz que esse recurso foi "temporariamente removido" e "está voltando em breve", sem data.
- **Evite quando:** depender de novas funcionalidades estáveis a curto prazo — o projeto pede explicitamente que não se abram issues/PRs de feature request para a v1, já que o esforço de desenvolvimento migrou para a v2 (reescrita completa, em fase de discussão).

## Limitações e cuidados

- **v1 em modo de manutenção, v2 em planejamento.** O README pede para represar pedidos de funcionalidade da v1 e direciona para o Zulip da comunidade de desenvolvimento da v2, "uma reescrita completa" ainda em discussão e planejamento inicial — por isso o `status` desta página é `maintenance`, não `active`.
- **Memória de longo prazo ausente.** Removida temporariamente; conversas persistem via log de chat, mas não há memória estruturada de longo prazo no momento.
- **Licenciamento misto e ambíguo.** O README atribui licença MIT ao projeto, mas a API do GitHub reporta `NOASSERTION` para o repositório — não verificado qual arquivo de licença está de fato publicado. Os modelos de amostra Live2D incluídos são licenciados separadamente pela Live2D Inc. (Live2D Free Material License + Terms of Use), não pela licença do projeto; uso comercial por empresas médias/grandes pode exigir permissão adicional da Live2D Inc., segundo o próprio README.
- Push mais recente registrado em 2026-05-15, bem anterior à data desta ingestão — consistente com o anúncio de que o foco migrou para a v2.

## Estado e adoção

- Observado em 2026-10-24: 14.356 stars, 1.727 forks, 160 issues abertas; push mais recente em 2026-05-15.
- Licença: MIT segundo o README (ver ressalva acima sobre `NOASSERTION` na API e a licença separada dos modelos Live2D de amostra).

## Relações

- Mantido por: organização `Open-LLM-VTuber`.
- Conceitos: [Clonagem de voz](../../../concepts/clonagem-de-voz.md) — GPT-SoVITS é um dos back-ends de TTS suportados, e o README menciona clonagem de voz como forma de personalizar o companheiro, mas o foco do projeto é a interação em tempo real (ASR+TTS+avatar), não a técnica de clonagem em si.
- Contrasta com: [duixcom/Duix-Avatar](../duixcom/duix-avatar.md) — Duix-Avatar gera vídeo de avatar pré-renderizado (clonagem de voz + aparência, offline, mas não interativo em tempo real); Open-LLM-VTuber é uma sessão de conversa ao vivo com um avatar Live2D 2D animado por tempo real, não um vídeo gerado.
- Projetos relacionados citados no README: [ylxmf2005/LLM-Live2D-Desktop-Assitant](https://github.com/ylxmf2005/LLM-Live2D-Desktop-Assitant) (assistente de desktop similar, com controle total do computador).

## Perguntas abertas

- Qual arquivo de licença está de fato no repositório, já que a API do GitHub não a identifica?
- Quando a memória de longo prazo volta, e em que formato?
- A v2 (reescrita completa) chega a ter uma primeira versão pública, ou o projeto se estabiliza na v1 em modo de manutenção?

## Fontes

- README: https://raw.githubusercontent.com/Open-LLM-VTuber/Open-LLM-VTuber/992309c0aa19845960228f880013d4685fde93b5/README.md (commit `992309c0aa19845960228f880013d4685fde93b5`, consultado em 2026-10-24). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados da API do GitHub, consultados em 2026-10-24.
