---
type: repo
url: https://github.com/pbakaus/impeccable
host: github.com
owner: pbakaus
repo: impeccable
commit: 0665bd812ae0908fcab17b96fd4f840defb882d9
license: Apache-2.0
language: Rust
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, frontend, agent-skills, cli, lint, navegador, rust]
---

# pbakaus/impeccable

> Linguagem de design para agentes de código: uma skill com 24 comandos, iteração visual no navegador e um detector determinístico de 61 regras contra os vícios do frontend gerado por IA.

## O que é

O Impeccable se apresenta como uma camada de direção de design para harnesses de código. O README parte da skill [frontend-design](https://github.com/anthropics/skills/tree/main/skills/frontend-design), da Anthropic, e argumenta que todo modelo foi treinado nos mesmos templates SaaS: Inter em tudo, gradientes roxo-azul, cards aninhados, texto cinza sobre fundo colorido e o mesmo ícone arredondado acima de cada título.

O projeto reúne três peças: uma **skill** (`impeccable`) acessada por `/impeccable <comando> <alvo>`, um **CLI** autocontido que roda o detector sem LLM nem chave de API, e **hooks nativos** que aplicam o detector durante edições de UI em harnesses selecionados. A proposta não é gerar imagens nem oferecer um catálogo de estilos, mas instalar um processo de contexto, execução e verificação.

## Como funciona

### Contexto persistente: `PRODUCT.md` e `DESIGN.md`

O fluxo começa com `/impeccable init`, que inspeciona o projeto, pergunta apenas o que falta e grava a "verdade durável do produto" em `PRODUCT.md` — audiência, propósito, contexto de uso, restrições, voz e evidências. A direção visual não se mistura a esses fatos: sistemas visuais existentes ou recém-criados ficam registrados à parte em `DESIGN.md`. `/impeccable document` gera esse arquivo a partir do código existente.

### 24 comandos

Os comandos são agrupados por função:

| Grupo | Comandos |
|---|---|
| Construir | `shape`, `init`, `document`, `extract` e o `craft` |
| Avaliar | `critique` (revisão de UX) e `audit` (a11y, performance, responsividade) |
| Refinar | `polish`, `bolder`, `quieter`, `distill`, `harden`, `onboard` |
| Realçar | `animate`, `colorize`, `typeset`, `layout`, `delight`, `overdrive` |
| Corrigir | `clarify`, `adapt`, `optimize` |
| Iterar | `live` (variantes no navegador) e `generate` (variantes de um elemento) |

`/impeccable pin <comando>` cria atalhos autônomos, como `/audit`. O README também lista anti-padrões explícitos: fontes desgastadas, texto cinza sobre cor, preto/cinza puros sem tinta, cards aninhados e easing elástico.

### Detector determinístico

O CLI detecta **61 problemas determinísticos**, divididos entre "AI slop" (bordas laterais em abas, gradientes roxos, easing com bounce, brilhos escuros) e qualidade geral de design (comprimento de linha, padding apertado, alvos de toque pequenos, níveis de título pulados). A varredura roda sem LLM e sem chave de API, em diretórios, arquivos HTML ou URLs renderizadas.

```bash
npx impeccable detect src/
npx impeccable detect https://example.com
npx impeccable detect --json .
```

Saídas legíveis vão para stderr; `--json` usa stdout. Códigos de saída: `0` sem achados primários, `2` com achados primários, `1` quando algum alvo não pôde ser varrido. O README ressalva que uma execução limpa é evidência, não prova de qualidade visual ou acessibilidade.

### Hooks e verificação contínua

Em Claude Code, GitHub Copilot, Codex, Cursor e Grok Build, o instalador grava um manifesto de hook nativo. O hook roda o detector em edições diretas de arquivos de UI e devolve os achados ao fluxo do agente. Cursor bloqueia escritas ruins antes de acontecerem; Claude Code, Copilot e Codex mostram os achados após a edição e fazem uma passada mais profunda no evento Stop; Grok Build aquece no Stop. O launcher da skill executa um binário autocontido — não exige Node, exceto no caminho `npx`.

### Build path: comp-first ou code-first

Superfícies novas podem gerar primeiro um comp de alta fidelidade e construir para igualá-lo (`comp`), ou construir direto em código com a ambição registrada em um contrato de direção (`code`). O primeiro compõe com mais ousadia e demora mais; o segundo é mais enxuto e rápido. A escolha é gravada em `.impeccable/config.json` como `buildPath`.

### Telemetria e modo live

A cada novo design, a skill consulta a API da Impeccable para sortear um "mundo visual" do catálogo. Por padrão, também envia um registro anônimo de qual mão foi mostrada e qual carta venceu. O README afirma que nomes de projeto, arquivos, código, `PRODUCT.md` e nomes de direção nunca são enviados, e documenta a desativação por `npx impeccable telemetry off`, `DO_NOT_TRACK=1` ou `IMPECCABLE_NO_TELEMETRY=1`.

O modo live edita um checkout local por servidor de desenvolvimento ou HTML estático local. Injetar o helper em um site em produção não é suportado. Para inspecionar produção, o caminho é `npx impeccable detect <url>` ou a extensão de navegador, que não editam o código.

### Artefatos de trabalho

Comandos gravam arquivos em `.impeccable/`: screenshots, estado de sessões, caches e configuração por desenvolvedor. O README publica um bloco de `.gitignore` com marcadores e separa o que é efêmero do que deve ser versionado — `config.json`, `live/config.json`, `design.json`, `surfaces/*.md` e `critique/*.md`.

## Instalação e uso rápido

Cinco caminhos são publicados:

1. **Instalador via CLI (recomendado):**
   ```bash
   npx impeccable install
   ```
   Detecta harnesses, permite escolher providers e escopo (`--scope=project|global`) e instala os hooks nativos quando aplicável. `npx impeccable update` atualiza.
2. **Git submodule:** adicionar o repositório como `.impeccable`, rodar `npx impeccable link --source=.impeccable --providers=claude,cursor` e versionar.
3. **Plugin:** extensão do GitHub Copilot no VS Code, marketplace do Claude Code (`/plugin marketplace add pbakaus/impeccable`) ou plugin do Grok Build.
4. **Download do site:** ZIP por ferramenta em [impeccable.style](https://impeccable.style).
5. **Cópia de `dist/`:** diretórios prontos para Cursor, Claude Code, OpenCode, DeepSeek Harness, Hermes, Pi, Gemini CLI, Codex, Copilot, Trae, Rovo Dev, Qoder, Mistral Vibe, Grok Build e Google Antigravity.

Depois da instalação, o uso básico é `/impeccable init` e, em seguida, comandos como `/impeccable audit`, `/impeccable polish` ou `/impeccable critique`. O README lista 17 ferramentas suportadas.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Auditoria de área:** `/impeccable audit blog` verifica hub e páginas de post.
- **Revisão de UX:** `/impeccable critique landing` produz parecer sobre hierarquia, clareza e ressonância.
- **Pré-lançamento:** `/impeccable polish settings` faz a passada final de alinhamento ao design system.
- **Robustez:** `/impeccable harden checkout` adiciona tratamento de erro, i18n, overflow e casos de borda.
- **Pedido livre:** `/impeccable redo this hero section` aciona o comando adequado a partir da descrição.
- **CI:** `npx impeccable detect --json .` gera saída legível por máquina para bloquear regressões.

## Quando usar (e quando não usar)

- **Use quando:** o projeto tem superfície visual e o objetivo é construir, revisar, auditar, polir ou evoluir UI com um vocabulário compartilhado entre pessoa e agente; ou quando se quer um lint determinístico de design em CI.
- **Use quando:** o time usa múltiplos harnesses e precisa da mesma skill e das mesmas regras em Claude Code, Cursor, Codex, Copilot e outros.
- **Evite quando:** a tarefa é backend ou não tem interface visual; ou quando hooks automáticos que executam binários e leem arquivos de projeto não são aceitáveis por política de segurança.
- **Alternativas documentadas na wiki:** [UI/UX Pro Max](../../../skills/github.com/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md) para uma base pesquisável de estilos e stacks; [Design Taste Frontend](../../../skills/github.com/leonxlnx/taste-skill/design-taste-frontend.md) para um processo anti-slop baseado em direção sorteada e screenshots; [UX Audit Rethink](../../../skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) para auditoria ampla de UX.

## Limitações e cuidados

- **Somente o README foi lido.** A implementação em Rust, os 61 detectores, o binário distribuído, os hooks e a API de telemetria não foram inspecionados.
- **Hooks executam código:** o instalador grava manifests que rodam o launcher em edições e no Stop. O README discute trust e confirmações por harness, mas a superfície de execução automática merece revisão antes de uso não assistido.
- **Telemetria ligada por padrão:** o README detalha o que é e o que não é enviado, mas a verificação depende de confiar na implementação e na política de privacidade publicada.
- **Modo live tem execução local:** aplicar edições de cópia roda opcionalmente `scripts["impeccable:manual-edit-validate"]` do `package.json` com as permissões do usuário. É preciso revisar esse script em checkouts não confiáveis.
- **Cobertura por harness:** o README descreve diferenças de hook e de comando entre ferramentas; a equivalência funcional entre todos os 17 suportados **A verificar**.
- **Detector não substitui inspeção visual:** a própria documentação diz que uma execução limpa não prova qualidade de design nem acessibilidade.
- **Mudanças no formato de contexto:** `PRODUCT.md`, `DESIGN.md` e `.impeccable/config.json` são estado do projeto; mudanças de schema entre versões exigem migração não detalhada no README.
- **Licença Apache-2.0**, compatível com uso comercial e modificação, com obrigações de aviso e patentes.

## Estado e adoção

- **Versão:** não publicada no README; a página da skill registra versão desconhecida.
- **Atividade e popularidade observadas em 2026-10-19:** 83.051 estrelas, 5.021 forks, 47 issues abertas; repositório criado em 2025-11-16, último push em 2026-10-19.
- **Licença:** Apache-2.0.
- **Linguagem principal (API):** Rust.
- **Documentação:** [impeccable.style](https://impeccable.style), com docs de hooks, detector e privacidade.
- **Instalação da skill pela página do marketplace:** 343.949 instalações observadas em 2026-10-19 (registro da página, não do README).

## Relações

- **Mantido por:** [Paul Bakaus (pbakaus)](../../../entities/pbakaus.md).
- **Skill documentada:** [Impeccable](../../../skills/github.com/pbakaus/impeccable/impeccable.md) — quatro modos de superfície, 24 comandos e contexto `PRODUCT.md`/`DESIGN.md`; esta página cobre o repositório, o CLI e os hooks.
- **Conceitos:** [Design system com agentes](../../../concepts/design-system-com-agentes.md) — o repositório materializa tokens e componentes em `DESIGN.md` e em comandos de extração; [Design taste para agentes](../../../concepts/design-taste-para-agentes.md) — anti-padrões e piso de qualidade explícitos; [Auditoria de UX](../../../concepts/auditoria-de-ux.md) — `critique` e `audit`; [Agent skills](../../../concepts/agent-skills.md) — distribuição por harnesses; [CLI agent-first](../../../concepts/cli-agent-first.md) — o detector roda sem LLM.
- **Deriva de:** [anthropics/skills — frontend-design](https://github.com/anthropics/skills/tree/main/skills/frontend-design), citado como ponto de partida.

## Perguntas abertas

- As 61 regras determinísticas têm taxa de falso positivo medida, e como evoluem entre versões?
- Qual é o custo real de contexto dos 24 comandos e das referências carregadas por sessão?
- Como os hooks se comportam em monorepos, workspaces aninhados e múltiplos harnesses no mesmo projeto?
- O binário autocontido é reproduzível a partir do código-fonte em Rust e verificável por checksum?
- A telemetria pode ser auditada de fora, ou a garantia depende apenas do servidor?
- Como `PRODUCT.md` e `DESIGN.md` interoperam com formatos equivalentes de outras ferramentas?

## Fontes

- README: https://github.com/pbakaus/impeccable/blob/main/README.md (commit `0665bd812ae0908fcab17b96fd4f840defb882d9`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19).
- [Impeccable](../../../skills/github.com/pbakaus/impeccable/impeccable.md) — página de skill já existente, usada para links e para evitar duplicação.
