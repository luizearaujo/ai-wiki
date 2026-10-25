---
type: repo
url: https://github.com/Jakeschincariol/trader-skill
host: github.com
owner: jakeschincariol
repo: trader-skill
commit: 5189e79b9a480755a3733ac9713f5353981dbe18
license: MIT
language: Python
status: active
created: 2026-10-25
ingested: 2026-10-25
updated: 2026-10-25
tags: [skills, trading, financas, sec-edgar, congress, agent-skills, alpaca]
---

# Jakeschincariol/trader-skill

> 11 skills de trading para Claude que copiam investidores via 13F, monitoram notícias e divulgações do Congresso, dimensionam ordens ao orçamento e nunca executam nada sem aprovação explícita do usuário.

## O que é

trader-skill é uma coleção de 11 skills para Claude Code (formato `SKILL.md` + ferramentas Python de biblioteca padrão). Cada skill cobre uma etapa do ciclo de trading: pesquisar, monitorar, dimensionar, verificar risco e executar — nessa ordem. O princípio central é que **nenhuma ordem é colocada sem que o usuário responda "yes"**: o skill `/trader-broker` só envia o ticket depois de aprovação explícita no chat, e Claude ainda exibe o cartão "Allow once / Deny" como segunda verificação.

Dados de mercado vêm de fontes públicas: SEC EDGAR, Clerk da Câmara (PTRs do STOCK Act), feeds RSS de notícias e o endpoint não oficial de preços do Yahoo Finance. Sem cadastro, sem chave de API de terceiros. Apenas Python 3.8+ com biblioteca padrão.

> **A verificar:** os scripts Python não foram lidos; lógica interna, cobertura de edge cases e comportamento offline não foram verificados.

## As onze skills

| Skill | Comando | Função |
|-------|---------|--------|
| **Copycat** | `/trader-copycat` | Lê o 13F-HR mais recente de um fundo no SEC EDGAR, reconstrói o portfólio como pesos e diff com o trimestre anterior (compras, adições, cortes, vendas). |
| **News** | `/trader-news` | Monitora manchetes e 8-Ks no SEC para cada ativo da carteira. |
| **Budget** | `/trader-budget` | Dimensiona cada posição ao orçamento: mantém buffer de caixa e cap por ativo. |
| **Pelosi** | `/trader-pelosi` | Lê divulgações de operações de membros do Congresso (PTRs) assim que postam, converte PDFs em linhas limpas e alerta por filing. |
| **Analyst** | `/trader-analyst` | Extrai dados financeiros do SEC XBRL: receita, lucro, EPS diluído, margens, crescimento. |
| **Screener** | `/trader-screener` | Filtra empresas por regras definidas pelo usuário e rankeia os que passam. |
| **Risk** | `/trader-risk` | Valida cada ordem proposta contra limites configurados (tamanho, concentração, buffer de caixa) — PASS ou BLOCK com motivo. |
| **Broker** | `/trader-broker` | Transforma uma ordem aprovada no ticket exato para o conector de corretora (Alpaca MCP, paper por padrão) e registra o "yes" do usuário. |
| **Tax** | `/trader-tax` | Rastreia lotes de custo, ganhos/perdas, candidatos a tax-loss harvesting e wash sales. |
| **Alerts** | `/trader-alerts` | Dispara quando preço-alvo, stop ou abertura da NYSE é atingido, com calendário real do NYSE. |
| **Rebalance** | `/trader-rebalance` | Recalcula trades necessários para voltar aos pesos-alvo quando o desvio ultrapassa a banda. |

## Como funciona

As skills se encadeiam por arquivos na pasta `trader/`: cada uma lê o que a anterior escreveu.

```
copycat → budget → risk → broker          (copiar um investidor)
news / pelosi / alerts                    (monitorar, em schedule)
analyst → screener → budget → risk → broker  (seleção própria)
rebalance / tax → risk → broker           (manutenção)
```

Exemplo com Berkshire Hathaway e US$5.000:

1. `/trader-copycat` busca CIK 1067983, lê o 13F-HR mais recente e calcula pesos normalizados dos top 5.
2. `/trader-budget` distribui US$5.000 respeitando buffer de 10% e cap de 25% — gera `trader/orders.json`.
3. `/trader-risk` valida cada ordem (tickers bloqueados, tamanho, concentração, caixa) → PASS ou BLOCK.
4. `/trader-broker` mostra o ticket ("Buy $1.250 de AAPL, market, day"), aguarda "yes" explícito e, após aprovação, chama o conector Alpaca (paper account por padrão).

## Instalação

```bash
# Via Claude (como skill)
https://github.com/Jakeschincariol/trader-skill
install skill

# Via plugin no Claude Code
/plugin marketplace add Jakeschincariol/trader-skill
/plugin install trader-skill@trader-skill

# Manual (global)
git clone https://github.com/Jakeschincariol/trader-skill.git
cp -r trader-skill/trader-* ~/.claude/skills/

# Local ao projeto
cp -r trader-skill/trader-* .claude/skills/
```

Configuração obrigatória para o SEC: `"sec_user_agent": "Seu Nome voce@example.com"` em `trader/config.json` ou na variável `SEC_USER_AGENT` (exigência do SEC: identifique-se, máx. 10 req/s).

## Limitações e cuidados

- **Não é conselho financeiro.** Lê dados públicos e faz aritmética; não conhece a situação do usuário; copiar um investidor não copia seus resultados.
- **13F é atrasado e parcial:** fundos divulgam 45 dias após o fim do trimestre; o 13F lista apenas posições longas em ativos listados nos EUA — sem shorts, caixa ou ativos estrangeiros.
- **Dados do Congresso são públicos, não informação privilegiada:** PTRs têm delay de até 45 dias (STOCK Act) e os valores são divulgados como faixas.
- **Fontes não oficiais:** o endpoint de preços do Yahoo Finance é informal e pode mudar. Verifique dados relevantes com a corretora antes de agir.
- **Paper trading por padrão:** `"paper": true` no `config.example.json`; o conector Alpaca aponta para a conta paper por padrão.
- Sem opções, margem, venda a descoberto ou alavancagem, a menos que ativados explicitamente.

## Estado e adoção

- Último push: 2026-10-14.
- Observado em 2026-10-25: ~541 stars, ~96 forks, ~1 issue aberta.
- Licença: MIT. Feito por [Jake Schincariol](https://opusjake.ai).

## Relações

- Mantido por: [Jakeschincariol](../../../entities/jakeschincariol.md)
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [Análise financeira multiagente](../../../concepts/analise-financeira-multiagente.md)
- Relacionado: [himself65/trade-skills](../himself65/trade-skills.md) — outra coleção de skills de trading, com foco em opções e base de conhecimento OKF.

## Fontes

- README: https://raw.githubusercontent.com/Jakeschincariol/trader-skill/5189e79b9a480755a3733ac9713f5353981dbe18/README.md (commit `5189e79b9a480755a3733ac9713f5353981dbe18`, consultado em 2026-10-25). Somente o README foi lido; os arquivos `SKILL.md` e os scripts Python não foram consultados.
- Metadados: API do GitHub em 2026-10-25.
