---
type: repo
url: https://github.com/garrytan/gstack
host: github.com
owner: garrytan
repo: gstack
commit: 6a4ab69dcdfd67377eaee6bc2d19a2c42038b037
license: MIT
language: TypeScript
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [agentes, harness, skills, claude-code, orquestracao, qa, seguranca]
---

# garrytan/gstack

> Configuração de Claude Code de Garry Tan distribuída como 23 especialistas e oito power tools em Markdown — slash commands que organizam o trabalho em um sprint de produto, do questionamento da ideia ao PR e à verificação em produção.

## O que é

O gstack é, nas palavras do README, a resposta de Garry Tan — presidente e CEO da Y Combinator — para a pergunta "como uma pessoa entrega como um time de vinte?". Em vez de um prompt ou de um agente único, ele instala um conjunto de especialistas com papéis de uma empresa de engenharia: CEO/founder, engenheiro-chefe, designer, revisor, QA lead que abre navegador real, security officer e release engineer.

O projeto se apresenta como **processo, não coleção de ferramentas**: as skills rodam na ordem de um sprint — **Think → Plan → Build → Review → Test → Ship → Reflect** — e cada etapa produz artefatos que a seguinte lê. O README fala em 23 especialistas e oito power tools, todos slash commands, todos em Markdown e sob licença MIT.

O público declarado são fundadores e CEOs técnicos que ainda querem construir, usuários iniciantes de Claude Code que preferem papéis estruturados a um prompt em branco, e tech leads que querem revisão, QA e release rigorosos em cada PR.

## Como funciona

O encadeamento é o mecanismo central: `/office-hours` escreve um documento de design; `/plan-ceo-review` questiona escopo; `/plan-eng-review` fixa arquitetura, fluxos e plano de testes; `/qa` consome esse plano; `/review` encontra bugs e `/ship` verifica que foram corrigidos. Nada "cai no chão" porque cada etapa conhece a anterior.

| Etapa | Skills principais | Papel |
|---|---|---|
| Pensar | `/office-hours` | Seis perguntas de forçamento que reformulam o produto antes do código; gera o design doc. |
| Planejar | `/plan-ceo-review`, `/plan-eng-review`, `/plan-design-review`, `/plan-devex-review`, `/autoplan` | Escopo, arquitetura, design e experiência de desenvolvedor; `/autoplan` roda CEO → design → DX → engenharia. |
| Construir | `/design-consultation`, `/design-shotgun`, `/design-html` | Sistema de design, variantes de mockup e HTML de produção com layout calculado. |
| Revisar | `/review`, `/deslop-shared-libs`, `/test-audit`, `/investigate`, `/design-review`, `/devex-review`, `/cso` | Bugs, simplificação, qualidade de testes, causa raiz, design, DX e segurança. |
| Testar | `/qa`, `/qa-only`, `/ios-qa` | Navegador, API, CLI, job, webhook e dispositivo iOS real; regressões nativas quando possível. |
| Entregar | `/ship`, `/land-and-deploy`, `/canary`, `/benchmark`, `/document-release` | Testes, cobertura, documentação, PR, merge, deploy e monitoramento pós-deploy. |
| Refletir | `/retro`, `/learn` | Retrospectiva semanal e memória de padrões do projeto. |

Há também ferramentas de apoio: `/codex` e `/claude-code` pedem revisão independente ao outro provedor; `/careful`, `/freeze` e `/guard` limitam comandos destrutivos e edições; `/browse`, `/scrape` e `/setup-browser-cookies` dão ao agente um navegador real; `/make-pdf` e `/diagram` publicam documentos e diagramas; `/gstack-upgrade` atualiza a instalação.

Além dos slash commands, o README lista binários autônomos para workflows fora de sessão — benchmark entre modelos, auditoria de egresso com hash encadeado, bill-of-materials de tokens, ledger de evidência de testes, fingerprint da árvore de trabalho, envelope de confiança para texto de issues e daemon de QA em iPhone/iPad.

### GBrain

O `/setup-gbrain` conecta o agente a uma base de conhecimento persistente (GBrain), com quatro caminhos: Supabase existente, provisionamento automático de Supabase, PGLite local ou MCP remoto. O `/sync-gbrain` reindexa o código do repositório e escreve um bloco de orientação no `CLAUDE.md` para o agente preferir busca no GBrain a `grep`. Cada repositório recebe um nível de confiança — `read-write`, `read-only` ou `deny`.

### Instalação e uso rápido

