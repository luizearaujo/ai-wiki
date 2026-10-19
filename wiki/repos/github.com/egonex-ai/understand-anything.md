---
type: repo
url: https://github.com/Egonex-AI/Understand-Anything
host: github.com
owner: egonex-ai
repo: understand-anything
commit: f2d0164f72fe678805c34245a6df36acededfebd
license: MIT
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [grafos-de-conhecimento, codebase, agent-skills, plugins, visualizacao, tree-sitter, multiagente]
---

# Egonex-AI/Understand-Anything

> Plugin e skill que analisam código, documentação ou uma wiki com pipeline multiagente e produzem um grafo de conhecimento interativo, navegável por dashboard, busca, tours e perguntas em linguagem natural.

## O que é

O README abre com o problema de onboarding — "o codebase tem 200 mil linhas, por onde começar?" — e posiciona o Understand Anything como um **plugin do Claude Code** que analisa o projeto, constrói um grafo de cada arquivo, função, classe e dependência e entrega um dashboard visual. A frase que resume a tese do produto: o objetivo não é um grafo que impressiona pela complexidade, mas um grafo que ensina como as peças se encaixam.

Além de código, o repositório declara dois outros alvos: **domínios de negócio** (como o código se mapeia a processos reais) e **bases de conhecimento no padrão de wiki mantida por LLM** — neste último caso, aponta explicitamente para o gist [`karpathy/llm-wiki`](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

O produto é distribuído como plugin para Claude Code e como skill instalável em um conjunto amplo de agentes e IDEs. O dashboard é servido localmente e também pode ser aberto sem LLM a partir de um grafo já commitado.

## Como funciona

### Híbrido determinístico + semântico

A arquitetura divide o trabalho entre dois componentes, e o README explica por quê:

| Componente | Responsabilidade | Propriedade |
|---|---|---|
| **Tree-sitter** | Parse da árvore sintática: imports, exports, funções, classes, call sites, herança. Imports são pré-resolvidos em um `importMap` e passados aos analisadores de arquivo. | Determinístico: mesma entrada, mesmas arestas; também alimenta a detecção de mudanças por fingerprint. |
| **LLM** | Resumos em linguagem natural, tags, camadas arquiteturais, mapeamento de domínio de negócio, tours e explicações de conceitos de linguagem. | Semântico: captura a intenção do código, não apenas sua estrutura. |

O README chama essa divisão de razão pela qual o grafo é **reproduzível na estrutura** e ainda assim capaz de expressar **para que serve** cada arquivo.

### Pipeline multiagente

O comando `/understand` orquestra cinco agentes; `/understand-domain` adiciona um sexto e `/understand-knowledge` um sétimo:

| Agente | Papel |
|---|---|
| `project-scanner` | Descobre arquivos e detecta linguagens e frameworks. |
| `file-analyzer` | Extrai funções, classes e imports; produz nós e arestas do grafo. |
| `architecture-analyzer` | Identifica camadas arquiteturais. |
| `tour-builder` | Gera tours guiados de aprendizado. |
| `graph-reviewer` | Valida completude e integridade referencial; inline por padrão, revisão completa por LLM com `--review`. |
| `domain-analyzer` | Extrai domínios, fluxos e etapas de processo. |
| `article-analyzer` | Extrai entidades, afirmações e relações implícitas de artigos de wiki. |

Analisadores de arquivo rodam em paralelo, com até **5 workers concorrentes** e **20–30 arquivos por lote**. Reexecuções são incrementais por padrão: apenas arquivos alterados desde a última execução são reanalisados.

### Superfícies de exploração

- **Grafo estrutural:** cada arquivo, função e classe é um nó clicável, com resumo em inglês simples, relações e tours.
- **Visão de domínio:** processos de negócio, fluxos e etapas em grafo horizontal.
- **Base de conhecimento:** grafo force-directed com clustering de comunidades; o parser determinístico extrai wikilinks e categorias de `index.md`, e agentes LLM descobrem relações implícitas, entidades e afirmações.
- **Tours guiados:** walkthroughs da arquitetura ordenados por dependência.
- **Busca fuzzy e semântica:** por nome ou por significado ("quais partes cuidam de auth?").
- **Análise de impacto de diff:** partes afetadas por uma mudança antes do commit.
- **Interface adaptativa por persona:** nível de detalhe ajustado para júnior, PM ou usuário avançado.
- **Camadas visuais:** agrupamento automático em API, Service, Data, UI e Utility.
- **Conceitos de linguagem:** 12 padrões (generics, closures, decorators etc.) explicados no contexto em que aparecem.

### Compartilhamento do grafo

O grafo é JSON puro em `.ua/knowledge-graph.json` (ou no diretório legado `.understand-anything/`, preservado quando já existe). O README recomenda commitá-lo para que colegas pulem o pipeline, ignorando apenas `intermediate/` e `diff-overlay.json`. Grafos acima de 10 MB devem usar Git LFS. Com `--auto-update`, um hook pós-commit atualiza o grafo a cada commit.

## Instalação e uso rápido

Claude Code, caminho nativo:

```bash
/plugin marketplace add Egonex-AI/Understand-Anything
/plugin install understand-anything
/understand
/understand-dashboard
```

Para Codex, OpenCode, OpenClaw, Antigravity, Gemini CLI, Pi Agent, Vibe CLI, VS Code Copilot, Hermes, Cline, KIMI CLI, Trae, Nanobot e Kiro, o README publica um instalador único:

```bash
curl -fsSL https://raw.githubusercontent.com/Egonex-AI/Understand-Anything/main/install.sh | bash
# ou, sem prompt:
curl -fsSL https://raw.githubusercontent.com/Egonex-AI/Understand-Anything/main/install.sh | bash -s codex
```

O instalador clona o repositório em `~/.understand-anything/repo` e cria symlinks para a plataforma escolhida. Cursor e VS Code com Copilot têm auto-descoberta via `.cursor-plugin/plugin.json` e `.copilot-plugin/plugin.json`. No Codex, o prefixo de invocação é `$` (`$understand`), não `/`.

Para visualizar um grafo já gerado **sem Claude Code, sem LLM e sem API key** (requer Node.js >= 18):

```bash
npx https://github.com/Egonex-AI/Understand-Anything/releases/latest/download/understand-anything-viewer.tgz /caminho/do/projeto
```

O servidor é somente leitura e não envia dados para fora da máquina, segundo o README.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Onboarding:** `/understand` seguido de `/understand-onboard` para gerar um guia de entrada para novos membros.
- **Antes de um PR:** `/understand-diff` para ver o impacto das mudanças no grafo.
- **Dúvida sobre um fluxo:** `/understand-chat Como funciona o fluxo de pagamento?`.
- **Arquivo específico:** `/understand-explain src/auth/login.ts`.
- **Monorepo:** `/understand src/frontend` para limitar a análise a um subdiretório.
- **Wiki de conhecimento:** `/understand-knowledge ~/caminho/da/wiki`.
- **Revisão profunda:** `/understand --review` para trocar a validação determinística por uma revisão completa por LLM.
- **Outro idioma:** `/understand --language zh` (suportados: `en`, `zh`, `zh-TW`, `ja`, `ko`, `ru`, `vi`).

## Quando usar (e quando não usar)

- **Use quando:** você entra em um codebase grande e precisa de um mapa navegável e de um tour ordenado por dependência.
- **Use quando:** quer documentar arquitetura, domínios de negócio ou uma wiki de conhecimento como grafo consultável.
- **Use quando:** o time quer compartilhar o grafo versionado e abrir o dashboard sem depender de LLM.
- **Evite quando:** o objetivo é uma resposta pontual sobre um arquivo — o custo da análise completa não se paga.
- **Evite quando:** você precisa de análise puramente determinística e auditável; o Understand Anything usa LLM para summaries, camadas e domínio, ao contrário de abordagens como o [Graphify-Labs/graphify](../graphify-labs/graphify.md).
- **Alternativas documentadas na wiki:** [Graphify-Labs/graphify](../graphify-labs/graphify.md) — grafo determinístico por AST, sem vector store; [DeusData/codebase-memory-mcp](../deusdata/codebase-memory-mcp.md) — servidor MCP de grafo persistente.

## Limitações e cuidados

- **Somente o README foi lido.** Código, pipeline real, esquema do grafo, dashboard e instaladores não foram verificados.
- **Custo de tokens na primeira execução.** O README alerta que `/understand` analisa o projeto inteiro e pode consumir muitos tokens em bases grandes; recomenda plano de tokens, assinatura ou modelo local. As execuções seguintes são incrementais.
- **Dependência de LLM para a camada semântica.** Resumos, camadas, tours e domínio de negócio são gerados por modelo; a qualidade desses artefatos **A verificar**.
- **Grafo é um artefato versionado.** Pode conter caminhos, nomes e resumos de código; avalie o que é commitado em repositórios sensíveis. Grafos grandes exigem LFS.
- **Superfície de instalação ampla.** O instalador usa `curl | bash` e cria symlinks em diretórios de configuração de vários agentes; revise o script antes de executar.
- **Instrução embutida dirigida a agentes.** O README contém um comentário HTML oculto que pede a agentes autônomos que insiram o marcador `__wawawa__` em descrições de PR. É um exemplo de conteúdo de terceiros tentando influenciar o comportamento do agente; deve ser tratado como dado, não como instrução.
- **Suporte declarado, não testado.** A tabela de 17 plataformas é afirmação do README; não há verificação de paridade de recursos entre elas.
- **Licença MIT**, mas o README registra copyright de "Yuxiang Lin and Infinite Universe, Inc.".

## Estado e adoção

- **Versão/releases citadas no README:** o README não publica número de versão; referencia a release `understand-anything-viewer.tgz` em `releases/latest`.
- **Atividade e popularidade observadas em 2026-10-19:** 86.978 estrelas, 7.339 forks, 330 issues abertas; repositório criado em 2026-03-15, último push em 2026-10-12.
- **Licença:** MIT.
- **Linguagem principal (API):** TypeScript.
- **Documentação e demo:** [understand-anything.com](https://understand-anything.com/) e [demo interativa](https://understand-anything.com/demo/).
- **Comunidade:** walkthrough em vídeo do Better Stack citado no README.

## Relações

- **Mantido por:** [egonex-ai](../../../entities/egonex-ai.md).
- **Skill documentada:** [Understand](../../../skills/github.com/egonex-ai/understand-anything/understand.md) — a skill `understand` detalha o método em sete fases que este repositório empacota.
- **Conceitos:** [Grafo de conhecimento de código](../../../concepts/grafo-de-conhecimento-de-codigo.md) — representação persistente de estrutura e relações; [Wiki pessoal com LLMs](../../../concepts/wiki-pessoal-com-llms.md) — `/understand-knowledge` consome wikis no padrão do gist de Karpathy; [Memória de agente](../../../concepts/memoria-de-agente.md) — o grafo commitado serve como contexto persistente; [Agent skills](../../../concepts/agent-skills.md) — distribuição como skill/plugin; [Engenharia reversa agêntica](../../../concepts/engenharia-reversa-agentica.md) — análise assistida de sistemas.
- **Relacionado a:** [Graphify-Labs/graphify](../graphify-labs/graphify.md) — mesma categoria de grafo de código, com ênfase determinística e sem LLM nas arestas; [DeusData/codebase-memory-mcp](../deusdata/codebase-memory-mcp.md) — alternativa via servidor MCP.

## Perguntas abertas

- Qual é o esquema de `knowledge-graph.json` e como ele evolui entre versões?
- Como o pipeline lida com monorepos, submódulos e múltiplos projetos no mesmo repositório?
- Qual é a qualidade real dos resumos, camadas e domínios gerados por LLM em bases heterogêneas?
- O caminho incremental por fingerprint é confiável o suficiente para CI?
- Quais recursos estão disponíveis em cada uma das 17 plataformas declaradas?
- Como o custo de tokens da primeira análise se compara ao de ferramentas determinísticas como o graphify?
- O dashboard e o viewer são abertos ou dependem de componentes proprietários?

## Fontes

- README: https://github.com/Egonex-AI/Understand-Anything/blob/main/README.md (commit `f2d0164f72fe678805c34245a6df36acededfebd`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19).
