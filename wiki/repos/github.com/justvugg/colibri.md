---
type: repo
url: https://github.com/JustVugg/colibri
host: github.com
owner: justvugg
repo: colibri
commit: e0db083cdc9e563e0766cc6fc661ef23c32298e0
license: Apache-2.0
language: C
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [inferencia, moe, modelos, local, cpu, c, streaming, offload, llm, runtime]
---

# JustVugg/colibri

> Motor de inferência em C puro que roda modelos MoE de centenas de bilhões a trilhões de parâmetros em hardware comum, mantendo a parte densa na RAM e lendo os experts roteados do disco sob demanda.

## O que é

Colibri é um runtime de inferência local para modelos **mixture-of-experts** (MoE). A tese publicada no README é que um MoE enorme no disco é pequeno por token: o GLM-5.2 tem 744 bilhões de parâmetros, usa cerca de 40 bilhões por token e apenas ~11 GB desses mudam de um token para o outro — os experts roteados. Em vez de exigir que o modelo inteiro caiba na memória rápida, o colibri **posiciona** o modelo em camadas: parte densa (atenção, shared experts, embeddings) na RAM, experts roteados no disco, e, quando há GPU, os experts mais quentes e as camadas densas na VRAM.

O README declara treze engines: dez para linguagem (GLM-5.2/5.3, GLM-5.3-Flash, Inkling, Kimi K3, DeepSeek V4 Flash, DeepSeek V4.1 Flash, MiMo-V2.6 Flash e Pro, Qwen3.8-Flash-Next, Qwen3.6 — que também roda Qwen3-Coder e o dense Qwen3.8-27B — e OLMoE), uma para imagem (Qwen-Image-2.1) e duas de decisão (Laya e GLiNER2.5-Decide), com Clef reaproveitando o engine do Qwen3.6.

O objetivo declarado é democratizar acesso a modelos de fronteira: rodar em hardware que as pessoas já têm (o projeto começou em um laptop de 12 núcleos e 25 GB de RAM), tornar o funcionamento observável no dashboard e manter o motor pequeno o bastante para ser medido e otimizado por terceiros.

## Como funciona

O README resume cada camada de cada token em cinco passos — **route, union, place, overlap, learn** — e fixa um invariante de projeto: **posicionamento só decide velocidade**. As decisões do roteador e a precisão dos pesos seriam as mesmas se um expert respondesse da VRAM, da RAM ou do disco.

| Componente | Papel |
|---|---|
| **Camada densa** | Atenção, shared experts e embeddings ficam residentes em RAM (ou VRAM) |
| **Experts roteados** | Ficam no disco e são lidos quando o roteador os pede |
| **Cache de experts** | LRU por camada, com um conjunto quente fixado aprendido do uso (`.coli_usage`, atualizado a cada turno) |
| **Prefetch** | Pool de loaders sobrepõe leitura e computação; lookahead do roteador pode prefetchar a próxima camada (71,6% previsível no GLM-5.2) |
| **Tiers de GPU** | Vulkan/CUDA/Metal opcionais: expert tier na VRAM e/ou cadeia densa submetida inteira à GPU |
| **Múltiplos discos** | `COLI_MODEL_MIRROR` lê de uma cópia em outro drive; dois NVMe independentes mediram +37,5% de decode |
| **Planejador** | Detecta RAM, VRAM, disco, CPU e GPUs; recomenda o modelo que cabe e o build mais rápido |

A metáfora que o README usa é a de um **JIT para pesos**: assim como um compilador JIT observa o que roda para compilar os caminhos quentes, o colibri usa o histórico de roteamento para decidir quais experts merecem VRAM, RAM ou disco. O cache aprende com as conversas do usuário e o sistema ficaria mais rápido com o uso — uma promessa que depende de estabilidade do padrão de roteamento.

Os engines são **um arquivo C por família de modelo** (`c/colibri.c`, `c/qwen36.c`, `c/kimi_k3.c` etc.) sobre headers compartilhados. Não há BLAS. Segundo o README, Python aparece apenas no setup, no launcher, nos conversores e no **gateway da API** — ou seja, o caminho servidor HTTP é Python, mesmo que a inferência seja C.

