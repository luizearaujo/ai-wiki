---
type: repo
url: https://github.com/sodiumsun/agenttrail
host: github.com
owner: sodiumsun
repo: agenttrail
commit: e4ba2daa270abd7ecb51565bbfb12386f47ea418
license: MIT
language: JavaScript
status: active
created: 2026-10-25
ingested: 2026-10-25
updated: 2026-10-25
tags: [observabilidade, agentes, claude-code, codex, dashboard, mapa, 3d, plano, progresso, kitchen]
---

# sodiumsun/agenttrail

> Observabilidade local para agentes de código com duas vistas independentes: Map (estrutura do projeto e mudanças de arquivo via PLAN.md) e Kitchen (visualização 3D de tarefas como pratos em uma cozinha com chefs).

## O que é

Agenttrail observa a atividade dos seus agentes de código (Codex, Claude Code, Cursor) a partir de logs locais e a transforma em uma vista ao vivo do trabalho. Não lança agentes, não atribui trabalho, não marca tarefas como concluídas — só visualiza evidências disponíveis.

Dois pacotes npm independentes e duas portas locais. Local by construction: serviços vinculados a `127.0.0.1`, sem conta, telemetria ou chamadas de modelo.

## Uma projeto, duas vistas

| | **Map** (`npx agenttrail`) | **Kitchen** (`npx agenttrail-kitchen .`) |
|---|---|---|
| Ajuda a acompanhar | Estrutura do projeto, progresso e quais componentes estão mudando | Tarefas atuais, contribuições por papel e trabalho concluído |
| Visualiza como | Componentes, dependências, atividade de arquivo e rastros de sessão | Chefs, pedidos, cozinha e entregas |
| Fontes principais | `PLAN.md`, mudanças de arquivo e hooks opcionais do Claude Code | Native todos, atividade local de Codex/Claude e hooks opcionais |
| Requer plano? | Opcional para atividade de arquivo; necessário para o mapa de componentes | Opcional; native todos fornecem os pedidos quando disponíveis |

### Agenttrail Map

Combina intenção declarada em `PLAN.md` com mudanças de arquivo observadas. Componentes concluídos acendem ao serem modificados novamente. Hooks do Claude Code adicionam atividade de sessão e tool calls. Tem árvore de arquivos ao vivo, links de dependência e rastros de sessão.

**Convenção PLAN.md**: componentes com ID estável `{#id}`, `files:` para conectar arquivos ao componente, `[x]` concluído, `[~]` em andamento, `[!]` travado, `by:` para registrar autoria, `needs:` para setas de dependência, `kind: knowledge` e `kind: human` para tipos especiais. Decisões afetando o plano são registradas antes de executá-las.

### Agenttrail Kitchen

Vista experimental 3D com metáfora de restaurante: chefs representam responsabilidades do projeto (não necessariamente processos separados), tickets/pratos representam native todos com seu próprio texto e status, a esteira de entrega representa um todo reportado completo.

```bash
npx agenttrail-kitchen .
# abre em localhost:4780
# --example para ver demo sem agente rodando
```

Um chef pode mover-se entre vários papéis conforme o trabalho muda. Ingrediente separado: `--example` executa um demo scriptado e rotulado, `Live` retorna ao projeto real.

## Integração com agentes

| Ferramenta | Conexão com Kitchen |
|---|---|
| Codex CLI / desktop | Lê logs de sessão locais automaticamente |
| Claude Code | Lê logs locais do projeto; hooks aditivos opcionais via **Connect agents** |
| Cursor | Hooks de repositório opcionais via **Connect agents → Cursor** |
| VS Code | Sem extensão — rodar Kitchen no terminal integrado e manter o browser ao lado |

Hooks são explícitos e reversíveis; não instalam automaticamente.

## Observabilidade declarada vs não declarada

O README distingue o que acontece automaticamente (atividade local, native todos, responsabilidades inferidas, conclusão de todos) do que requer metadados extras (handoffs confirmados, compartilhar um todo entre sessões separadas). Itens sem plano ficam marcados **progress unknown**.

## Posicionamento

Foco em **progresso e fluxo de trabalho visual** (PLAN.md, metáfora de cozinha, rastreamento de todos), diferentemente de [camtrik/agent-trail](../camtrik/agent-trail.md), que foca em **custo e rastreabilidade** (token accounting, árvore de subagentes, contexto injetado). Kitchen é o único projeto que usa Three.js para visualização 3D de trabalho de agentes.

**A verificar:** sem informações sobre Windows (não verificado), suporte a sessões remotas (não descoberto automaticamente) e eventual extensão para VS Code/Cursor Marketplace. Somente o README foi lido.

## Fontes

- README no commit `e4ba2daa270abd7ecb51565bbfb12386f47ea418` (consultado em 2026-10-25). Somente o README foi lido.
- Metadados: GitHub API — JavaScript, MIT, 960 estrelas, 68 forks (2026-10-25).
