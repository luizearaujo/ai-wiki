---
type: concept
aliases: [Streaming de experts em MoE, Expert streaming, Expert offloading, MoE expert offloading, Offload de experts]
status: draft
created: 2026-10-19
updated: 2026-10-25
tags: [inferencia, moe, modelos, memoria, disco, offload, runtime, hardware]
---

# Streaming de experts em MoE

> Técnica de inferência que mantém residente a parte densa de um modelo mixture-of-experts e lê do disco (ou de uma camada inferior de memória) apenas os experts roteados para cada token, permitindo executar modelos muito maiores do que a RAM ou a VRAM disponíveis.

## Definição

Um modelo MoE ativa uma fração pequena dos parâmetros por token: roteadores escolhem alguns experts por camada, e o restante não participa daquele passo. O GLM-5.2 citado pelo colibri tem 744 bilhões de parâmetros, usa cerca de 40 bilhões por token e apenas ~11 GB de pesos de experts mudam de um token para o outro — aproximadamente 5,4% dos parâmetros ativos.

Streaming de experts explora essa esparsidade para separar **capacidade** de **residência**. Em vez de exigir que o modelo inteiro caiba na memória mais rápida, distribui os pesos em tiers — VRAM, RAM e disco — e move para a memória apenas o que o roteador pede. O modelo continua sendo o mesmo; o que muda é onde cada peso espera.

A diferença em relação a quantization ou destilação é importante: streaming **não altera os pesos nem as decisões do roteador**. Ele troca memória por latência. Essa é a distinção que o colibri formaliza como "placement só decide velocidade".

## Como funciona

O pipeline observado no colibri é descrito em cinco passos por camada:

```text
route  -> o roteador escolhe os experts do token
union  -> agrupa os experts de várias posições para ler cada um uma vez
place  -> decide o tier de cada expert: VRAM, RAM ou disco
overlap -> carrega experts ausentes enquanto os residentes computam
learn  -> registra o roteamento e ajusta o conjunto quente
```

| Componente | Papel |
|---|---|
| **Parte densa** | Atenção, shared experts e embeddings ficam residentes |
| **Experts roteados** | Permanecem no disco e são lidos sob demanda |
| **Cache** | LRU por camada; um conjunto quente pode ser fixado a partir do histórico de uso |
| **Prefetch** | Lookahead do próximo roteamento ou pool de loaders sobrepõe I/O e computação |
| **Tier de GPU** | Experts quentes e camadas densas podem ir para VRAM (Vulkan, CUDA, Metal) |
| **Múltiplos discos** | Espelhar ou distribuir o modelo entre drives aumenta a banda agregada |

O gargalo deixa de ser FLOPS e passa a ser **banda de disco e latência de leitura**. Por isso o README do colibri recomenda NVMe, mede o ganho de dois drives independentes (+37,5% de decode) e discute leitura direta (`O_DIRECT`), que pode ajudar em alguns drives e prejudicar em outros.

Há uma camada de aprendizado: o cache observa o roteamento real da máquina e promove experts recorrentes. É a analogia do "JIT para pesos" — o sistema compila um perfil de residência a partir do uso. O risco é overfitting ao prompt ou à carga de trabalho recente; o próprio README lista A/Bs com dados held-out como experimento ainda necessário.

## Onde aparece

- [JustVugg/colibri](../repos/github.com/justvugg/colibri.md) — implementação em C puro, 13 engines, tiers VRAM/RAM/disco, cache aprendido (`.coli_usage`), prefetch por lookahead do roteador, múltiplos discos e dashboard que mostra cada expert disparando.
- [Drumih/turbo-fieldfare](../repos/github.com/drumih/turbo-fieldfare.md) — implementação model-specific (Gemma 4 26B-A4B) em Swift + Metal para Apple Silicon: core denso residente, cache LFU de 16 slots por camada, `pread` paralelo limitado para misses, overlap de I/O e Metal compute, chunked prefill (128 tokens), servidor OpenAI-compatible em loopback. Distingue-se do colibri por ser nativo para macOS/Metal em vez de multiplataforma, por ser model-specific em vez de genérico, e por documentar 103 experimentos medidos.
- **Referências citadas pelo projeto** (não documentadas na wiki): kTransformers, llama.cpp e vLLM aparecem como trabalhos de offload e comparabilidade; REAP, EASY-EP, SERE, ReMoE, MC-SMoE, MoBE, D²-MoE, HybriMoE, ScMoE e OD-MoE são citados como pesquisa sobre importância, compressão, roteamento e carregamento sob demanda de experts.

## Trade-offs

- **Vantagens:** permite rodar modelos de centenas de bilhões a trilhões de parâmetros em hardware modesto; preserva os pesos e a semântica do roteador; escala de laptop a rack conforme os tiers; o perfil de residência pode melhorar com o uso.
- **Limitações:** o throughput é limitado pela banda e latência do disco; o primeiro token e os primeiros turnos tendem a ser lentos; SSDs rápidos e muita capacidade de armazenamento são pré-requisitos práticos; o cache aprendido pode não generalizar entre cargas; a complexidade do runtime cresce (cache, prefetch, múltiplos backends, concorrência); modelos densos não se beneficiam.
- **Custo escondido:** o download e o armazenamento passam a ser o principal custo de entrada — dezenas de GB a mais de 1 TB por modelo.
- **Não é compressão:** não reduz a qualidade por si só; se a quantização acompanha o container, essa é uma decisão separada.

## Relações

- **Relacionado a:** [Grafo de conhecimento de código](grafo-de-conhecimento-de-codigo.md) — outro caso de mover trabalho do caminho quente para uma representação persistente; [Model Context Protocol (MCP)](model-context-protocol.md) — o colibri expõe um servidor MCP para controlar o runtime.
- **Contrasta com:** servir o modelo inteiro em VRAM; modelos densos menores; APIs hospedadas que escondem o custo de hardware.
- **Depende de:** esparsidade real do MoE, roteador previsível o suficiente para prefetch, armazenamento rápido e um container de pesos que permita leitura por expert.

## Perguntas abertas

- Qual é o break-even de banda de disco para diferentes taxas de acerto de cache e profundidades de prefetch?
- O conjunto quente aprendido generaliza entre sessões, domínios e idiomas, ou memoriza o prompt?
- Como streaming se compara a quantization agressiva e a destilação para o mesmo orçamento de hardware?
- Qual é o impacto em consumo de energia e desgaste do SSD em execuções longas?
- Modelos com roteamento mais uniforme ou com shared experts maiores se beneficiam menos?
- É possível obter garantias de latência (SLO) quando o pior caso depende de I/O aleatório?

## Fontes

- [JustVugg/colibri](../repos/github.com/justvugg/colibri.md) — README no commit `e0db083cdc9e563e0766cc6fc661ef23c32298e0` (consultado em 2026-10-19). Somente o README foi lido.
- [Drumih/turbo-fieldfare](../repos/github.com/drumih/turbo-fieldfare.md) — README no commit `2e9ea50e8c35a65d9170e3bff9d1063be8931ec0` (consultado em 2026-10-25). Somente o README foi lido.
