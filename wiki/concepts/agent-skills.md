---
type: concept
aliases: [Agent Skills, Skills para agentes, SKILL.md]
status: draft
created: 2026-10-17
updated: 2026-10-19
tags: [agentes, skills, claude-code, distribuicao]
---

# Agent skills

> Instruções empacotadas em um diretório com `SKILL.md` que ensinam um agente a executar um tipo de tarefa, distribuídas e instaladas como artefatos versionáveis.

## Definição

Uma agent skill é um pacote de conhecimento procedural para um agente: um diretório com um arquivo `SKILL.md` — descrição, quando usar e instruções — e, opcionalmente, referências, scripts e outros recursos. Em vez de repetir um prompt longo em cada sessão, o usuário instala a skill e o agente carrega as instruções quando a tarefa corresponde.

A diferença central em relação a um prompt avulso é a **distribuição**: a skill tem repositório-fonte, caminho, versão, licença e um comando de instalação. Isso a torna um artefato que pode ser compartilhado, auditado e atualizado.

## Como funciona

O padrão observado no ecossistema:

1. A skill vive em um repositório-fonte, tipicamente em `skills/<slug>/SKILL.md`.
2. Um CLI — como o `skills`, usado pelo claudemarketplaces.com — instala a skill no agente escolhido, por projeto ou globalmente.
3. O agente decide quando aplicar a skill a partir da descrição publicada.
4. O carregamento pode ser **progressivo** — como no DeerFlow, em que a skill e suas referências só entram no contexto quando a tarefa exige. O comportamento exato ainda varia por agente e formato; nesta wiki ele foi observado apenas no que os READMEs e as páginas de catálogo publicam.

Instalação típica observada:

```bash
npx -y skills add owner/repo --skill <slug> --agent claude-code
```

## Onde aparece

