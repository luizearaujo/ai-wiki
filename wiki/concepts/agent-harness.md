---
type: concept
aliases: [Agent harness, harness de agente, harness engineering]
status: draft
created: 2026-10-19
updated: 2026-10-21
tags: [agentes, harness, contexto, ferramentas, seguranca]
---

# Agent harness

> Camada de software que envolve um agente ou CLI de código existente e passa a definir como ele recebe contexto, ferramentas, permissões, memória, workflows e supervisão — sem substituir o modelo nem o CLI.

## Definição

Um *agent harness* é o ambiente operacional de um agente. Ele não treina nem hospeda o modelo: ele instala e coordena o que o agente vê e pode fazer — instruções persistentes, skills, subagentes, hooks, regras, servidores MCP, memória, políticas de aprovação e adaptadores para diferentes clientes.

A distinção útil é com três vizinhos:

- **Modelo/LLM** — gera tokens; o harness não muda o modelo, muda o contexto e as ações disponíveis.
- **CLI de agente** — Claude Code, Codex, Gemini CLI, OpenCode etc.; o harness geralmente se instala *sobre* um ou vários deles.
- **Framework de agentes** — biblioteca para construir agentes do zero (loop, tools, estado); o harness pressupõe um agente já existente e otimiza seu uso.

O termo ganhou força com projetos que se descrevem como "agent harness operating system" ([affaan-m/ECC](../repos/github.com/affaan-m/ecc.md)), "super agent harness" ([bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md)), "harness to run an office of your clones" ([HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md)) e configurações que transformam um CLI em equipe ([garrytan/gstack](../repos/github.com/garrytan/gstack.md)).

## Como funciona

Os componentes se repetem entre implementações:

| Componente | Função | Exemplo |
|---|---|---|
| Instruções persistentes | Fixar convenções e comportamento | `CLAUDE.md`, `AGENTS.md`, rules por linguagem |
| Skills / workflows | Conhecimento procedural carregado por tarefa | TDD, revisão de segurança, QA |
| Subagentes / papéis | Isolar contexto e permissões | planner, code-reviewer, designer, QA |
| Hooks | Executar checagens fora do contexto do modelo | bloquear `rm -rf`, validar edição, salvar sessão |
| Memória | Persistir decisões e handoffs entre sessões | Memory Vault do ECC, GBrain do gstack, palácio do Munder, DeerMem do DeerFlow |
| Ferramentas | Expor ações e dados | servidores MCP, navegador, CLI, git |
| Adaptadores | Levar o mesmo workflow a vários clientes | `--host` do gstack, targets do ECC |
| Política e segurança | Aprovações, isolamento, auditoria | AgentShield, gates humanos, recibos de egresso |

O harness normalmente é instalado como plugin, pacote npm ou clone em um diretório de skills. A instalação grava arquivos que passam a fazer parte do runtime do agente, o que a torna uma decisão de **supply chain**, não apenas de produtividade.

## Onde aparece

- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — harness multi-cliente com 71 agentes, 311 skills, hooks, regras, Memory Vault e AgentShield; chama a si mesmo de "agent harness operating system".
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — "super agent harness" self-hosted sobre LangGraph, reescrito do zero na versão 2.0, com agente líder, subagentes, skills de carregamento progressivo, MCP, sandbox e memória DeerMem.
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — harness de processo sobre Claude Code e outros hosts, com especialistas por etapa de sprint, QA em navegador e GBrain.
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — harness desktop que orquestra CLIs de terminal como agentes em um escritório, com hive de memória e mensageria.
- [vastsa/PI-Desktop](../repos/github.com/vastsa/pi-desktop.md) — workspace desktop que embarca o runtime `pi` (`pi-ai`, `pi-agent-core`, `pi-coding-agent`) e adiciona sessões persistentes, permissões, plugins e orquestração de Worker Sessions.
- [SynkraAI/aiox-core](../repos/github.com/synkraai/aiox-core.md) — harness/framework CLI-first com agentes especializados e artefatos persistentes.
- [Fosowl/agenticSeek](../repos/github.com/fosowl/agenticseek.md) — assistente local com seleção automática entre agentes de navegação web, código e planejamento; sem catálogo de skills nem MCP, mas com o mesmo padrão de roteamento sobre um runtime único.
- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) — não são harnesses em si, mas aplicações construídas sobre um: `neon-meal-helper-agent` e `neon-notes-app` usam o runtime `pi` sobre o backend da Neon (Postgres, Auth, Object Storage, Functions, AI Gateway) como agente sempre ativo; `eve-pocket-research` usa o framework `eve`, da Vercel, ainda sem página própria nesta wiki.

