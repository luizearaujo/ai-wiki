---
type: repo
url: https://github.com/ComposioHQ/awesome-claude-skills
host: github.com
owner: composiohq
repo: awesome-claude-skills
commit: be2a406907dbc61b73e6827ded415c96139d13a2
license: Apache-2.0
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [skills, catalogo, claude, mcp, automacao, produtividade, composio]
---

# ComposioHQ/awesome-claude-skills

> Lista curada de mais de mil skills e plugins para Claude e agentes de código, acompanhada de um plugin de conexão e de skills de automação para aplicações SaaS via Composio.

## O que é

O repositório se apresenta como uma **awesome list** de skills "prontas para produção" para Claude.ai, Claude Code, API e agentes como Codex, Cursor, Gemini CLI, Antigravity e Windsurf. A lista reúne tanto skills oficiais da Anthropic quanto contribuições da comunidade, agrupadas por domínio de uso.

Além do catálogo, o repositório distribui material próprio: o plugin `connect-apps`, que liga o Claude a mais de mil aplicações, skills locais como `changelog-generator`, `mcp-builder` e `webapp-testing`, e um conjunto de skills de automação para 78 aplicações SaaS construídas sobre o Rube MCP da Composio.

O README declara licença Apache-2.0, mas a API do GitHub não identifica arquivo de licença no repositório; skills individuais podem ter licenças próprias, segundo o próprio README.

## Como funciona

### Skills, MCP e ferramentas

O README faz uma distinção que organiza todo o catálogo:

| Camada | Papel |
|---|---|
| **Skills** | Definem o **fluxo de trabalho**: o que fazer, em que ordem e com quais salvaguardas. |
| **MCP** | Define **como o agente se conecta** a sistemas externos: autenticação, transporte e descoberta de ferramentas. |
| **Ferramentas (tools)** | São as **ações individuais** que o agente invoca. |

Segundo o README, a produção combina as três: MCP para acesso, ferramentas para ações e skills para comportamento.

### Carregamento progressivo

A lista explica o mecanismo que permite a um agente hospedar centenas de skills sem inflar o contexto: no início da sessão, o agente vê apenas nome e descrição de cada skill (cerca de 100 tokens); o corpo do `SKILL.md` (normalmente menos de 5.000 tokens) só é carregado quando a skill parece relevante; arquivos auxiliares em `scripts/` e `references/` entram sob demanda.

### Organização do catálogo

As entradas são agrupadas nas seguintes seções:

| Seção | Exemplos publicados |
|---|---|
| Processamento de documentos | `docx`, `pdf`, `pptx`, `xlsx`, conversão para EPUB |
| Desenvolvimento e código | `artifacts-builder`, `mcp-builder`, Playwright, TDD, worktrees, revisão |
| Dados e análise | resumo de CSV, `deep-research`, consultas PostgreSQL somente leitura |
| Negócios e marketing | brand guidelines, extração de anúncios, geração de domínios |
| Comunicação e escrita | extração de artigos, pesquisa de conteúdo, análise de reuniões |
| Criatividade e mídia | design, geração de imagens, GIFs, temas, download de vídeo |
| Produtividade e organização | organização de arquivos e faturas, currículos, `kaizen` |
| Colaboração e projetos | git, Google Workspace, Outline, revisão e correção de testes |
| Segurança e sistemas | forense digital, exclusão segura, metadados, Sigma |
| Automação via Composio | 78 skills para CRM, projeto, comunicação, e-mail, DevOps, storage, planilhas, calendário, redes sociais, marketing, suporte, pagamentos, design, analytics e RH |

### Camada de ação

O README posiciona o **MCP Gateway** da Composio como complemento às skills: um único endpoint MCP com autenticação, controle de acesso por equipe, logs de auditoria e integrações prontas. O plugin `connect-apps` usa essa camada para permitir que o Claude envie e-mails, crie issues e publique mensagens. As skills de automação por SaaS combinam sequências de ferramentas, orientação de parâmetros, armadilhas conhecidas e tabelas de referência.

### Estrutura de uma skill

Cada skill é uma pasta com `SKILL.md` (frontmatter YAML com `name` e `description`, seguido de instruções em Markdown) e, opcionalmente, `scripts/`, `templates/` e `resources/`. O README inclui um template básico e recomenda foco em tarefas repetíveis, exemplos, casos de borda, testes nas três plataformas e documentação de pré-requisitos.

## Instalação e uso rápido

O README descreve três caminhos:

| Plataforma | Como usar |
|---|---|
| **Claude.ai** | Ícone de skills no chat → adicionar do marketplace ou enviar skill própria. |
| **Claude Code** | Copiar a pasta da skill para `~/.config/claude-code/skills/`; ela carrega automaticamente. |
| **API** | Passar `skills=["skill-id"]` em `client.messages.create` (exemplo em Python no README). |

Para o plugin de conexão:

```bash
claude --plugin-dir ./connect-apps-plugin
# depois, no Claude:
/connect-apps:setup
```

