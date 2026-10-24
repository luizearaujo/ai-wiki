---
type: entity
kind: org
url: https://github.com/zai-org
created: 2026-10-24
updated: 2026-10-24
tags: []
---

# Z.ai (zai-org / Zhipu AI)

> Empresa chinesa (antes Zhipu AI) conhecida pela família de modelos GLM e ChatGLM; nesta wiki, documentada pontualmente pelo GLM-5.3-FlashX, variante de alta velocidade servida apenas via API.

## O que é

Z.ai mantém a organização GitHub `zai-org` (antes `THUDM`), com histórico de publicação aberta de modelos como ChatGLM, GLM-4.5, CogVLM, CodeGeeX, CogView e CogVideoX. **Esta página documenta apenas o GLM-5.3-FlashX**, uma variante de alta velocidade do GLM-5.3-Flash oferecida como serviço de API — não há repositório no GitHub nem pesos abertos identificados para essa variante especificamente; o que segue vem da página oficial de preços da Z.ai e de agregadores de terceiros, não de um README.

**A verificar nesta ingestão:** janela de contexto, saída máxima, velocidade declarada (tokens/s) e data de lançamento — nenhum desses dados aparece na página oficial de preços consultada; os números abaixo vêm só de agregadores terceiros e podem estar desatualizados ou incorretos.

## Repositórios e projetos

Nenhum repositório específico do GLM-5.3-FlashX foi identificado. A organização `zai-org` publica gerações anteriores (ChatGLM, GLM-4.5 e famílias CogVLM/CogView/CogVideoX) fora do escopo desta ingestão.

## Relevância no ecossistema

GLM-5.3-FlashX é um caso de **otimização de infraestrutura de serving, não de nova arquitetura**: segundo agregadores consultados, o lançamento não trouxe novos benchmarks nem mudanças arquiteturais em relação ao GLM-5.3-Flash, apenas maior throughput de inferência. Preços oficiais (USD por 1M de tokens, página de preços da Z.ai, consultada em 2026-10-24):

| Modelo | Entrada | Entrada em cache | Saída |
| --- | --- | --- | --- |
| GLM-5.3 | $1,40 | $0,26 | $4,40 |
| GLM-5.3-Flash | $0,15 | $0,03 | $0,50 |
| GLM-5.3-FlashX | $0,37 | $0,075 | $1,25 |

Agregadores de terceiros (não oficiais) relatam adicionalmente: pico de saída de ~200 tokens/s (vs. ~98 tok/s no GLM-5.3-Flash base), lançamento por volta de 18 de setembro de 2026, contexto de 1M tokens e saída máxima de 128K — nenhum desses números foi confirmado na página oficial de preços.

## Relações

- Colabora com: comunidade de servidores de inferência (unsloth, entre outros, lista GLM-5.3-Flash como modelo suportado).
- Associado a: `THUDM`/Knowledge Engineering Group (KEG) da Tsinghua, origem histórica da família GLM/ChatGLM.
- Concorre com: outros provedores de modelos via API com variantes de velocidade/custo, fora do escopo desta ingestão.

## Fontes

- https://docs.z.ai/guides/overview/pricing (consultado em 2026-10-24) — página oficial de preços; não é um README nem documentação de repositório, pois não há repositório identificado para esta variante.
- Agregadores de terceiros (kucoin.com/news/flash, cometapi.com, cloudprice.net, anotherwrapper.com) consultados em 2026-10-24 para contexto/velocidade/data de lançamento — não oficiais, tratados como não verificados.
