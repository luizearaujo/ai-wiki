---
type: repo
url: https://github.com/DeusData/codebase-memory-mcp
host: github.com
owner: DeusData
repo: codebase-memory-mcp
commit: 354ccecbe612a9fdb624396a6738fa87f2617434
license: MIT
language: C
status: active
created: 2026-10-18
ingested: 2026-10-18
updated: 2026-10-18
tags: [mcp, servidor-mcp, grafo-de-conhecimento, code-intelligence, tree-sitter, sqlite, agentes]
---

# DeusData/codebase-memory-mcp

> Servidor MCP local de alta performance que indexa qualquer base de código em um grafo de conhecimento persistente, fornecendo busca estrutural, rastreamento de chamadas e visualização de arquitetura para agentes de codificação — com ~120× menos tokens que exploração arquivo por arquivo.

## O que é

codebase-memory-mcp (CBM) é um servidor [Model Context Protocol](../../../concepts/model-context-protocol.md) escrito em C puro que constrói e consulta um grafo de conhecimento de código. Ele indexa funções, classes, importações, rotas HTTP e seus relacionamentos em 162 linguagens via gramáticas tree-sitter compiladas no próprio binário. O binário é estático, sem dependências de runtime, Docker ou chaves de API.

O servidor expõe 17 ferramentas MCP e suporta 45 integrações automáticas ou condicionais com clientes de codificação (Claude Code, Cursor, Codex, Gemini CLI, OpenCode etc.). Inclui também CBM Lens Beta — uma interface browser com mapa de arquitetura 3D, visualização de grafo (Galaxy), leitor de código (Explore) e chat local com modelo WebGPU.

## Como funciona

O pipeline de indexação opera em três camadas:

1. **Parser**: gramáticas tree-sitter compiladas extraem símbolos e relacionamentos para 162 linguagens. Para Python, TypeScript, JavaScript, PHP, C#, Go, C, C++, Java, Kotlin, Rust e Perl existe resolução semântica de tipos via **Hybrid LSP** — uma implementação C leve inspirada em tsserver, pyright, gopls, Roslyn e rust-analyzer.
2. **Pipeline RAM-first**: LZ4 HC + SQLite em memória. Um único dump ao final libera memória ao SO.
3. **Grafo persistente**: SQLite em `~/.cache/codebase-memory-mcp/`. Consultas Cypher-like, BM25 FTS5, busca semântica por embeddings (Nomic `nomic-embed-code`, 40K tokens, 768d int8 compilados no binário).

O **Session Coordination Daemon** compartilha um único daemon por conta entre todos os clientes configurados. O daemon gerencia watchers de mudança por git, jobs de indexação em background e a UI. Processos CBM simultâneos devem usar exatamente a mesma versão e cache root — uma barreira OS garante isso.

Tipos de aresta no grafo (seleção):

| Aresta | Significado |
|--------|-------------|
| `CALLS` / `CALL_REFERENCE` | Invocação direta ou referência exata de callable |
| `IMPORTS`, `DEFINES`, `IMPLEMENTS`, `INHERITS` | Relações estruturais |
| `HTTP_CALLS`, `ASYNC_CALLS` | Chamadas cross-service |
| `SPAWNS` | Programa iniciando outro processo |
| `DEPLOYS` | CI/CD, kubectl, Helm, Terraform aplicando manifests |
| `INFRA_MAPS`, `CONNECTS_TO`, `CONFIGURES` | Infraestrutura (K8s, Compose, Terraform, Ansible) |
| `EMITS`, `LISTENS_ON` | Canais (Socket.IO, EventEmitter, pub-sub) |
| `SIMILAR_TO`, `SEMANTICALLY_RELATED` | Near-clone e similaridade semântica |

## Instalação e uso rápido

**macOS / Linux (instalador automático):**

```bash
curl -fsSL https://raw.githubusercontent.com/DeusData/codebase-memory-mcp/main/install.sh | bash
```

**Windows (PowerShell):**

```powershell
Invoke-WebRequest -Uri https://raw.githubusercontent.com/DeusData/codebase-memory-mcp/main/install.ps1 -OutFile install.ps1
Unblock-File .\install.ps1
.\install.ps1
```

**Via Claude Code:**

```
"Install this MCP server: https://github.com/DeusData/codebase-memory-mcp"
```

Disponível também via npm, PyPI, Homebrew, Scoop, AUR e Nix flake.

Após instalar, reiniciar o agente e dizer **"Index this project"** — pronto.

## Exemplos de uso

