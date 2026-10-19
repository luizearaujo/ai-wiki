---
type: repo
url: https://github.com/msitarzewski/agency-agents
host: github.com
owner: msitarzewski
repo: agency-agents
commit: 652b2692f8d8ec2b1f1a38e559073e287dfdc469
license: MIT
language: Shell
status: active
created: 2026-10-18
ingested: 2026-10-18
updated: 2026-10-18
tags: [agentes, prompts, personalidades, multi-agente, claude-code, cursor]
---

# msitarzewski/agency-agents

> Coleção de mais de 150 personalidades de agente de IA organizadas em divisões especializadas, instaláveis em Claude Code, Cursor, Codex, Gemini CLI e outros clientes com um script ou um app nativo.

## O que é

O Agency Agents é uma biblioteca de definições de agente em Markdown — cada arquivo descreve uma especialidade com identidade, missão, regras críticas, entregáveis técnicos, workflows e métricas de sucesso. A metáfora é uma agência criativa com divisões (Engenharia, Design, Marketing, Vendas, Segurança etc.); o usuário "contrata" o especialista que precisa ativando o arquivo no cliente de IA correspondente.

Diferencia-se de prompts genéricos ("act as a developer") por definir processos passo a passo, exemplos de código reais e critérios mensuráveis de qualidade, o que torna o comportamento do agente mais previsível e reutilizável.

## Como funciona

Cada agente é um arquivo `.md` com seções padronizadas:

1. **Identity & Memory** — persona, voz e estilo de comunicação.
2. **Core Mission** — foco e o que o agente se recusa a fazer fora do escopo.
3. **Critical Rules** — regras específicas do domínio (ex.: o Security Architect nunca bypass controles para conveniência).
4. **Technical Deliverables** — saídas esperadas com exemplos de código.
5. **Workflow Process** — passo a passo repetível.
6. **Success Metrics** — indicadores objetivos de qualidade.