- [UX Audit Rethink](../skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — skill de auditoria de UX instalada pelo CLI `skills`, com `SKILL.md` em `skills/ux-audit-rethink/`.
- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — catálogo de 311 skills organizadas por linguagem, framework e domínio; o README trata skills como a superfície primária de workflow e mantém comandos como shims de compatibilidade.
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — skills como slash commands em Markdown, encadeadas por etapa de sprint; o mesmo conteúdo é renderizado para vários agentes por `./setup --host`.
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — skills em Markdown com **carregamento progressivo**: só entram no contexto quando a tarefa precisa, podem ser ativadas por `/skill-name` e declarar `allowed-tools`.
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — a skill `/graphify` ensina o agente a construir e consultar um grafo de conhecimento, empacotada junto com o CLI.
- [OpenMontage](../repos/github.com/calesthio/openmontage.md) — 700+ arquivos de skills e conhecimento em três camadas: capacidades executáveis, convenções de produção e conhecimento técnico profundo de tecnologias externas.
- [mukul975/Anthropic-Cybersecurity-Skills](../repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — biblioteca de 818 skills de cibersegurança em 34 domínios, com descoberta progressiva (~30 tokens por frontmatter) e mapeamento a seis frameworks de segurança.
- [Skill understand](../skills/github.com/egonex-ai/understand-anything/understand.md) — método em sete fases para gerar um grafo de conhecimento da base de código, distribuído como skill de plugin.
- [Skill Frontend Slides](../skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — processo de design de apresentações HTML autocontidas, com prévias de estilo e verificação.
- [Skill Diagram Design](../skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — sistema de design e contrato de SVG acessível que a skill aplica a 44 tipos visuais.
- [Skill Humanizer](../skills/github.com/blader/humanizer/humanizer.md) — catálogo de 26 padrões de escrita por IA em seis famílias, com três modos de saída e regra de preservação de afirmações.
- [Skill Stop Slop](../skills/github.com/hardikpandya/stop-slop/stop-slop.md) — oito regras centrais, lista de checagens e pontuação em cinco dimensões para revisar prosa.
- [D4Vinci/Scrapling](../repos/github.com/d4vinci/scrapling.md) — Agent Skill instalável que ensina a um agente de código a API atual da biblioteca, para que o código gerado corresponda à versão corrente em vez de uma versão adivinhada.
- [twentyhq/twenty](../repos/github.com/twentyhq/twenty.md) — skills oficiais do produto (`packages/twenty-agent-skills`), instaláveis via CLI `skills` em Claude Code, Codex, Cursor e Pi para desenvolver apps sobre o CRM.
- [anthropics/skills](../repos/github.com/anthropics/skills.md) — implementação de referência da Anthropic: exemplos criativos/técnicos/enterprise, especificação do formato e skills de documento (docx/pdf/pptx/xlsx) source-available que também alimentam o Claude em produção.
- [vercel-labs/agent-skills](../repos/github.com/vercel-labs/agent-skills.md) — oito skills oficiais da Vercel: auditoria de projeto, boas práticas React/Next.js/React Native, guidelines de design e escrita, e deploy "claimable".
- [github/awesome-copilot](../repos/github.com/github/awesome-copilot.md) — catálogo comunitário (hospedado pelo GitHub, alimentado por terceiros) de agentes, instructions, skills e plugins para o GitHub Copilot, com site de busca e `llms.txt` para agentes.
- [remotion-dev/skills](../repos/github.com/remotion-dev/skills.md) — doze skills oficiais do Remotion para criação, markup, render, mapas animados e legendas em projetos de vídeo programático.
- [cloudflare/skills](../repos/github.com/cloudflare/skills.md) — 18 skills oficiais da Cloudflare para Workers, Agents SDK, Durable Objects e Sandbox, empacotadas com o servidor MCP principal da plataforma.
- [firecrawl/cli](../repos/github.com/firecrawl/cli.md) — três famílias de skills (core, build, workflows) distribuídas por um catálogo próprio e instaladas pelo CLI em todos os harnesses detectados.

## Trade-offs

- **Vantagens:** reutilização de instruções complexas; versionamento e fonte rastreável; instalação em um comando; possibilidade de distribuir conhecimento especializado sem escrever código.
- **Limitações:** a skill é texto executado pelo agente, não um sandbox — instruções de terceiros podem ser maliciosas ou simplesmente ruins; a qualidade e a manutenção variam; atualizações podem mudar o comportamento sem aviso; o formato ainda não é padronizado entre fornecedores.

## Relações

- **Relacionado a:** [Agent harness](agent-harness.md) — skills são um dos componentes que um harness instala e orquestra; [Model Context Protocol](model-context-protocol.md) — camada complementar: skills empacotam *instruções*, MCP expõe *ferramentas e dados* em runtime.
- **Distingue-se de:** [CLAUDE.md](../concepts/claude-md.md) — instruções persistentes do projeto, carregadas em toda sessão; skills são acionadas por tarefa e distribuídas como pacote.
- **Contrasta com:** prompts avulsos copiados entre sessões e plugins específicos de um único cliente.
- **Pré-requisito para:** usar skills de catálogo com segurança — revisar fonte, licença, conteúdo e permissões antes da instalação.

## Perguntas abertas

- Qual é o modelo exato de carregamento e de uso de contexto das skills em cada agente?
- Como o `skills` CLI resolve conflitos de nome, versões e atualizações?
- Que garantias de segurança existem além da revisão manual do `SKILL.md`?
- Como skills e servidores MCP se combinam na prática — instruções que chamam ferramentas?

## Fontes

- [UX Audit Rethink](../skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — comandos de instalação e caminho do `SKILL.md` publicados no catálogo (consultado em 2026-10-17).
- https://github.com/mastepanoski/claude-skills — árvore do repositório com `skills/<slug>/SKILL.md` (consultada em 2026-10-17).
- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — README no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34` (consultado em 2026-10-19).
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037` (consultado em 2026-10-19).
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — README no commit `fee0cd0c180874325305e995197db99f03fa6a6f` (consultado em 2026-10-19).
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — README no commit `86c57be8204673c2a1b9849a3292a7dd3ab373d8` (consultado em 2026-10-19).
- [OpenMontage](../repos/github.com/calesthio/openmontage.md) — README no commit `c8066452325cb57c8fc1ba8c2a71b6e8842e6b65` (consultado em 2026-10-19).
- [mukul975/Anthropic-Cybersecurity-Skills](../repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — README no commit `54a798831d2266a3ca61ce68a7acb80b81160d57` (consultado em 2026-10-19).
- [Skill understand](../skills/github.com/egonex-ai/understand-anything/understand.md) — página do skills.sh (consultada em 2026-10-19).
- [Skill Frontend Slides](../skills/github.com/zarazhangrui/frontend-slides/frontend-slides.md) — página do skills.sh (consultada em 2026-10-19).
- [Skill Diagram Design](../skills/github.com/cathrynlavery/diagram-design/diagram-design.md) — página do skills.sh (consultada em 2026-10-19).
- [Skill Humanizer](../skills/github.com/blader/humanizer/humanizer.md) — página do skills.sh e metadados do repositório `blader/humanizer` no commit `8c307f367c91bd974002f10f2be2965d642c13df` (consultados em 2026-10-19).
- [Skill Stop Slop](../skills/github.com/hardikpandya/stop-slop/stop-slop.md) — página do skills.sh e metadados do repositório `hardikpandya/stop-slop` no commit `8da1f030185bdfe8471220585162991eaeb970e9` (consultados em 2026-10-19).
- [D4Vinci/Scrapling](../repos/github.com/d4vinci/scrapling.md) — README no commit `fd531313a499092d8471bf24a0e08dc5771f2b40` (consultado em 2026-10-19).
- [twentyhq/twenty](../repos/github.com/twentyhq/twenty.md) — README no commit `31d95e98a2217e187d6f7d51f7ab69bb048e22bc` (consultado em 2026-10-19).
- [anthropics/skills](../repos/github.com/anthropics/skills.md) — README no commit `dbd4588f9e1033efb41dad4bef2f7947c8993d44` (consultado em 2026-10-19).
- [vercel-labs/agent-skills](../repos/github.com/vercel-labs/agent-skills.md) — README no commit `063bee94c3f4df8453406c830b0a7df0f2860278` (consultado em 2026-10-19).
- [github/awesome-copilot](../repos/github.com/github/awesome-copilot.md) — README no commit `cb64ad12e32737ae764becd6885462e9b4c7cb00` (consultado em 2026-10-19).
- [remotion-dev/skills](../repos/github.com/remotion-dev/skills.md) — README no commit `039e8a2fc78b67efc228d5645367838b85818a1c` (consultado em 2026-10-19).
- [cloudflare/skills](../repos/github.com/cloudflare/skills.md) — README no commit `86505e44f87d801aa1864a3c4109e9a8ae5c409f` (consultado em 2026-10-19).
- [firecrawl/cli](../repos/github.com/firecrawl/cli.md) — README no commit `84c82119a186bc50a27457f81e1d672ec8f28eaf` (consultado em 2026-10-19).
