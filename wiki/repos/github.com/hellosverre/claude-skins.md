---
type: repo
url: https://github.com/hellosverre/claude-skins
host: github.com
owner: hellosverre
repo: claude-skins
commit: 985ad63fdb3483bbb98f61cf57955cac3f56a449
license: MIT
language: TypeScript
status: active
created: 2026-10-28
ingested: 2026-10-28
updated: 2026-10-28
tags: [plugins-de-agente, claude-code, mods, temas]
---

# hellosverre/claude-skins

> Mod de Claude Code (`/skin`) que redesenha tool calls, diffs, tabelas, Mermaid e uma faixa de uso em dezesseis temas, repintáveis ou desenhados pelo próprio Claude.

## O que é

`skins` é um mod — plugin em processo, baseado em hooks de função — que reconstrói a forma como o Claude Code desenha a conversa: chamadas de ferramenta com ícone e tempo de execução, edições como cards de diff, tabelas e gráficos Mermaid como cards, uma faixa de uso acima do prompt, e dezesseis temas visuais (`noir`, `tokyo-night`, `dracula`, `catppuccin`, `rose-pine`, `nord`, `gruvbox`, `kanagawa`, `everforest`, `one-dark`, `solarized`, `night-owl`, `ayu`, `github`, `mono`, `terminal`) trocáveis com `/skin`. Funciona tanto no terminal quanto no app desktop, com fallback para o desenho nativo do Claude Code em casos não cobertos.

## Como funciona

Requer Claude Code 2.1.287+. É instalado como plugin de marketplace e embarca um módulo de hooks (`hooks/register.tsx`) que intercepta o que seria desenhado e devolve sua própria representação — cards SVG para tabelas, diffs, gráficos Mermaid (17 tipos, com layout próprio para sequência/estado/classe/ER só no terminal) e blocos de matemática, mais um realce de sintaxe para 20 famílias de linguagem no terminal.

Expõe `$.skins.markdown` para outros mods reaproveitarem o mesmo desenho de markdown (declarando `skins` como dependência em `plugin.json`), e documenta explicitamente onde cede para o desenho nativo do Claude Code: agentes, plan mode, prompt de permissão, imagens/PDF/notebook abertos, edições no terminal, blocos de código em linguagem não reconhecida, diagramas de sequência/estado/classe/ER no desktop, textos muito longos (blocos acima de 9.000 caracteres, prompts acima de 4.000).

**Privacidade declarada:** lê o diretório de sessão, uso de contexto/plano, a configuração de tema e `SKINS_THEME`/`COLORFGBG`; guarda configurações no mod store local. A única chamada de rede é uma verificação diária de versão (GET do `plugin.json` do próprio repositório no `raw.githubusercontent.com`), sem enviar dados.

### Comparação com mods semelhantes (do próprio README, 2026-10-10)

O README compara `skins` com cinco outros mods de transcrição: `Prismantis` (fork-base, lida com texto da direita para a esquerda e tipografia de matemática via RaTeX), `glint` (fork do Prismantis, torna caminhos de arquivo clicáveis), `tweakcc` (recolore o Claude Code inteiro via patch binário, não hooks), `claude-gfm-render` (desenha diagramas Mermaid como SVG no desktop) e `ccstatusline` (status line com Powerline, sem redesenho de transcrição). Segundo o README, `skins` é o único com API para outros mods (`$.skins.markdown`) e o único que oferece desenhar um tema com o próprio Claude a partir de um pedido em linguagem natural.

## Instalação e uso rápido

```
/plugin marketplace add hellosverre/claude-skins
/plugin install skins@hellosverre-mods
```

Reiniciar o Claude Code depois; o tema `noir` vem ativo, `/skin` troca. Atualização: `claude plugin marketplace update hellosverre-mods` + `claude plugin update skins@hellosverre-mods`. Desinstalação: `claude plugin uninstall skins@hellosverre-mods`, ou `/skin off` para manter instalado mas voltar ao desenho nativo.

O mesmo autor distribui um "mod store" (`/plugin install mod-store@hellosverre-mods`) que, segundo o README, navega e instala cerca de 2.700 mods de uma lista, mostrando o que cada um pode acessar antes de instalar.

## Exemplos de uso

- Trocar para um tema de alto contraste para apresentações ou capturas de tela, com `/skin <nome>`.
- Pedir "faça um skin que pareça um pôr do sol" — o mod dá ao Claude uma ferramenta de design (`design`) para gerar e aplicar o tema enquanto o usuário observa.
- Ativar `/skin quiet` para dobrar leituras, buscas e comandos somente-leitura em uma linha, reduzindo ruído visual em sessões longas.

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é melhorar a legibilidade e a estética da transcrição do Claude Code (diffs, tabelas, gráficos, código), sem alterar o que o modelo lê ou a conversa armazenada.
- **Evite quando:** a versão do Claude Code é anterior a 2.1.287, ou quando a prioridade é recolorir a interface inteira do Claude Code (não só o que os hooks conseguem redesenhar) — nesse caso o próprio README aponta o `tweakcc` como melhor opção, ao custo de fazer patch no binário.

## Limitações e cuidados

- Depende da mesma API de hooks de função em early access usada por outros mods do ecossistema (ex.: [JohnnyVizz/claude-kit](../johnnyvizz/claude-kit.md)); o README não declara uma versão mínima estável além de 2.1.287.
- Lista extensa de "Known limitations" no próprio README: dois mods salvando no mesmo `CLAUDE.md` simultaneamente podem perder uma linha; sessões antigas (pré-2.1.286) ainda abertas podem desativar mods para sessões novas; diagramas com caracteres largos (CJK) em nós do Mermaid no terminal caem para código; blocos de código após 80 linhas são cortados com nota "N more lines".
- Compatibilidade testada manualmente só em Windows e Linux (terminal); macOS, VS Code e mobile "não foram olhados à mão", segundo o README — há CI em Linux/Windows/macOS, mas sem verificação manual nessas plataformas.
- Esta página documenta apenas o `README.md` da raiz; o código dos hooks, os temas individuais em `hooks/themes/` e os testes não foram lidos.

## Estado e adoção

- Repositório criado em 2026-10-02; push mais recente em 2026-10-23, observado em 2026-10-28.
- 223 estrelas, 36 forks, observado em 2026-10-28.
- Licença: MIT (confirmada pela API do GitHub).

## Relações

- Mantido por: [Sverre (hellosverre)](../../../entities/hellosverre.md).
- Conceitos: [Plugins de agente](../../../concepts/plugins-de-agente.md).
- Repositório irmão com o mesmo mecanismo de mods: [JohnnyVizz/claude-kit](../johnnyvizz/claude-kit.md).
- Outros mods do mesmo autor citados no README (não ingeridos nesta wiki): `hellosverre/redgreen`, `hellosverre/smart-compact`, `hellosverre/mod-store`.

## Perguntas abertas

- Como o "mod store" (`mod-store`) cura e lista ~2.700 mods — o que distingue um mod confiável nessa lista?
- O que o código de `hooks/vendor/mermaid-ascii.js` (vendorizado de `beautiful-mermaid`) cobre exatamente nos diagramas de terminal não listados como limitação?

## Fontes

- README: https://raw.githubusercontent.com/hellosverre/claude-skins/985ad63fdb3483bbb98f61cf57955cac3f56a449/README.md (commit `985ad63fdb3483bbb98f61cf57955cac3f56a449`, consultado em 2026-10-28). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/hellosverre/claude-skins`, `api.github.com/users/hellosverre`), consultada em 2026-10-28.
