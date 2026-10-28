---
type: repo
url: https://github.com/mvanhorn/last30days-skill
host: github.com
owner: mvanhorn
repo: last30days-skill
commit: e06af25a9a78487b75e8509e0e1687fec137176e
license: MIT
language: Python
status: active
created: 2026-10-28
ingested: 2026-10-28
updated: 2026-10-28
tags: [agent-skills, deep-research, reddit, twitter, youtube, tiktok, polymarket, hackernews, github-trends, claude-code, mcp, openclaw]
---

# mvanhorn/last30days-skill

> Skill de agente (`/last30days`) que pesquisa um tópico em paralelo por Reddit, X, YouTube, TikTok, Hacker News, Polymarket, GitHub e outras ~20 fontes, e sintetiza um brief ranqueado por engajamento real, não por SEO.

## O que é

`/last30days` busca o que pessoas reais estão dizendo e fazendo nos últimos 30 dias sobre um tópico — pessoa, empresa, produto, tecnologia ou comparação ("X vs Y") — em vez do que editores e motores de busca tradicionais indexam. A tese do README: cada plataforma social é um jardim murado com sua própria API; um agente de IA com credenciais do usuário pode cruzar todas elas ao mesmo tempo, pontuar o conteúdo pelo engajamento (upvotes, likes, visualizações, odds de mercado) e sintetizar o que de fato importa, em vez de "aqui está o que achei".

## Como funciona

Pipeline em sete passos descrito no README (versão v3; a especificação de runtime vive em `skills/last30days/SKILL.md`, citado como fonte da verdade para comando e setup — não lido nesta ingestão):

1. O usuário digita um tópico (pessoa, empresa, produto, comparação).
2. O agente resolve quem/o que importa: handles do X, repositórios GitHub, subreddits, hashtags do TikTok, canais do YouTube.
3. Todas as fontes são buscadas em paralelo, com expansão de múltiplas queries; resultados pontuados por engajamento, relevância e frescor.
4. Profundidade incomum: transcrições completas de vídeos do YouTube, comentários do Reddit com contagem de upvotes, legendas do TikTok, odds do Polymarket — não só títulos e links.
5. Clusterização: a mesma história relatada em fontes diferentes (ex.: Reddit + X + TikTok) é mesclada em um item, não triplicada.
6. Síntese em um brief único, citado por fonte, ranqueado pelo que as pessoas realmente engajaram.
7. O resultado persiste como contexto da sessão do agente, permitindo perguntas de acompanhamento.

Também tem um modo de descoberta sem tópico ("topic-less discovery"): em host de agente, roda um protocolo de três comandos julgado pelo próprio modelo (nomeia tópicos candidatos, filtra ruído, pontua relevância e escreve ângulos de conteúdo), varrendo listagens de categoria do Reddit, front/best do Hacker News, feeds do Digg e X quando autenticado.

### Fontes cobertas

O README lista ~28 fontes; as principais, por grau de atrito de configuração:

| Grupo | Fontes | Credencial |
|---|---|---|
| Sem configuração | Reddit (com comentários), Hacker News, Polymarket, GitHub, StockTwits | Nenhuma |
| CLIs gratuitas auto-instaladas | arXiv, Techmeme, Digg | Nenhuma (instaladas no primeiro uso) |
| Chave/sessão própria | X/Twitter (`X_BEARER_TOKEN` ou sessão de navegador), YouTube (`yt-dlp`), Bluesky (app password), Perplexity, Brave Search (busca web) | Do usuário |
| ScrapeCreators (uma chave, vários destinos) | TikTok, Instagram Reels, Threads, Pinterest, LinkedIn, comentários do YouTube | 10.000 chamadas gratuitas, depois pay-as-you-go |
| Opt-in explícito | Xiaohongshu (via serviço local de sessão de navegador), Telegram, Trustpilot, Amazon (via Bright Data), Truth Social, DripStack, vagas/páginas de carreira, corpus local (Markdown/texto/PDF) | Variada; várias sem chave do last30days |

## Instalação e uso rápido

```bash
# Claude Code (recomendado — atualiza via marketplace)
/plugin marketplace add mvanhorn/last30days-skill
/plugin install last30days

# Codex, Cursor, Copilot, Gemini CLI ou qualquer um dos 50+ hosts do agentskills.io
npx skills add mvanhorn/last30days-skill -g
```

Também documentados: instalação nativa no Grok (xAI Build CLI), upload manual como `.skill` no claude.ai web, bundle `.mcpb` para Claude Desktop (expõe `/last30days` como servidor MCP, requer Python 3.12+ no PATH), `clawhub install last30days-official` no OpenClaw, e instalação manual via symlink para desenvolvimento.

Zero configuração: Reddit, Hacker News, Polymarket e GitHub funcionam de imediato. Rodar `/last30days` uma vez dispara um wizard de setup que habilita X, YouTube, TikTok, arXiv, Techmeme e outras fontes em ~30 segundos.

