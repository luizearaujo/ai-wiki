---
type: concept
aliases: [Latent MoE, MoE latente, Latent Mixture-of-Experts]
status: draft
created: 2026-11-13
updated: 2026-11-13
tags: [moe, inferencia, arquitetura, eficiencia]
---

> Variante de MoE em que as entradas dos especialistas são comprimidas para um espaço latente de dimensionalidade reduzida antes do roteamento, mantendo a atenção em largura completa.

## Como funciona

No MoE padrão, o token é roteado em sua representação de largura completa para um subconjunto de especialistas. No **MoE latente**, uma projeção adicional comprime a representação antes de alimentar os especialistas:

```
token (largura completa d_model)
    → atenção (largura completa, mantida sem compressão)
    → projeção → espaço latente (d_latent < d_model)
    → roteamento entre especialistas comprimidos
    → des-projeção → largura completa
```

O resultado é duplo: os pesos dos especialistas são menores (pool de especialistas mais compacto), e o roteamento opera em um espaço mais denso.

## Exemplo: Edge0

O [Edge0 145B](../repos/github.com/edge0-ai/edge0.md) usa largura latente de 1792 dimensões (versus a largura completa da atenção). Cada camada tem 512 especialistas roteados + 1 compartilhado; cada token ativa 10 dos 512. O pool de especialistas resultante é de 84,6B parâmetros — menor do que seria com MoE padrão na mesma capacidade total.

| Modelo | d_latent | Especialistas | Pool de especialistas |
|--------|---------|---------------|----------------------|
| Edge0 145B | 1792 | 512 roteados + 1 | 84,6B parâmetros |
| Edge0 120B | 1280 | 512 roteados + 1 | 60,4B parâmetros |

## Relação com conceitos vizinhos

- Distinto de [Streaming de experts em MoE](streaming-de-experts-em-moe.md): aquele trata de *onde os pesos residem* (disco vs. VRAM); este trata da *arquitetura dos especialistas*.
- Próximo da atenção latente (MLA do DeepSeek-V2/Kimi K3), que comprime o KV cache por uma projeção latente; o Latent MoE aplica a mesma ideia de compressão ao feed-forward.
- Distinto de [Atenção esparsa para contexto longo](atencao-esparsa-para-contexto-longo.md): esparsidade em atenção vs. compressão de especialistas.

## Limitações do conceito

**A verificar:** referências acadêmicas formais que cunham o termo "Latent MoE"; pode ser nomenclatura própria da Edge0-AI sem publicação associada até o momento da ingestão.

## Fontes

- `docs/models/edge0-145b.md` e README.md do repositório `Edge0-AI/Edge0` (`da9cc526747759227714ddde0728763d95306c04`), lidos em 2026-11-13.
