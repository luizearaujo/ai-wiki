---
type: repo
url: https://github.com/vercel-labs/agent-browser
host: github.com
owner: vercel-labs
repo: agent-browser
commit: dac13bb87468fe9d74a040d862720f6cc17a9565
license: Apache-2.0
language: Rust
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [navegacao-web, cli, mcp, automacao, rust]
---

# vercel-labs/agent-browser

> CLI de automação de navegador em Rust nativo, feita para agentes de IA: controla o Chrome via CDP sem Node.js ou Playwright, com snapshots de acessibilidade estáveis como superfície principal de interação.

## O que é

agent-browser é uma ferramenta da Vercel Labs para que agentes abram páginas, leiam sua estrutura e interajam com elas por comandos curtos, com saída machine-readable e integrações pensadas para uso agêntico (MCP, dashboard, skills).

## Como funciona

- Uma CLI Rust envia comandos para um **daemon em segundo plano** que controla o navegador diretamente via Chrome DevTools Protocol (CDP) — sem Node.js ou Playwright.
- O daemon inicia no primeiro comando, persiste entre comandos e encerra após período de inatividade, podendo salvar estado se a restauração estiver configurada.
- Fluxo principal: tirar um **snapshot de acessibilidade**, que atribui refs a elementos (ex.: `@e2`), e agir sobre esses refs; novo snapshot é necessário após mudanças na página.
- Saída pode ser JSON (`--json`) para consumo por agentes.
- **Seletores:** refs de snapshot (recomendado), CSS, texto, XPath e localizadores semânticos (`find role button click --name "Submit"`).
- **Sessões e estado:** `--session` isola instâncias; perfis, restauração de sessão e um vault de autenticação criptografado tratam logins persistentes.
- **Abas, frames, diálogos, rede:** rótulos de aba e IDs estáveis, troca de iframe, tratamento automático de diálogos `alert`/`beforeunload`, roteamento e mock de requisições, gravação HAR.
- **Diagnóstico:** logs de console e erro, tracing, profiling, gravação de vídeo, auditorias de acessibilidade com axe-core e comando `doctor` para checar o ambiente.
- **Leitura de página:** comando `read` busca texto/markdown amigável a agentes, preferindo `llms.txt` quando disponível, sem abrir o Chrome.
- **Integrações:** servidor MCP (`agent-browser mcp`) com perfis de ferramentas selecionáveis, dashboard ao vivo, comando `chat` via Vercel AI Gateway, skills embutidas (`skills get`) e descoberta de ferramentas WebMCP.
- **Outras plataformas:** iOS Simulator e dispositivos reais via Appium; provedores em nuvem como Browserless, Browserbase e Browser Use.

## Instalação e uso rápido

- Recomendado: instalação global via npm (inclui o binário nativo). Alternativas: dependência local do projeto, Homebrew (macOS), `cargo install`, ou build a partir do código-fonte.
- Após instalar, `agent-browser install` baixa o Chrome for Testing; instalações existentes de Chrome, Brave, Playwright e Puppeteer são detectadas automaticamente. No Linux, `agent-browser install --with-deps` tenta instalar bibliotecas de sistema.
- `agent-browser upgrade` detecta o método de instalação e atualiza.
- Pré-requisitos: Chrome (o próprio comando `install` resolve); Node.js 24+ e pnpm 11+ apenas para build a partir do código-fonte; Rust apenas para build; Linux pode exigir bibliotecas extras; suporte iOS requer macOS com Xcode e Appium.

## Exemplos de uso

- Fluxo básico: abrir site → `snapshot` → `click` num ref → `fill` num campo → `screenshot` → `close`.
- Seletores tradicionais: `click "#submit"`, `fill "#email" "..."`.
- Reaproveitar login: `--profile`, `--restore`, ou `state save`/`state load`.
- Conectar a navegador já aberto: `--cdp 9222` ou `--auto-connect`.
- Auditoria de acessibilidade: `agent-browser a11y <url>`.
- Adicionar a skill a um assistente de código: `npx skills add vercel-labs/agent-browser`.

## Quando usar (e quando não usar)

- **Use quando:** o agente precisa automatizar um navegador real com saída estruturada e estável (refs de acessibilidade) e integração nativa com MCP, sem a sobrecarga de Node.js/Playwright.
- **Evite quando:** precisar de recursos bloqueados por `--allowed-domains` (CDP attach, auto-connect, perfis Chrome, restore, Safari, iOS) ou operar em páginas com SSE/WebSocket/polling constante, onde `networkidle` pode nunca resolver.

## Limitações e cuidados

- Cliques falham quando outro elemento cobre o alvo (ex.: banner de cookies); é preciso dispensar o overlay e tirar novo snapshot.
- `--allowed-domains` desativa várias funcionalidades (listadas acima) e também o WebRTC.
- `--annotate` não funciona no backend Safari/WebDriver.
- Timeouts acima de 30s podem causar erros EAGAIN; comandos que mudam o estado da página não são reexecutados após o daemon recebê-los.
- Screenshots WebGPU saem pretos em Chrome headless no Windows e Linux — exigem modo headed ou workaround.
- Recursos experimentais: WebMCP e o "Obscura engine".
- Arquivos de estado salvam tokens de sessão em texto plano, salvo criptografia habilitada.

## Estado e adoção

- Licença: Apache-2.0.
- Linguagem principal (API do GitHub): Rust.
- Atividade observada em 2026-10-19: push mais recente no mesmo dia.

## Relações

- Mantido por: [Vercel Labs (vercel-labs)](../../../entities/vercel-labs.md).
- Conceitos: [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md), [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md).
- Alternativas: [jo-inc/camofox-browser](../jo-inc/camofox-browser.md) (servidor REST de browser com anti-detecção) e [D4Vinci/Scrapling](../d4vinci/scrapling.md) (fetchers stealth e servidor MCP para scraping).

## Perguntas abertas

- Qual o escopo exato do "Obscura engine" citado como experimental?
- Como o roteamento de requisições e mock de rede se comparam em robustez com soluções baseadas em Playwright?

## Fontes

- README: https://raw.githubusercontent.com/vercel-labs/agent-browser/dac13bb87468fe9d74a040d862720f6cc17a9565/README.md (commit `dac13bb87468fe9d74a040d862720f6cc17a9565`, consultado em 2026-10-19; leitura cobriu os primeiros ~100.000 caracteres do arquivo). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Perfil do GitHub (`api.github.com/repos/vercel-labs/agent-browser`), consultado em 2026-10-19.
