---
type: repo
url: https://github.com/lfnovo/open-notebook
host: github.com
owner: lfnovo
repo: open-notebook
commit: a0f6f3081ae06328f0a451b3a3ef2959ca25721d
license: MIT
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [pesquisa-pessoal, notebooklm, self-hosted, mcp]
---

# lfnovo/open-notebook

> Alternativa self-hosted e multi-provedor ao Google Notebook LM: organiza PDFs, vídeos, áudio e páginas web em notebooks de pesquisa, com busca full-text e vetorial, chat com citação de fonte e geração de podcast com até quatro falantes.

## O que é

Open Notebook endereça a mesma proposta do Notebook LM do Google — pesquisa assistida por IA sobre o próprio material — mas self-hosted, com escolha de mais de 20 provedores de modelo (OpenAI, Anthropic, Google, Mistral, Ollama e qualquer servidor compatível com a API da OpenAI, como LM Studio e vLLM) via a biblioteca própria [Esperanto](https://github.com/lfnovo/esperanto). O README compara lado a lado com o Notebook LM: controle de dados, escolha de provedor, até quatro falantes no podcast (contra dois), API REST completa e deploy em qualquer lugar.

## Como funciona

- **Notebooks multi-modais**: PDFs, vídeos, áudio, páginas web e outros formatos organizados em notebooks de pesquisa separados.
- **Busca full-text e vetorial** sobre todo o conteúdo indexado, com controle fino de o que entra no contexto de cada conversa.
- **Transformações de conteúdo**: ações customizáveis para resumir e extrair insights, além de suporte a modelos de raciocínio como DeepSeek-R1 e Qwen3.
- **Geração de podcast** multi-falante com "Episode Profiles", roteiro sob controle total do usuário.
- **Citações**: respostas citam as fontes, notas e insights usados.
- **API REST completa** para integração programática, e integração MCP para conectar com Claude Desktop, VS Code e outros clientes MCP.
- Stack: Python, FastAPI, Next.js, React e SurrealDB como banco.

## Instalação e uso rápido

```bash
mkdir open-notebook && cd open-notebook
curl -o docker-compose.yml https://raw.githubusercontent.com/lfnovo/open-notebook/main/docker-compose.yml
# editar OPEN_NOTEBOOK_ENCRYPTION_KEY no docker-compose.yml para um segredo próprio
docker compose up -d
# abrir http://localhost:8502 e conectar um provedor de IA na UI (não em arquivo de config)
```

A UI (porta 8502) e a API (porta 5055) ficam expostas em todas as interfaces de rede, sem senha por padrão — o README recomenda restringir a `127.0.0.1` ou definir `OPEN_NOTEBOOK_PASSWORD` antes de iniciar em uma máquina compartilhada. Também há caminho de instalação local-only com Ollama (sem custo de API).

## Quando usar (e quando não usar)

- **Use quando:** quer um Notebook LM auto-hospedado, com dados sob controle próprio e liberdade de provedor de modelo (incluindo 100% local via Ollama).
- **Evite quando:** precisa de suporte multiusuário robusto ou de agentes operando o Open Notebook via MCP de forma madura — o próprio README lista isso como direção futura ("Horizon" em `VISION.md`), não recurso atual.

## Limitações e cuidados

- Sem senha e exposto em todas as interfaces por padrão — requer configuração manual de segurança para deploys compartilhados.
- Anthropic e Groq não oferecem modelo de embedding; o README recomenda parear com outro provedor para essa função.
- Documentação extensa (guias de instalação, conceitos, troca de provedor) não foi lida além do README nesta ingestão.

## Estado e adoção

- 40.427 estrelas, 4.650 forks, 180 issues abertas — observado em 2026-10-21.
- Repositório criado em 2024-10-21 (exatos dois anos antes desta ingestão), com push mais recente em 2026-10-20 — observado em 2026-10-21.
- Licença: MIT.

## Relações

- Mantido por: [Luis Novo (lfnovo)](../../../entities/lfnovo.md)
- Alternativa comparável (também NotebookLM-like, documentada nesta mesma ingestão): [MODSetter/SurfSense](../modsetter/surfsense.md) — SurfSense é um app desktop air-gapped que também edita arquivos; Open Notebook é self-hosted via Docker com foco em notebooks de pesquisa e podcast.

## Perguntas abertas

- Como o suporte a MCP atual (cliente conectando Claude Desktop/VS Code ao Open Notebook) se diferencia da direção futura de "agentes operando o Open Notebook via MCP" citada em `VISION.md`?

## Fontes

- README: https://raw.githubusercontent.com/lfnovo/open-notebook/a0f6f3081ae06328f0a451b3a3ef2959ca25721d/README.md (commit `a0f6f3081ae06328f0a451b3a3ef2959ca25721d`, consultado em 2026-10-21). Somente o README foi lido; a documentação em `docs/` não foi consultada.
- Metadados: API do GitHub (`api.github.com/repos/lfnovo/open-notebook`), consultada em 2026-10-21.
