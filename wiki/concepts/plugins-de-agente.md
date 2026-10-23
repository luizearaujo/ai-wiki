---
type: concept
aliases: [Plugins de agente, Agent plugins, Plugin architecture, Extensões de agente, Extensibilidade por plugins]
status: draft
created: 2026-10-19
updated: 2026-10-23
tags: [agentes, plugins, extensibilidade, desktop, supply-chain]
---

# Plugins de agente

> Unidades de extensão empacotadas e instaláveis que adicionam capacidades a um agente ou workspace — ferramentas, painéis, serviços, temas, MCP — sem alterar o núcleo do produto.

## Definição

Um plugin de agente é um artefato distribuível que se registra em um **contrato de extensão** oferecido pelo host. O host define pontos de extensão e ciclo de vida; o plugin fornece a implementação. A distinção útil é com três vizinhos:

- **Skill:** instruções e workflows carregados pelo agente. Pode ser *um tipo de conteúdo* dentro de um plugin, mas não define superfícies de UI, serviços residentes ou permissões.
- **Servidor MCP:** protocolo para expor ferramentas e dados. Um plugin pode embarcar ou conectar um servidor MCP; MCP sozinho não adiciona painéis, widgets ou temas.
- **Extensão de IDE:** integra-se a um editor específico. O plugin de agente pressupõe um host próprio — desktop, CLI ou plataforma — e pode cobrir agente, interface e runtime ao mesmo tempo.

O conceito ganha força quando o produto trata o **Core como fundação e os plugins como definição do produto**: em vez de decidir no núcleo quais fluxos existem, o host publica pontos de extensão e deixa o ecossistema montar o workspace.

## Como funciona

Um contrato de plugin costuma ter quatro partes:

1. **Manifesto e empacotamento** — identidade, versão, dependências e formato de distribuição (por exemplo, `.piplug` ou marketplace).
2. **Pontos de extensão** — onde o plugin se conecta: ferramentas do agente, painéis, widgets, views, comandos, temas, serviços.
3. **Ciclo de vida** — instalação, ativação, atualização, desativação e isolamento de estado.
4. **Permissões e confiança** — o que o plugin pode acessar e como o usuário autoriza.

O catálogo de capacidades publicado pelo [vastsa/PI-Desktop](../repos/github.com/vastsa/pi-desktop.md) é um exemplo concreto de taxonomia:

| Capacidade | O que adiciona |
|---|---|
| **Command** | Ações no sistema global de comandos |
| **Panel** | Interface própria do plugin |
| **Floating Widget** | UI flutuante (voz, status, timers) |
| **Work Panel View** | Novas views na área de trabalho lateral |
| **Agent Tool** | Ferramentas chamáveis pelo agente |
| **Completion** | Uso dos modelos já configurados pelo usuário |
| **Skill** | Capacidades e workflows reutilizáveis do agente |
| **Theme** | Aparência do workspace |
| **MCP Server** | Conexão com servidores MCP locais ou remotos |
| **Service** | Trabalho persistente em background |
| **Message Bus** | Comunicação entre plugins |

Uma extensão pode combinar várias capacidades e virar um produto inteiro: um agente de voz, por exemplo, reúne widget flutuante, serviço de fala, agent tool e comandos. Isso diferencia o plugin de uma integração pontual.

## Onde aparece

- [vastsa/PI-Desktop](../repos/github.com/vastsa/pi-desktop.md) — workspace desktop que mantém o Core pequeno e define o workflow por plugins em três camadas (agente, workspace e plataforma); distribui pacotes `.piplug` e oferece marketplace, templates de desenvolvimento e plugins carregáveis em modo de desenvolvimento.
- [Agent harness](agent-harness.md) — harnesses costumam ser instalados como plugin, pacote npm ou clone em um diretório de skills; a instalação é tratada como decisão de supply chain.
- [openai/codex-plugin-cc](../repos/github.com/openai/codex-plugin-cc.md) — plugin do marketplace do Claude Code que adiciona slash commands (`/codex:*`) e um subagente (`codex:codex-rescue`) sem embarcar runtime próprio: chama o binário e o app server do Codex já instalados, reaproveitando a autenticação local — um caso de plugin como ponte entre harnesses de fornecedores diferentes.
- [davila7/claude-code-templates](../repos/github.com/davila7/claude-code-templates.md) — inclui um "Plugin Dashboard" (`--plugins`) para visualizar marketplaces, plugins instalados e permissões a partir de uma interface própria, além de instalar componentes individuais por `npx` sem passar pelo fluxo nativo de plugin.
- **Não documentado na wiki:** marketplaces e formatos de plugin de outros hosts. A comparação de contratos, versionamento e isolamento entre produtos ainda é uma lacuna.

## Trade-offs

- **Vantagens:** núcleo menor e mais estável; o produto se adapta a domínios diferentes sem forks; terceiros podem construir produtos completos; atualizações de capacidade não exigem rebuild do host; o usuário instala só o que usa.
- **Limitações:** fragmentação de qualidade e de compatibilidade; cada plugin amplia a superfície de ataque e de permissões; APIs de extensão em Early Preview quebram plugins; marketplace sem curadoria vira vetor de distribuição de código não confiável; custo de contexto e de suporte cresce com o ecossistema; serviços residentes e message bus dificultam isolamento e depuração.
- **Critério prático:** vale quando o domínio de uso é amplo e mutável o bastante para justificar um contrato estável. Para um único fluxo bem definido, um monólito ou uma skill é mais barato.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — skill é uma das capacidades que um plugin pode empacotar; [Agent harness](agent-harness.md) — o host que define o contrato e o ciclo de vida; [Model Context Protocol](model-context-protocol.md) — um plugin pode expor ou consumir MCP; [Orquestração multiagente](orquestracao-multiagente.md) — plugins podem adicionar ferramentas e superfícies usadas na coordenação.
- **Contrasta com:** extensão de IDE presa a um editor; skill isolada sem UI nem serviços; monólito que embute todos os fluxos no núcleo.
- **Pré-requisito para:** ecossistema de terceiros e marketplace — sem contrato de extensão, versionamento e política de confiança, a distribuição vira código arbitrário.

## Perguntas abertas

- Qual é o contrato mínimo que permite plugins portáveis entre hosts diferentes?
- Como versionar a API de plugins sem quebrar o ecossistema a cada release?
- Que modelo de isolamento (processo, sandbox, permissões declarativas) é suficiente para plugins com UI e serviços residentes?
- Como um marketplace revisa, assina e revoga pacotes?
- O plugin deve receber credenciais diretamente ou apenas chamadas mediadas pelo host?
- Como medir o custo de contexto e de manutenção de um ecossistema de plugins em comparação com um núcleo maior?

## Fontes

- [vastsa/PI-Desktop](../repos/github.com/vastsa/pi-desktop.md) — README no commit `87a48b953e8bada43a7a63f8922846198b9efb61` (consultado em 2026-10-19).
- [Agent harness](agent-harness.md) — página existente da wiki, usada como contexto sobre instalação e supply chain.
- [openai/codex-plugin-cc](../repos/github.com/openai/codex-plugin-cc.md) — README no commit `db52e28f4d9ded852ab3942cea316258ae4ef346` (consultado em 2026-10-23).
- [davila7/claude-code-templates](../repos/github.com/davila7/claude-code-templates.md) — README no commit `7d85535533914ff0880945570a94fcbec4adc042` (consultado em 2026-10-23).
