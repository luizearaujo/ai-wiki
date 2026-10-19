---
type: entity
kind: person
url: https://github.com/affaan-m
created: 2026-10-19
updated: 2026-10-19
tags: [agentes, harness, claude-code, seguranca]
---

# affaan-m (Affaan Mustafa)

> Engenheiro e autor do ECC, um dos harnesses de agente de código de maior adoção no GitHub, com foco em processo de engenharia, memória entre sessões e auditoria de configuração de agentes.

## O que é

Affaan Mustafa é desenvolvedor sediado em Nova York. O perfil do GitHub o descreve como *Compute Trading Lead* na Jump Trading e fundador anterior do *Agentic Desk for Compute* na Itô Markets (adquirida). Também mantém o site pessoal affaanmustafa.com e a conta [@affaanmustafa](https://x.com/affaanmustafa).

O README do ECC acrescenta que ele usa Claude Code desde o rollout experimental, venceu o hackathon Anthropic x Forum Ventures em setembro de 2025 com [@DRodriguezFX](https://x.com/DRodriguezFX) e construiu o zenith.chat inteiramente com workflows agênticos.

## Repositórios e projetos

- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — harness de agente com 71 agentes, 311 skills, memória portátil, hooks, regras e o scanner AgentShield; licença MIT e caminhos para Claude Code, Codex, Qoder e adaptadores.
- `affaan-m/agentshield` — scanner de configuração de agentes citado pelo ECC (segredos, permissões, hooks, MCP e arquivos de agente). Não ingerido nesta wiki.
- ECC Pro / ECC Tools — GitHub App hospedado para repositórios privados, análise de PR e suporte; a documentação descreve o Pro como forma de financiar o OSS.

## Relevância no ecossistema

O ECC ajudou a popularizar a ideia de **harness como produto**: um pacote que instala processo, especialistas, memória e segurança sobre um CLI já existente, em vez de competir com o modelo. O projeto também trata o próprio agente como superfície de ataque — o AgentShield audita `CLAUDE.md`, hooks, MCP, permissões e segredos — e mantém um Memory Vault portátil entre harnesses.

A combinação de catálogo amplo, licença MIT e caminhos multi-harness deu ao projeto adoção expressiva (mais de 280 mil stars observadas em 2026-10-19), o que o torna uma referência para comparar formatos de skill, distribuição e governança de contexto.

## Relações

- Associado a: Jump Trading (ocupação atual), Itô Markets (projeto anterior), ECC Tools / ECC Pro (produto hospedado).
- Mantém: [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md), `affaan-m/agentshield`.
- Comparável a: [garrytan](../entities/garrytan.md) e [HarnessMD](../entities/harnessmd.md) — outros autores de harnesses documentados na wiki.

## Fontes

- Perfil do GitHub: https://github.com/affaan-m (API em 2026-10-19).
- README de [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) no commit `76aaa77df6adc5b889e689007bf99b9a4f74af34` (consultado em 2026-10-19).
