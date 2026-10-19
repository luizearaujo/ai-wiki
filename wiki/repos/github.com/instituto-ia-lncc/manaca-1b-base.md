---
type: repo
url: https://github.com/Instituto-IA-LNCC/manaca-1b-base
host: github.com
owner: instituto-ia-lncc
repo: manaca-1b-base
commit: 408cba1fb765cdc496df2a518fe32f192270e5ee
license: CC-BY-4.0
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [llm, portugues, pre-treinamento, reprodutibilidade, megatron, modelos-abertos, lncc]
---

# Instituto-IA-LNCC/manaca-1b-base

> Modelo de linguagem decoder-only de ~1,72B de parâmetros treinado do zero para o português do Brasil, com pipeline containerizado que promete reproduzir pré-treino, conversão e avaliação.

## O que é

O Manacá-1B é um **modelo base** — não ajustado para instrução — treinado do zero para o português do Brasil. O repositório não entrega apenas os pesos: reúne o ambiente Docker, o pipeline de corpus, o treino do tokenizador, o pré-treino em Megatron-LM, a conversão para HuggingFace e a suíte de avaliação com testes pareados de significância. O objetivo declarado é permitir que um leitor do artigo reproduza o pré-treino e a avaliação.

O projeto é uma cooperação entre o **LNCC** (Laboratório Nacional de Computação Científica, Brasil) e o **NII/LLM-jp** (National Institute of Informatics, Japão) e deriva da linhagem LLM-jp. Os pesos estão publicados no Hugging Face como `AIInstituteLNCC/manaca-1b-base`; há um preprint na arXiv (`2608.30114`).

## Como funciona

### Arquitetura

| Item | Valor |
|---|---|
| Parâmetros | 1.722.951.680 (~1,72B) |
| Camadas / dim / FFN | 24 / 2048 / 8192 (SwiGLU) |
| Cabeças / grupos KV / head dim | 32 / 8 (GQA) / 64 |
| Posição / norma / bias | RoPE (θ=500000) / RMSNorm / bias em todas as lineares |
| Contexto / precisão | 4096 / bfloat16 |
| Tokenizador | SentencePiece unigram, 64k (padded 64.128), `nmt_nfkc_cf` |
| Framework | Megatron-LM (fork LLM-jp), otimizador distribuído |
| Passos / batch global / tokens | 20.000 / 512 / ~41,9B (~24 tok/parâmetro) |
| Referência de arquitetura | LLM-jp-3.1-1.8B |

A conversão Megatron → HuggingFace preserva os biases e desempacota QKV/GQA e SwiGLU, segundo o README.

### Corpus

O corpus foi dimensionado ao modelo: o ponto de Chinchilla para ~1,72B seria da ordem de ~34B tokens, e o projeto usa ~20,1B tokens únicos com ~2 épocas (~41,9B tokens de atualização). O README cita Muennighoff et al. (2023) para justificar repetição de até ~4 épocas.

| Fonte | Domínio | Tokens | Licença declarada |
|---|---|---:|---|
| GigaVerbo (TucanoBR), subamostra | Web geral PT-BR | ~14,7B (73,1%) | Apache-2.0 |
| Ulysses Tesemõ (USP) | Jurídico / legislativo | ~4,8B (23,9%) | Domínio público |
| Wikipedia-pt (2023-11) | Enciclopédico | ~0,6B (3,1%) | CC BY-SA 4.0 |
| **Total** | 33,7M documentos | **~20,1B** | aberta |

### Treino e hardware

O README relata uma corrida estável: 0 iterações puladas e 0 NaN, loss de treino de 11,41 para 2,48 e loss de validação de 2,07 nats (perplexidade 7,96), ainda em queda ao final. O pré-treino foi validado ponta a ponta em **2 GPUs de 24 GB (NVIDIA Ampere, sem NVLink)**, com bf16 e FlashAttention — uma alegação de hardware acessível, não de supercomputador.

