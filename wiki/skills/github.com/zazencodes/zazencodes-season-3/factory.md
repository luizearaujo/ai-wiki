---
type: skill
name: Factory
slug: factory
url: https://github.com/zazencodes/zazencodes-season-3/tree/main/src/software-factory-claude-code
source_url: https://github.com/zazencodes/zazencodes-season-3
source_path: src/software-factory-claude-code/.claude/skills/factory
author: zazencodes
version: desconhecida
license: desconhecida
status: active
created: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, orquestracao-multiagente, claude-code, subagentes, git-worktree]
---

# Factory

> Skill do Claude Code que transforma a sessão que a executa na orquestradora de um loop spec → build → revisão em quatro frentes → aprovação, com sete subagentes, cada job isolado em seu próprio git worktree.

## O que é

`factory` é a skill central de uma pequena "fábrica de software" publicada como material de apoio ao vídeo "[Build Your Own AI Software Factory with Claude Code](https://youtu.be/ctoaIC4LHmI)", do canal ZazenCodes, dentro do monorepo [zazencodes/zazencodes-season-3](../../../../repos/github.com/zazencodes/zazencodes-season-3.md) (pasta `src/software-factory-claude-code`). Não vem de um marketplace ou catálogo de skills: é lida diretamente do `SKILL.md` e dos sete arquivos de subagente no repositório, com clone local autorizado explicitamente pelo usuário.

A ideia: o usuário digita `/factory <funcionalidade>` em linguagem natural, e a própria sessão do Claude Code que recebe o comando se torna a orquestradora — ela nunca escreve código, spec, revisão ou decisão por conta própria. Cada subagente escreve exatamente um arquivo; a orquestradora só move o job entre as etapas e mantém `job.json` atualizado.

## Como funciona

```
feature → spec-writer → builder → [security, ux, ui, code] → WAIT FOR ALL
                           ▲                                      │
                           └──── any CHANGES: resume builder ◄────┤
                                                                  ▼ all PASS
                                     merge to main ◄─ APPROVE ─ approver ─ ESCALATE → needs-human
```

| Etapa | Subagente (`subagent_type`) | Model | Tools | Escreve |
|---|---|---|---|---|
| spec | `spec-writer` | opus | Read, Grep, Glob, Bash, Write | `spec.md` |
| build | `builder` | opus | Read, Grep, Glob, Bash, Edit, Write | `build.md` + commits em `factory/<job-id>` |
| review | `reviewer-security` | opus | Read, Grep, Glob, Bash, Write | `round-N/review-security.md` |
| review | `reviewer-ux` | sonnet | Read, Grep, Glob, Bash, Write | `round-N/review-ux.md` |
| review | `reviewer-ui` | sonnet | Read, Grep, Glob, Bash, Write | `round-N/review-ui.md` |
| review | `reviewer-code` | sonnet | Read, Grep, Glob, Bash, Write | `round-N/review-code.md` |
| approve | `approver` | opus | Read, Grep, Glob, Bash, Write | `decision.md` |

Nenhum subagente de revisão ou aprovação tem `Edit`: só o `builder` pode mudar código, e só dentro do worktree do próprio job.

- **Isolamento por worktree**: cada job roda em `git worktree add -b factory/<job-id> <worktree> main`, fora do checkout principal. A orquestradora fica no checkout principal; os subagentes trabalham no worktree. Isso permite várias sessões do Claude Code rodando `/factory` em paralelo no mesmo repositório, cada uma orquestrando só o job que iniciou.
- **Rodada de revisão**: os quatro revisores são despachados em uma única mensagem (paralelo real, não sequencial). A rodada só termina quando os quatro arquivos `review-*.md` existem ("WAIT FOR ALL"); o veredito de cada um (`VERDICT: PASS`/`VERDICT: CHANGES`) é lido e gravado em `job.json` assim que o arquivo aparece, para o dashboard atualizar os chips em tempo real. A orquestradora nunca retoma o builder no meio de uma rodada.
- **Limite de retrabalho**: `MAX_RESUMES = 2` — depois da rodada 1, o builder pode ser retomado no máximo duas vezes, então um job tem no máximo 3 rodadas de revisão antes de escalar para humano.
- **Portas isoladas por job**: com `n` o número do job (`003` → `3`), o builder recebe a porta `5100 + 10n`, `reviewer-ux` recebe `5101 + 10n` e `reviewer-ui` recebe `5102 + 10n` — para que revisores de jobs diferentes nunca inspecionem a página um do outro.
- **`job.json`** é reescrito por completo em cada mudança de estado (`stage`: `spec`, `build`, `review`, `approve`, `merged` ou `needs-human`; `round`; `reviews` da rodada atual), e é a fonte que o dashboard lê.
- **Merge**: só acontece no checkout principal, exige-o limpo e em `main` (`factory/backlog.md` é a única exceção aceita como "sujo"); roda `git merge --no-ff factory/<job-id>`, remove o worktree e a branch. **Nunca faz push.**
- **Checagem visual**: builder e os revisores de UX/UI usam a CLI [`agent-browser`](../../../../repos/github.com/vercel-labs/agent-browser.md) (`agent-browser skills get core` para aprender o uso), sempre com `--session <job-id>-<papel>` para não disputar a mesma sessão de navegador entre jobs.

