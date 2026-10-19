---
type: repo
url: https://github.com/calesthio/OpenMontage
host: github.com
owner: calesthio
repo: openmontage
commit: c8066452325cb57c8fc1ba8c2a71b6e8842e6b65
license: AGPL-3.0
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, video, producao, pipelines, skills, remotion, ffmpeg]
---

# calesthio/OpenMontage

> Sistema de produção de vídeo agêntico em que o assistente de código do usuário é o orquestrador: ele pesquisa, escreve, gera ativos, edita e monta o vídeo seguindo pipelines declarados em YAML e skills em Markdown.

## O que é

O OpenMontage se apresenta como o primeiro sistema open-source de produção de vídeo agêntico. A proposta é transformar um assistente de código — Claude Code, Cursor, Copilot, Windsurf ou Codex — em um estúdio de produção: o usuário descreve o vídeo em linguagem natural e o agente conduz pesquisa, roteiro, geração de imagens e clipes, locução, trilha, legendas e composição final.

O README insiste em uma distinção: o projeto não apenas anima imagens estáticas. Ele também monta vídeos a partir de **filmagem real** de acervos livres (Archive.org, NASA, Wikimedia Commons, Pexels, Pixabay, Unsplash), recuperadas semanticamente e editadas em uma linha do tempo.

Números declarados: 10+ pipelines (12 segundo a descrição do repositório), 100+ ferramentas de produção, 60+ integrações de provedores e 700+ arquivos de skills e conhecimento de produção.

## Como funciona

A arquitetura é **agent-first**: não existe um orquestrador em código. O assistente de IA lê os manifestos e executa as etapas.

1. O agente lê um manifesto de pipeline em `pipeline_defs/` — etapas, ferramentas, critérios de revisão e gates.
2. Lê a skill de direção daquela etapa em `skills/pipelines/` — instruções Markdown de *como* executar.
3. Chama ferramentas Python registradas; a seleção de provedor é pontuada em sete dimensões (adequação à tarefa 30%, qualidade 20%, controle 15%, confiabilidade 15%, custo 10%, latência 5%, continuidade 5%).
4. Faz auto-revisão com a skill de revisor e grava um checkpoint JSON resumível com log de decisões e custo.
5. Pede aprovação humana nos pontos criativos (proposta, roteiro, plano de cenas, ativos e publicação).
6. Passa por validação pré-composição (promessa de entrega, risco de "slideshow", renderizador) e renderiza.
7. Executa auto-revisão pós-render com `ffprobe`, amostragem de frames, análise de áudio, verificação da promessa e checagem de legendas. Se falhar, o vídeo não é apresentado.

Fluxo comum a todos os pipelines:

```text
research -> proposal -> script -> scene_plan -> assets -> edit -> compose
```

A **pesquisa web** é uma etapa de primeira classe: o README afirma que o agente faz 15–25+ buscas em YouTube, Reddit, Hacker News, notícias e fontes acadêmicas antes de escrever o roteiro, e cita tudo em um briefing estruturado.

### Arquitetura em camadas

| Camada | Conteúdo | Papel |
|---|---|---|
| 1 | `tools/` e `pipeline_defs/` | O que existe: capacidades executáveis e orquestração |
| 2 | `skills/` | Como usar: convenções, playbooks e critérios de qualidade do OpenMontage |
| 3 | `.agents/skills/` | Como funciona: conhecimento técnico profundo de tecnologias externas |

Cada ferramenta declara quais skills da camada 3 usa. A composição pode ser feita com **Remotion** (React, padrão para explainers e conteúdo orientado a dados) ou **HyperFrames** (HTML/CSS/GSAP, padrão para motion graphics); o runtime escolhido no proposal é travado e trocá-lo silenciosamente é tratado como violação de governança. FFmpeg faz a pós-produção.

### Backlot

O Backlot é um quadro local que se preenche conforme a produção roda: etapas acendem, o roteiro aparece como página de screenplay, cartões de cena mostram ativos em geração, custo por ativo e decisões de provedor. Ele também funciona como gate de aprovação visual e permite replay de uma execução a partir dos timestamps.

## Instalação e uso rápido

Pré-requisitos publicados: Python 3.10+, FFmpeg, Node.js 18+ e um assistente de código compatível.

```bash
git clone https://github.com/calesthio/OpenMontage.git
cd OpenMontage
make setup
```

Sem `make`, o README publica o caminho manual: criar venv, instalar `requirements.txt`, rodar `npm install` em `remotion-composer`, instalar `piper-tts` e copiar `.env.example` para `.env`. No Windows, há instruções separadas.

Depois, basta abrir o projeto no assistente e pedir o vídeo:

```text
"Make a 60-second animated explainer about how neural networks learn"
```

Chaves de API são opcionais e acumulativas — mais chaves liberam mais ferramentas. Sem nenhuma chave, o projeto oferece Piper TTS, acervos livres, Remotion/HyperFrames e FFmpeg. Com GPU, `make install-gpu` habilita modelos locais de vídeo (WAN, Hunyuan, CogVideo, LTX-Video).