Consultas de exemplo via MCP (o agente traduz perguntas para chamadas de ferramenta):

```
"What calls ProcessOrder?"
→ trace_path(function_name="ProcessOrder", direction="inbound")

"Find all HTTP routes in the payment service"
→ get_architecture(aspects=["routes"])

"Are there unused functions?"
→ detect_dead_code()

"Show how module A depends on module B"
→ search_graph(cypher_query="MATCH (a:Module)-[*]->(b:Module) WHERE a.name='A' AND b.name='B' RETURN path")
```

**CBM Lens Beta** (interface browser):

```bash
codebase-memory-mcp daemon start --open --port=9749
# Abre http://127.0.0.1:9749
```

Workspaces disponíveis: Architecture (mapa 3D), Galaxy (grafo 3D), Explore (leitor de código), ADR (decisões arquiteturais), Coverage, System.

**Auto-index:**

```bash
codebase-memory-mcp config set auto_index true
```

## Quando usar (e quando não usar)

- **Use quando:** o agente precisa navegar uma base de código grande sem ler arquivo por arquivo; quando chamadas cross-service, rotas HTTP ou dependências de infraestrutura precisam ser rastreadas; quando ~120× redução de tokens é relevante para custo ou contexto.
- **Evite quando:** a base de código é trivialmente pequena (< 1K LOC) — overhead de indexação não compensa; quando a linguagem não é suportada por tree-sitter (improvável dado 162 linguagens); quando resolução semântica profunda de tipos é necessária para linguagens fora do Hybrid LSP.

## Limitações e cuidados

- **CBM Lens Beta** (interface visual avançada) está apenas em `main`; a release v0.11.0 inclui apenas a UI anterior. Para usar o Lens atual é preciso [compilar da fonte](https://github.com/DeusData/codebase-memory-mcp?tab=readme-ov-file#build-from-source).
- Métricas de redução de tokens (~120×) são do próprio projeto para cinco queries específicas; o estudo independente (arXiv 2603.27277) reporta 10× em 31 repositórios — contextos diferentes.
- O chat local do CBM Lens usa modelos pequenos (Qwen2.5 Coder 0.5B padrão) via WebGPU; requer `shader-f16`. "Escreve frouxamente, especialmente em idiomas fora do inglês."
- O **Team-Shared Graph Artifact** (`.codebase-memory/graph.db.zst`) pode crescer rapidamente se commitado a cada reindexação — o README documenta um caso de ~6 GB em ~350 commits.
- Windows: SmartScreen e Defender podem gerar alertas (falso positivo documentado); o README instrui verificação manual de checksums SHA-256.
- A barreira de versão exata entre processos CBM significa que atualizar o daemon enquanto sessões estão ativas requer fechar todas as sessões.
- Não lidos: `docs/`, código-fonte, SECURITY.md, CONFIGURATION.md, manifestos de release.

## Estado e adoção

- Última release: v0.11.0 (conforme README); `main` está à frente com CBM Lens Beta.
- Observado em 2026-10-18: ~46.796 stars, ~3.860 forks, ~643 issues abertas.
- Licença: MIT.
- Pesquisa acadêmica: arXiv 2603.27277.
- Certificações: SLSA 3, OpenSSF Scorecard, VirusTotal a cada release.
- Distribuição: npm, PyPI, Homebrew, Scoop, AUR, Nix flake, binários nativos por plataforma.

## Relações

- Mantido por: [DeusData](../../../entities/deusdata.md)
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Grafo de conhecimento de código](../../../concepts/grafo-de-conhecimento-de-codigo.md)
- Relacionado: [morluto/rea](../morluto/rea.md) — outro servidor MCP local para análise de código, com foco em engenharia reversa de binários em vez de indexação contínua.

## Perguntas abertas

- Qual é o estado exato de suporte no Windows para hooks e agentes (vários clientes têm hooks "withheld on Windows")?
- Como o Hybrid LSP lida com projetos multilinguagem com dependências cruzadas entre Python e TypeScript, por exemplo?
- Qual é o plano de release para CBM Lens Beta sair de `main` para uma release estável?
- A pesquisa do arXiv (2603.27277) foi peer-reviewed ou é apenas preprint?

## Fontes

- README: https://raw.githubusercontent.com/DeusData/codebase-memory-mcp/354ccecbe612a9fdb624396a6738fa87f2617434/README.md (commit `354ccecbe612a9fdb624396a6738fa87f2617434`, consultado em 2026-10-18). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub em 2026-10-18.