## Exemplos de uso

- Preparar uma reunião: `/last30days Peter Steinberger` traz o que a pessoa fez nas últimas semanas (PRs, posts, debates), não o LinkedIn de anos atrás.
- Sinais de contratação: `/last30days Listen Labs --hiring-signals` usa vagas abertas como evidência citada de mudança de foco da empresa.
- Descoberta de tópicos em ascensão: `/last30days what's exploding in AI agents?` devolve 5–10 tópicos ranqueados por velocidade, cada um com um comando `/last30days "<topic>"` pronto para rodar.
- Comparação de ferramentas: `/last30days OpenClaw vs Hermes vs Paperclip`, cruzando estrelas do GitHub em tempo real com citações de X.
- Monitoramento contínuo: `--store` persiste achados em SQLite entre execuções, combinado com os scripts `watchlist.py` (alertas agendados via Slack/webhook) e `briefing.py` (digests diários/semanais).

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é saber o que pessoas reais estão dizendo/fazendo agora sobre um tópico — pesquisa pré-reunião, monitoramento de tendência, comparação de ferramentas, pesquisa de conteúdo — e o usuário aceita configurar pelo menos algumas chaves de API/sessões de navegador para ir além de Reddit/HN/Polymarket/GitHub.
- **Evite quando:** o objetivo é pesquisar os próprios documentos do usuário (nesse caso, ver a categoria [Pesquisa e notas pessoais com IA](../../../categorias.md#pesquisa-e-notas-pessoais-com-ia)), ou quando não há tolerância para dependências externas pagas (ScrapeCreators, Bright Data, Perplexity) além do nível gratuito.

## Limitações e cuidados

- Suporte ao Windows no Claude Desktop está declarado como pendente ("deferred") até que os pontos de entrada de manifesto por plataforma sejam resolvidos.
- Chaves não sincronizam entre Claude Desktop e o skill do Claude Code — são repositórios de credenciais separados por design.
- Reranking (pontuação de relevância) é opt-in: só ocorre se o usuário configurar uma chave de provedor de raciocínio (OpenAI, xAI, OpenRouter, Google); sem chave, usa um modelo de pontuação local e nenhum dado sai da máquina para esse fim.
- O armazenamento local (`LAST30DAYS_STORE=1`) grava um SQLite local; o README afirma que não há upload desse banco para serviço remoto, mas isso não foi verificado de forma independente nesta ingestão.
- Dependências de terceiros com custo real além do nível gratuito: ScrapeCreators (10k chamadas grátis, depois PAYG), Bright Data (créditos do usuário para Amazon), Perplexity/OpenRouter.
- `npx skills` não deduplica instalações: usar ao mesmo tempo o plugin da marketplace do Claude Code e a instalação via `npx skills` faz `/last30days` aparecer duas vezes.
- Esta página documenta apenas o `README.md` da raiz; `skills/last30days/SKILL.md` (citado como fonte da verdade do comando/setup), `CONFIGURATION.md`, `CHANGELOG.md` e o código-fonte não foram lidos.

## Estado e adoção

- Repositório criado em 2026-01-23; push mais recente em 2026-10-27, observado em 2026-10-28.
- 65.710 estrelas, 5.717 forks, 15 issues abertas, observado em 2026-10-28 — "Repository Of The Day" no GitHub Trending e #1 em velocidade de estrelas no Trendshift, segundo os badges do próprio README (não verificado de forma independente).
- Licença: MIT (`LICENSE`, confirmada pela API do GitHub).
- Arquitetura v3 do engine atribuída a `@j-sperling` (colaborador), segundo o README.

## Relações

- Mantido por: [Matt Van Horn (mvanhorn)](../../../entities/mvanhorn.md).
- Conceitos: nenhum conceito dedicado nesta wiki cobre "pesquisa social multiplataforma ranqueada por engajamento"; a página fica listada na nova categoria [Pesquisa social e monitoramento de tendências](../../../categorias.md#pesquisa-social-e-monitoramento-de-tendências).
- Companheiro citado (não dependência, não endossado como mantido pelo mesmo autor): [TweetClaw](https://github.com/Xquik-dev/tweetclaw), plugin OpenClaw para ações de postagem no X/Twitter, de Xquik-dev — não ingerido nesta wiki.

## Perguntas abertas

- O que a especificação completa em `skills/last30days/SKILL.md` define além do que o README resume (comportamento exato de comando, setup wizard)?
- Como o pipeline de clusterização decide que itens de fontes diferentes são "a mesma história", e qual o risco de falso-positivo nessa fusão?

## Fontes

- README: https://raw.githubusercontent.com/mvanhorn/last30days-skill/e06af25a9a78487b75e8509e0e1687fec137176e/README.md (commit `e06af25a9a78487b75e8509e0e1687fec137176e`, consultado em 2026-10-28). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/mvanhorn/last30days-skill`, `api.github.com/users/mvanhorn`), consultada em 2026-10-28.
