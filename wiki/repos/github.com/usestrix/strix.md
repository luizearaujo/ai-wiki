---
type: repo
url: https://github.com/usestrix/strix
host: github.com
owner: usestrix
repo: strix
commit: fde37a149fc942dd107666441a1989f187d30c3b
license: Apache-2.0
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [ciberseguranca, agentes, orquestracao-multiagente, mcp, pentest]
---

# usestrix/strix

> Agentes de IA autônomos que rodam código dinamicamente, encontram vulnerabilidades e as validam com provas de conceito reais — um "graph of agents" especializado em recon, exploração e pós-exploração, com CLI local, viewer offline e nove skills para agentes de código.

## O que é

Strix se posiciona como alternativa a pentest manual e a scanners estáticos: em vez de heurísticas que geram falsos positivos, os agentes exploram o alvo de verdade e produzem um PoC funcional por achado. Serve tanto desenvolvedores individuais quanto times de segurança, com três camadas de uso — CLI open source local, Strix Cloud (hospedado, com autofix e revisão de PR) e Enterprise (SSO, relatórios de compliance, deploy em VPC).

## Como funciona

- **Toolkit ofensivo completo**: proxy de interceptação HTTP (Caido), browser automatizado para XSS/CSRF/clickjacking, shell interativo para desenvolvimento de exploit, sandbox Python para PoCs, reconhecimento/OSINT, SAST+DAST e uma base de conhecimento de vulnerabilidades com CVSS e classificação OWASP.
- **Graph of Agents**: orquestração multiagente especializada — agentes de recon, exploração e pós-exploração compartilham descobertas, encadeiam vulnerabilidades e colaboram como um red team, com execução paralela em múltiplos alvos.
- **Alvos flexíveis**: diretório local, URL de repositório GitHub, aplicação web ao vivo, domínio/IP, ou um contrato de API (OpenAPI/Swagger/Postman) pareado com a URL base para testar todo endpoint declarado em vez de descobri-los por crawling.
- **Modo headless** (`-n/--non-interactive`) para servidores e jobs automatizados, com código de saída não-zero quando acha vulnerabilidade — pensado para CI/CD (há um workflow de GitHub Actions de exemplo no README).
- **Viewer local**: `strix view` abre um dashboard (`127.0.0.1`, link com token) com os achados, um mapa ao vivo do time de agentes e execuções passadas — nada sai da máquina.
- **MCP de entrada e saída**: Strix pode se conectar a servidores MCP próprios do usuário (`~/.strix/mcp-servers.json`, `stdio` ou `http`) para dar às suas ferramentas acesso ao agente durante uma execução; na direção inversa, `npx skills add usestrix/strix` instala nove skills para que Claude Code, Cursor, Codex ou qualquer agente compatível com SKILL.md rode pentests, corrija achados e configure scanning em CI.
- Modelo é plugável: recomenda GLM-5.3 (padrão via OpenRouter), GPT-5.4, Claude Sonnet 4.6, Gemini 3 Pro Preview, DeepSeek V4 Pro ou Kimi K3; também aceita login via assinatura ChatGPT Plus/Pro em vez de chave de API metrada.

## Instalação e uso rápido

```bash
curl -sSL https://strix.ai/install | bash
export STRIX_LLM="openrouter/z-ai/glm-5.3"
export LLM_API_KEY="your-api-key"
strix --target ./app-directory
```

Pré-requisitos: Docker em execução (a primeira rodada baixa a imagem do sandbox) e uma chave de API de um provedor de LLM suportado. `strix --update` atualiza o binário standalone ou imprime o comando certo para quem instalou via pipx/uv/pip.

## Quando usar (e quando não usar)

- **Use quando:** quer testes de penetração rápidos com evidência real (PoC), integrados a CI/CD, sobre código, API ou aplicação web — e tem autorização para testar o alvo.
- **Evite quando:** não tem permissão explícita e por escrito para testar o sistema-alvo — o próprio README avisa que uso não autorizado é ilegal na maioria das jurisdições e que a responsabilidade é inteiramente do usuário.

## Limitações e cuidados

- **Aviso do próprio projeto**: só rodar contra sistemas próprios ou com permissão explícita e por escrito, dentro do escopo acordado; Strix é fornecido "como está", sem garantia nem responsabilidade por uso indevido.
- Execução local exige Docker e uma chave de LLM paga (ou assinatura ChatGPT); a via gratuita sem setup é só a nuvem da Strix.
- Construído sobre LiteLLM, Caido, Nuclei, Playwright e Bubble Tea — dependências externas que carregam suas próprias superfícies de risco, não auditadas nesta ingestão.

## Estado e adoção

- 70.673 estrelas, 7.840 forks, 492 issues abertas — observado em 2026-10-21.
- Repositório criado em 2025-08-05, com push mais recente em 2026-10-21 — observado em 2026-10-21.
- Também distribuído via PyPI (`strix-agent`).
- Licença: Apache-2.0.

## Relações

- Mantido por: [Strix (usestrix)](../../../entities/usestrix.md)
- Conceitos: [Cibersegurança com agentes](../../../concepts/ciberseguranca-com-agentes.md), [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — "Graph of Agents", [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md), [Agent skills](../../../concepts/agent-skills.md) — nove skills instaláveis via `npx skills add`.
- Alternativas (cibersegurança ofensiva com agentes já documentadas): [SnailSploit/Claude-Red](../snailsploit/claude-red.md), [mukul975/Anthropic-Cybersecurity-Skills](../mukul975/anthropic-cybersecurity-skills.md) — ambas bibliotecas de skills para um agente de código genérico, enquanto Strix é um agente/produto dedicado e autônomo.

## Perguntas abertas

- Como o "Graph of Agents" decide quando parar de explorar um alvo e declarar a varredura completa?
- Qual é a taxa de falso positivo real das PoCs geradas, fora dos números promocionais do README?

## Fontes

- README: https://raw.githubusercontent.com/usestrix/strix/fde37a149fc942dd107666441a1989f187d30c3b/README.md (commit `fde37a149fc942dd107666441a1989f187d30c3b`, consultado em 2026-10-21). Somente o README foi lido; `AGENTS.md` e as nove skills não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/usestrix/strix`), consultada em 2026-10-21.