Requisitos declarados: Claude Code, Git, Bun **v1.4.2+** (o setup recusa versões anteriores a 1.3.3, que permitiriam a ferramentas compiladas ler o `.env` do projeto) e Node.js apenas no Windows. No macOS, o README recomenda o navegador [Aside](https://aside.com); sem ele, o setup compila um Chromium próprio.

Instalação global, como o README manda colar no Claude Code:

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack \
  && cd ~/.claude/skills/gstack && ./setup
```

O README orienta ainda adicionar uma seção "gstack" ao `CLAUDE.md` para usar `/browse` em vez de ferramentas MCP de navegador. O modo equipe (`./setup --team` mais `gstack-team-init required`) versiona apenas `.claude/` e `CLAUDE.md` e faz auto-update checado no máximo uma vez por hora.

Instalação em outros agentes usa `--host <nome>` ou `--host auto`:

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup --host auto      # ou: ./setup --host codex
./setup --status                         # uma linha por instalação
```

Os hosts têm tiers declarados: **full** (Claude Code, certificado por workflow real), **experimental** (Codex, OpenCode, Cursor, Factory Droid, Kiro, Copilot CLI etc.) e **instruction-only**. O README não promete paridade entre eles.

## Exemplos de uso

O README percorre um caso ponta a ponta: o usuário pede um "app de briefing diário"; `/office-hours` reformula para "chefe de gabinete pessoal", extrai capacidades, desafia premissas e recomenda o menor recorte; `/plan-ceo-review` e `/plan-eng-review` revisam escopo e arquitetura; o agente implementa; `/review` corrige dois problemas automaticamente e pede aprovação em uma condição de corrida; `/qa` abre o navegador e corrige um bug; `/ship` roda testes e abre um PR. O README resume: "oito comandos, de ponta a ponta".

Outro uso documentado é QA sem página web: apontar `/qa` ou `/qa-only` para um CLI, API, job ou webhook com fixture local isolada, exigindo comando exato, resultado esperado, resultado obtido e checagens não testadas.

## Quando usar (e quando não usar)

- **Use quando:** você usa Claude Code (ou outro host suportado) e quer um processo completo de produto com revisão adversarial, QA em navegador real, release e documentação; quando trabalha em vários sprints paralelos e precisa de artefatos e gates por etapa.
- **Evite quando:** quer uma instalação pequena e de baixo contexto; não usa Bun/Claude Code; não quer que o agente abra navegador com suas sessões reais; ou precisa de garantia de paridade entre harnesses. Para um catálogo de agentes/skills mais amplo e multi-harness, compare com [affaan-m/ECC](../affaan-m/ecc.md); para uma orquestração visual de vários CLIs, com [HarnessMD/munder-difflin](../harnessmd/munder-difflin.md).

## Limitações e cuidados

- **Superfície grande e em movimento.** São dezenas de skills, binários, hooks, hosts e integrações. O repositório muda rápido (o README cita versões como v1.91.13.0 e v1.43.0.0 para iOS, sem um cabeçalho único de versão). Apenas o README foi lido; a implementação e os docs não foram verificados.
- **Dependências de ferramenta.** Exige Bun em versão específica, Claude Code e, para `/cso` em modo abrangente, toolchain nativo e flags de build específicas; sem isso o relatório diz "not assessed".
- **Rede e credenciais.** Revisões externas enviam código/diff/plano ao outro provedor usando o login do usuário; o update check consulta o GitHub; o GBrain pode usar Supabase ou servidor remoto; o navegador usa sessões reais. O README documenta consentimentos e recibos de egresso, mas o usuário precisa configurar isso.
- **Telemetria e privacidade.** Telemetria é opt-in e desligada por padrão; o update check é ligado por padrão; cada skill run pode gravar estado local. O README afirma que código, caminhos, repositórios, branches e prompts nunca são enviados na telemetria — isso é uma afirmação do projeto, não uma auditoria.
- **Segurança de conteúdo.** O README descreve defesa em camadas contra prompt injection no navegador (filtros, datamarking, classificador local, combiner) e envelope de confiança para texto de issues; o mecanismo não foi verificado aqui.
- **Alegações de produtividade.** Os números de produtividade e de LOC são do autor e vêm com metodologia própria; trate-os como narrativa do projeto.
- **Custo.** Sprints com múltiplos revisores, QA em navegador e revisões externas consomem tokens e chamadas; o README menciona `/eval-plan` e `gstack-context-bill` justamente para controlar gasto e orçamento de contexto.

## Estado e adoção

- Versões citadas no README: v1.91.13.0 (tempo de setup) e iOS QA v1.43.0.0+; não há um "current release" único no topo.
- Observado em 2026-10-19: ~136.905 stars, ~20.312 forks, ~81 issues abertas; último push em 2026-10-19; criado em 2026-03-11.
- Licença: MIT (API do GitHub e README concordam).
- Linguagem principal na API: TypeScript.

## Relações

- Mantido por: [garrytan](../../../entities/garrytan.md)
- Conceitos: [Agent harness](../../../concepts/agent-harness.md), [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md), [Agent skills](../../../concepts/agent-skills.md), [CLAUDE.md](../../../concepts/claude-md.md)
- Relacionado: [affaan-m/ECC](../affaan-m/ecc.md) — também instala processo, agentes e skills no Claude Code, com foco em TDD, memória e segurança; [HarnessMD/munder-difflin](../harnessmd/munder-difflin.md) — harness desktop com orquestração por escritório; [multica-ai/andrej-karpathy-skills](../../../repos/github.com/multica-ai/andrej-karpathy-skills.md) — diretrizes que o README cita como inspiração para os quatro modos de falha.
- Projetos citados: GBrain (`garrytan/gbrain`), OpenClaw, Conductor, Aside, impeccable.

## Perguntas abertas

- Como os 23 especialistas e as oito power tools se distribuem exatamente, e quais skills são mantidas versus experimentais?
- O auto-update e a reconciliação de hosts preservam customizações locais?
- Qual é a cobertura real dos testes de conformidade por host (full vs experimental)?
- Como o GBrain lida com segredos e com memória envenenada ao compartilhar um cérebro entre repositórios e máquinas?
- O modo de QA em navegador com sessões reais tem isolamento suficiente para uso em produção?
- Qual é o custo típico em tokens de um sprint completo?

## Fontes

- README: https://raw.githubusercontent.com/garrytan/gstack/6a4ab69dcdfd67377eaee6bc2d19a2c42038b037/README.md (commit `6a4ab69dcdfd67377eaee6bc2d19a2c42038b037`, consultado em 2026-10-19). Somente o README foi lido; código, `docs/`, `ARCHITECTURE.md` e demais arquivos não foram consultados.
- Metadados: API do GitHub (`/repos/garrytan/gstack`) em 2026-10-19.
