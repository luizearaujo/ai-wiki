---
type: concept
aliases: [LLMs on-device, Modelos compactos, Small language models, SLM, On-device AI, Modelos de borda]
status: draft
created: 2026-10-19
updated: 2026-10-24
tags: [llm, on-device, edge, modelos-compactos, quantizacao, inferencia, privacidade, latencia]
---

# LLMs compactos on-device

> Estratégia de executar modelos de linguagem de pequeno porte diretamente no dispositivo do usuário — laptop, celular, placa de borda ou desktop — em vez de depender de uma API hospedada, trocando teto de capacidade por privacidade, latência previsível e custo marginal próximo de zero.

## Definição

Um LLM compacto é um modelo cujo footprint cabe no hardware local e cujo custo de inferência é baixo o bastante para rodar sem GPU dedicada ou sem rede. O termo cobre desde modelos densos de 0,5B a 8B até variantes quantizadas de modelos maiores, e se distingue de **streaming de experts**: em vez de mover pesos de um modelo enorme entre disco e memória, o modelo inteiro já cabe no dispositivo.

A escolha é uma troca explícita:

- **Capacidade** cede para **viabilidade local**. Um modelo de 2B dificilmente iguala um modelo de fronteira em conhecimento amplo; o ganho aparece em tarefas estreitas, latência, offline e controle de dados.
- **Treino** cede para **implantação**. O diferencial competitivo migra do tamanho do checkpoint para a receita de dados, o pós-treino e a integração com runtimes reais.

## Como funciona

O padrão observado em projetos como o MiniCPM combina quatro decisões:

| Camada | Decisão típica | Efeito |
|---|---|---|
| **Arquitetura** | Transformer denso padrão (`LlamaForCausalLM`) em vez de kernels proprietários | Qualquer runtime mainstream carrega o checkpoint; menos atrito de implantação |
| **Dados** | Corpus filtrado e aberto, com estágios de base, mid-training e pós-treino | Capacidade concentrada em código, matemática, tool use e contexto longo |
| **Pós-treino** | SFT seguido de RL e destilação on-policy | Especialistas viram um único checkpoint sem perder as capacidades |
| **Formato** | BF16, GGUF, MLX, GPTQ, int4/int8 | O mesmo modelo cobre CPU, GPU integrada, Apple Silicon e aceleradores de borda |

O ecossistema de execução é parte do conceito: vLLM e SGLang para servidores compatíveis com OpenAI, llama.cpp/Ollama/LM Studio para GGUF local, MLX para Apple Silicon e LiteRT-LM para Android, iOS, desktop e IoT. Um modelo só é realmente "on-device" se houver um caminho de conversão e um runtime para o hardware alvo.

O **raciocínio híbrido** aparece como padrão: o mesmo checkpoint alterna entre resposta rápida e modo de raciocínio profundo por um parâmetro de chat template (`enable_thinking`). Isso evita manter dois modelos para dois perfis de uso.

## Onde aparece

- [OpenBMB/MiniCPM](../repos/github.com/openbmb/minicpm.md) — MiniCPM5-2B com arquitetura padrão e contexto de 131K, o 1B da mesma geração com suporte nativo a contexto longo, modos Think/No Think, formatos GGUF/MLX/GPTQ e cookbooks distribuídos como Agent Skills; a família também inclui gerações de borda com atenção esparsa.
- [JustVugg/colibri](../repos/github.com/justvugg/colibri.md) — contraste deliberado: em vez de reduzir o modelo, mantém um MoE enorme no disco e transmite só os experts roteados. Serve ao mesmo objetivo de rodar localmente, com outra troca (capacidade alta, latência alta).
- [PrismML-Eng/Bonsai-demo](../repos/github.com/prismml-eng/bonsai-demo.md) — variante mais agressiva do mesmo princípio: em vez de treinar um modelo pequeno do zero, comprime um modelo de ~27B (Qwen3.8) para pesos ternários (~1,75 bit/peso), retendo 98,2% do desempenho FP16 segundo o projeto; ternário/1-bit é um ponto bem mais extremo na escala de quantização do que o BF16/GGUF/MLX/GPTQ já documentado via MiniCPM.
- [unslothai/unsloth](../repos/github.com/unslothai/unsloth.md) — em vez de um modelo específico, é a ferramenta (app desktop + biblioteca) para treinar e rodar localmente modelos compactos e de tamanho completo, com exportação para GGUF e outros formatos de borda.
- **Não documentados na wiki:** Phi, Gemma, Qwen small, Llama small e demais famílias compactas são referências do ecossistema, mas não têm página própria.

## Trade-offs

- **Vantagens:** privacidade (dados não saem do dispositivo), operação offline, latência previsível, custo marginal baixo, controle sobre versão e ajuste fino, e possibilidade de trocar de persona ou domínio por LoRA.
- **Limitações:** teto de capacidade menor; qualidade sensível a quantização; memória e bateria ainda são restrições reais; fragmentação de runtimes e formatos; benchmarks publicados tendem a usar conjuntos escolhidos pelo próprio projeto.
- **Custo escondido:** manter um pipeline de conversão (GGUF/MLX/GPTQ), testar em cada backend e acompanhar atualizações de runtime costuma custar mais do que baixar um checkpoint.
- **Não é o mesmo que compressão:** quantização reduz precisão e memória, mas o conceito de modelo compacto é sobre o tamanho e o alvo de implantação; as duas decisões se combinam, não se substituem.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — cookbooks de deploy e fine-tune distribuídos como instruções para agentes de código; [Orquestração multiagente](orquestracao-multiagente.md) — modelos locais baratos viabilizam subagentes e chamadas frequentes; [CLI agent-first](cli-agent-first.md) — runtimes locais expõem CLIs e servidores compatíveis com OpenAI.
- **Contrasta com:** APIs hospedadas de modelos de fronteira; [Streaming de experts em MoE](streaming-de-experts-em-moe.md) — capacidade alta com latência alta e dependência de disco.
- **Depende de:** quantization e formatos de checkpoint, runtimes por plataforma, e uma receita de dados/pós-treino que compense o tamanho reduzido.

## Perguntas abertas

- Qual é a fronteira prática de capacidade por tamanho para tarefas agênticas de múltiplos passos?
- Quanto a quantização int4 custa em qualidade fora dos benchmarks publicados pelos projetos?
- Modelos compactos conseguem manter tool use confiável quando o contexto cresce para dezenas de milhares de tokens?
- Como comparar modelos on-device de forma justa quando cada projeto escolhe seus baselines?
- Qual é o custo total de manter vários formatos (GGUF, MLX, GPTQ) em produção?
- Modelos compactos e streaming de experts convergem ou permanecem estratégias separadas?

## Fontes

- [OpenBMB/MiniCPM](../repos/github.com/openbmb/minicpm.md) — README no commit `316cfb1cea39f39cfa16b4f5703b77495c2340be` (consultado em 2026-10-19); apenas o README foi lido.
- [JustVugg/colibri](../repos/github.com/justvugg/colibri.md) — README no commit `e0db083cdc9e563e0766cc6fc661ef23c32298e0` (consultado em 2026-10-19), usado como contraste.
- [PrismML-Eng/Bonsai-demo](../repos/github.com/prismml-eng/bonsai-demo.md) — README no commit `ee6ee05ae01ed7483178a14d81530c5b4c4fa36f` (consultado em 2026-10-24).
- [unslothai/unsloth](../repos/github.com/unslothai/unsloth.md) — README no commit `0edb8f511efd32654487af5c2f57a921c7dd63ef` (consultado em 2026-10-24).