## Trade-offs

- **Vantagens:** instala processo e conhecimento uma vez; reduz prompt repetido; padroniza revisão, testes e segurança; permite memória e handoff entre sessões; pode levar o mesmo workflow a vários clientes.
- **Limitações:** consome contexto (catálogos grandes competem com a tarefa); paridade entre hosts costuma ser parcial; hooks e comandos são código executável e ampliam a superfície de ataque; adaptadores e atualizações podem quebrar workflows; o comportamento do modelo não é determinístico, então a instalação não garante adesão; custo de tokens e de manutenção pode superar o ganho em equipes pequenas.
- **Critério prático:** vale quando o ganho de consistência e governança é maior que o custo de contexto, instalação e auditoria — e quando o usuário consegue revisar o que está instalando.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — skills são um dos componentes do harness; [CLAUDE.md](claude-md.md) — instruções persistentes como camada de contexto; [Model Context Protocol](model-context-protocol.md) — protocolo para expor ferramentas e dados ao harness; [Orquestração multiagente](orquestracao-multiagente.md) — coordenação de vários agentes dentro do harness.
- **Distingue-se de:** framework de agentes (constrói o loop do zero), plugin de IDE (integração pontual) e prompt avulso (sem instalação nem versionamento).
- **Pré-requisito para:** usar catálogos de skills e agentes com segurança — revisar fonte, licença, hooks e permissões antes de instalar.

## Perguntas abertas

- Como medir o retorno de um harness em qualidade e custo, e não apenas em velocidade percebida?
- Qual é o custo real de contexto de rules, skills e catálogos MCP em cada host?
- Como garantir que hooks e adaptadores não dupliquem execução ou alterem permissões silenciosamente?
- Que modelo de assinatura, versão e proveniência está emergindo para distribuição de harnesses?
- Como comparar harnesses que otimizam contextos diferentes (processo de engenharia, sprint de produto, escritório multiagente)?

## Fontes

- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — README no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34` (consultado em 2026-10-19).
- [bytedance/deer-flow](../repos/github.com/bytedance/deer-flow.md) — README no commit `fee0cd0c180874325305e995197db99f03fa6a6f` (consultado em 2026-10-19).
- [garrytan/gstack](../repos/github.com/garrytan/gstack.md) — README no commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037` (consultado em 2026-10-19).
- [HarnessMD/munder-difflin](../repos/github.com/harnessmd/munder-difflin.md) — README no commit `436d65a74a69d347c57641fbace4eb822bf98600` (consultado em 2026-10-19).
- [vastsa/PI-Desktop](../repos/github.com/vastsa/pi-desktop.md) — README no commit `87a48b953e8bada43a7a63f8922846198b9efb61` (consultado em 2026-10-19).
- [SynkraAI/aiox-core](../repos/github.com/synkraai/aiox-core.md) — página existente da wiki, usada como comparação.
- [Fosowl/agenticSeek](../repos/github.com/fosowl/agenticseek.md) — README no commit `b46bcca482218643236999221720586e7f410e04` (consultado em 2026-10-19).
- [zazencodes/zazencodes-season-3](../repos/github.com/zazencodes/zazencodes-season-3.md) — clone local no commit `555467c365e6750278efba09349369109f62f65f`, READMEs de `neon-meal-helper-agent` e `eve-pocket-research` (consultado em 2026-10-21).