O setup pede uma API key da Composio; após reiniciar o Claude, o plugin passa a executar ações nas aplicações conectadas. A documentação oficial de skills é referenciada em vez de reproduzida.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Descoberta:** procurar uma skill para uma tarefa (PDF, TDD, Playwright, Jira) e instalar a pasta correspondente.
- **Automação de aplicações:** instalar uma skill de automação (por exemplo, GitHub, Slack ou Linear) e combinar com o MCP Gateway para executar ações.
- **Criação de skills:** usar `skill-creator` e `mcp-builder` como referência de estrutura e de integração.
- **Triagem de contribuições:** seguir os passos de contribuição — caso de uso real, checagem de duplicata, estrutura, teste multiplataforma e pull request.

## Quando usar (e quando não usar)

- **Use quando:** você quer descobrir skills existentes antes de escrever uma, ou precisa de um ponto de partida para automação de aplicações SaaS com MCP.
- **Use quando:** a equipe já usa Composio/Rube e quer skills que falem com os mesmos slugs de ferramentas.
- **Evite quando:** você precisa de um catálogo auditado e com licenças uniformes; a lista agrega projetos de terceiros com qualidade e licenças variadas.
- **Evite quando:** a organização não permite dependência de uma camada comercial de integração; o README promove o MCP Gateway e o Rube MCP da Composio.
- **Alternativas:** bibliotecas de skills com escopo único e curadoria própria, como [mukul975/Anthropic-Cybersecurity-Skills](../mukul975/anthropic-cybersecurity-skills.md), ou coleções de personalidades como [msitarzewski/agency-agents](../msitarzewski/agency-agents.md).

## Limitações e cuidados

- **Somente o README foi lido.** A qualidade, a manutenção e a segurança das milhares de entradas não foram verificadas; o catálogo é uma lista, não um runtime testado.
- **Licença inconsistente:** o README declara Apache-2.0, mas a API do GitHub não registra licença e o próprio README avisa que cada skill pode ter licença diferente.
- **Superfície de supply chain:** instalar skills de terceiros significa executar instruções e, muitas vezes, scripts com acesso ao agente e ao ambiente; o README não descreve revisão de segurança das contribuições.
- **Conflito de interesse:** a lista é mantida pela Composio e direciona parte do conteúdo para o MCP Gateway e as automações da própria empresa; a curadoria não é independente.
- **Volume e manutenção:** são 1.791 issues abertas observadas em 2026-10-19, coerente com um catálogo grande e aberto a contribuições; links e descrições podem envelhecer.
- **Exemplos podem estar defasados:** o trecho de API usa o modelo `claude-3-5-sonnet-20241022` e uma chamada com parâmetro `skills`; a sintaxe atual da API não foi verificada nesta wiki.
- **Contagem não verificada:** "1000+ skills" é uma afirmação do README; não foi feita contagem independente.
- **Carregamento progressivo não é gratuito:** metadados de centenas de skills ainda ocupam contexto; a economia depende de quantas estão instaladas.

## Estado e adoção

- **Atividade e popularidade observadas em 2026-10-19:** 77.430 estrelas, 9.197 forks, 1.791 issues abertas; repositório criado em 2025-10-17, último push em 2026-09-18.
- **Licença:** Apache-2.0 declarada no README; API sem licença detectada.
- **Linguagem principal (API):** Python.
- **Branch padrão:** `master`.
- **Promoção:** o README divulga a plataforma Composio, o MCP Gateway, o Discord e a newsletter da empresa.

## Relações

- **Mantido por:** [Composio (ComposioHQ)](../../../entities/composiohq.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — o catálogo documenta o formato, o carregamento progressivo e a estrutura `SKILL.md`; [Model Context Protocol](../../../concepts/model-context-protocol.md) — distingue MCP de skills e ferramentas; [Plugins de agente](../../../concepts/plugins-de-agente.md) — o plugin `connect-apps` empacota conexões e comandos.
- **Relacionado a:** [multica-ai/andrej-karpathy-skills](../multica-ai/andrej-karpathy-skills.md) — diretrizes de comportamento; [mukul975/Anthropic-Cybersecurity-Skills](../mukul975/anthropic-cybersecurity-skills.md) — biblioteca temática de skills.
- **Alternativas:** catálogos mantidos por comunidades independentes, sem uma camada comercial de integração associada.

## Perguntas abertas

- Qual é o critério efetivo de curadoria para incluir e remover entradas da lista?
- Como a licença Apache-2.0 declarada se aplica às skills de terceiros e aos arquivos auxiliares?
- As skills de automação por SaaS funcionam sem o MCP Gateway da Composio?
- Que revisão de segurança existe para scripts incluídos em skills da comunidade?
- O catálogo mede uso real ou apenas reúne links e descrições?
- Como o carregamento progressivo se comporta com centenas de skills instaladas em um agente?

## Fontes

- README: https://github.com/ComposioHQ/awesome-claude-skills/blob/master/README.md (commit `be2a406907dbc61b73e6827ded415c96139d13a2`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório e do perfil `ComposioHQ` via API do GitHub (consultados em 2026-10-19).