### Exemplo real de escalação

Um dos dois jobs de exemplo incluídos no repositório (`001-blog-reading-time`, rodado sobre o próprio site zazencodes.com) passou nas quatro revisões, mas o `approver` escalou mesmo assim:

> *"I am escalating only because the branch edits a prerender script (`scripts/prerender-blog.js`), which is on the list of deploy/hosting changes that need a human."*

O `decision.md` desse job detalha cada um dos dez critérios de aceite, cita o commit exato e pede ao humano uma decisão de produto sobre invalidar o cache de prerender — um exemplo concreto de que "todas as revisões passaram" não é o único critério para merge automático.

## Instalação e uso

A pasta `src/software-factory-claude-code` é organizada como a raiz de um repositório, para ser copiada direto:

```
.claude/
  skills/factory/SKILL.md        # este arquivo
  agents/                        # os sete subagentes
factory/
  backlog.md
  dashboard.html
  jobs/                          # estado de runtime, gitignored
```

1. Copiar `.claude/` e `factory/` para a raiz do repositório de destino.
2. Apagar os jobs de exemplo em `factory/jobs/` e os itens já marcados em `factory/backlog.md`.
3. Adicionar `factory/jobs/` ao `.gitignore` — é estado de execução, nunca deve ser commitado.
4. Garantir que o `AGENTS.md` (ou `CLAUDE.md`) do repositório de destino descreva setup de checkout limpo, como iniciar o servidor de dev em uma porta dada, e os comandos de teste, build e lint — nenhum subagente carrega nada específico do projeto; todos leem isso dali.
5. Instalar a CLI [`agent-browser`](../../../../repos/github.com/vercel-labs/agent-browser.md), usada pelo builder e pelos revisores de UX/UI.
6. Commitar tudo em `main` e rodar `/factory <funcionalidade>`.

Comandos da skill:

```
/factory <feature>               roda um novo job pelo loop completo
/factory next                    toma o primeiro item não marcado de factory/backlog.md
/factory approve <job-id>        faz merge de um job em needs-human para main
/factory rework <job-id> <nota>  devolve um job em needs-human ao builder, com feedback
```

Dashboard visual (lê `job.json` de cada pasta, sem servidor dedicado):

```bash
cd factory && python3 -m http.server
# abrir http://localhost:8000/dashboard.html
```

## Exemplos de uso

> Exemplos derivados da descrição publicada e dos dois jobs de exemplo incluídos no repositório — não são instruções oficiais além do que o `SKILL.md` descreve.

- `/factory add reading time to blog posts` — produziu o job `001-blog-reading-time`: passou nas quatro revisões, mas foi escalado por tocar um script de prerender (mudança de deploy).
- `/factory add a 404 page` — produziu o job `002-not-found-page`: passou e foi mergeado em `main` sem intervenção humana.
- `/factory next` — toma o próximo item não marcado da fila em `factory/backlog.md` e roda o loop completo para ele.

## Saídas esperadas

Por job: `spec.md` (critérios de aceite testáveis), `build.md` (resumo, evidência por critério, log por rodada), um `round-N/review-{security,ux,ui,code}.md` por rodada (cada um começando com `VERDICT: PASS` ou `VERDICT: CHANGES`), `decision.md` (começando com `APPROVE` ou `ESCALATE`, com a justificativa) e, no final, ou um merge em `main` com a branch e o worktree removidos, ou um job em `needs-human` com a branch e o worktree preservados para inspeção.

