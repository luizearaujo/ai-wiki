---
type: repo
url: https://github.com/volcengine/OpenViking
host: github.com
owner: volcengine
repo: openviking
commit: 4ab22a4923452362b60aef2826c2083ce36168d2
license: AGPL-3.0
language: Python
status: active
created: 2026-10-24
ingested: 2026-10-24
updated: 2026-10-24
tags: [memoria-de-agente, mcp, agent-skills, rag]
---

# volcengine/OpenViking

> Banco de contexto open-source para agentes de IA que unifica memória, conhecimento e skills num único filesystem virtual sob o esquema `viking://`.

## O que é

OpenViking ataca o problema de memória de agente como caixa-preta: texto entra, embeddings saem, e ninguém vê o que foi de fato armazenado. Em vez disso, organiza todo o contexto de um agente — documentos/código (`resources`), preferências e experiência (`memories`) e instruções de tarefa (`skills`) — como um filesystem navegável por `ls`, `tree`, `read`, `write`, `grep`, com cada diretório carregando um resumo gerado automaticamente.

É mantido pela Volcano Engine (Volcengine), braço de cloud/IA da ByteDance.

## Como funciona

O espaço de nomes principal se divide em `resources/` (projetos, docs, repositórios, páginas web) e `user/{user_id}/` (memories, resources privados, skills, peers). Cada recurso processado ganha três camadas de carregamento progressivo:

- **L0 (Abstract):** resumo de uma frase para checagem rápida de relevância.
- **L1 (Overview):** estrutura e pontos-chave para planejamento.
- **L2 (Details):** conteúdo completo, lido só quando necessário.

Duas ferramentas de busca: `find` roda uma query direta; `search` planeja a recuperação a partir do contexto da sessão — ambas podem ser restritas a um diretório/subárvore em vez de varrer todo o índice vetorial. Sessões podem ser "commitadas": a conversa é arquivada e memórias são extraídas como Markdown inspecionável e editável. Com o VikingBot (framework de agente embutido) habilitado, `ov compile` organiza material-fonte em wiki, grafo de conhecimento ou relatório.

## Instalação e uso rápido

Requer um servidor OpenViking rodando (uv + Python 3.10+ e um provedor de modelo com embedding e VLM):

```bash
uv tool install openviking --upgrade && openviking-server init
```

`init` grava `~/.openviking/ov.conf` e suporta Volcengine, OpenAI, Codex OAuth, Kimi, GLM e Ollama local. Alternativas: instalador único (`curl -fsSL https://openviking.ai/install | bash`), Docker (imagem oficial já traz VikingBot), ou o serviço hospedado pela própria Volcengine (50 primeiros arquivos grátis).

A CLI `ov` (incluída no pacote `openviking`) expõe `ov status`, `ov add-resource <url>`, `ov task status`, `ov ls`, `ov tree`, `ov find`, `ov grep`. SDKs oficiais em Python, Go e TypeScript, mais API HTTP.

## Exemplos de uso

```bash
ov add-resource https://github.com/volcengine/OpenViking
ov find "what is openviking"
ov grep "openviking" --uri viking://resources/volcengine/OpenViking/docs/en
```

Para conectar um agente de código (Claude Code, Codex, Cursor, TRAE, OpenCode e outros) à memória cross-sessão, o README orienta instalar o "memory plugin" via `curl -fsSL https://openviking.ai/install | bash -s -- --yes --url <SERVER_URL>`.

## Quando usar (e quando não usar)

- **Use quando:** quiser uma camada única e inspecionável de memória + conhecimento + skills, compartilhada entre vários agentes/CLIs, com granularidade de busca por diretório.
- **Evite quando:** precisar de um núcleo totalmente permissivo (o projeto principal é AGPLv3, não Apache/MIT) ou não quiser depender de um servidor adicional só para memória.

## Limitações e cuidados

- Licenciamento misto: projeto principal AGPLv3; `crates/ov_cli` e `examples` em Apache 2.0 (o plugin Hermes em `examples/hermes-plugin` mantém MIT); adapters em `integrations/frameworks` declaram AGPLv3 mas seus exemplos executáveis ficam em Apache 2.0.
- README proíbe explicitamente reescrita integral do projeto para "reabri-lo" sob outra licença, e exige autorização por escrito da Volcano Engine para traduzir partes substanciais do código para outra linguagem.
- Os benchmarks (LoCoMo, tau2-bench) usam modelos Doubao da própria Volcengine como VLM e embedding; são resultados do projeto, não verificados de forma independente nesta ingestão.
- Desktop app está em beta (macOS/Windows); Linux não tem build de desktop listado.
- **A verificar:** maturidade e cobertura real de cada integração de agente (Claude Code, Codex, Cursor, TRAE, OpenCode, Hermes, pi, DeerFlow, DSH, Doubao Work, LangChain) além do que o README descreve.

## Estado e adoção

- Observado em 2026-10-24: ~40.700 stars, 3.297 forks, 1.071 issues abertas, push mais recente em 2026-10-24.
- Versão de benchmark citada no README: OpenViking 0.3.22.
- Licença: AGPLv3 (núcleo), Apache 2.0 e MIT em componentes específicos (ver acima).

## Relações

- Mantido por: [Volcengine](../../../entities/volcengine.md), braço de IA/cloud da [ByteDance](../../../entities/bytedance.md).
- Conceitos: [Memória de agente](../../../concepts/memoria-de-agente.md), [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md).
- Alternativas/parceiros citados no README: mem0, Honcho, [bytedance/deer-flow](../bytedance/deer-flow.md) (DeerFlow usa OpenViking como um dos backends opcionais de memória), NoKV, loopx, Hermes Agent, NVIDIA cuVS.

## Perguntas abertas

- Qual o status real de produção fora dos benchmarks internos da Volcengine?
- Como a cláusula contra "reescrita integral e reabertura" se sustenta juridicamente fora da China?
- Os adaptadores de framework (LangChain/Microsoft Agent Framework) têm paridade de recursos com o CLI `ov`?

## Fontes

- README: https://raw.githubusercontent.com/volcengine/OpenViking/4ab22a4923452362b60aef2826c2083ce36168d2/README.md (commit `4ab22a4923452362b60aef2826c2083ce36168d2`, consultado em 2026-10-24). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados da API do GitHub, consultados em 2026-10-24.