### Avaliação

Quatro benchmarks em português, todos sob o mesmo harness: CALAME-PT por geração da última palavra; ARC-Challenge-PT (25-shot), HellaSwag-PT (10-shot) e LAMBADA-PT (0-shot) por log-verossimilhança. O Manacá usa o tokenizador do próprio treino.

| Modelo | Params (B) | CALAME-PT | ARC-Ch-PT | HellaSwag-PT | LAMBADA-PT |
|---|---:|---:|---:|---:|---:|
| Tucano-1b1 | 1,10 | 59,08 | 29,66 | **44,23** | 31,50 |
| GlórIA-1b3 | 1,30 | 60,39 | 24,44 | 25,83 | 35,30 |
| mGPT-1b3 | 1,30 | 55,57 | 23,93 | 25,42 | 37,38 |
| **Manacá-1B** | 1,72 | **60,63** | 27,18 | 41,61 | **45,31** |
| Tucano-2b4 | 2,40 | 59,57 | 30,85 | 48,63 | 34,35 |
| Sabiá-7B | 7,00 | **63,23** | **46,67** | **64,55** | **63,67** |

A leitura do próprio README: melhor modelo abaixo de 7B em LAMBADA-PT, empate no CALAME-PT com os melhores de 1–2B, e ARC-Challenge-PT próximo do acaso, como outros modelos base nessa escala. O README menciona testes pareados (McNemar) e um relatório com 10 modelos.

## Instalação e uso rápido

Pré-requisitos: Docker Engine 24+, Docker Compose v2 e, para as fases de GPU, NVIDIA Container Toolkit.

```bash
git clone https://github.com/brunoleomenezes/manaca-1b-base.git
cd manaca-1b-base
cp .env.example .env            # DATA_DIR, HF_TOKEN, ...

make build-corpus && make verify
make gigaverbo && make wikipedia && make ulysses-gdrive && make validate
make tokenizer
make build-train && make preprocess-megatron && make pretrain
make build-eval
./scripts/eval/run_lm_eval_pt.sh
./scripts/eval/run_eval.sh
```

**Atenção:** o comando de clone publicado no README aponta para `brunoleomenezes/manaca-1b-base`, não para a organização `Instituto-IA-LNCC` onde o repositório está hoje. O redirecionamento do GitHub pode funcionar, mas o caminho canônico é o desta página. É o mesmo padrão de link de instalação defasado já observado em outros repositórios da wiki.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Reproduzir a avaliação:** montar as imagens de avaliação e rodar os dois scripts, comparando os números com a tabela publicada.
- **Reproduzir o corpus:** baixar e validar as três fontes com os alvos do Makefile.
- **Usar os pesos:** carregar `AIInstituteLNCC/manaca-1b-base` como modelo base para fine-tune ou avaliação própria; o repositório não inclui instruções de inferência nem chat.

## Quando usar (e quando não usar)

- **Use quando:** você precisa de um LLM base aberto para português do Brasil, com pipeline de pré-treino documentado e avaliação em benchmarks PT-BR.
- **Use quando:** o objetivo é estudar reprodutibilidade, corpus, tokenizador ou treino em hardware modesto.
- **Evite quando:** você precisa de um assistente instruído ou de chat — este é um modelo base, e o ajuste de instrução está listado como trabalho futuro.
- **Evite quando:** a decisão depende de benchmark independente; os resultados são publicados pelo próprio projeto.
- **Alternativas:** [OpenBMB/MiniCPM](../openbmb/minicpm.md) para modelos compactos e multilíngues com pipeline aberto; modelos PT-BR como Tucano, GlórIA e Sabiá citados na própria comparação.

## Limitações e cuidados

