---
type: skill
name: reflect-mod
slug: reflect-mod
url: https://claudemods.dev/en/builds/reflect-mod-7b9b6f
source_url: https://github.com/BayramAnnakov/claude-reflect
source_path: mod
author: BayramAnnakov
version: desconhecida
license: desconhecida
status: active
created: 2026-10-28
updated: 2026-10-28
tags: [plugins-de-agente, claude-code, memoria-de-agente, mods, claude-md]
---

# reflect-mod

> Mod de Claude Code que revisa cada prompt curto no momento da correção e oferece, em uma faixa acima do prompt, salvar a regra aprendida direto no `CLAUDE.md`.

## O que é

`reflect-mod` é descrito na página de origem (`claudemods.dev`) como "claude-reflect como um mod de Claude Code" — um plugin em processo, em TypeScript, de hooks de função. **Não é tecnicamente uma Agent Skill em `SKILL.md`**: é um mod, no mesmo formato do ecossistema de [hellosverre/claude-skins](../../../../repos/github.com/hellosverre/claude-skins.md) e [JohnnyVizz/claude-kit](../../../../repos/github.com/johnnyvizz/claude-kit.md) — documentado aqui como skill por decisão explícita do usuário, dado que a wiki não tem um workflow próprio para páginas de catálogo de mods. O repositório-fonte, `claude-reflect`, é descrito na própria API do GitHub como "a self-learning system for Claude Code that captures corrections, positive feedback, and preferences — then syncs them to CLAUDE.md and AGENTS.md"; `reflect-mod` é a reimplementação desse sistema como mod, vivendo no caminho `mod` desse repositório.

## Como funciona

Segundo a página de origem:

1. **`prompt.submit`:** filtros baratos descartam prompts candidatos — comandos de barra, confirmações curtas, prompts acima de 500 caracteres e qualquer texto que pareça credencial.
2. **A verificação:** uma chamada de modelo (`haiku`) retorna `{is_rule, rule, scope, confidence}`. Resultados com confiança abaixo de 0,7, regras em múltiplas linhas, regras acima de 200 caracteres ou texto parecido com segredo são descartados.
3. **A faixa:** opções de "Save to `./CLAUDE.md`" ou "`~/.claude/CLAUDE.md`", "Global", "This repo instead", "Edit" e "Skip".
4. **Salvar:** o arquivo é relido antes da escrita; uma regra já presente não é duplicada; marcadores quebrados interrompem a escrita.

O comando `remember: <regra>` pula a verificação por modelo e envia a regra direto para a faixa. `/reflect-queue` lista as regras encontradas; `/reflect-pause` pausa e retoma a verificação.

### Comparação com o plugin Python do mesmo autor (segundo a página de origem)

| | Plugin Python (`claude-reflect`) | `reflect-mod` |
|---|---|---|
| Detecção | 63 regexes na captura, verificação por modelo depois, via `/reflect` | Verificação por modelo em todo prompt curto, qualquer idioma |
| Revisão | `/reflect`, quando o usuário lembra de rodar | Faixa acima do prompt, no momento |
| Repetições | Cada uma entra de novo na fila | Mescladas em uma linha com contador |
| Aplicação | Depois que o `CLAUDE.md` é relido | Na sessão atual, imediatamente, e no `CLAUDE.md` |
| Roda em | Claude Code, Codex/Cursor via `AGENTS.md` | Claude Code 2.1.286+ com mods |

A página cita que a fila do plugin Python "held 102 items across 37 projects, none ever cleared; about 16 were reusable rules" e resume a limitação do regex: "Regex cannot tell a rule from a one-off redirect." O aviso explícito da página: usar um ou outro, não os dois, "every correction would be captured twice".

## Instalação e uso

```
claude plugin marketplace add BayramAnnakov/claude-reflect
claude plugin install reflect-mod@claude-reflect-marketplace
```

A própria página recomenda checar o README do autor antes, já que os nomes de comando podem mudar. Requer Claude Code 2.1.286+ com mods (early access). Comandos de desenvolvimento citados: `claude plugin validate mod` e `claude plugin test mod` (10 testes, com modelo mockado, gratuitos).

