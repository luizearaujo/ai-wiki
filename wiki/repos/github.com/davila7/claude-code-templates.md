---
type: repo
url: https://github.com/davila7/claude-code-templates
host: github.com
owner: davila7
repo: claude-code-templates
commit: 7d85535533914ff0880945570a94fcbec4adc042
license: MIT
language: Python
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [claude-code, templates, cli, plugins, observabilidade]
---

# davila7/claude-code-templates

> CLI (`npx claude-code-templates`) e catálogo web ([aitmpl.com](https://aitmpl.com)) de mais de 100 agentes, comandos, MCPs, settings, hooks e skills prontos para instalar no Claude Code, acompanhado de ferramentas próprias de analytics, monitoramento de conversas, health check e dashboard de plugins.

## O que é

O projeto resolve a distância entre "ler sobre um recurso do Claude Code" e "tê-lo configurado". Em vez de escrever um agente, comando ou hook do zero, o usuário navega um catálogo (via web ou CLI interativa) e instala o componente com um comando `npx`. O README descreve seis tipos de componente: **Agents** (especialistas de domínio), **Commands** (slash commands customizados), **MCPs** (integrações como GitHub, PostgreSQL, Stripe, AWS, OpenAI), **Settings** (configurações do Claude Code), **Hooks** (gatilhos de automação) e **Skills** (capacidades reutilizáveis com disclosure progressivo).

Além do catálogo, o repositório empacota ferramentas de operação do próprio Claude Code: analytics de sessão em tempo real, monitor de conversas com acesso remoto seguro, diagnóstico de instalação e um dashboard de marketplaces/plugins instalados.

## Como funciona

Instalação é feita component a component ou em lote, combinando múltiplas flags em um só comando:

```bash
npx claude-code-templates@latest --agent development-team/frontend-developer \
  --command testing/generate-tests --mcp development/github-integration --yes
```

| Componente | Descrição | Exemplos citados |
|---|---|---|
| Agents | Especialistas de domínio | Auditor de segurança, otimizador de performance React, arquiteto de banco |
| Commands | Slash commands customizados | `/generate-tests`, `/optimize-bundle`, `/check-security` |
| MCPs | Integrações com serviços externos | GitHub, PostgreSQL, Stripe, AWS, OpenAI |
| Settings | Configurações do Claude Code | Timeouts, memória, estilos de saída |
| Hooks | Gatilhos de automação | Validação pré-commit, ações pós-conclusão |
| Skills | Capacidades reutilizáveis | Processamento de PDF, automação de Excel, workflows customizados |

Ferramentas adicionais, cada uma com seu próprio modo de CLI:

```bash
npx claude-code-templates@latest --analytics       # métricas de sessão em tempo real
npx claude-code-templates@latest --chats            # monitor de conversas (local)
npx claude-code-templates@latest --chats --tunnel   # monitor via Cloudflare Tunnel
npx claude-code-templates@latest --health-check     # diagnóstico da instalação
npx claude-code-templates@latest --plugins          # dashboard de marketplaces e plugins
```

### Proveniência dos componentes

O README documenta explicitamente que parte do catálogo vem de outras fontes, com atribuição e licença preservadas: 139 skills científicas de `K-Dense-AI/claude-scientific-skills` (MIT), skills e exemplos oficiais de `anthropics/skills` e `anthropics/claude-code`, 14 skills de workflow de [obra/superpowers](../obra/superpowers.md) (MIT), 36 skills de papel profissional de `alirezarezvani/claude-skills` (MIT), 48 agentes de `wshobson/agents` (MIT), 21 comandos de [hesreallyhim/awesome-claude-code](../hesreallyhim/awesome-claude-code.md) (CC0 1.0) e skills de `mehdi-lamrani/awesome-claude-skills` (Apache 2.0), entre outras.

## Instalação e uso rápido

```bash
npx claude-code-templates@latest                 # navegação interativa
npx claude-code-templates@latest --agent development-tools/code-reviewer --yes
npx claude-code-templates@latest --command performance/optimize-bundle --yes
npx claude-code-templates@latest --setting performance/mcp-timeouts --yes
npx claude-code-templates@latest --hook git/pre-commit-validation --yes
npx claude-code-templates@latest --mcp database/postgresql-integration --yes
```

Documentação completa em [docs.aitmpl.com](https://docs.aitmpl.com/); o README não detalha pré-requisitos além do runtime Node.js implícito no uso de `npx`.

## Exemplos de uso

Exemplo de stack completa derivado do README, combinando quatro tipos de componente em uma única instalação:

```bash
npx claude-code-templates@latest \
  --agent development-team/frontend-developer \
  --command testing/generate-tests \
  --mcp development/github-integration \
  --yes
```

## Quando usar (e quando não usar)

- **Use quando:** você quer partir de componentes já testados pela comunidade (agentes, comandos, hooks, MCPs, skills) em vez de escrevê-los do zero, ou precisa de visibilidade operacional (analytics, monitor de chats, health check) sobre uma instalação existente do Claude Code.
- **Evite quando:** você precisa entender o *porquê* de cada padrão antes de instalá-lo — nesse caso um guia como [FlorianBruniaux/claude-code-ultimate-guide](../florianbruniaux/claude-code-ultimate-guide.md) ou a lista anotada [hesreallyhim/awesome-claude-code](../hesreallyhim/awesome-claude-code.md) explicam contexto e trade-offs que um catálogo de instalação não cobre.

## Limitações e cuidados

- **Supply chain de catálogo agregado.** O projeto reempacota componentes de dezenas de fontes de terceiros sob suas licenças originais; o README não declara um processo de revisão de segurança próprio para cada componente antes da inclusão no catálogo.
- **Monitor de conversas remoto.** A opção `--chats --tunnel` expõe o monitor via Cloudflare Tunnel; o README não detalha no texto lido quais controles de acesso protegem esse túnel.
- Apenas o README foi lido: a implementação da CLI, os templates individuais e `docs.aitmpl.com` não foram consultados.

## Estado e adoção

- Observado em 2026-10-23: 32.854 estrelas, 3.782 forks, 437 issues abertas; criado em 2025-07-04; último push em 2026-10-23.
- Licença: MIT (API do GitHub e README concordam); componentes individuais mantêm suas próprias licenças de origem.
- Linguagem principal na API: Python.
- Distribuído também como pacote npm (`claude-code-templates`), com badge de downloads no README.

## Relações

- Mantido por: [davila7](../../../entities/davila7.md)
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [Plugins de agente](../../../concepts/plugins-de-agente.md)
- Cita como fontes de componentes: [obra/superpowers](../obra/superpowers.md), [hesreallyhim/awesome-claude-code](../hesreallyhim/awesome-claude-code.md), [anthropics/skills](../anthropics/skills.md).
- Citado por [FlorianBruniaux/claude-code-ultimate-guide](../florianbruniaux/claude-code-ultimate-guide.md) como rota de instalação de templates prontos.

## Perguntas abertas

- Como o projeto audita a segurança de hooks e MCPs de terceiros antes de listá-los no catálogo?
- Qual é o volume real de uso das ferramentas de analytics e monitor de conversas, fora dos downloads do pacote npm?

## Fontes

- README: https://raw.githubusercontent.com/davila7/claude-code-templates/7d85535533914ff0880945570a94fcbec4adc042/README.md (commit `7d85535533914ff0880945570a94fcbec4adc042`, consultado em 2026-10-23). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`/repos/davila7/claude-code-templates`) em 2026-10-23.
