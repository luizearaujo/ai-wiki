---
type: skill
name: Codex Image Gen
slug: codex-image-gen
url: https://github.com/zazencodes/skills/tree/main/skills/codex-image-gen
source_url: https://github.com/zazencodes/skills
source_path: skills/codex-image-gen
author: zazencodes
version: 0.1.1
license: MIT
status: active
created: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, geracao-de-imagem, codex, cli]
---

# Codex Image Gen

> Gera e edita imagens via a ferramenta de imagem embutida na CLI `codex`, reaproveitando o login do ChatGPT já autenticado — sem `OPENAI_API_KEY` e, deliberadamente, sem nenhum caminho alternativo que cobre por uso de API.

## O que é

Skill do catálogo [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md) que resolve geração/edição de imagem para quem já tem a CLI `codex` (da OpenAI) autenticada, evitando contratar ou configurar uma chave de API paga separada só para isso. Dispara para pedidos de gerar, criar, desenhar, ilustrar ou editar imagem, foto, textura, sprite, ícone, mockup, poster, capa, thumbnail, conceito de logo ou corte com fundo transparente — e também quando nenhum outro backend de imagem foi especificado.

## Como funciona

- `codex exec` não tem uma flag "salvar em tal caminho": ele grava o que gera em `$CODEX_HOME/generated_images/<session id>/`. O script `scripts/codex_image.py` roda um turno não interativo e recupera só as imagens salvas sob o ID de sessão exato daquele turno — se o ID ou as imagens estiverem ausentes, falha sem escrever nada.
- **Sempre passar pelo script.** Um `codex exec "draw me a cat"` direto costuma devolver prosa ou um desenho do ImageMagick em vez de uma imagem gerada, deixando o usuário para achar a saída por conta própria.
- **Nunca cair para a API da OpenAI.** A skill não tem — e não deve ganhar — um caminho alternativo via SDK da OpenAI ou `OPENAI_API_KEY` que cobre por uso. Se `codex_image.py` falhar, a instrução é relatar a falha e parar, nunca trocar silenciosamente para um caminho de API paga.
- Extensões de saída seguem o formato real da imagem: bytes PNG pedidos como `.jpg` são salvos como `.png`. `--fit` sempre produz PNG.
- Geração consome a cota da conta `codex`; quando esgotada, o script falha com mensagem clara e não escreve nada — a instrução é relatar isso ao usuário, não tentar de novo em loop.

### Flags principais

| Flag | Efeito |
|---|---|
| `--aspect` | Dica de proporção (`16:9`, `9:16`, `1:1`, `4:5`, …) passada ao modelo; molda a imagem mas não garante dimensões exatas. |
| `--fit WxH` | Garante dimensões exatas depois do fato: letterbox com padding por padrão (`--fit-mode pad`, cor via `--fit-background`) ou `--fit-mode crop` para corte central. |
| `-n/--variants N` | Pede N variações em uma rodada; a primeira vai para `-o`, as demais como `<nome>-2.png`, `<nome>-3.png`. O modelo nem sempre honra o número pedido. |
| `--edit` | Anexa uma imagem como alvo de edição; o prompt deve descrever a *mudança* ("remove o poste"), não a imagem inteira de novo. |
| `--sandbox` | `read-only` por padrão (suficiente para geração de imagem); `bypass` só quando o sandbox aninhado do codex não consegue iniciar. |
| `--reasoning` | `high` por padrão — esforço menor faz o modelo às vezes pular a ferramenta de imagem e responder em texto. |
| `--print-prompt` | Mostra o prompt completo que seria enviado, sem gastar cota. |
| `-r` | Usa uma imagem de referência. |
| `--prompt-file` | Lê um prompt longo de um arquivo em vez da linha de comando. |
| `--quiet --json` | Saída mínima e estruturada, para consumo por outro programa. |

## Instalação e uso

```bash
# Plugin do Claude Code
claude plugin marketplace add zazencodes/skills
claude plugin install zazencodes-skills@zazencodes

# skills.sh, só esta skill
npx skills@latest add zazencodes/skills --skill codex-image-gen
```

Requer `codex` no `PATH` e autenticado (`codex login`) — `CODEX_BIN` aponta para um binário diferente, se necessário — e Python 3.9+ (biblioteca padrão; `--fit` precisa de Pillow).

```bash
python3 scripts/codex_image.py \
  --prompt "a lone red bicycle leaning against a wet stone wall at dusk, cinematic photograph" \
  --output ~/Desktop/bike.png
```

Uma rodada leva de 30 a 60 segundos; a saída imprime cada caminho escrito.

## Exemplos de uso

> Exemplos derivados da descrição publicada — não são instruções oficiais da skill.

- `codex_image.py -p "..." -o out.png --aspect 9:16` — gerar uma imagem em retrato.
- `codex_image.py --edit v1.png -p "make the sky purple" -o v2.png` — editar uma imagem existente.
- `codex_image.py -p "..." -o cover.png --aspect 9:16 --fit 1080x1920` — garantir dimensões exatas de capa.

## Saídas esperadas

Um ou mais arquivos de imagem no caminho pedido (`-o`, mais `-2`, `-3`, … se `-n` > 1), com extensão correspondente ao formato real gerado; ou, em falha, nenhum arquivo e uma mensagem clara do que falhou (sessão/imagens ausentes, cota esgotada) — nunca uma imagem de fallback de outra fonte.

## Quando usar (e quando não usar)

- **Use quando:** já tem `codex` autenticado e quer gerar/editar imagens sem configurar uma chave de API paga separada.
- **Evite quando:** precisa de um backend de imagem garantido e independente de cota/disponibilidade do `codex` — a skill proíbe explicitamente qualquer fallback para uma API paga quando o `codex` falha ou está sem cota.

## Limitações e cuidados

- Sem `codex` autenticado e com `PATH` configurado, a skill não funciona — e, por design, não tenta nenhuma alternativa.
- `--fit` depende de Pillow, não só da biblioteca padrão.
- O número de variações pedido via `-n` não é garantido pelo modelo.
- Script completo (`scripts/codex_image.py`) não foi lido linha a linha nesta ingestão; o comportamento descrito vem do `SKILL.md`.

## Estado e adoção

- Versão: `0.1.1` — o único patch documentado no `CHANGELOG.md` do catálogo é justamente nesta skill: "recover images only from the exact generation session's saved files, failing clearly when its session ID or images are missing. Match output extensions to the actual image format and validate all variants before writing them."
- Preço/licença: MIT.

## Relações

- Autor: [zazencodes (Alexander Galea)](../../../../entities/zazencodes.md)
- Repositório-fonte: [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md)
- Conceitos: [Agent skills](../../../../concepts/agent-skills.md)
- Contraste: a skill `movie-poster`, incluída (não publicada separadamente) em [zazencodes/zazencodes-season-3](../../../../repos/github.com/zazencodes/zazencodes-season-3.md), usa a API paga do Gemini (`google-genai`, `GEMINI_API_KEY`) para geração de imagem — o oposto da política desta skill de nunca usar uma API paga como fallback.

## Perguntas abertas

- O que exatamente conta como "imagem ausente" no script — um timeout, um diretório de sessão vazio, ou ambos?

## Fontes

- `SKILL.md`: https://raw.githubusercontent.com/zazencodes/skills/9f2d7c8f0e112e03d0e440676afd49fde3c9dff2/skills/codex-image-gen/SKILL.md (commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2`, lido via clone local autorizado, consultado em 2026-10-21).
- `CHANGELOG.md` do mesmo repositório e commit, consultado em 2026-10-21.
