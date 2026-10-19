---
type: skill
name: Impeccable
slug: impeccable
url: https://www.skills.sh/pbakaus/impeccable/impeccable
source_url: https://github.com/pbakaus/impeccable
source_path: .agents/skills/impeccable/SKILL.md
author: pbakaus
version: desconhecida
license: Apache-2.0
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, direcao-de-arte, frontend, ux, motion, acessibilidade, agent-skills]
---

# Impeccable

> Skill de direção de design para interfaces frontend: organiza o trabalho em quatro modos, um playbook de mais de vinte comandos e um contexto persistente de produto e design, com verificação no navegador real.

## O que é

`impeccable` é uma camada de direção de arte e revisão para qualquer interface frontend — sites, landing pages, dashboards, componentes, formulários, onboarding, estados vazios e telas nativas iOS/Android. O `SKILL.md` se apresenta como permissão para produzir "craft out-of-distribution", no papel de um diretor de design premiado: código de produção, ponto de vista claro e verificação no resultado renderizado.

Não é uma skill de geração de imagens nem um catálogo de estilos prontos. Ela instala um processo: carregar contexto do projeto, escolher o playbook adequado, editar com um piso de qualidade explícito e verificar o que foi renderizado nas dimensões em que a interface será usada.

## Como funciona

A direção começa pela classificação da superfície em quatro **modos**, cada um com um critério de sucesso diferente:

| Modo | Sucesso do visitante | Exemplos |
| --- | --- | --- |
| **Persuade** | Decide e age; o design é o produto. | Landing pages, marketing, campanhas, preços. |
| **Operate** | Completa uma tarefa. | App UI, dashboards, editores, admin, settings. |
| **Read** | Entende algo. | Documentação, artigos, guias, changelogs. |
| **Experience** | Está dentro da obra. | Portfólios, galerias, showcases. |

O modo é escolhido pela superfície, não pelo produto: a landing page de uma ferramenta é Persuade; a documentação de uma casa de moda é Read.

O fluxo de setup é explícito:

1. **Carregar contexto** com `<skill-base-dir>/scripts/impeccable context`, que lê `PRODUCT.md`, `DESIGN.md`, o brief da superfície e orientação nativa quando aplicável. O launcher executa um binário autocontido distribuído junto da skill (sem Node).
2. **Carregar o playbook** do comando explícito ou implícito, ou `reference/new-work.md` para uma superfície nova. Antes de editar, inspecionar a verdade visual existente; se o app não roda, usar goldens de regressão visual ou fixtures.
3. **Ler `reference/craft-floor.md`** imediatamente antes de qualquer edição de UI — piso de qualidade, bans absolutos e reflexos que detectores não pegam.
4. Se o launcher falhar, declarar isso ao usuário e ler `PRODUCT.md`/`DESIGN.md` diretamente, sem inventar contexto.

O playbook cobre 24 comandos em seis categorias:

- **Build:** `shape`, `init`, `document`, `extract` (e o alias depreciado `craft`).
- **Evaluate:** `critique` (revisão heurística com nota) e `audit` (a11y, performance, responsividade).
- **Refine:** `polish`, `bolder`, `quieter`, `distill`, `harden`, `onboard`.
- **Enhance:** `animate`, `colorize`, `typeset`, `layout`, `delight`, `overdrive`.
- **Fix:** `clarify`, `adapt`, `optimize`.
- **Iterate:** `live` (selecionar elementos no navegador) e `generate` (variantes de um elemento).

Três regras editoriais estruturam as decisões: **o brief vence** (estética fixada pelo cliente não é redirecionada para o gosto do modelo); **refinamento preserva, redesign substitui** (redesign trata o visual antigo como anti-referência e troca o `DESIGN.md`); e **autoridade visual é evidência, não nome de arquivo** (a ausência de `DESIGN.md` não torna um projeto greenfield).

## Instalação e uso

```bash
npx skills add https://github.com/pbakaus/impeccable --skill impeccable
```

A página não publica instalação global. O repositório distribui a skill em diretórios de vários harnesses (`.agents/`, `.claude/`, `.cursor/`, `.gemini/`, `.github/`, `.codex`, `.opencode/`, entre outros), além de um plugin de Cursor e um pacote VS Code.

