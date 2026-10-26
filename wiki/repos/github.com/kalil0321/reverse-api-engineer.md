---
type: repo
url: https://github.com/kalil0321/reverse-api-engineer
host: github.com
owner: kalil0321
repo: reverse-api-engineer
commit: b9337039bb68aeb59e652aca00ce42d241d33211
license: MIT
language: Python
status: active
created: 2026-10-26
ingested: 2026-10-26
updated: 2026-10-26
tags: [engenharia-reversa, api, har, navegacao-web, agentes, claude-code, codex, playwright, cli]
---

# kalil0321/reverse-api-engineer

> Transforma qualquer site em um cliente de API tipado: um agente (ou o próprio usuário) navega no site, o tráfego de rede é capturado em um arquivo HAR e um LLM gera o cliente em até 10 linguagens.

## O que é

Reverse API Engineer automatiza o processo que antes era manual: abrir o DevTools do navegador, copiar requisições cURL e montar um cliente na mão. O fluxo completo é:

1. Você informa um site e um objetivo ("buscar todas as vagas da Apple")
2. Um browser visita o site — conduzido por você ou por um agente de IA
3. O tráfego HTTP é capturado em um arquivo HAR
4. O modelo configurado lê o tráfego e escreve um cliente funcional

**Output:** diretório `./scripts/{nome_descritivo}/` com `api_client.<ext>`, `README.md` e `example_usage.<ext>`.

## Quatro modos de operação

| Modo | O que faz |
|---|---|
| `manual` | Você navega; o modelo gera o cliente a partir do tráfego capturado |
| `agent` | Agente de IA navega e captura autonomamente |
| `engineer` | Regera o cliente a partir de uma captura anterior (sem novo browsing) |
| `collector` | Agente coleta dados estruturados (JSON/CSV) via busca web + fetch |

Alterna entre modos com **Shift+Tab** dentro da CLI interativa.

## Provedores de agente (modo `agent`)

| Provedor | Como funciona |
|---|---|
| `auto` (padrão) | Playwright MCP — um workflow para browsing + reverse engineering |
| `chrome-mcp` | Controla o Chrome real com sessões e cookies existentes; requer Chrome 146+ e Node.js 20.19+ |
| `agent-browser` | Usa o CLI [Vercel agent-browser](https://github.com/vercel-labs/agent-browser); instalado automaticamente se não encontrado no `PATH` |

## Linguagens de saída e SDKs

**Linguagens:** Python (padrão), JavaScript, TypeScript, Go, Java, C#, PHP, Ruby, C, PowerShell.

**SDKs:** `claude` (padrão), `opencode`, `cursor`, `copilot` (GitHub Copilot). Com `opencode`, RAE reutiliza um servidor existente ou inicia `opencode-ai@latest` via `npx`.

Configuração em `~/.reverse-api/config.json` ou via `/settings` na CLI interativa.

## Instalação

```bash
uv tool install reverse-api-engineer
# com modo manual (Playwright local):
uv tool install "reverse-api-engineer[manual]"
playwright install chromium
```

Requer Python 3.11+. Modo agent (padrão) usa browser via `npx`; não precisa do extra `[manual]`.

## CLI scriptável

```bash
# captura agêntica com saída JSON
reverse-api-engineer agent --prompt "capture public jobs api" \
  --url https://example.com/jobs --json | jq

# listar e inspecionar histórico
reverse-api-engineer list --json
reverse-api-engineer show <run_id> --json

# reexecutar script gerado
reverse-api-engineer run <run_id> --file api_client.py --no-interactive
```

Saída JSON tem schema versionado (`schema_version: 1`) com `status`, `run_id`, `har_path`, `script_path` e `usage` (tokens + custo).

## Comparação com ferramentas similares

| | reverse-api-engineer | [littledivy/mimic](../littledivy/mimic.md) | [D4Vinci/Scrapling](../d4vinci/scrapling.md) |
|---|---|---|---|
| Captura | HAR via Playwright/Chrome MCP/agent-browser | mitmproxy (iOS + web) | Playwright + HTTP direto |
| Geração | cliente em 10 linguagens | cliente Python | dados estruturados |
| Linguagens de saída | 10 | Python | Python |
| SDKs | Claude, OpenCode, Cursor, Copilot | Claude | não gera código |
| Modo agente | sim (navegação autônoma) | não | sim (Agent Skill) |

## Posicionamento

Distingue-se pelo foco em **gerar código de cliente**, não em extrair dados ou analisar binários. O HAR torna a captura reproduzível: é possível regerar o cliente em outra linguagem sem navegar novamente (`engineer` mode). O modo `collector` é complementar: em vez de um cliente de API, entrega dados estruturados.

**A verificar:** sem informações sobre taxa de sucesso em sites com proteção anti-bot agressiva, integração com outros provedores de LLM além dos listados ou suporte a captura de tráfego fora de HTTP (ex.: WebSockets). Somente o README foi lido.

## Fontes

- README no commit `b9337039bb68aeb59e652aca00ce42d241d33211` (consultado em 2026-10-26). Somente o README foi lido.
- Metadados: GitHub API — Python, MIT, 1.940 estrelas, 210 forks (2026-10-26).
