---
type: repo
url: https://github.com/goul4rt/lgpd-skills
host: github.com
owner: goul4rt
repo: lgpd-skills
commit: d85d79abeeb37cb99fc0785e735a9ca790698a77
license: MIT
language: Shell
status: active
created: 2026-11-05
ingested: 2026-11-05
updated: 2026-11-05
tags: [agent-skills, lgpd, compliance, privacidade, portugues-brasileiro]
---

# goul4rt/lgpd-skills

> Pacote de 19 Agent Skills — um maestro (`lgpd-audit`) e 18 sub-skills — que conduz uma auditoria de conformidade com a LGPD (Lei 13.709/2018), resoluções da ANPD e o ECA Digital (Lei 15.211/2025) sobre uma base de código, produzindo artefatos versionados em `.lgpd/`.

## O que é

Um conjunto modular de Agent Skills que transforma um pedido como "preciso adequar isso à LGPD" em um pipeline executável e auditável. Em vez de uma skill monolítica, o pacote tem um **maestro** (`lgpd-audit`) que decide o pipeline, mantém estado e pausa em checkpoints críticos, e **18 sub-skills** especializadas que podem rodar isoladas ou encadeadas pelo maestro. Funciona em cinco agentes: Claude Code, Codex, Gemini CLI, Cursor e OpenCode, seguindo o formato aberto Agent Skills (agentskills.io).

## Como funciona

O maestro escolhe um de quatro pipelines segundo o cenário informado pelo usuário: **A** (greenfield, privacy-by-design, 1–2 semanas), **B** (legado em produção, auditoria + retrofit, 2–6 semanas), **C** (híbrido, 3–8 semanas) ou **D** (resposta a incidente em andamento, 3 dias úteis — prazo da Resolução CD/ANPD nº 15/2024). Os tempos são estimativas do projeto, não garantias.

As 18 sub-skills cobrem, entre outras frentes: base legal e LIA (`lgpd-legal-basis`), mapeamento de dados (`lgpd-data-mapping`), Registro de Operações de Tratamento — ROPA (`lgpd-ropa`, modelo ANPD ATPP), Relatório de Impacto — RIPD (`lgpd-ripd`, metodologia ISO 31000), ledger de consentimento em Prisma (`lgpd-consent-schema`), direitos do titular com SLA de 15 dias (`lgpd-dsar`), política de privacidade (`lgpd-privacy-policy`), resposta a incidentes com runbook e prazo de 3 dias úteis (`lgpd-incident-response`), designação de encarregado (`lgpd-dpo-encarregado`), DPA com operadores (`lgpd-dpa`), transferência internacional via Cláusulas-Padrão (`lgpd-international-transfer`), auditoria de fornecedores (`lgpd-vendor-audit`), log de auditoria imutável (`lgpd-audit-logging`), criptografia e gestão de chaves (`lgpd-encryption-keys`), anonimização (`lgpd-anonymization`), retenção e eliminação (`lgpd-retention-erasure`), ECA Digital para menores (`lgpd-eca-digital-minors`) e gap analysis para legado (`lgpd-legacy-retrofit`).

Cada sub-skill produz artefatos vivos versionáveis em Git sob `.lgpd/` (`STATUS.md`, `ROPA.md`, `RIPD/`, política versionada, log de incidentes, etc.), pensados para revisão em PR e auditoria em retrospectiva — o mesmo padrão de "artefato persistente, não conversa" já visto em outras skills de auditoria desta wiki. O encode das normas (texto e citação por artigo) vive em `skills/lgpd-audit/references/normative-reference.md`, não lido nesta ingestão.

## Instalação e uso rápido

Instalação por agente (comandos publicados no README):

- **Claude Code:** `/plugin marketplace add goul4rt/lgpd-skills` e `/plugin install lgpd-skills@lgpd-skills`.
- **Codex:** `codex plugin marketplace add goul4rt/lgpd-skills` e `codex plugin add lgpd-skills@lgpd-skills`, ou `/plugins` dentro do Codex.
- **Gemini CLI:** `gemini extensions install https://github.com/goul4rt/lgpd-skills` — as 19 skills são auto-descobertas e disparam via `activate_skill`.
- **Cursor:** `/add-plugin` com a URL do repositório, ou pela vitrine em cursor.com/marketplace.
- **OpenCode:** adicionar `lgpd-skills@git+https://github.com/goul4rt/lgpd-skills.git` ao array `plugin` do `opencode.json`. **Atenção:** no OpenCode as skills não disparam sozinhas — precisam ser ativadas explicitamente pela ferramenta `skill`.
- **Manual:** clonar o repositório e copiar `skills/lgpd-*` para `~/.claude/skills/` (global) ou `.claude/skills/` (por projeto), em qualquer agente compatível com esse layout.

