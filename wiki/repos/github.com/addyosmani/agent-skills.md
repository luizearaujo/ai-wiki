---
type: repo
url: https://github.com/addyosmani/agent-skills
host: github.com
owner: addyosmani
repo: agent-skills
commit: aeac41d4d005999432bb7312f7ff06383a91d59d
license: MIT
language: JavaScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, skills, engenharia-de-software, qualidade, testes, revisao-de-codigo, ciclo-de-vida, claude-code]
---

# addyosmani/agent-skills

> Pacote de 25 skills que codifica o ciclo de vida de engenharia de produção — especificar, planejar, construir, verificar, revisar e lançar — como workflows com gates de verificação para agentes de código.

## O que é

O README posiciona o projeto como a resposta a um comportamento padrão de agentes de código: escolher o caminho mais curto e pular especificação, testes e revisão. As skills empacotam o julgamento de engenharia que separa software de produção de protótipo — quando escrever uma spec, o que testar, como revisar e quando lançar.

O pacote é composto por **24 skills de ciclo de vida** mais uma meta-skill (`using-agent-skills`), organizadas em seis fases: **Define, Plan, Build, Verify, Review, Ship**. O conteúdo é Markdown portátil (`SKILL.md`), com adaptadores nativos para vários hosts.

## Como funciona

### Nove comandos de ciclo de vida

| Fase | Comando | Princípio declarado |
|---|---|---|
| Definir | `/spec` | Spec antes do código |
| Planejar | `/plan` | Tarefas pequenas e atômicas |
| Construir | `/build` | Uma fatia por vez |
| Provar | `/test` | Testes são a prova |
| Fixar a barra | `/constraints` | Decidir uma vez, impor em todo lugar |
| Revisar | `/review` | Melhorar a saúde do código |
| Auditar performance web | `/webperf` | Medir antes de otimizar |
| Simplificar | `/code-simplify` | Clareza acima de esperteza |
| Lançar | `/ship` | Mais rápido é mais seguro |

`/build auto` gera o plano e executa todas as tarefas em uma passada aprovada, mas mantém verificação por tarefa, commits individuais e pausa em falhas ou passos de risco. As skills também podem ser acionadas automaticamente pelo tipo de trabalho (por exemplo, desenho de API ativa `api-and-interface-design`).

### Anatomia das skills

Toda skill segue a mesma estrutura:

- **Frontmatter** com `name` e `description` (incluindo condições de uso).
- **Overview**, **When to Use**, **Process** com passos e critérios de saída.
- **Rationalizations** — tabela de desculpas comuns de agentes ("depois eu adiciono testes") e contra-argumentos.
- **Red Flags** e **Verification** — exigência de evidência: testes passando, saída de build, dados de runtime.

O README chama isso de *process, not prose*: skills são workflows a seguir, não documentação de referência. O carregamento é progressivo — o `SKILL.md` é a porta de entrada e referências compartilhadas entram só quando necessárias.

### Cobertura das 25 skills

| Fase | Skills |
|---|---|
| Meta | `using-agent-skills` — mapeia o trabalho para a skill certa e define regras operacionais. |
| Define | `interview-me`, `idea-refine`, `spec-driven-development`, `constraint-driven-development`. |
| Plan | `planning-and-task-breakdown`. |
| Build | `incremental-implementation`, `test-driven-development`, `context-engineering`, `source-driven-development`, `doubt-driven-development`, `frontend-ui-engineering`, `api-and-interface-design`. |
| Verify | `browser-testing-with-devtools`, `debugging-and-error-recovery`. |
| Review | `code-review-and-quality`, `code-simplification`, `security-and-hardening`, `performance-optimization`. |
| Ship | `git-workflow-and-versioning`, `ci-cd-and-automation`, `deprecation-and-migration`, `documentation-and-adrs`, `observability-and-instrumentation`, `shipping-and-launch`. |

Destacam-se `constraint-driven-development`, que entrevista o usuário para fixar uma barra de qualidade em `CONSTRAINTS.md` e detecta agentes que silenciam checagens; `doubt-driven-development`, com revisão adversarial em contexto novo (CLAIM → EXTRACT → DOUBT → RECONCILE → STOP); e `code-simplification`, que aplica Chesterton's Fence e a Rule of 500 preservando comportamento.

### Pessoas e checklists

O repositório inclui quatro personas de agente (`code-reviewer`, `test-engineer`, `security-auditor`, `web-performance-auditor`) e sete checklists de referência (definition of done, testes, segurança, performance, acessibilidade, observabilidade e padrões de orquestração). O README declara a regra "personas não invocam personas".

O conteúdo incorpora práticas de engenharia do Google: Hyrum's Law, Beyonce Rule, pirâmide de testes, trunk-based development, Shift Left, feature flags e deprecação tratada como passivo.

## Instalação e uso rápido

O caminho universal é o skills CLI da Vercel, que instala em mais de 70 agentes:

```bash
npx skills add addyosmani/agent-skills
npx skills add addyosmani/agent-skills --list
npx skills add addyosmani/agent-skills --skill test-driven-development
```

