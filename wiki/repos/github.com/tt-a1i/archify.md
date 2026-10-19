---
type: repo
url: https://github.com/tt-a1i/archify
host: github.com
owner: tt-a1i
repo: archify
commit: 25cf37080fc8b1dbe758a4efc3935b55f3327083
license: MIT
language: JavaScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, skills, diagramas, visualizacao, arquitetura, html, artefatos]
---

# tt-a1i/archify

> Skill para agentes de código que transforma uma ideia, um plano ou um repositório em um diagrama interativo autocontido em HTML, com validação tipada antes da entrega.

## O que é

Archify é uma **skill** distribuída como repositório e instalada em agentes como Claude Code, Codex CLI, Cursor e opencode. O ponto de partida é uma descrição em linguagem natural — um sistema, um fluxo, uma pergunta — e o resultado é um **arquivo HTML autocontido**, com nós navegáveis, rotas, focos e exportação de imagens, que pode ser aberto e compartilhado sem instalar nada.

O README explicita o posicionamento: não é um editor de desenho genérico nem um tema de Mermaid. O objetivo é converter **intenção técnica em artefato de comunicação**, seja um mapa de arquitetura, um diagrama de sequência ou uma página explicativa de uma pergunta.

O projeto está na versão estável `v3.2.0` (changelog datado de 2026-10-18) e se declara gratuito e open source sob licença MIT. Serviços online de terceiros e planos pagos citados no README pertencem aos respectivos provedores.

## Como funciona

O README descreve um pipeline de cinco etapas:

| Etapa | O que acontece |
|---|---|
| **Generate** | O agente cria um **JSON IR tipado** a partir da descrição. |
| **Validate** | Validadores e regras de layout embutidos checam o JSON; falhas retornam reparos localizados em JSON legível por máquina. |
| **Preview (opcional)** | Um modo desktop em loopback observa um arquivo JSON e recarrega apenas revisões verificadas, mantendo o último artefato válido em caso de erro. |
| **Deliver** | Um candidato no mesmo diretório é renderizado e checado; só um artefato aprovado substitui atomicamente o destino. |
| **Iterate** | O agente atualiza a fonte tipada preservando a estrutura não relacionada. |

### Garantias declaradas

- **JSON IR tipado:** cada modo suportado pelo renderer tem schema e fonte reproduzível.
- **Validação atômica:** schema, layout, HTML/SVG, rotas e folga entre rótulos e rotas precisam passar antes da entrega.
- **Recibos de reparo:** `validate --json` e `deliver --json` retornam códigos de regra estáveis, o sujeito exato e a evidência medida, em vez de stack trace ou retry sem critério.
- **Preview last-good:** um loop desktop opcional mantém o último diagrama verificado visível enquanto um candidato inválido é corrigido.
- **Interação honesta:** foco, alcance upstream/downstream, rotas e comparação de papéis reutilizam nós e relações **autorados**, sem inventar topologia nem alegar impacto em runtime.
- **Evidência sob demanda:** nós de arquitetura com evidência marcam-se `SRC n` e abrem arquivos e intervalos de linha verificados no Git, fixados a um commit público. Artefatos comuns ficam sem fonte.
- **Portabilidade:** o resultado é um único HTML; exportações preservam o diagrama completo e não incluem estado temporário do viewer.

### Tipos de diagrama

O README lista dez tipos, cada um com um perfil de prompt recomendado:

| Tipo | Melhor para |
|---|---|
| **Architecture** | Componentes, serviços, armazenamento e fronteiras |
| **Workflow** | CI/CD, aprovações, chamadas de ferramentas e runbooks |
| **Sequence** | Chamadas de API, fallback de cache, autenticação e traces assíncronos |
| **Data Flow** | Pipelines, linhagem, PII e consumidores |
| **Lifecycle** | Estados, esperas, retries e desfechos terminais |
| **ERD** | Esquemas de banco: tabelas, colunas, chaves e cardinalidade |
| **Class** | Classes, interfaces, membros e relações de tipo |
| **Tree** | Hierarquias de pai único: repositórios, módulos e capacidades |
| **Timeline** | Revisões de incidente e históricos de release |
| **Waterfall** | Onde o tempo foi gasto em uma requisição ou execução de agente |

