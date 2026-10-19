---
type: skill
name: Skill Creator
slug: skill-creator
url: https://github.com/anthropics/skills/tree/main/skills/skill-creator
source_url: https://github.com/anthropics/skills
source_path: skills/skill-creator
author: anthropics
version: desconhecida
license: Apache-2.0
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [agent-skills, meta-skill, avaliacao]
---

# Skill Creator

> Skill da Anthropic para criar, editar, testar e otimizar outras skills: interview, redação do `SKILL.md`, evals, benchmark e ajuste da descrição que dispara o gatilho.

## O que é

Skill meta do repositório oficial [anthropics/skills](../../../../repos/github.com/anthropics/skills.md): guia o usuário desde a intenção inicial até uma skill testada e com descrição otimizada para disparar no momento certo.

## Como funciona

Workflow descrito no `SKILL.md`:

1. **Capturar intenção:** definir o que a skill deve fazer, quando deve disparar, o formato de saída esperado e se há casos de teste úteis; extrair o workflow da conversa, se já existir.
2. **Entrevistar e pesquisar:** perguntar sobre casos de borda, formatos e critérios de sucesso antes de escrever qualquer coisa; opcionalmente pesquisar skills ou documentação similares.
3. **Escrever o `SKILL.md`:** preencher nome, uma descrição deliberadamente "insistente" (já que o Claude tende a sub-disparar skills) e as instruções, priorizando explicar o raciocínio em vez de regras rígidas em caixa alta; manter o arquivo com menos de 500 linhas.
4. **Testar:** salvar 2–3 prompts realistas em `evals/evals.json`; rodar cada um com e sem a skill (ou contra a versão anterior, ao melhorar uma skill existente), organizados em `<skill-name>-workspace/iteration-N/`.
5. **Avaliar:** pontuar as execuções contra assertions, agregar em um benchmark, analisar padrões (assertions que não discriminam, evals instáveis, trade-off de tempo/tokens) e abrir um visualizador de revisão para o usuário.
6. **Melhorar e repetir:** ler feedback do usuário, generalizar a partir de reclamações específicas, agrupar código auxiliar repetido em `scripts/` e repetir até satisfação.
7. **Otimizar a descrição:** gerar ~20 queries realistas que deveriam e não deveriam disparar a skill, revisar com o usuário, e rodar um loop de otimização automatizado que escolhe a melhor descrição por pontuação em teste hold-out.
8. **Empacotar:** se houver ferramental de apresentação de arquivos disponível, empacotar o resultado como arquivo `.skill`.

Variações por ambiente: Claude.ai e Cowork têm workflows ajustados — Claude.ai roda testes sequencialmente, sem subagentes nem navegador; Cowork usa saída HTML estática em vez de servidor ao vivo.

Scripts e recursos citados: `scripts/aggregate_benchmark.py` (gera `benchmark.json`/`benchmark.md`), `scripts/run_loop.py` e `scripts/run_eval.py` (otimização de descrição), `scripts/package_skill.py` (empacotamento), `eval-viewer/generate_review.py` e `assets/eval_review.html` (visualizador de revisão), `agents/grader.md`, `agents/comparator.md`, `agents/analyzer.md` (subagentes de avaliação, comparação cega e análise), `references/schemas.md` (estruturas JSON de evals, grading e benchmarks).

## Instalação e uso

Via marketplace de plugins do Claude Code:
```
/plugin marketplace add anthropics/skills
/plugin install example-skills@anthropic-agent-skills
```
ou em Claude.ai/Claude API conforme descrito na página do repositório [anthropics/skills](../../../../repos/github.com/anthropics/skills.md).

## Exemplos de uso

> Exemplos derivados da descrição publicada, não são instruções oficiais da skill.

- Pedir para criar uma nova skill a partir de um workflow repetido manualmente em várias conversas, deixando o skill-creator conduzir a entrevista e gerar o `SKILL.md`.
- Pedir para melhorar uma skill existente após reclamações específicas de usuários, usando o loop de iteração em `<skill-name>-workspace/`.

## Saídas esperadas

Um `SKILL.md` testado, com descrição otimizada por avaliação hold-out, evals salvos em `evals/evals.json`, um benchmark agregado (`benchmark.json`/`benchmark.md`) e, quando aplicável, um arquivo `.skill` empacotado.

## Quando usar (e quando não usar)

- **Use quando:** quiser formalizar uma skill nova ou medir e melhorar o disparo/qualidade de uma skill existente com evidência (evals, benchmark), não só por inspeção manual.
- **Evite quando:** a necessidade for uma instrução pontual de uma única conversa, sem intenção de reutilizar como skill versionável.

## Limitações e cuidados

- Depende de ferramental de subagentes e, em alguns ambientes, de navegador para o visualizador de revisão — ausentes em Claude.ai, que roda testes sequencialmente.
- A qualidade da otimização de descrição depende da amostra de ~20 queries geradas e revisadas; viés nessa amostra se propaga ao resultado.
- `SKILL.md` cru não foi lido diretamente nesta ingestão; resumo vem do conteúdo buscado via URL raw no commit registrado.

## Estado e adoção

- Versão: desconhecida (sem changelog próprio além do histórico do repositório `anthropics/skills`).
- Preço/licença: Apache-2.0 (licença geral do repositório para as skills de exemplo, distinta das skills de documento source-available).

## Relações

- Autor: [Anthropic (anthropics)](../../../../entities/anthropics.md).
- Conceitos: [Agent skills](../../../../concepts/agent-skills.md).
- Alternativas: nenhuma skill equivalente de meta-criação documentada nesta wiki até 2026-10-19.

## Perguntas abertas

- Como o loop de otimização de descrição lida com skills cujo gatilho depende fortemente de contexto de projeto, não só da query?

## Fontes

- Página de origem: https://github.com/anthropics/skills/tree/main/skills/skill-creator (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/anthropics/skills, `SKILL.md` lido em https://raw.githubusercontent.com/anthropics/skills/dbd4588f9e1033efb41dad4bef2f7947c8993d44/skills/skill-creator/SKILL.md (commit `dbd4588f9e1033efb41dad4bef2f7947c8993d44`, consultado em 2026-10-19).