- **Somente o README foi lido.** `paper/`, `docs/`, `corpus/`, `models/`, `scripts/` e os pesos no Hugging Face não foram consultados; arquitetura, corpus, dinâmica de treino e números são afirmações do README e do preprint.
- **Benchmarks são do projeto.** O harness é declarado comum a todos os modelos e há testes pareados, mas a medição foi desenhada pelos autores e não foi reproduzida por esta wiki.
- **Licença divergente:** o README e o badge declaram **CC BY 4.0**, mas a API do GitHub reporta `NOASSERTION` (licença não reconhecida). O arquivo `LICENSE` existe; seu texto não foi lido.
- **Licença dos pesos não é declarada no README.** A licença do repositório não necessariamente descreve o checkpoint publicado no Hugging Face; verificar antes de uso comercial.
- **Link de clone defasado:** o comando aponta para o perfil pessoal do autor, não para a organização.
- **Alegação de hardware não verificada:** treinar um 1,72B em 2×24 GB com bf16 é plausível com paralelismo e offload, mas o README não detalha a configuração exata nem publica tempos por passo.
- **Modelo base, não alinhado:** não deve ser usado como assistente sem ajuste e avaliação adicionais.
- **Corpus e licenças upstream:** o README declara todas as fontes abertas, mas os termos de cada corpus (GigaVerbo, Ulysses Tesemõ, Wikipedia) não foram verificados individualmente.

## Estado e adoção

- **Atividade e popularidade observadas em 2026-10-19:** 249 estrelas, 16 forks, 2 issues abertas; repositório criado em 2026-08-31, último push em 2026-09-23.
- **Licença:** CC BY 4.0 declarada no README; API do GitHub sem licença reconhecida.
- **Linguagem principal (API):** Python.
- **Branch padrão:** `main`.
- **Estágio:** modelo base publicado, com ajuste de instrução e benchmarks do Open Portuguese LLM Leaderboard listados como trabalho futuro.

## Relações

- **Mantido por:** [Instituto de IA do LNCC](../../../entities/instituto-ia-lncc.md).
- **Cooperação:** NII/LLM-jp (Japão); a arquitetura de referência é o LLM-jp-3.1-1.8B.
- **Conceitos:** [Evidência e proveniência](../../../concepts/evidencia-e-proveniencia.md) — o projeto registra commit, hiperparâmetros e versões por corrida e usa testes pareados para sustentar a comparação.
- **Relacionado a:** [OpenBMB/MiniCPM](../openbmb/minicpm.md) — outra família aberta com pipeline e pesos publicados, mas voltada a modelos compactos e multilíngues; [llms compactos on-device](../../../concepts/llms-compactos-on-device.md) contrasta com a escala de 1,72B treinada para servidor.
- **Alternativas:** Tucano, GlórIA, mGPT, Sabiá (citados no próprio benchmark) e outros LLMs abertos para português.

## Perguntas abertas

- Os pesos no Hugging Face têm licença própria? Qual?
- O pipeline foi reproduzido por terceiros fora do LNCC?
- Qual é a configuração exata de paralelismo que permitiu treinar 1,72B em 2×24 GB?
- Como o tokenizador próprio afeta a comparabilidade com os demais modelos nos quatro benchmarks?
- Os números se mantêm com o harness e as versões atuais das bibliotecas?
- Quais são os 10 modelos do relatório de avaliação e por que a tabela do README mostra seis?
- O pré-treino em ~2 épocas sobre 20,1B tokens únicos é suficiente para generalização, ou o modelo está subtreinado em relação ao ponto de Chinchilla?

## Fontes

- README: https://github.com/Instituto-IA-LNCC/manaca-1b-base/blob/main/README.md (commit `408cba1fb765cdc496df2a518fe32f192270e5ee`, consultado em 2026-10-19). Somente o README foi lido; `paper/`, `docs/`, `corpus/`, `models/`, `scripts/` e os pesos não foram consultados.
- Metadados do repositório e da organização via API do GitHub (consultados em 2026-10-19).
- Preprint citado pelo README: https://arxiv.org/abs/2608.30114 (não lido).
