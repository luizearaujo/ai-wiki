---
type: repo
url: https://github.com/jo-inc/camofox-browser
host: github.com
owner: jo-inc
repo: camofox-browser
commit: 39c82094013480b373df6600d44c7f036f58356e
license: MIT
language: JavaScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [browser, agentes, automacao, scraping, stealth, playwright, camoufox, rest-api]
---

# jo-inc/camofox-browser

> Servidor de browser headless com anti-detecção para agentes de IA, baseado no Camoufox e exposto como API REST com snapshots de acessibilidade, refs estáveis e importação de cookies.

## O que é

Camofox Browser é um servidor que embrulha o [Camoufox](https://camoufox.com) — um fork do Firefox com spoofing de fingerprint implementado em C++ — em uma API REST pensada para agentes. O README declara o problema: "AI agents need to browse the real web. Playwright gets blocked. Headless Chrome gets fingerprinted. Stealth plugins become the fingerprint."

O público são agentes e produtos que precisam navegar em sites reais com sessão autenticada e menos bloqueio automatizado. O projeto se posiciona como substituto de Puppeteer/Playwright, com três diferenciais de interface: snapshots de acessibilidade em vez de HTML bruto (alegadamente ~90% menores), refs estáveis (`e1`, `e2`) para clicar e digitar, e macros de busca para sites comuns.

**Nota de uso responsável.** O objetivo declarado inclui contornar detecção de bots e mecanismos anti-scraping. Documentar a ferramenta não valida seu uso: termos de serviço, robots.txt, direitos autorais e legislação aplicável continuam sendo responsabilidade do operador. A wiki não endossa evasão de controles em sistemas de terceiros.

## Como funciona

A arquitetura é **um processo de browser com sessões isoladas**:

```text
Browser Instance (Camoufox)
\-- User Session (BrowserContext) — cookies/storage isolados
    |-- Tab Group (sessionKey)
    |   |-- Tab
    \-- Tab Group (sessionKey)
```

- Sessões expiram após 30 minutos de inatividade; o browser encerra após 5 minutos sem sessões ativas e relança sob demanda.
- Ao atingir o limite de abas, a mais antiga/menos usada é reciclada em vez de retornar erro.
- A comunicação é HTTP em `localhost:9377`, com spec OpenAPI em `/openapi.json` e docs em `/docs`.
- Cookies e localStorage persistem em `~/.camofox/profiles/<hashed-userId>/`; IndexedDB é opcional e aumenta o tamanho das sessões.
- O browser roda headless por padrão; `CAMOFOX_INTERACTIVE=desktop` abre uma janela local.

### Recursos publicados

| Recurso | Comportamento |
| --- | --- |
| **Anti-detecção** | Camoufox spoofa `hardwareConcurrency`, WebGL, AudioContext, geometria de tela e WebRTC antes do JavaScript |
| **Element refs** | Snapshot devolve refs estáveis para clique e digitação |
| **Cookie import** | Arquivos Netscape; desabilitado a menos que `CAMOFOX_API_KEY` esteja definido |
| **Proxy + GeoIP** | Proxy simples ou backconnect rotativo; locale, timezone e geolocalização derivados do IP de saída |
| **VNC** | Login visual via noVNC e exportação de storage state |
| **Session tracing** | Trace Playwright em zip (screenshots, DOM, rede, console) |
| **Downloads e imagens** | Captura de downloads e extração de `<img>`, opcionalmente inline |
| **YouTube transcript** | Via yt-dlp ou fallback no browser |
| **Structured extract** | `POST /tabs/:tabId/extract` com JSON Schema e `x-ref` |
| **Search macros** | 14 macros, incluindo Google, YouTube, Amazon, Reddit, LinkedIn, TikTok |
| **Telemetria** | Crash/hang anonimizado para o repositório, com opt-out |

### API

| Grupo | Endpoints principais |
| --- | --- |
| Ciclo de abas | `POST /tabs`, `GET /tabs?userId=`, `DELETE /tabs/:id`, `DELETE /sessions/:userId` |
| Interação | `/snapshot`, `/click`, `/type`, `/press`, `/scroll`, `/navigate`, `/wait`, `/back`, `/forward`, `/refresh` |
| Extração | `/links`, `/images`, `/downloads`, `/screenshot`, `/extract`, `/youtube/transcript` |
| Servidor | `/health`, `/start`, `/stop` |
| Sessão | `/sessions/:userId/storage_state`, `/sessions/:userId/cookies`, `/sessions/:userId/traces` |

Snapshots grandes são truncados com paginação por `offset`. Requisições por usuário têm limite de concorrência (padrão 3) e cada sessão tem limite de abas (padrão 10).

## Instalação e uso rápido

Pré-requisitos: Node.js e, na primeira execução, download do binário Camoufox (~300 MB). `yt-dlp` é opcional.

```bash
git clone https://github.com/jo-inc/camofox-browser
cd camofox-browser
npm install
npm start          # porta 9377
```

Via npm:

```bash
npx @askjo/camofox-browser
```

Como plugin do OpenClaw:

```bash
openclaw plugins install @askjo/camofox-browser
```

Ferramentas expostas: `camofox_create_tab`, `camofox_snapshot`, `camofox_click`, `camofox_type`, `camofox_navigate`, `camofox_scroll`, `camofox_screenshot`, `camofox_close_tab`, `camofox_list_tabs`, `camofox_import_cookies`.

Docker (recomendado usar o Makefile, que baixa os binários antes do build):

```bash
make up      # detecta a arquitetura
make down
make reset
```

Windows usa `build.ps1`; Fly.io e Railway têm caminhos próprios (`railway.toml`, `Dockerfile.ci`).

### Variáveis de segurança relevantes

| Variável | Efeito |
| --- | --- |
| `CAMOFOX_API_KEY` | Habilita importação de cookies; sem ela, `POST /sessions/:userId/cookies` retorna 403 |
| `CAMOFOX_ACCESS_KEY` | Exige Bearer token em todas as rotas, exceto `/health` e `/stop` |
| `CAMOFOX_ADMIN_KEY` | Necessária para `POST /stop` |
| `CAMOFOX_BIND_HOST` | Restringe o bind; sem ela o Node usa o padrão de todas as interfaces |
| `CAMOFOX_CRASH_REPORT_ENABLED` | `false` desliga a telemetria |

## Exemplos de uso

Exemplos derivados do README.

```bash
# Abrir aba
curl -X POST http://localhost:9377/tabs \
  -H 'Content-Type: application/json' \
  -d '{"userId":"agent1","sessionKey":"task1","url":"https://example.com"}'

# Snapshot com refs
curl "http://localhost:9377/tabs/TAB_ID/snapshot?userId=agent1"
# -> {"snapshot":"[button e1] Submit  [link e2] Learn more", ...}

# Clicar por ref
curl -X POST http://localhost:9377/tabs/TAB_ID/click \
  -H 'Content-Type: application/json' \
  -d '{"userId":"agent1","ref":"e1"}'

# Buscar com macro
curl -X POST http://localhost:9377/tabs/TAB_ID/navigate \
  -H 'Content-Type: application/json' \
  -d '{"userId":"agent1","macro":"@google_search","query":"best coffee beans"}'
```

Importação de cookies autenticados:

```bash
openssl rand -hex 32                     # gera CAMOFOX_API_KEY
export CAMOFOX_API_KEY="..."
mkdir -p ~/.camofox/cookies
cp ~/Downloads/linkedin_cookies.txt ~/.camofox/cookies/linkedin.txt
```

O agente chama `camofox_import_cookies`; o servidor valida, sanitiza campos e injeta no contexto. O diretório é sandboxed, com proteção contra path traversal, limite de 500 cookies e 5 MB por arquivo.

## Quando usar (e quando não usar)

- **Use quando:** um agente precisa interagir com páginas reais e o snapshot de acessibilidade reduz contexto em relação a HTML bruto.
- **Use quando:** você precisa manter sessão autenticada, reaproveitar cookies ou rodar login visual uma vez.
- **Use quando:** o deployment é isolado e você controla as credenciais e o ambiente.
- **Evite quando:** a navegação pode ser feita por API oficial, feeds ou HTML estático — menos frágil e sem questões de detecção.
- **Evite quando:** o uso envolve contornar controles de acesso ou termos de serviço de terceiros sem autorização.
- **Evite quando:** você não pode expor um browser com sessão autenticada e cookies; o raio de impacto de um vazamento é alto.

## Limitações e cuidados

- **Somente o README foi lido.** Código, testes, plugins, worker de telemetria, Dockerfiles e configuração não foram consultados. Capacidades de anti-detecção e de isolamento são afirmações do projeto.
- **Finalidade controversa.** O projeto existe para reduzir fingerprint e contornar detecção; a legalidade e a aderência a termos de uso dependem do site e da jurisdição. Não há na wiki avaliação jurídica.
- **Superfície de credenciais.** Cookies importados e storage state dão acesso autenticado; o servidor guarda cookies e localStorage em disco por padrão. Proteja `~/.camofox/`, desligue persistência quando não precisar e nunca exponha a porta sem `CAMOFOX_ACCESS_KEY`.
- **Bind padrão amplo.** Sem `CAMOFOX_BIND_HOST`, o Node escuta em todas as interfaces; o README recomenda token de acesso para qualquer deployment além de localhost.
- **Telemetria ligada por padrão.** O envio é anonimizado e o README publica o código e um endpoint de verificação de hash, mas o padrão é enviar. Desligue com `CAMOFOX_CRASH_REPORT_ENABLED=false`.
- **`POST /tabs/:tabId/evaluate`** aparece nas variáveis de ambiente, mas a seção de API do README não o documenta em detalhe; **a verificar** quais garantias existem sobre execução arbitrária de JavaScript.
- **Binário de ~300 MB** baixado no install e mantido em cache; ambientes air-gapped exigem `CAMOUFOX_EXECUTABLE` ou instalação manual.
- **Dependência direta de um fork de browser.** Mudanças no Camoufox ou no Firefox afetam o projeto; a integridade do download é delegada ao `camoufox-js`.
- **Muitos issues abertos.** 240 issues abertas observadas em 2026-10-19 sugerem superfície ampla de falhas e manutenção ativa.
- **Aviso do próprio README:** tokens, moedas ou NFTs usando o nome Camofox não têm relação com o projeto.

## Estado e adoção

- **Versão citada:** npm `@askjo/camofox-browser`; o README não fixa uma versão numérica, apenas a instalação.
- **Atividade e popularidade observadas em 2026-10-19:** ~11,7 mil estrelas, ~1,2 mil forks, 240 issues abertas; criado em 2026-01-26 e último push em 2026-10-16.
- **Licença:** MIT.
- **Linguagem principal:** JavaScript.
- **Branch padrão:** `master`.
- **Commit de referência:** `39c82094013480b373df6600d44c7f036f58356e`.

## Relações

- **Mantido por:** [jo-inc](../../../entities/jo-inc.md), equipe do agente pessoal jo (askjo.ai); o README credita Pradeep Elankumaran como co-fundador e CTO.
- **Conceitos:** [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md) — browser como ferramenta de agente; [CLI agent-first](../../../concepts/cli-agent-first.md) — API desenhada para consumo por agentes, com snapshot estruturado e refs; [Agent skills](../../../concepts/agent-skills.md) — plugin OpenClaw com dez ferramentas; [Evidência e proveniência](../../../concepts/evidencia-e-proveniencia.md) — traces e snapshots como registro do que o agente viu.
- **Alternativas:** Playwright e Puppeteer (não documentados na wiki) — automação convencional, com maior risco de fingerprint; [bytedance/deer-flow](../bytedance/deer-flow.md) usa browser Playwright dentro do harness.
- **Construído sobre:** Camoufox, OpenClaw, yt-dlp.

## Perguntas abertas

- Quão estável é o spoofing do Camoufox contra detecção atual, e quanto ele custa em memória e latência?
- Qual é o isolamento real entre usuários? Um contexto comprometido alcança outro?
- `POST /tabs/:tabId/evaluate` permite execução arbitrária de JS? Há limites?
- Como o servidor se comporta com sites que exigem CAPTCHA interativo?
- Qual é a taxa de falsos negativos do snapshot de acessibilidade em SPAs?
- A telemetria pode vazar conteúdo de página por stack trace ou URL?
- Qual é a política de retenção e proteção de cookies e traces em disco?

## Fontes

- README: https://github.com/jo-inc/camofox-browser/blob/master/README.md (commit `39c82094013480b373df6600d44c7f036f58356e`, consultado em 2026-10-19). Somente o README foi lido; código, testes, plugins e worker de telemetria não foram consultados.
- Metadados do repositório e do perfil: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas e branch padrão).