## Exemplos de uso

- Corrigir o Claude no meio de uma sessão e, na própria faixa que aparece, salvar a correção como regra permanente do repositório sem interromper o fluxo.
- Usar `remember: sempre rodar testes antes de commitar` para forçar uma regra direto na faixa, sem passar pela verificação por modelo.
- Pausar a verificação com `/reflect-pause` durante uma sessão de exploração onde muitas correções não representam regras reais.

Exemplos derivados da página de origem; não são instruções oficiais do mod.

## Saídas esperadas

Entradas na seção marcada "Learned rules" do `CLAUDE.md` do repositório ou do usuário (`~/.claude/CLAUDE.md`), uma por correção aceita, sem duplicatas.

## Quando usar (e quando não usar)

- **Use quando:** o usuário já está em Claude Code 2.1.286+ com mods habilitados e quer captura de regras em tempo real, no momento da correção, em qualquer idioma.
- **Evite quando:** o plugin Python (`claude-reflect`) já está instalado — a página adverte que rodar os dois duplica toda correção capturada; ou quando múltiplas sessões escrevem no mesmo `CLAUDE.md` ao mesmo tempo, cenário em que a própria página descreve risco de perda de uma regra.

## Limitações e cuidados

- Licença não informada na página de origem; o repositório-fonte (`claude-reflect`) é licenciado como MIT pela API do GitHub, mas essa licença cobre o repositório como um todo, não necessariamente confirmada especificamente para o subdiretório `mod`.
- Pegada de permissão declarada como "L3" na página, com seis correspondências de scan: execução de comandos, variáveis de ambiente, leitura de arquivos, chamadas de modelo e escrita de arquivos.
- Risco de corrida documentado: duas sessões salvando no mesmo `CLAUDE.md` ao mesmo tempo podem perder uma regra.
- Uma sessão de Claude Code anterior à 2.1.286 ainda em execução pode desativar mods para sessões novas; a página recomenda reiniciar sessões antigas se a faixa nunca aparecer.
- Cada prompt elegível faz uma chamada de modelo pequena, contabilizada no uso do Claude.
- O `SKILL.md`/código do mod em si (`mod/` no repositório-fonte) não foi lido nesta ingestão — a página de catálogo foi a única fonte, conforme workflow de skill do schema desta wiki.

## Estado e adoção

- Versão: não informada na página (repositório-fonte com push mais recente em 2026-10-03, criado em 2026-01-03).
- Observado em 2026-10-28, segundo a página: 1.872 estrelas, 0 votos, 194 visualizações; adicionado ao catálogo em 2026-10-05.
- Preço/licença: gratuito; licença não mencionada na página (ver Limitações).

## Relações

- Autor: [Bayram Annakov (BayramAnnakov)](../../../../entities/bayramannakov.md).
- Conceitos: [Plugins de agente](../../../../concepts/plugins-de-agente.md), [Memória de agente](../../../../concepts/memoria-de-agente.md).
- Alternativas: o próprio plugin Python `claude-reflect` (mesmo repositório-fonte, mesmo autor) — detecção por regex e revisão manual via `/reflect`, em vez de verificação por modelo em tempo real.
- Mods do mesmo ecossistema de catálogo (não comparados diretamente pela página de origem): [hellosverre/claude-skins](../../../../repos/github.com/hellosverre/claude-skins.md), [JohnnyVizz/claude-kit](../../../../repos/github.com/johnnyvizz/claude-kit.md).

## Perguntas abertas

- O que o `SKILL.md`/manifesto do mod em `mod/` especifica além do que a página de catálogo resume?
- Qual licença se aplica especificamente ao subdiretório `mod`, já que a licença MIT do repositório não foi confirmada arquivo a arquivo?

## Fontes

- Página de origem: https://claudemods.dev/en/builds/reflect-mod-7b9b6f (consultada em 2026-10-28).
- Repositório-fonte: https://github.com/BayramAnnakov/claude-reflect (metadados via API do GitHub, HEAD `b6c42326903af3dd2bf3772b979730a44d8548ca`, consultado em 2026-10-28). Não clonado; o conteúdo de `mod/` não foi lido.
