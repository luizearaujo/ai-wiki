---
type: repo
url: https://github.com/hesreallyhim/awesome-claude-code
host: github.com
owner: hesreallyhim
repo: awesome-claude-code
commit: f44a84b657a47c7771b690d118c5c1d47acf8bd4
license: desconhecida
language: Python
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [claude-code, catalogo, documentacao, agent-skills, seguranca]
---

# hesreallyhim/awesome-claude-code

> Lista "awesome" canônica do ecossistema Claude Code — mais de 270 recursos anotados em 24 categorias, de guias e skills a status lines, segurança e orquestração multiagente, cada entrada com uma frase de curadoria e badges dinâmicos de criação, atividade, licença e estrelas.

## O que é

O README se descreve, com humor declarado, como "uma coleção cuidadosamente escolhida dos melhores recursos para o mais incrível dos agentes, Claude Code". Na prática é a lista "awesome-*" de maior visibilidade do ecossistema (56 mil estrelas em 2026-10-23), curada manualmente: cada entrada tem uma frase explicando por que o recurso é incluído, não apenas um link. O projeto está em transição de formato — o README avisa que a iteração atual prioriza recursos "novos" e seleções da lista de recomendações, e que recursos "legados" ainda mantidos estão sendo migrados de volta gradualmente, preservados nesse meio tempo em `README_ALTERNATIVES/`.

## Como funciona

A página mantém um sumário gerado automaticamente com 24 categorias de primeiro nível (algumas com subcategorias):

```text
Start Here · From Anthropic · Documentation, Knowledge & Learning
  (Obsidian · Data Visualization)
Open Source Contribution & Maintenance · Research & Scientific Inquiry
Providers, Runtime & Integration Infrastructure
Remote Control, Notifications & Voice I/O · Alternative Clients
Status Lines · Mods · Design & UI/UX · Writing & Prose Quality
Creative Media · Infrastructure & DevOps · Security
Agent Orchestration (Ralph Wiggum · Dynamic Workflows · SDLC)
Skills · Memory & Context Persistence
Observability & Monitoring (Session Monitors · Usage & Cost · Observability)
Configuration · Testing · Linting · Multi-Purpose · Lists & Collections
```

No commit lido, o README tem 276 entradas no formato `- [Nome](url) by [Autor](url) - descrição`. Entradas de repositórios GitHub carregam quatro badges dinâmicos (`shields.io`) de data de criação, último commit, licença e estrelas, renderizados a partir do próprio README — ou seja, as métricas aparecem atualizadas a cada visualização da página, não apenas na data da ingestão.

O repositório também publica dois elementos visuais gerados automaticamente no topo: um "ticker" com uma amostra de projetos Claude Code no GitHub, e uma seção "Recently Added" com os recursos mais recentes — ambos como imagens SVG.

### Seções com maior densidade

As categorias mais extensas no commit lido são **Agent Orchestration** (com subseções próprias para o padrão "Ralph Wiggum", workflows dinâmicos e SDLC), **Security**, **Observability & Monitoring** (dividida em monitores de sessão, uso/custo e observabilidade geral) e **Skills** — refletindo onde a comunidade mais produz ferramentas em 2026.

## Instalação e uso rápido

Não há instalação: é uma lista de links em Markdown, lida diretamente no GitHub ou usada como índice para navegar o ecossistema. O README não documenta um site dedicado (campo `homepage` vazio na API); a leitura acontece no próprio repositório.

## Exemplos de uso

Exemplo de entrada típica, no formato usado em todas as 276 linhas da lista (citado como amostra, não como conteúdo oficial do projeto referenciado):

```text
- [Nome do projeto](https://github.com/owner/repo) by [Autor](https://github.com/owner) -
  frase explicando o que o projeto faz e por que está na lista.
  <badges de criação, último commit, licença e estrelas>
```

## Quando usar (e quando não usar)

- **Use quando:** você quer descobrir o que existe no ecossistema Claude Code — de guias de aprendizado a ferramentas de observabilidade, segurança ou status line — com uma frase de contexto por item em vez de apenas um link cru.
- **Evite quando:** você já sabe o que procura e quer instalar diretamente; nesse caso um catálogo instalável como [davila7/claude-code-templates](../davila7/claude-code-templates.md) ou [VoltAgent/awesome-claude-code-subagents](../voltagent/awesome-claude-code-subagents.md) é mais direto do que navegar uma lista de 276 entradas.

## Limitações e cuidados

- **Lista em transição.** O próprio README avisa que a iteração atual ainda não migrou todos os recursos "legados"; quem busca um projeto específico pode precisar checar `README_ALTERNATIVES/` (não lido nesta ingestão) além da lista principal.
- **Badges dinâmicos, não estáticos.** As contagens de estrelas e a data de último commit exibidas no README mudam a cada carregamento da página; o número `276` registrado aqui reflete apenas a contagem de entradas no commit lido, não as métricas de cada projeto individual.
- **Licença não declarada no README lido.** A API do GitHub retorna `NOASSERTION` para a licença do repositório; não foi possível confirmar nesta ingestão sob qual licença a lista em si é distribuída (os itens listados mantêm suas próprias licenças).
- Apenas o README foi lido: `README_ALTERNATIVES/`, os assets SVG gerados e o código de geração do ticker/"Recently Added" não foram consultados.

## Estado e adoção

- Observado em 2026-10-23: 56.330 estrelas, 4.854 forks, 941 issues abertas; criado em 2025-04-19; último push em 2026-10-23 (mesmo dia da ingestão).
- Licença: não declarada de forma assertiva pela API do GitHub (`NOASSERTION`).
- Linguagem principal na API: Python (scripts de geração de ticker, badges e tabela de conteúdo).

## Relações

- Mantido por: [hesreallyhim](../../../entities/hesreallyhim.md)
- Conceitos: [Agent skills](../../../concepts/agent-skills.md)
- Citado por [davila7/claude-code-templates](../davila7/claude-code-templates.md) como fonte de 21 comandos (CC0 1.0) e por [FlorianBruniaux/claude-code-ultimate-guide](../florianbruniaux/claude-code-ultimate-guide.md) como ponto de descoberta de projetos da comunidade.
- Lista, entre outros, [shareAI-lab/learn-claude-code](../shareai-lab/learn-claude-code.md) na seção "Start Here".

## Perguntas abertas

- Qual critério de curadoria decide o que entra na lista "atual" versus o que fica só em `README_ALTERNATIVES/`?
- Sob qual licença a seleção e as descrições curadas (não os projetos listados) são distribuídas?
- Como a comunidade reporta recursos desatualizados ou abandonados para remoção?

## Fontes

- README: https://raw.githubusercontent.com/hesreallyhim/awesome-claude-code/f44a84b657a47c7771b690d118c5c1d47acf8bd4/README.md (commit `f44a84b657a47c7771b690d118c5c1d47acf8bd4`, consultado em 2026-10-23). Somente o README foi lido; `README_ALTERNATIVES/` e os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`/repos/hesreallyhim/awesome-claude-code`) em 2026-10-23.