## Instalação e uso rápido

Pré-requisitos declarados: **8 GB de RAM no mínimo** (16 GB ou mais recomendado), **22 GB livres em disco** para o menor modelo e conexão de internet. GPU é opcional.

O caminho de um passo:

```bash
# Linux (Ubuntu/Debian)
sudo apt install git python3 build-essential
git clone https://github.com/JustVugg/colibri
cd colibri
./start-here.sh
```

No Windows, baixar o ZIP e executar `START-HERE.bat`; no macOS, `xcode-select --install`, `brew install libomp git python` e `./start-here.sh`. O setup então:

1. inspeciona RAM, disco, CPU e GPUs;
2. recomenda o modelo mais capaz que cabe;
3. compila o engine para a máquina (ou baixa um prebuilt) e escolhe CUDA, Vulkan ou CPU;
4. baixa o modelo com progresso e retomada;
5. sobe o servidor e abre o dashboard em `http://127.0.0.1:8000/`.

As URLs impressas incluem a base compatível com OpenAI (`/v1`) e com Anthropic. O README aponta `docs/quickstart.md` para o passo a passo completo e `docs/AI_SETUP.md` para um assistente de código executar a instalação — inclusive via servidor MCP (`coli mcp`).

## Exemplos de uso

Exemplos derivados do README:

```bash
./coli chat  --model /nvme/qwen36          # chat no terminal
./coli web   --model /nvme/qwen36          # API + dashboard
./coli serve --model /nvme/qwen36          # API + dashboard, sem navegador
./coli plan  --model /nvme/qwen36          # onde o modelo vai viver: VRAM, RAM, disco
./coli doctor --model /nvme/qwen36         # checagem somente leitura
./coli tune  --model /nvme/qwen36          # mede e salva os ajustes mais rápidos
```

O servidor é compatível com OpenAI (`/v1/chat/completions`, `/v1/completions`, `/v1/models`, streaming, JSON, stop sequences, logprobs) e com Anthropic (`/v1/messages`), aceita tool calling na maioria dos engines e até 16 contextos KV independentes (`--kv-slots`).

O modo **System One** troca geração por decisão:

```bash
curl -s http://127.0.0.1:8000/v1/systemone -H 'Content-Type: application/json' -d '{
  "state": "340 lines, 8 files, no tests. CI is green but nothing covers that path.",
  "questions": {
    "review": {"type": "choice", "instructions": "What should the reviewer do?",
               "criteria": {"merge": null, "request changes": null, "close": null}},
    "risky":  {"type": "noul", "instructions": "Is this change risky?"}}}'
```

A resposta traz a opção escolhida, uma probabilidade para cada opção permitida e uma confiança; nada é gerado, então a saída nunca cai fora da lista. O README declara compatibilidade com a API do Jev (TypeSafe), permitindo trocar apenas a base URL.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é rodar modelos MoE grandes em máquina própria, sem GPU dedicada, aceitando throughput baixo em troca de capacidade; ou quando se quer um servidor local compatível com OpenAI/Anthropic e um dashboard para observar o roteamento.
- **Evite quando:** a aplicação precisa de baixa latência ou alto throughput. As medições publicadas vão de 0,05–0,1 tok/s a frio em um laptop de 25 GB a ~9 tok/s em seis RTX 5090; para cargas interativas, uma API hospedada ou um modelo menor residente em RAM tende a ser mais adequado. Também evite se o disco não for rápido ou se o download de centenas de GB a 1,5 TB não for viável.

## Limitações e cuidados

