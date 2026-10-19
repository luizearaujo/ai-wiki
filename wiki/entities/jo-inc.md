---
type: entity
kind: org
url: https://github.com/jo-inc
created: 2026-10-19
updated: 2026-10-19
tags: [organizacao, agentes, browser, automacao, produto]
---

# jo-inc

> Organização por trás do agente pessoal jo (askjo.ai) que publica o Camofox Browser, servidor de browser com anti-detecção para agentes.

## O que é

`jo-inc` é a conta de organização no GitHub ligada ao produto **jo**, descrito no README do Camofox como "a personal AI agent that runs half on your Mac, half on a dedicated cloud machine just for you", disponível em macOS, Telegram, WhatsApp e e-mail. O perfil informa o site `askjo.ai`, localização nos Estados Unidos e bio "a personal agent".

A conta foi criada em 2025-08-12, declara 9 repositórios públicos e cerca de 92 seguidores observados em 2026-10-19. O README do Camofox credita **Pradeep Elankumaran** (@pradeep24) como co-fundador e CTO técnico da Jo.

## Repositórios e projetos

- [jo-inc/camofox-browser](../repos/github.com/jo-inc/camofox-browser.md) — servidor REST de browser baseado em Camoufox, com snapshots de acessibilidade, refs estáveis, sessões isoladas, cookies, proxy e tracing; MIT, JavaScript, ~11,7 mil estrelas em 2026-10-19.
- **jo (produto comercial)** — agente pessoal hospedado; citado pelo README como o contexto em que o Camofox nasceu, não documentado nesta wiki.
- Demais repositórios públicos: 9 no total, não inventariados nesta ingestão.

## Relevância no ecossistema

O caso ilustra um padrão de **componente interno virando produto open source**: uma empresa de agente pessoal publica o servidor de browser que usa, com API voltada a agentes e um plugin para o OpenClaw. O README mistura a divulgação do produto comercial (jo, beta gratuito) com documentação técnica detalhada — inclusive uma seção de modelo de segurança escrita explicitamente para revisores automatizados.

O Camofox também é um exemplo de especialização em uma camada do stack: em vez de construir o agente inteiro, entrega a ferramenta de navegação com observação estruturada e contenção de sessão. **A verificar** se a promessa de anti-detecção se sustenta fora dos sites citados.

## Relações

- **Criou:** [camofox-browser](../repos/github.com/jo-inc/camofox-browser.md).
- **Conceitos:** [Navegação web agêntica](../concepts/navegacao-web-agentica.md), [CLI agent-first](../concepts/cli-agent-first.md), [Agent skills](../concepts/agent-skills.md).
- **Associado a:** Camoufox (engine), OpenClaw (framework de agente), askjo.ai (produto).

## Fontes

- https://github.com/jo-inc — perfil e bio via API do GitHub em 2026-10-19 (repositórios públicos, seguidores, localização e data de criação).
- https://github.com/jo-inc/camofox-browser — README no commit `39c82094013480b373df6600d44c7f036f58356e`; metadados da API do GitHub observados em 2026-10-19.