Há integrações nativas para Claude Code (marketplace `/plugin`), Cursor, Antigravity CLI, Gemini CLI, Windsurf, OpenCode, GitHub Copilot, Kiro, Codex, Command Code e outros. Cada host tem um guia em `docs/`.

O README alerta para uma limitação de portabilidade: instalar uma skill isolada copia apenas `skills/<name>/` e não o diretório `references/` do repositório, deixando checklists compartilhados indisponíveis (issue #361).

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais além do que ele publica:

- **Projeto novo:** `/spec` → `/plan` → `/build` → `/test` → `/review` → `/ship`, com `/constraints` para fixar a barra de qualidade.
- **Spec já existente:** `/build auto` aprova o plano uma vez e executa as tarefas com teste e commit por unidade.
- **Antes do merge:** invocar `code-review-and-quality` para revisão em cinco eixos, com tamanho-alvo de ~100 linhas por mudança.
- **Bug em produção:** `debugging-and-error-recovery` com triagem em cinco passos e regra stop-the-line.
- **Decisão de alto risco:** `doubt-driven-development` para revisão adversarial em contexto novo antes de seguir.
- **Otimização:** `/webperf` para auditoria de Core Web Vitals com modos Quick/Deep.

## Quando usar (e quando não usar)

- **Use quando:** o time quer impor disciplina de engenharia de produção a agentes de código e trabalha com um host compatível com skills Markdown.
- **Use quando:** o objetivo é um ciclo completo e opinionado, com gates de verificação e resistência a atalhos.
- **Evite quando:** o trabalho é exploratório e a cerimônia de spec/teste/revisão custa mais que o resultado; ou quando o host não aceita `SKILL.md` nem plugins.
- **Comparações declaradas:** o README remete a uma comparação com [Superpowers](https://github.com/obra/superpowers) e [mattpocock/skills](../mattpocock/skills.md), incluindo um experimento controlado.

## Limitações e cuidados

- **Somente o README foi lido.** O conteúdo interno das 25 skills, a qualidade dos gates e a eficácia dos anti-rationalization tables não foram verificados.
- **Instalação parcial:** skills isoladas perdem o diretório `references/` compartilhado; o próprio README rastreia a lacuna na issue #361.
- **Adaptadores variam:** comandos de ciclo de vida são nativos no Claude Code; em Copilot, por exemplo, é preciso invocar as skills pelo nome. O README remete a guias por host.
- **Antigravity CLI:** o README relata que, em algumas releases, wrappers de comando legados não são descobertos e recomenda invocar as skills namespaced diretamente.
- **Custo de contexto:** são 25 skills e checklists; o README afirma carregamento progressivo, mas o impacto real por sessão **A verificar**.
- **Sem runtime:** o pacote é instrução em Markdown; não há enforcement automático. O agente pode ignorar uma skill ou um gate.

## Estado e adoção

- **Skills:** 25 (24 de ciclo de vida + `using-agent-skills`); 4 personas; 7 checklists.
- **Atividade e popularidade observadas em 2026-10-19:** 108.513 estrelas, 11.309 forks, 144 issues abertas; repositório criado em 2026-02-15, último push em 2026-10-13.
- **Licença:** MIT.
- **Linguagem principal (API):** JavaScript.
- **Documentação:** [skills.addy.ie](https://skills.addy.ie) e guias em `docs/`.
- **Equipe declarada:** Addy Osmani (criador), Federico Bartoli e Joan León (colaboradores).

## Relações

- **Mantido por:** [addyosmani](../../../entities/addyosmani.md).
- **Conceitos:** [Agent skills](../../../concepts/agent-skills.md) — o pacote é um catálogo de skills de ciclo de vida; [TDD para agentes](../../../concepts/tdd-para-agentes.md) — `test-driven-development` impõe red-green-refactor; [Contratos tipados de serviço](../../../concepts/contratos-tipados-de-servico.md) — `api-and-interface-design` parte de contrato; [Saída completa de agente](../../../concepts/saida-completa-de-agente.md) — os gates de verificação exigem evidência, não "parece certo"; [Design system com agentes](../../../concepts/design-system-com-agentes.md) — `frontend-ui-engineering` cobre componentes e design systems.
- **Alternativas:** [mattpocock/skills](../mattpocock/skills.md) — skills menores e diretas, comparadas no próprio README; [Superpowers](https://github.com/obra/superpowers) — também citado na comparação.

## Perguntas abertas

- As skills realmente reduzem atalhos em sessões longas, ou o agente as contorna quando o contexto aperta?
- Como os gates de verificação se comportam quando o host não tem slash commands nem hooks?
- Qual é o custo de contexto de instalar as 25 skills de uma vez?
- A comparação com Superpowers e Matt Pocock mede qualidade, velocidade ou apenas preferência de fluxo?
- Como as skills evoluem quando as práticas de engenharia do Google mudam?

## Fontes

- README: https://github.com/addyosmani/agent-skills/blob/main/README.md (commit `aeac41d4d005999432bb7312f7ff06383a91d59d`, consultado em 2026-10-19). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do repositório via API do GitHub (consultados em 2026-10-19).