- **Somente o README foi lido.** Benchmarks, páginas de `docs/`, código e testes não foram consultados; os números são afirmações do projeto, muitos deles enviados pela comunidade.
- **Benchmarks são por máquina e datados.** O README é explícito em alguns pontos: ainda não mediu uma GPU discreta no caminho Vulkan (o primeiro número vem de um usuário) e o caminho sem Resizable BAR não foi medido em hardware real. A velocidade depende de disco, cache, histórico de roteamento e número de experts por camada.
- **Download e armazenamento são o custo real.** O menor checkpoint do catálogo é o OLMoE, com 14 GB (7 GB após conversão para int8); o Qwen3-Coder-30B-A3B ocupa 19 GB e o Qwen3.6-35B-A3B, 23 GB. Os maiores chegam a 1,56 TB (Kimi K3), e o setup exige 22 GB livres para o menor modelo.
- **Licença do repositório ≠ licença dos modelos.** O código é Apache-2.0, mas cada checkpoint mantém a licença dos autores: GLM-5.2 é MIT, enquanto Qwen-Image-2.1 é **apenas para uso não comercial**.
- **“Pure C” não significa ausência de Python.** O README declara que o gateway da API, o setup, o launcher e os conversores são Python; o runtime de inferência é C, mas o caminho servidor usa Python.
- **Precisão e qualidade são verificadas pelo projeto, não por esta página.** O README afirma que o container int4 tem custo medido e que os mirrors int4 por linha mediam ~9 pontos piores, mas não há avaliação independente aqui. A promessa de que “posicionamento só muda a velocidade” é um invariante de projeto, não uma verificação externa.
- **Superfície de segurança.** O README imprime as URLs do servidor em `127.0.0.1`, mas não explicita se o bind é restrito ao loopback (**A verificar**); a chave de API é opcional (`COLI_API_KEY`), e expor o serviço sem autenticação dá a qualquer cliente a capacidade de consumir o modelo e os recursos da máquina. Downloads de checkpoints de terceiros também exigem cuidado com proveniência.
- **Nomes de modelos são os do README.** A página registra os nomes exatamente como publicados; não há verificação independente dos checkpoints citados.

## Estado e adoção

- **Versão citada no README:** `colibri v2.0.0` no exemplo de chat.
- **Atividade e popularidade observadas em 2026-10-19:** ~42,8 mil estrelas, ~4,8 mil forks, 151 issues abertas, criado em 2026-07-01 e último push em 2026-10-19; branch padrão `main`; site em `justvugg.github.io/colibri`.
- **Licença:** Apache-2.0 para o código; Apache 2.0, Copyright 2026 Vincenzo Fornaro.

## Relações

- **Mantido por:** [Vincenzo Fornaro (JustVugg)](../../../entities/vincenzo-fornaro.md).
- **Conceitos:** [Streaming de experts em MoE](../../../concepts/streaming-de-experts-em-moe.md) — o mecanismo central; [CLI agent-first](../../../concepts/cli-agent-first.md) — `coli` expõe comandos com saída e planejamento explícitos; [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md) — `coli mcp` expõe detecção de hardware, recomendação, instalação e controle.
- **Alternativas:** llama.cpp e vLLM (não documentados na wiki) — o README os cita como referências de sistemas de inferência e offload; kTransformers também aparece como trabalho relacionado. Modelos pequenos em RAM (Qwen3.6-35B-A3B, Qwen3-Coder-30B-A3B) dispensam streaming e são alternativas para hardware modesto.
- **Relacionado a:** ecossistema de safetensors (container de pesos), tiktoken (tokenizer reimplementado), transformers (oráculo de paridade em CI).

## Perguntas abertas

- Como o throughput se compara a llama.cpp e vLLM em uma máquina real, com o mesmo modelo e o mesmo int4?
- Quão estável é o cache aprendido entre sessões e cargas de trabalho diferentes? O ganho se mantém fora dos padrões vistos no treino?
- Qual é o custo real de RAM e de latência por contexto no servidor com `--kv-slots` alto?
- A promessa “placement só muda velocidade” se sustenta em avaliações de qualidade além do container int4?
- O que muda em consumo de energia e temperatura em execuções longas com experts lidos do disco?
- Como o servidor se comporta quando exposto na rede: autenticação, limites de taxa e isolamento de contexto são suficientes?
- Os benchmarks de 6x RTX 5090 e de laptops são reprodutíveis em versões futuras do engine?

## Fontes

- README: https://github.com/JustVugg/colibri (commit `e0db083cdc9e563e0766cc6fc661ef23c32298e0`, consultado em 2026-10-19). Somente o README foi lido; `docs/`, código, testes, releases e checkpoints não foram consultados.
- Metadados do repositório e do perfil: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas, branch e site).