## Quando usar (e quando não usar)

- **Use quando:** quer um ciclo spec → build → revisão em quatro frentes → merge/escalação, dirigido inteiramente por arquivos markdown e subagentes do Claude Code, sem servidor ou banco de estado externo, e está disposto a adaptar os checklists de revisão (deliberadamente genéricos) ao próprio stack.
- **Evite quando:** precisa de aprovação humana obrigatória em toda mudança — o `approver` pode mergear sozinho quando as quatro revisões passam e o merge-tree é limpo —, ou já tem um pipeline de CI/CD com gates equivalentes, já que a fábrica não se integra a ele, apenas opera em paralelo sobre git.

## Limitações e cuidados

- Os sete arquivos de subagente e o `SKILL.md` foram lidos integralmente nesta ingestão (clone local, autorizado explicitamente pelo usuário), mas nenhum job real foi executado por este agente — o exemplo de escalação citado acima vem dos dois jobs já incluídos no repositório, não de uma execução nova.
- `MAX_RESUMES = 2` é um limite rígido no próprio `SKILL.md`; mudar o comportamento do loop exige editar esse arquivo e os arquivos de agente em `.claude/agents/`.
- Depende da CLI `agent-browser` para qualquer critério de aceite verificável visualmente; sem ela, builder e revisores de UX/UI não têm como inspecionar a página.
- Nunca faz push — só merge local. Um pipeline de CI/deploy downstream precisa ser acionado separadamente.
- Sem licença própria declarada; o repositório-pai (`zazencodes/zazencodes-season-3`) também não declara licença.

## Estado e adoção

- Versão: desconhecida — sem changelog próprio além do histórico do repositório `zazencodes/zazencodes-season-3`.
- Preço/licença: desconhecida (ver Limitações).
- Dois jobs de exemplo incluídos (`001-blog-reading-time`, `002-not-found-page`), ambos rodados sobre o site zazencodes.com (Vue + Firebase) durante a gravação do vídeo.

## Relações

- Autor: [zazencodes (Alexander Galea)](../../../../entities/zazencodes.md)
- Repositório-fonte: [zazencodes/zazencodes-season-3](../../../../repos/github.com/zazencodes/zazencodes-season-3.md)
- Conceitos: [Agent skills](../../../../concepts/agent-skills.md), [Orquestração multiagente](../../../../concepts/orquestracao-multiagente.md)
- Depende de: [vercel-labs/agent-browser](../../../../repos/github.com/vercel-labs/agent-browser.md), para checagem visual de critérios de aceite.
- Alternativas (orquestração em etapas sobre Claude Code): [obra/superpowers](../../../../repos/github.com/obra/superpowers.md), [garrytan/gstack](../../../../repos/github.com/garrytan/gstack.md).

## Perguntas abertas

- Como o `SKILL.md` resolve conflito se duas sessões tentam `/factory next` no mesmo item do backlog ao mesmo tempo além da tentativa simples de reclaim por Edit?
- Os checklists de revisão (security, ux, ui, code) têm algum conteúdo padrão além de "deliberadamente genéricos", ou cada reviewer parte de um prompt vazio a ser ajustado pelo usuário?
- Existe algum caso registrado de um job que esgotou as três rodadas de revisão sem todos os vereditos em PASS, além do texto genérico que `SKILL.md` descreve para esse caminho?

## Fontes

- `SKILL.md`: https://raw.githubusercontent.com/zazencodes/zazencodes-season-3/555467c365e6750278efba09349369109f62f65f/src/software-factory-claude-code/.claude/skills/factory/SKILL.md (commit `555467c365e6750278efba09349369109f62f65f`, lido via clone local autorizado, consultado em 2026-10-21).
- Sete arquivos de subagente em `.claude/agents/` (mesmo commit, mesmo clone), consultados em 2026-10-21.
- `factory/jobs/001-blog-reading-time/decision.md` e `002-not-found-page/` (mesmo commit, mesmo clone), consultados em 2026-10-21.
- README de `src/software-factory-claude-code` e README raiz de [zazencodes/zazencodes-season-3](../../../../repos/github.com/zazencodes/zazencodes-season-3.md), já registrados na página do repositório.