O README também inclui um caminho de instalação/verificação para agentes, com `AGENT_GUIDE.md`, `PROJECT_CONTEXT.md` e comandos para inspecionar o envelope de capacidades e o menu de provedores.

## Exemplos de uso

Exemplos derivados dos prompts publicados no README:

- **Explainer sem chaves:** "Make a 45-second animated explainer about why the sky is blue".
- **Documentário com filmagem real:** "Make a 90-second documentary montage about what a city feels like at 4am. Use real footage only, no narration, elegiac tone."
- **Referência visual:** colar um YouTube Short, Reel ou TikTok e pedir "Make me something like this, but about quantum computing" — o agente analisa transcrição, ritmo, cenas, keyframes e estilo, e devolve 2–3 conceitos diferenciados com custo estimado.
- **Trailer cinematográfico:** "Create a cinematic 30-second trailer for a sci-fi concept: humanity receives a warning from 1000 years in the future" (caminho com provedores, custo declarado de ~US$ 1–3).

## Quando usar (e quando não usar)

- **Use quando:** você quer produzir vídeos de forma estruturada com um assistente de código, prefere provedores locais/livres ou quer combinar acervos abertos com geração por IA, e valoriza gates de qualidade, orçamento e trilha de decisão.
- **Evite quando:** você precisa de um editor de vídeo tradicional com timeline manual; não pode operar Python/Node/FFmpeg; quer um serviço SaaS pronto; ou não aceita a AGPL-3.0 para derivados distribuídos.

## Limitações e cuidados

- **Somente o README foi lido.** Código, `docs/`, `AGENT_GUIDE.md`, `PROJECT_CONTEXT.md`, manifestos e skills não foram verificados.
- **Licença AGPL-3.0.** É copyleft forte; usar o software como serviço de rede ou distribuir derivados pode acionar obrigações de disponibilização do código. Avalie com cuidado em contexto comercial.
- **Custo e provedores.** Muitos recursos dependem de APIs pagas; o README fala em estimativas e limites (padrão de US$ 10 por produção, aprovação acima de US$ 0,50), mas os preços e a disponibilidade dos provedores mudam.
- **Alegações do projeto.** "Primeiro sistema open-source", ganhos de qualidade e cobertura de 60+ provedores são afirmações do README, não auditorias independentes.
- **Qualidade automatizada não é garantia.** Os gates verificam promessa, slideshow, áudio e frames; isso não substitui revisão criativa humana.
- **Superfície de integração ampla.** Chaves de API, CLIs, modelos locais, acervos e servidores externos aumentam a superfície operacional e de segurança.
- **Conteúdo de terceiros.** O agente trata material de referência (vídeos, transcrições, web) como entrada; prompt injection e direitos autorais precisam ser considerados.

## Estado e adoção

- Versão/releases citadas no README: não há um número único de versão no topo; o README descreve a arquitetura corrente.
- Observado em 2026-10-19: ~69.744 stars, ~9.027 forks, ~410 issues abertas; criado em 2026-03-29; último push em 2026-10-16.
- Licença: GNU AGPLv3.
- Linguagem principal na API: Python.
- Site oficial: [openmontage.video](https://www.openmontage.video/).

## Relações

- Mantido por: [calesthio](../../../entities/calesthio.md)
- Conceitos: [Produção de vídeo agêntica](../../../concepts/producao-de-video-agentica.md), [Agent skills](../../../concepts/agent-skills.md), [Agent harness](../../../concepts/agent-harness.md)
- Relacionado: [Graphify-Labs/graphify](../graphify-labs/graphify.md) — outra ferramenta que combina skills com um pipeline determinístico e verificação explícita; [SynkraAI/aiox-core](../synkraai/aiox-core.md) — orquestração por artefatos e agentes especializados.
- Projetos citados: [Remotion](../remotion-dev/skills.md), HyperFrames, FFmpeg, Piper, WhisperX, Real-ESRGAN, SadTalker, MuseTalk, Wav2Lip, Kling, Veo, Runway, Seedance, Suno, ElevenLabs.

## Perguntas abertas

- Como o agente escolhe entre pipelines e como lida com pedidos que não se encaixam em nenhum?
- Os gates humanos são aplicados por hooks, por convenção nas skills ou pelo próprio fluxo do agente? Onde está a garantia?
- Qual é o custo real de uma produção completa em tokens e chamadas de API?
- Como o projeto evita direitos autorais e atribuição inadequada ao usar acervos e conteúdos de referência?
- Qual é a cobertura de testes de contrato e de integração, e como ela lida com provedores instáveis?
- O suporte a modelos locais via Ollama/LM Studio, citado como "coming soon", já existe?

## Fontes

- README: https://raw.githubusercontent.com/calesthio/OpenMontage/c8066452325cb57c8fc1ba8c2a71b6e8842e6b65/README.md (commit `c8066452325cb57c8fc1ba8c2a71b6e8842e6b65`, consultado em 2026-10-19). Somente o README foi lido; código, `docs/`, skills e demais arquivos não foram consultados.
- Metadados: API do GitHub (`/repos/calesthio/OpenMontage`) em 2026-10-19.