As definições ficam no diretório da divisão correspondente (`engineering/`, `security/`, `design/` etc.). Scripts de instalação (`scripts/install.sh`, `scripts/convert.sh`) copiam os arquivos para os diretórios de configuração dos clientes alvo. O app nativo [agencyagents.app](https://agencyagents.app) faz o mesmo sem terminal.

## Instalação e uso rápido

**Opção 1 — App nativo** (macOS, Linux, Windows; sem terminal):

```
https://agencyagents.app
```

**Opção 2 — Script para Claude Code:**

```bash
./scripts/install.sh --tool claude-code
# ou só uma divisão:
./scripts/install.sh --tool claude-code --division engineering,security
```

**Opção 3 — Cópia manual (exemplo: divisão de engenharia):**

```bash
cp engineering/*.md ~/.claude/agents/
```

Após instalar, ative no cliente: *"Hey Claude, activate Frontend Developer mode"*.

**Outros clientes suportados:** Cursor, GitHub Copilot, Antigravity, Gemini CLI, OpenCode, Aider, Windsurf, Kimi Code, Codex, Osaurus, Hermes, Mistral Vibe, DeepSeek Harness.

> **Limitação do OpenCode:** suporta apenas ~119 agentes; instalações maiores são truncadas silenciosamente. O instalador avisa quando o limite é ultrapassado.

## Exemplos de uso

O README documenta seis cenários de uso coordenado ("montagem de equipe"):

- **Startup MVP:** Frontend Developer + Backend Architect + Growth Hacker + Rapid Prototyper + Reality Checker.
- **Campanha de marketing:** Content Creator + Twitter Engager + Instagram Curator + Reddit Community Builder + Analytics Reporter.
- **Feature enterprise:** Senior Project Manager + Senior Developer + UI Designer + Experiment Tracker + Evidence Collector + Reality Checker.
- **Takeover de conta de mídia paga:** Paid Media Auditor + Tracking Specialist + PPC Strategist + Search Query Analyst + Ad Creative Strategist + Analytics Reporter.
- **Descoberta de produto completa:** oito agentes em paralelo cobrindo mercado, tecnologia, marca, GTM, suporte, UX, gestão e XR (ver `examples/nexus-spatial-discovery.md`).
- **Gêmeo digital de campus:** Technical Consultant + BIM/GIS Specialist + Drone/Reality Mapping + Web GIS Developer + 3D Scene Developer + GeoAI/ML Engineer + GIS QA Engineer.

## Divisões e agentes

| Divisão | Agentes (exemplos) |
|---|---|
| Engineering | Frontend Developer, Backend Architect, AI Engineer, DevOps Automator, Multi-Agent Systems Architect, RAG Pipeline Engineer, LLM Post-Training Engineer, Prompt Engineer, Knowledge Graph Engineer, e mais ~40 |
| Design | UI Designer, UX Researcher, Whimsy Injector, Brand Guardian, UI Finish-Gate Reviewer |
| Security | Security Architect, Penetration Tester, Incident Responder, AI-Generated Code Security Auditor, Blockchain Security Auditor |
| Marketing | Growth Hacker, SEO Specialist, AI Citation Strategist, AEO Foundations Architect, Agentic Search Optimizer, e mais ~30 |
| Sales | Outbound Strategist, Discovery Coach, Deal Strategist, Pipeline Analyst |
| Product | Sprint Prioritizer, Feedback Synthesizer, DX Engineer, Product Manager |
| Testing | Evidence Collector, Reality Checker, Test Automation Engineer, Accessibility Auditor |
| Project Management | Studio Producer, Senior Project Manager, Jira Workflow Steward |
| Spatial Computing | XR Interface Architect, visionOS Spatial Engineer, macOS Spatial/Metal Engineer |
| Specialized | Agents Orchestrator, MCP Builder, Agentic Identity & Trust Architect, Codebase Archaeologist |
| Finance | Bookkeeper & Controller, Financial Analyst, Tax Strategist |
| Game Development | Unity Architect, Unreal Systems Engineer, Godot Gameplay Scripter, Roblox Systems Scripter |
| Academic | Anthropologist, Historian, Narratologist, Statistician |
| GIS | GeoAI/ML Engineer, Spatial Data Scientist, Web GIS Developer, Cartography Designer |
| Healthcare | Clinical Evidence Agent, Healthcare Innovation Strategist |
| Research | Research Synthesist |
| Support | Support Responder, Finance Tracker, Legal Compliance Checker |

## Quando usar (e quando não usar)

- **Use quando:** quiser carregar comportamento especializado e reproduzível em um cliente de IA sem escrever prompts do zero; quando o fluxo de trabalho envolve múltiplas perspectivas (ex.: lançar produto, fazer takeover de conta de ads, auditar segurança).
- **Evite quando:** precisar de comportamento muito específico para seu contexto: os agentes são genéricos por design, e valores como "regras críticas" do agente podem conflitar com convenções próprias do projeto. Nesse caso, adaptar um arquivo existente é mais rápido do que partir do zero.

## Limitações e cuidados

- Os arquivos `.md` definem comportamento esperado, não garantido: o agente pode ignorar partes da instrução dependendo do cliente e do contexto da sessão.
- Instruções de terceiros ampliando o comportamento do agente criam superfície de supply chain: um arquivo malicioso ou corrompido pode alterar o que o agente faz. **A verificar:** o projeto descreve algum mecanismo de assinatura ou validação dos arquivos instalados?
- O README não explica como os agentes interagem quando usados em paralelo ou em cadeia — coordenação multi-agente fica a cargo do usuário.
- O conteúdo de cada arquivo de agente não foi lido; apenas o README foi consultado. Qualidade, completude e atualização de cada especialista são a verificar.
- Popularidade observada em 2026-10-18 (160 k stars, 26 k forks) indica adoção expressiva, mas métricas são voláteis.

## Estado e adoção

- Último push: 2026-10-15.
- Observado em 2026-10-18: ~160.916 stars, ~26.038 forks, ~217 issues abertas.
- Licença: MIT.
- App nativo complementar: [msitarzewski/agency-agents-app](https://github.com/msitarzewski/agency-agents-app).

## Relações

- Mantido por: [msitarzewski](../../../entities/msitarzewski.md)
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [CLAUDE.md](../../../concepts/claude-md.md)
- Relacionado: [multica-ai/andrej-karpathy-skills](../multica-ai/andrej-karpathy-skills.md) — outro repositório de definições de comportamento para agentes, com foco em diretrizes gerais em vez de especialidades.

## Perguntas abertas

- Como os arquivos de agente lidam com conflito de instruções quando dois agentes são ativados na mesma sessão?
- Existe alguma forma de composição ou herança entre divisões (ex.: um agente que herda regras de Security + Engineering)?
- Os arquivos de agente têm versão própria ou seguem o commit do repositório?
- O app nativo e os scripts estão em sincronia com o repositório, ou há um ciclo de release separado?

## Fontes

- README: https://raw.githubusercontent.com/msitarzewski/agency-agents/652b2692f8d8ec2b1f1a38e559073e287dfdc469/README.md (commit `652b2692f8d8ec2b1f1a38e559073e287dfdc469`, consultado em 2026-10-18). Somente o README foi lido; os arquivos de agente individuais, scripts e demais conteúdos do repositório não foram consultados.
- Metadados: API do GitHub em 2026-10-18.
