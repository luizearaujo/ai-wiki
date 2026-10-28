---
type: repo
url: https://github.com/zenbu-labs/terminal-browser
host: github.com
owner: zenbu-labs
repo: terminal-browser
commit: e8ca7483af401672a377c45f931439fde5a67dfa
license: MIT
language: TypeScript
status: active
created: 2026-10-28
ingested: 2026-10-28
updated: 2026-10-28
tags: [navegacao-web-agentica, terminal, electron, claude-code, agent-browser]
---

# zenbu-labs/terminal-browser

> Browser real (Chromium via Electron) renderizado dentro do terminal pelo protocolo gráfico kitty, com CLI compatível com `agent-browser` para que um agente de código interaja com páginas abertas ao lado dele.

## O que é

`terminal-browser` desenha pixels de um Chromium real dentro de terminais que suportam o protocolo gráfico kitty (ghostty, kitty, cmux, VS Code e outros), usando a API de offscreen rendering do Electron para ler os pixels direto da GPU e enviar só os patches de região alterada ao terminal. O caso de uso central, segundo o README: manter um agente de código e o site que ele está construindo na mesma aba de terminal, com o agente tendo acesso total para interagir com os navegadores abertos.

## Como funciona

- **Renderização:** Electron em modo offscreen lê os pixels gerados pelo Chromium diretamente da GPU; só as regiões da página que mudaram visualmente são reenviadas ao terminal, evitando frames perdidos.
- **Entrada:** cliques, posição do mouse e teclado vêm do terminal e são sintetizados como eventos para o Chromium. Eventos que o terminal não expõe (ex. trackpad) são lidos diretamente do sistema operacional por um app Swift em background, o que permite scroll suave em canvases infinitos.
- **UI:** a camada externa do navegador é um motor gráfico em Rust; a interface é definida em React com um renderer customizado (TypeScript), desenhada na mesma superfície compartilhada que o conteúdo do navegador — permitindo empilhar UI sobre o conteúdo da página.
- **CLI para agentes:** `terminal-browser action` é descrito como "an agent-browser compatible cli for interacting with open terminal-browsers" — compatibilidade direta com a convenção de CLI do ecossistema `agent-browser`.
- **SSH:** `terminal-browser open --ssh <user@host> <url>` roda a renderização localmente e só repassa requisições de rede pela conexão SSH, em vez de enviar cada frame pela rede — permite abrir sites em `localhost` de uma máquina remota.
- **API para terminais:** terminais podem implementar um pequeno protocolo via socket Unix (métodos `getCurrentPane`, `split`, `listPanes`, `neighbor`, `sendText`, `pasteKey`, `focusPane`) para que o `terminal-browser` abra painéis, envie texto/imagens a um agente de código e alterne o foco entre o navegador e o agente de forma integrada. Suporte embutido (sem precisar dessa API) para ghostty, kitty, wezterm, cmux, tmux, VS Code, tty7, herdr e supacode.
- A lógica de renderização/entrada foi extraída como biblioteca JavaScript reutilizável, [`pixel`](https://github.com/zenbu-labs/terminal-browser/tree/main/pixel), para quem quiser construir outras aplicações gráficas no terminal.

## Instalação e uso rápido

```bash
# macOS e Linux
curl -fsSL https://terminal-browser.sh/install | bash
# ou
brew install terminal-browser
```

Windows requer WSL (terminais com suporte a gráficos kitty são limitados nativamente). Há também um plugin de Claude Code, com instruções em `/claude-code-plugin/README.md` do próprio repositório (não lido nesta ingestão).

```bash
terminal-browser                 # abre o navegador
terminal-browser open <url>      # abre em uma URL
terminal-browser --split right   # abre em painel dividido à direita
terminal-browser open --ssh <user@host> <url>
terminal-browser action          # CLI compatível com agent-browser
terminal-browser ls              # lista navegadores abertos
```

## Exemplos de uso

- Manter um agente de código e o site que ele está construindo na mesma aba de terminal, em painéis divididos.
- Pedir a um agente para gerar um plano em HTML e abri-lo automaticamente em painel dividido ao lado via `terminal-browser open`.
- Revisar, pelo próprio agente, uma página rodando em `localhost` de uma máquina remota via `--ssh`, sem expor a renderização à rede.
- Embutir o navegador dentro de uma TUI existente (ver `examples/embedded`).

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** o terminal usado suporta o protocolo gráfico kitty e o objetivo é ter um navegador real controlável por um agente de código, lado a lado com o próprio agente, incluindo sobre SSH.
- **Evite quando:** o terminal/SO não suporta gráficos kitty nativamente (Windows fora de WSL, com suporte limitado mesmo assim) — nesse caso, considere alternativas como [jo-inc/camofox-browser](../jo-inc/camofox-browser.md) (servidor REST headless) ou [vercel-labs/agent-browser](../vercel-labs/agent-browser.md) (CLI Rust via CDP), que não dependem de renderização gráfica no terminal.

## Limitações e cuidados

- Suporte ao Windows depende inteiramente de WSL, e a lista de terminais testados com gráficos kitty em Windows é pequena (o README cita apenas `noctty.com`).
- Telemetria de uso pseudo-anônima e relatórios de falha são coletados por padrão; desativáveis por variáveis de ambiente (`DO_NOT_TRACK=1`, `TERMINAL_BROWSER_NO_TELEMETRY=1`) ou pela GUI de configurações — dados ficam auditáveis localmente em `~/.local/state/terminal-browser-*/logs/telemetry.jsonl`. A biblioteca `pixel/`, isolada, não coleta telemetria.
- O roadmap do próprio README lista "design mode" e suporte a extensões Chrome como pendentes (⏳); suporte Linux já declarado concluído (✅).
- Regra de contribuição exigida pelo projeto: descrições de PR devem ser escritas por humanos, não por agentes — "PR descriptions must be authored by humans and explained well, otherwise we will close them".
- Esta página documenta apenas o `README.md` da raiz; `claude-code-plugin/README.md`, `examples/embedded/`, e o código em `pixel/` e `shared/` não foram lidos.

## Estado e adoção

- Repositório criado em 2026-07-06; push mais recente em 2026-10-28, observado no mesmo dia.
- 4.307 estrelas, 206 forks, observado em 2026-10-28.
- Licença: MIT (confirmada pela API do GitHub).

## Relações

- Mantido por: [zenbu-labs](../../../entities/zenbu-labs.md).
- Conceitos: [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md).
- Comparáveis já documentados nesta wiki, na categoria [Engenharia e interfaces agent-first](../../../categorias.md#engenharia-e-interfaces-agent-first): [jo-inc/camofox-browser](../jo-inc/camofox-browser.md) (servidor REST headless com anti-detecção), [vercel-labs/agent-browser](../vercel-labs/agent-browser.md) (CLI Rust via CDP), [browser-use/browser-use](../browser-use/browser-use.md) (biblioteca/agente com modelo próprio).

## Perguntas abertas

- O que o plugin de Claude Code (`claude-code-plugin/README.md`) expõe especificamente além da CLI `terminal-browser action`?
- Como a implementação embutida de cada terminal em `pixel/packages/pixel/src/terminal/terminals` difere em capacidades da API via socket Unix documentada no README?

## Fontes

- README: https://raw.githubusercontent.com/zenbu-labs/terminal-browser/e8ca7483af401672a377c45f931439fde5a67dfa/README.md (commit `e8ca7483af401672a377c45f931439fde5a67dfa`, consultado em 2026-10-28). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/zenbu-labs/terminal-browser`, `api.github.com/orgs/zenbu-labs`), consultada em 2026-10-28.