Os tipos ERD, Class, Tree, Timeline e Waterfall entraram na versão 3.1. O perfil opcional `deployment-ownership` da arquitetura falha de forma fechada quando faltam donos, regiões, escopo de banco privado ou cruzamentos nomeados; ele não inspeciona infraestrutura ao vivo.

Há ainda o modo **Architecture Delta**, que compara snapshots Before / Delta / After validados com recibo de máquina e não infere impacto, risco ou segurança de merge.

### Páginas explicativas

Além de diagramas, a skill pode responder "como uma página": o agente monta um **explainer** com a conclusão primeiro e um painel por pergunta, incluindo tabelas, passos, gráficos, código e diagramas validados. As afirmações citam fontes numeradas, e trechos de repositório aparecem fixados a um commit.

### Viewer e formatos

O HTML entregue funciona sem instalação. O README lista atalhos para foco de nó, alcance upstream/downstream, inspeção de rota, comparação de papéis, mapa geral, apresentação, estilos visuais, tema e exportação. Links estáveis restauram `#focus`, `#reach`, `#route`, `#relation` e `#lens`. Exportações incluem PNG, WebP, JPG, PDF via impressão e *share cards* de rota e alcance; o movimento respeita `prefers-reduced-motion` e não entra nas exportações canônicas.

## Instalação e uso rápido

Instalação padrão, conforme o README:

```bash
npx skills add tt-a1i/archify -g
```

Instalação explícita e não interativa no Cursor:

```bash
npx -y skills add tt-a1i/archify --skill archify --agent cursor --global --copy --yes
```

Para experimentar sem instalar:

```bash
npx skills use tt-a1i/archify@archify --agent codex
```

Superfícies citadas:

| Superfície | Forma de instalação |
|---|---|
| Claude Code | `~/.claude/skills/` ou `.claude/skills/` |
| Codex CLI | `~/.agents/skills/` ou `.agents/skills/` |
| opencode | `~/.config/opencode/skills/`, `.opencode/skills/` ou `.agents/skills/` |
| Claude.ai | Upload de `archify.zip` em Settings → Capabilities → Skills; depende de Node.js no sandbox |
| Project Knowledge | Upload de `archify.zip` no projeto; fallback guiado por prompt |
| Hermes Agent | `hermes skills install skills-sh/tt-a1i/archify/archify -y`, integração comunitária |
| DeepSeek Harness | Plugin `@tt-a1i/archify-dsh@1.0.0`, integração comunitária para developer preview |

Requisitos declarados: Node.js `>=18` para a integração Hermes e `^22.19.0 || >=24.0.0` para a integração DSH. O caminho principal via `npx skills` não fixa explicitamente uma versão mínima de Node no README.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Arquitetura a partir de descrição:** "Use Archify to diagram a web request: Browser calls the API, the API checks Redis, and a cache miss queries PostgreSQL and fills the cache."
- **A partir de um repositório:** pedir ao agente para analisar o repositório e gerar um diagrama de arquitetura de runtime com 8–12 componentes, um caminho principal, dependências externas e fronteiras de confiança.
- **Refinamento em chat:** "Add authentication", "Highlight the cache-miss path" ou "Switch to the light theme".
- **Página explicativa:** "Use Archify to answer as one page: our API's P99 went from 80 ms to 600 ms while the mean barely moved. What is the likely cause, and how should we investigate?"
- **CLI direta:** `node archify/bin/archify.mjs guide "Show an API request with Redis cache miss"`.
- **Validação e entrega:** `validate ... --quality showcase --json` e `deliver ... --open --json`.

## Quando usar (e quando não usar)

