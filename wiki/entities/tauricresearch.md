---
type: entity
kind: org
url: https://github.com/TauricResearch
created: 2026-10-19
updated: 2026-10-19
tags: [organizacao, trading, financas, agentes, pesquisa]
---

# Tauric Research

> Organização de pesquisa aplicada em trading com IA, criadora do TradingAgents — framework multiagente que simula uma firma de trading com LLMs.

## O que é

Tauric Research é uma organização no GitHub criada em 2024-12-26, sediada nos Estados Unidos, com a descrição "Pioneering Trading Intelligence with AI Precision". O perfil informa três repositórios públicos e cerca de 4,2 mil seguidores.

A produção documentada nesta wiki é o [TradingAgents](../repos/github.com/tauricresearch/tradingagents.md), framework que organiza analistas, pesquisadores, trader, risco e gestor de portfólio em um fluxo LangGraph. O README do projeto cita os autores do paper associado — Yijia Xiao, Edward Sun, Di Luo e Wei Wang — e mantém comunidade em Discord e X, além de divulgar o projeto sob a marca Tauric.

## Repositórios e projetos

- [TauricResearch/TradingAgents](../repos/github.com/tauricresearch/tradingagents.md) — framework multiagente de análise e decisão de trading; Apache-2.0; ~112 mil estrelas observadas em 2026-10-19.
- [TauricResearch/Trading-R1](https://github.com/TauricResearch/Trading-R1) — repositório com descrição "Terminal coming soon"; ~500 estrelas; não documentado nesta wiki.
- `TauricResearch/.github` — repositório de perfil/configuração da organização.

## Relevância no ecossistema

O TradingAgents é um dos maiores exemplos públicos de **orquestração multiagente aplicada a um domínio regulado**: os agentes não apenas conversam, mas precisam respeitar datas de publicação de dados, produzir trilha de decisão e passar por aprovação de risco. O projeto também trata memória como mecanismo de aprendizado — decisões passadas são liquidadas e transformadas em reflexões lidas pelo gestor de portfólio.

A organização é nova e concentrada em trading; não há, nas fontes consultadas, portfólio além do TradingAgents e do Trading-R1. O limite entre o framework open-source e eventuais produtos ou serviços da Tauric não está documentado no README. **A verificar.**

## Relações

- **Criou:** [TradingAgents](../repos/github.com/tauricresearch/tradingagents.md).
- **Conceitos:** [Orquestração multiagente](../concepts/orquestracao-multiagente.md), [Memória de agente](../concepts/memoria-de-agente.md), [Análise financeira multiagente](../concepts/analise-financeira-multiagente.md).
- **Associado ao paper:** arXiv 2412.20138, *TradingAgents: Multi-Agents LLM Financial Trading Framework*.

## Fontes

- https://github.com/TauricResearch — perfil da organização e repositórios via API do GitHub em 2026-10-19.
- https://github.com/TauricResearch/TradingAgents — README no commit `e8f5503e9b86d5c2710b0c76b1f686703968c9df`; metadados da API do GitHub observados em 2026-10-19.
