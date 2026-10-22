---
type: repo
url: https://github.com/cjpais/Handy
host: github.com
owner: cjpais
repo: Handy
commit: 5a9451e70aedc90648ce2befd9d7e0304746f9c1
license: MIT
language: Rust
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [speech-to-text, dictation, offline]
---

# cjpais/Handy

> App de desktop gratuito, open source e extensível que transcreve fala para texto totalmente offline, colando o resultado em qualquer campo de texto via atalho de teclado.

## O que é

Handy resolve o problema de dictation/transcrição sem depender de nuvem: pressiona um atalho, fala, e o texto transcrito aparece no campo ativo, sem enviar áudio para fora da máquina. O README posiciona o projeto como preenchendo uma lacuna por uma ferramenta de speech-to-text verdadeiramente open source e extensível, com quatro princípios declarados: gratuito, open source, privado e simples ("uma ferramenta, um trabalho").

## Como funciona

Fluxo: pressionar um atalho configurável (modos hold-to-record, toggle, ou hold-only/toggle-only) → falar → Handy processa o áudio com Whisper → o texto transcrito é colado na aplicação ativa. A detecção de silêncio usa VAD via Silero; a transcrição aceita Whisper (Small/Medium/Turbo/Large, com aceleração de GPU quando disponível) ou Parakeet V3 (otimizado para CPU, com detecção automática de idioma). É um app Tauri multiplataforma (Windows, macOS, Linux); no Linux depende de `gtk-layer-shell` para o overlay de gravação e de `xdotool`/`wtype`/`dotool` para colar texto de forma confiável, variando por servidor de display (X11 ou Wayland).

## Instalação e uso rápido

- **Download**: [releases do GitHub](https://github.com/cjpais/Handy/releases) ou [handy.computer](https://handy.computer).
- **macOS**: também via Homebrew (`brew install --cask handy`, não mantido pelos desenvolvedores do Handy).
- **Windows**: também via winget (`winget install cjpais.Handy`, idem não oficial).
- **Debian/Ubuntu**: `sudo apt install ./Handy_*.deb` (não usar `dpkg -i` diretamente, para resolver dependências automaticamente).
- Após instalar: conceder permissões de microfone e acessibilidade, configurar atalhos em Settings.
- Flags de linha de comando controlam uma instância já em execução (`--toggle-transcription`, `--cancel`) ou o comportamento de inicialização (`--start-hidden`, `--no-tray`, `--debug`).

## Exemplos de uso

- Configurar um atalho global no GNOME/KDE/Sway/Hyprland para `handy --toggle-transcription`, permitindo dictation sem depender do atalho interno do Handy em compositores Wayland — exemplo do README.
- Instalar um modelo Whisper GGML personalizado (fine-tuned ou comunitário) colocando o `.bin` no diretório de modelos para descoberta automática — exemplo do README.

## Quando usar (e quando não usar)

- **Use quando:** quer dictation/transcrição rápida, offline e sem custo em qualquer app de desktop, com escolha entre vários modelos locais (Whisper ou Parakeet).
- **Evite quando:** precisa também de clonagem de voz, dublagem ou TTS — [debpalash/VoiceStudio](../debpalash/voicestudio.md) cobre essas outras frentes de voz além de transcrição.

## Limitações e cuidados

- O README documenta várias limitações conhecidas em detalhe: qualidade de microfone Bluetooth reduzida no macOS durante a gravação; atalhos com a tecla `fn`/Globe só funcionam em teclados Apple (limitação de hardware, não bug); overlay de gravação pode interferir na colagem de texto no Linux X11; e crashes de inicialização no Linux ligados a `gtk-layer-shell` ou ao renderer DMA-BUF do WebKitGTK, com variáveis de ambiente de contorno para ambos.
- Mudança de comportamento relevante: versões antigas also aceitavam `SIGUSR1` para alternar transcrição com pós-processamento; o WebKitGTK embutido usa esse mesmo sinal internamente para coleta de lixo do JavaScript, causando gravações fantasma — o README pede explicitamente a remoção de bindings `pkill -USR1` antigos.
- O nome, logo e marca "Handy" não são open source, apenas o código; forks devem usar marca própria.
- Apenas o README foi lido; `BUILD.md`, código Rust/Tauri e os scripts de verificação de assinatura não foram consultados em detalhe além do comando documentado.

## Estado e adoção

- Versão/releases citadas no README: última release no GitHub, `v0.9.8` (2026-10-03); artefatos assinados com o formato de updater do Tauri (minisign).
- Atividade e popularidade observadas em 2026-10-23: 34.324 estrelas, 3.256 forks (GitHub API); push em 2026-10-22.
- Licença: MIT para o código; marca/logo excluídos.

## Relações

- Mantido por: [CJ Pais (cjpais)](../../../entities/cjpais.md).
- Conceitos: [Clonagem de voz](../../../concepts/clonagem-de-voz.md) (relação de domínio — transcrição em vez de síntese/clonagem).
- Alternativas: [debpalash/VoiceStudio](../debpalash/voicestudio.md) — cobre transcrição como uma das várias capacidades de voz, ao lado de clonagem, design e dublagem; [Handy CLI](https://github.com/cjpais/handy-cli) — versão original em linha de comando Python, citada no próprio README como "Related Projects".

## Perguntas abertas

- Como o modelo Parakeet V3 se compara a Whisper em precisão e latência para idiomas além do inglês, dado que o README destaca detecção automática de idioma só para ele?
- Qual é a cobertura real de confiabilidade da colagem de texto (`enigo`) em compositores Wayland sem `wtype`/`dotool` instalados?

## Fontes

- README: https://raw.githubusercontent.com/cjpais/Handy/5a9451e70aedc90648ce2befd9d7e0304746f9c1/README.md (commit `5a9451e70aedc90648ce2befd9d7e0304746f9c1`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
