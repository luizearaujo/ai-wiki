---
type: concept
aliases: [Sparse attention, Atenção esparsa, Trainable sparse attention, Hybrid attention, InfLLM-V2, Lightning Attention]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [atencao, contexto-longo, inferencia, arquitetura, transformers, kv-cache, eficiencia]
---

# Atenção esparsa para contexto longo

> Conjunto de mecanismos que substitui a atenção densa quadrática por conexões seletivas — ou por uma mistura de atenção esparsa e linear — para permitir contexto de centenas de milhares a milhões de tokens com custo de computação e KV cache viável.

## Definição

Na atenção densa, cada token consulta todos os tokens anteriores: o custo cresce com o quadrado do comprimento e o KV cache cresce linearmente. **Atenção esparsa** restringe cada token a um subconjunto relevante — janelas locais, blocos selecionados, padrões fixos ou seleção aprendida — reduzindo o número de pares computados. **Atenção linear** troca o produto softmax quadrático por uma forma recorrente de custo linear.

O conceito aqui cobre três variações que aparecem juntas em modelos recentes:

| Variação | Ideia | Exemplo documentado |
|---|---|---|
| **Esparsidade treinável** | o padrão de seleção é aprendido junto com os pesos, não fixado a priori | InfLLM-V2 no MiniCPM4/4.1 |
| **Híbrido esparso + linear** | algumas camadas usam atenção esparsa; a maioria usa linear | SALA: 25% InfLLM-V2, 75% Lightning Attention |
| **Extrapolação posicional** | embeddings posicionais e treino continuado preservam qualidade além do comprimento treinado | HyPE no SALA; YaRN no MiniCPM4.x |

## Como funciona

O pipeline conceitual é:

```text
token -> seleciona subconjunto de chaves -> calcula atenção só nesse subconjunto
      -> mantém KV cache reduzido -> repete por camada
```

Nos modelos documentados:

- **InfLLM-V2** é descrito como atenção esparsa treinável em que cada token interage com **menos de 5% dos tokens** em contexto de 128K, com kernels de treino próprios.
- **Lightning Attention** fornece o caminho linear para a maior parte das camadas no SALA, reduzindo o overhead global.
- **HyPE (Hybrid Positional Embedding)** equilibra desempenho em contexto curto e longo, sem depender apenas de extrapolação posicional.
- **HALO** é uma receita de destilação que transfere capacidades de atenção densa para a arquitetura híbrida, mitigando a degradação típica de modelos puramente lineares.
- **Conversão por treino continuado** transforma pesos de um Transformer denso em híbrido, com orçamento declarado de ~25% do custo de treinar do zero.

O ganho aparece em **tempo até o primeiro token (TTFT)**, throughput de decode e, principalmente, **memória**: o SALA declara processar 1M de tokens em uma única RTX 5090, enquanto o Qwen3-8B comparado sofre OOM. O MiniCPM4/4.1 declara ~7× de decode contra Qwen3-8B em Jetson AGX Orin, e o 4.1 declara 3× em decodificação de raciocínio.

Há um custo de compatibilidade: nem todo runtime implementa o caminho esparso. No MiniCPM4.x, vLLM e SGLang suportam apenas atenção densa; o modo esparso exige Transformers ou o runtime CPM.cu do projeto. A arquitetura só entrega o ganho quando o stack de inferência também a suporta.

## Onde aparece

- [OpenBMB/MiniCPM](../repos/github.com/openbmb/minicpm.md) — SALA (híbrido esparso + linear, 1M+ tokens) e MiniCPM4/4.1 (InfLLM-V2, atenção esparsa treinável, BitCPM e CPM.cu).
- **Referências citadas pelo projeto** (não documentadas na wiki): InfLLM-V2 (arXiv 2509.24663), HyPE (arXiv 2601.22156), Lightning Attention e Qwen3-8B como baseline.
- **Não documentados na wiki:** outros modelos com atenção esparsa ou linear (por exemplo, variantes de DeepSeek e Mistral) não têm página própria.

## Trade-offs

- **Vantagens:** contexto muito maior com memória viável; TTFT e decode mais rápidos em sequências longas; menos pressão sobre o KV cache; possibilidade de rodar em GPU de consumidor.
- **Limitações:** qualidade depende de o padrão de seleção capturar as dependências relevantes; modelos puramente lineares podem degradar em tarefas gerais; kernels e runtimes precisam suportar o modo esparso; benchmarks de contexto longo são sensíveis ao tipo de tarefa e ao comprimento de treino.
- **Custo escondido:** treinar esparsidade exige dados longos e engenharia de kernels; converter um modelo denso exige treino continuado e avaliação cuidadosa de regressão.
- **Não é compressão de pesos:** atenção esparsa reduz o custo do contexto, não o tamanho dos parâmetros; pode ser combinada com quantização (como o BitCPM) ou com streaming de experts.

## Relações

- **Relacionado a:** [LLMs compactos on-device](llms-compactos-on-device.md) — contexto longo é um dos eixos em que modelos pequenos tentam competir; [Streaming de experts em MoE](streaming-de-experts-em-moe.md) — outra forma de reduzir o trabalho por token, atacando parâmetros em vez de atenção.
- **Contrasta com:** atenção densa completa; janelas locais fixas sem seleção aprendida; truncar ou resumir o contexto.
- **Depende de:** kernels de atenção esparsa, treino com sequências longas, estratégia posicional (HyPE, YaRN, NoPE) e runtimes que implementem o modo.

## Perguntas abertas

- Qual é a perda de qualidade em tarefas gerais ao substituir atenção densa por um híbrido esparso + linear?
- A extrapolação para 1M+ tokens se sustenta em tarefas que exigem recuperação precisa em todo o contexto, não só em RULER/NoLiMa?
- Como esparsidade treinável se compara a janelas fixas e a atenção linear pura no mesmo orçamento de treino?
- Quanto custa manter kernels próprios (como CPM.cu) em comparação a esperar suporte nos runtimes mainstream?
- A combinação de atenção esparsa com quantização ternária preserva raciocínio e tool use?
- Modelos compactos com contexto longo são uma alternativa real a RAG para bases de documentos grandes?

## Fontes

- [OpenBMB/MiniCPM](../repos/github.com/openbmb/minicpm.md) — README no commit `316cfb1cea39f39cfa16b4f5703b77495c2340be` (consultado em 2026-10-19). Somente o README foi lido; papers, kernels e código não foram consultados.