## Exemplos de uso

Exemplos derivados do `SKILL.md` renderizado, não instruções oficiais:

- **Nova landing page:** o pedido entra como trabalho geral; sem `PRODUCT.md`, o fluxo passa por `init` e depois por `new-work`, escolhendo um "mundo visual" substituto.
- **Revisão:** `$impeccable critique` produz revisão heurística com nota; `audit` cobre acessibilidade, performance e responsividade.
- **Ajuste pontual:** `bolder`, `quieter`, `distill` ou `harden` atuam sobre um alvo específico sem trocar a identidade.
- **Iteração visual:** `live` abre o navegador para escolher elementos e comparar alternativas; `generate` cria variantes sem seleção manual.

## Saídas esperadas

Código de produção completo, com um veredito de design explícito, arquivos `PRODUCT.md`/`DESIGN.md` quando o fluxo os cria ou atualiza, achados de crítica/auditoria e, no modo `live`, variantes comparáveis no navegador. A skill insiste em verificar o resultado renderizado nas dimensões reais e em agrupar as checagens, corrigindo o que uma olhada revela antes de olhar de novo.

## Quando usar (e quando não usar)

- **Use quando:** o pedido envolve desenhar, redesenhar, dar forma, criticar, auditar, polir, simplificar, endurecer, animar ou melhorar uma interface frontend — inclusive estados vazios, onboarding, formulários e telas nativas.
- **Evite quando:** a tarefa é exclusivamente backend ou não tem superfície visual. Para gerar imagens de referência antes do código, a família [image-to-code](../../../../concepts/image-to-code.md) é mais adequada.

## Limitações e cuidados

- O setup depende de um binário autocontido; em shell Windows sem `sh` é preciso usar `impeccable.cmd`. Se o launcher falhar, o procedimento de fallback exige leitura manual do contexto.
- `PRODUCT.md` e `DESIGN.md` são estado do projeto: o `doctor` reporta drift, mas a skill proíbe reparar drift como efeito colateral de uma tarefa de design.
- O `SKILL.md` lista símbolos históricos que não devem virar ornamento (insígnias nazistas, bandeira confederada, raios da bandeira do Sol Nascente), com a ressalva de que conteúdo documental permanece.
- O conteúdo foi lido a partir do `SKILL.md` renderizado na página do skills.sh; scripts, binário, referências internas e a implementação Rust não foram inspecionados.
- Auditoria Socket publicada como "Warn" (as demais, "Pass") — o motivo não é detalhado na página.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **343.949** (343,9 mil), primeira aparição em 8 de abril de 2026.
- Auditorias publicadas: Gen Agent Trust Hub "Pass", Socket "Warn", Snyk "Pass".
- Repositório: 82.979 estrelas, 5.018 forks, 45 issues abertas; criado em 2025-11-16, último push em 2026-10-19.
- Licença do repositório: Apache-2.0. Linguagem principal: Rust.

## Relações

- Autor: [Paul Bakaus](../../../../entities/pbakaus.md).
- Conceitos: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md), [Design system com agentes](../../../../concepts/design-system-com-agentes.md), [Auditoria de UX](../../../../concepts/auditoria-de-ux.md).
- Alternativas: [UI/UX Pro Max](../../nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max.md) para base pesquisável; [Design Taste Frontend](../../leonxlnx/taste-skill/design-taste-frontend.md) para processo anti-slop; [UX Audit Rethink](../../mastepanoski/claude-skills/ux-audit-rethink.md) para auditoria ampla.

## Perguntas abertas

- O binário autocontido é auditável e reproduzível a partir do código Rust?
- Como `PRODUCT.md` e `DESIGN.md` se relacionam com o formato DESIGN.md do Google Labs?
- Os 24 comandos têm cobertura de teste equivalente entre harnesses?
- Qual o custo de contexto de carregar o playbook e as referências em cada sessão?
- O modo `live` funciona em todos os navegadores suportados?

## Fontes

- Página de origem: https://www.skills.sh/pbakaus/impeccable/impeccable (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/pbakaus/impeccable (metadados e árvore via API do GitHub, commit `0665bd812ae0908fcab17b96fd4f840defb882d9`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