## Exemplos de uso

- "veja como estamos de LGPD" → ativa `lgpd-audit`, que pergunta o cenário (greenfield/legado/híbrido/resposta a incidente) e inicia o pipeline correspondente.
- "tivemos um vazamento de e-mails, preciso comunicar a ANPD" → ativa `lgpd-incident-response` em modo emergencial, guiando pelo runbook da Resolução 15/2024.
- "implementa o endpoint de exclusão de conta" → ativa `lgpd-dsar` para gerar código, schema e log de auditoria.

Exemplos derivados do fluxo descrito no README, não instruções oficiais verificadas em execução real pela wiki.

## Quando usar (e quando não usar)

- **Use quando:** precisar estruturar uma auditoria ou retrofit de conformidade LGPD/ECA Digital sobre uma base de código, com artefatos versionáveis e rastreáveis por commit/PR.
- **Evite quando:** precisar de aconselhamento jurídico vinculante — o próprio README é explícito que o pacote não substitui isso (ver Limitações) — ou quando a stack do projeto está muito distante da assumida (Next.js, Prisma/PostgreSQL, Better Auth, React Native/Expo, AWS/GCP), caso em que os templates de código precisam de adaptação manual.

## Limitações e cuidados

- **Disclaimer do próprio projeto:** não constitui aconselhamento jurídico. Comunicação à ANPD deve envolver o Encarregado e o jurídico; avaliação de "incidente notificável" é caso a caso; cláusulas contratuais negociadas e o texto final da política de privacidade devem passar por revisão de advogado especializado.
- As skills assumem (sem exigir) uma stack específica: Next.js 14+ App Router, Prisma + PostgreSQL, Better Auth, React Native + Expo, AWS/GCP, Datadog/Sentry, Stripe/Pagar.me. Fora dessa stack, os templates de código precisam de adaptação.
- Cobertura normativa é um "encode rígido" mantido manualmente (`normative-reference.md`); a própria seção de contribuição do README pede correções porque a ANPD publica resoluções com frequência — desatualização é um risco declarado, não hipotético.
- **A verificar:** apenas o `README.md` foi lido. O conteúdo de cada `SKILL.md`, o `normative-reference.md` com o texto legal citado, e o código de exemplo (Shell/JavaScript) não foram consultados.

## Estado e adoção

- Sem versionamento semântico de release citado no README.
- Atividade observada em 2026-11-05: último push em 2026-05-31; 111 estrelas; 16 forks; 2 issues abertas (API do GitHub — não um fato estável).
- Linguagens predominantes no repositório (API do GitHub): Shell e JavaScript.
- Licença: MIT.

## Relações

- Mantido por: [goul4rt](../../../entities/goul4rt.md) ("O Polar" — bacharel em Ciência da Computação, pós-graduação em Arquitetura de Software, Ciência de Dados e Cibersegurança, iniciando mestrado em IHC).
- Conceitos: ver [Conformidade regulatória com agentes](../../../concepts/conformidade-regulatoria-com-agentes.md) (síntese nova a partir deste repositório — primeiro exemplo documentado do padrão na wiki).
- Alternativas: nenhuma outra skill de conformidade com lei de proteção de dados documentada nesta wiki até o momento; compare com o padrão de evidência/cobertura graduada do [Claude Ads](../agricidaniel/claude-ads.md) (auditoria de mídia paga) e com a biblioteca de skills de segurança do [Anthropic Cybersecurity Skills](../mukul975/anthropic-cybersecurity-skills.md), que cobrem controles técnicos adjacentes (criptografia, logging) sem o enquadramento jurídico específico.

## Perguntas abertas

- O texto normativo citado pelas skills (artigos, resoluções) não foi verificado contra a fonte oficial nesta ingestão — apenas a lista de normas cobertas, publicada no README.
- Não há, no README, relato de uso real em um projeto de produção — o fluxo descrito é a documentação do próprio projeto, não um caso de uso auditado pela wiki.

## Fontes

- README: https://raw.githubusercontent.com/goul4rt/lgpd-skills/d85d79abeeb37cb99fc0785e735a9ca790698a77/README.md (commit `d85d79abeeb37cb99fc0785e735a9ca790698a77`, consultado em 2026-11-05). Somente o README foi lido; os 19 `SKILL.md`, o `normative-reference.md` e o código não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/goul4rt/lgpd-skills`, `api.github.com/users/goul4rt`), consultada em 2026-11-05.