- **Use quando:** você quer transformar uma explicação técnica em um artefato visual compartilhável, com fonte tipada e validação antes da entrega.
- **Use quando:** precisa mostrar arquitetura, sequência, fluxo de dados ou hierarquia a partir de um repositório, com evidência de código fixada a um commit.
- **Use quando:** quer entregar um HTML autocontido que outra pessoa abre sem instalar o Archify.
- **Evite quando:** precisa de um editor visual WYSIWYG, de compartilhamento hospedado ou de parsing automático de Mermaid — itens declarados fora do escopo atual.
- **Evite quando:** o objetivo é analisar a estrutura do código como grafo consultável, e não comunicá-la visualmente; nesse caso, ferramentas como [Graphify-Labs/graphify](../graphify-labs/graphify.md) são mais adequadas.
- **Alternativas documentadas:** [Graphify-Labs/graphify](../graphify-labs/graphify.md) — grafo de conhecimento de código consultável; [calesthio/OpenMontage](../calesthio/openmontage.md) — produção de vídeo com HTML/CSS, não diagramas.

## Limitações e cuidados

- **Somente o README foi lido.** Não foram verificados o código, os schemas, os validadores, a qualidade dos diagramas gerados nem o comportamento do viewer.
- **Escopo deliberadamente limitado:** o README declara fora do escopo parsing automático de Mermaid, auto-layout genérico, compartilhamento hospedado e edição WYSIWYG.
- **Dependência de um agente capaz:** a geração depende de o agente produzir JSON IR válido; a qualidade do diagrama herda a interpretação do modelo.
- **Evidência é declarada, não auditada nesta wiki:** o README afirma que nós `SRC n` abrem arquivos verificados no Git em um commit público, mas o mecanismo não foi inspecionado.
- **Update checker:** instalações com o verificador fazem uma requisição GET a um manifesto estável para exibir lembrete de atualização; o README afirma que nenhum dado de versão, projeto, prompt ou dispositivo é enviado e que `ARCHIFY_UPDATE_CHECK_DISABLED=1` desliga a rede e a escrita de estado.
- **Integrações comunitárias:** Hermes e DeepSeek Harness não são produtos oficiais das respectivas empresas segundo o README.
- **Métricas e prêmios são declarações do README:** o selo de 130K+ instalações no skills.sh, a posição #1 no GitHub Trending e a cobertura de imprensa vêm do próprio projeto e não foram verificados.
- **Licença MIT:** permite uso, modificação e distribuição; o README alerta que serviços de terceiros têm preços e políticas próprios.

## Estado e adoção

- **Versão citada:** `v3.2.0`, changelog de 2026-10-18.
- **Atividade e popularidade observadas em 2026-10-19:** 85.761 estrelas, 5.839 forks, 249 issues abertas; repositório criado em 2026-04-15, último push em 2026-10-19.
- **Licença:** MIT.
- **Linguagem principal (API):** JavaScript.
- **Site e documentação:** [archify.si](https://archify.si) — galeria, guia de cenários e página de instalação.
- **Instalações declaradas:** selo de 130K+ instalações no skills.sh.

## Relações

- **Mantido por:** [tt-a1i](../../../entities/tt-a1i.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — modelo de distribuição e instalação; [Artefatos HTML autocontidos](../../../concepts/artefatos-html-autocontidos.md) — o entregável é um único HTML com interações embutidas; [Grafo de conhecimento de código](../../../concepts/grafo-de-conhecimento-de-codigo.md) — compartilha a ideia de mapear estrutura de código, mas para comunicação visual, não consulta.
- **Alternativas:** [Graphify-Labs/graphify](../graphify-labs/graphify.md) — grafo consultável em vez de diagrama; [calesthio/OpenMontage](../calesthio/openmontage.md) — pipeline de mídia.
- **Distinto de:** Mermaid — Archify não faz parsing automático de Mermaid e usa um IR tipado próprio.

## Perguntas abertas

- Qual é o custo de tokens para gerar um diagrama grande, e o validador realmente impede alucinações de topologia?
- Como o agente escolhe entre os dez tipos de diagrama sem intervenção do usuário?
- O HTML gerado mantém acessibilidade adequada (teclado, leitores de tela) além do `lang` e do `prefers-reduced-motion` citados?
- Como o controle de atualização se comporta em ambientes sem rede ou com proxy?
- O formato do JSON IR é estável entre versões, ou artefatos antigos quebram em versões novas?
- Quais são os limites práticos de tamanho do repositório e do diagrama antes de a validação ou o viewer degradar?

## Fontes

- README: https://github.com/tt-a1i/archify/blob/main/README.md (commit `25cf37080fc8b1dbe758a4efc3935b55f3327083`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19).
