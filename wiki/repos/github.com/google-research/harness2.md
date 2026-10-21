---
type: repo
url: https://github.com/google-research/harness2
host: github.com
owner: google-research
repo: harness2
commit: 1cfe254e8d25b15f37048c3730134686abe60335
license: Apache-2.0
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agent-harness, orquestracao-multiagente, pesquisa-aplicada, benchmarks]
---

# google-research/harness2

> Framework de pesquisa para "harnessing" recursivo de agentes em mundo aberto — refina o harness de execução de uma tarefa (prompt, guardrails, memória, skills, subagentes, scripts, plugins) por contraste comportamental entre execuções, sem feedback de gabarito, e acumula lições entre tarefas em um "harness de melhoria" persistente.

## O que é

Harness² parte de uma definição explícita: um **harness** é o sistema em torno de um modelo que o permite agir como agente (prompts, ferramentas, memória, skills, orquestração); **harnessing** é o processo de otimizar esse sistema. O projeto mantém os pesos do modelo fixos e otimiza só o harness, em dois níveis de recursão:

- **Recursão em nível de tarefa**: um passo contrastivo **Propose–Probe–Compose** — propõe edições ao harness, testa seus efeitos na mesma tarefa (probe) e compõe um harness refinado a partir dos contrastes comportamentais entre execuções, sem precisar de gabarito.
- **Recursão em nível de harnessing**: atualiza um **harness de melhoria** persistente com harnesses adotados e lições apoiadas em evidência, para orientar o refinamento de tarefas futuras.

Acompanha um paper (arXiv:2610.14224, "Harness²: Recursive Agent Harnessing for an Open World") com resultados em três benchmarks profissionais e quatro combinações de modelo/harness: até 11,5 pontos de ganho em WorkBuddy-Bench, 4,5 pontos em JobBench e 11,8 pontos percentuais na taxa de aprovação parcial do LAB, para GLM-5 e Gemini 3.5 Flash sobre seus harnesses de base.

## Como funciona

- **Oito componentes editáveis** do harness, agrupados por papel no runtime: *system prompt*, *guardrails*, *memória* e *skills* constroem o contexto; *tool guidance* e *scripts* definem a interface de ferramentas; *subagentes* orquestram trabalho delegado; *plugins* controlam middleware.
- **Dois modos de escala da recursão em nível de tarefa**: recursão **paralela** (explora K candidatos gerais e K específicos de domínio, compõe K refinamentos a partir da evidência compartilhada) e recursão **sequencial** (carrega o harness refinado e a evidência acumulada por K passos Propose–Probe–Compose sucessivos). Paralela explora mais amplo; sequencial refina mais profundo.
- **Executores plugáveis**: OpenCode (padrão) ou Codex (`--substrate cx`) — ambos runtimes de coding agent.
- **Três benchmarks**: JobBench (trabalho profissional), LAB (trabalho jurídico, precisa de Pandoc e Poppler) e WorkBuddy-Bench (escritório/web/código, precisa de Docker, com subconjuntos `office`/`web`/`code`).
- Resultados ficam em `runs/`, organizados por benchmark e subconjunto, com resumos de tarefa, entregáveis, harnesses adotados, notas de reflexão e resultados de avaliação; repetir o mesmo comando retoma a execução.
- **Acesso à web é irrestrito** durante a execução dos executores, e o Codex roda com o próprio sandbox desativado — o README recomenda configurar restrições de rede antes de avaliar, para não deixar o agente acessar as respostas e critérios de avaliação do benchmark.

## Instalação e uso rápido

```bash
uv venv --python 3.12 .venv
source .venv/bin/activate
uv pip install -e '.[render]'
harness2-demo --output runs/demo --k 2
```

O demo local roda sem credenciais de modelo, com editores determinísticos e execuções Python reais. Para benchmarks com modelo real: Node.js 20+, Google Cloud CLI, e `gcloud auth application-default login` com um projeto Vertex AI configurado em `.env`.

```bash
harness2-setup lab
harness2-check --bench lab
harness2 --bench lab --k 1 --mode parallel --only-domains antitrust-competition --max-tasks 1
harness2-judge --bench lab --k 1 --mode parallel
harness2-report --bench lab --k 1 --mode parallel
```

Requer Linux, Python 3.12 e `uv`.

## Quando usar (e quando não usar)

- **Use quando:** quer estudar ou reproduzir refinamento automático de harness de agente sem gabarito, comparando configurações de modelo/harness em benchmarks profissionais controlados.
- **Evite quando:** precisa de um harness de produção pronto para uso — este é um framework de pesquisa com benchmarks acadêmicos, não um produto; o próprio projeto se declara não suportado oficialmente pelo Google e inelegível para o programa de recompensas de vulnerabilidade de código aberto do Google.

## Limitações e cuidados

- Execuções com modelo real geram custo de API — o README recomenda começar com seleção pequena de tarefas.
- Julgamento e relatório precisam usar exatamente o mesmo benchmark, executor, subconjunto, `--k`, `--mode` e seed da execução de refinamento, ou os números não são comparáveis.
- "Este não é um produto oficialmente suportado pelo Google", segundo o próprio aviso legal do README.
- Licenças de terceiros (`third_party/`), benchmarks e datasets seguem seus próprios termos upstream, distintos da licença Apache 2.0 do projeto.

## Estado e adoção

- 16.789 estrelas, 1.552 forks, 116 issues abertas — observado em 2026-10-21.
- Repositório criado em 2026-10-06, com push mais recente em 2026-10-14 — observado em 2026-10-21. Projeto recente.
- Licença: Apache-2.0.

## Relações

- Mantido por: [Google Research (google-research)](../../../entities/google-research.md)
- Conceitos: [Agent harness](../../../concepts/agent-harness.md) — o projeto trata o harness como objeto de otimização automática, não só como camada instalada manualmente; [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — subagentes como um dos oito componentes editáveis.
- Autores (paper arXiv:2610.14224): Ruiyao Xu, Yanfei Chen, Zhongying CuiZhu, Bhavana Dalvi Mishra, Yifei Ming, Han Yu, Rujun Han, Chen-Yu Lee, Tomas Pfister.

## Perguntas abertas

- Como o harness de melhoria persistente evita acumular lições que se aplicavam só a uma tarefa específica (overfitting de harness)?
- Que parte dos ganhos reportados (até 11,8 pontos) se mantém em tarefas fora dos três benchmarks publicados?

## Fontes

- README: https://raw.githubusercontent.com/google-research/harness2/1cfe254e8d25b15f37048c3730134686abe60335/README.md (commit `1cfe254e8d25b15f37048c3730134686abe60335`, consultado em 2026-10-21). Somente o README foi lido; `docs/`, o código e o paper completo não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/google-research/harness2`), consultada em 2026-10-21.
