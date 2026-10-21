---
type: skill
name: Git Commit Conventions
slug: git-commit-conventions
url: https://github.com/zazencodes/skills/tree/main/skills/git-commit-conventions
source_url: https://github.com/zazencodes/skills
source_path: skills/git-commit-conventions
author: zazencodes
version: 0.1.1
license: desconhecida
status: active
created: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, git, convencoes, claude-code]
---

# Git Commit Conventions

> Impõe um commit por lote de mudanças relacionadas por intenção (não por arquivo), mensagens curtas de uma linha, autoria só do `git config` do usuário — nunca atribuição de IA — e um método mecânico para separar um working tree que já misturou vários lotes.

## O que é

Skill do catálogo [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md) que fixa as convenções de commit do autor, para ser aplicada antes de qualquer commit ou push — pedido explicitamente ou iniciado pelo próprio agente, incluindo "commit this", "commit and push" ou `/commit`.

## Como funciona

Duas regras centrais, aplicadas sempre:

- Autoria do commit segue só a configuração git do sistema do usuário — **sem trailers de co-autoria**.
- Mensagens muito simples: uma linha curta por lote distinto de mudanças.

Convenções de trabalho:

- Ler `git diff` e checar arquivos não rastreados antes de decidir os commits.
- Um commit por lote distinto; só agrupar arquivos quando estiverem de fato relacionados, senão commitar separadamente.
- Seguir o estilo das mensagens recentes do próprio repositório.
- Nunca adicionar atribuição de IA — nem `Co-Authored-By`, nem rodapé "Generated with".
- Tentar correções simples por conta própria; pedir orientação só em conflito de merge ou algo que arrisque perder trabalho.

### Dividindo um working tree misturado

Lotes são definidos por **intenção**, não por arquivo — duas mudanças que se entrelaçam dentro do mesmo arquivo (uma feature e uma correção de acompanhamento, um refactor e uma mudança de comportamento) não são razão para desistir e fazer um commit só. A regra é dividir por padrão, sem pedir permissão primeiro, porque a divisão é mecânica e reversível:

- Trabalho pedido em turnos separados do usuário é sempre um lote separado, mesmo que o segundo edite arquivos que o primeiro criou.
- Não combinar lotes só porque "a divisão seria um rebase, não staging", ou porque um arquivo foi reescrito por completo — nenhum dos dois é motivo válido.
- `git add -p` precisa de um TTY, que não está disponível para o agente. No lugar, o **método de reconstrução**:
  1. Copiar a versão final de cada arquivo com mais de um lote para fora do repositório.
  2. `git reset --soft HEAD~1` se já comitado; senão, começar aqui.
  3. Editar esses arquivos de volta ao estado do **primeiro** lote isoladamente, e comitar.
  4. Restaurar as versões finais salvas, e comitar o segundo lote.
  5. Repetir os passos 3–4 para um terceiro lote em diante.
- Ordenar os commits para que cada um funcione isoladamente: o commit anterior precisa buildar e passar os testes sem o próximo. Verificar isso de fato — `git stash -u`, fazer checkout do commit anterior, rodar a suíte de testes, voltar.
- Usar caminhos explícitos no `git add`; `git add -A` varre silenciosamente arquivos não rastreados não relacionados — checar `git show --stat` depois do commit e corrigir com `amend` se algo entrou sem querer.
- Ao terminar, confirmar que a divisão preservou o trabalho: `git diff <sha-original> HEAD` deve ficar vazio, ou mostrar só mudanças que o agente consegue nomear e justificar.

Se uma divisão genuinamente não for possível, a instrução é dizer isso e explicar o que bloqueia, em vez de comitar tudo junto e só mencionar depois.

## Instalação e uso

```bash
# Plugin do Claude Code
claude plugin marketplace add zazencodes/skills
claude plugin install zazencodes-skills@zazencodes

# skills.sh, só esta skill
npx skills@latest add zazencodes/skills --skill git-commit-conventions
```

Precisa só de `git`; não depende de ferramenta externa.

## Exemplos de uso

> Exemplos derivados da descrição publicada — não são instruções oficiais da skill.

- Pedir "commit this" depois de implementar duas features não relacionadas na mesma sessão — a skill separa em dois commits, mesmo que os arquivos se misturem.
- Pedir para comitar um working tree já com mudanças empilhadas de turnos diferentes, deixando o método de reconstrução dividir por lote.

## Saídas esperadas

Um ou mais commits no repositório, cada um correspondendo a exatamente um lote de intenção, com mensagem curta de uma linha no estilo do histórico recente, autoria só do `git config` do usuário e nenhum trailer de atribuição de IA.

## Quando usar (e quando não usar)

- **Use quando:** quer um histórico de commits limpo, com um commit por intenção, sem depender de lembrar de pedir isso em toda sessão.
- **Evite quando:** o fluxo do time exige atribuição de IA nos commits (padrão comum em outras organizações) — esta skill proíbe isso explicitamente, sem opção de configurar.

## Limitações e cuidados

- Convenção de opinião do autor, não neutra: a ausência de atribuição de IA é uma escolha explícita, não um padrão universal — times que exigem rastreabilidade de autoria por IA precisam editar a skill antes de instalar.
- O método de reconstrução reescreve histórico local (`git reset --soft`) — seguro antes de qualquer push, arriscado depois, embora o `SKILL.md` não detalhe esse caso.
- Não há suporte a `git add -p` (sem TTY disponível ao agente); o método de reconstrução é o substituto documentado, não uma alternativa automática.

## Estado e adoção

- Versão: parte do catálogo [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md) desde o release `v0.1.0`, segundo o `CHANGELOG.md`.
- Preço/licença: desconhecida no próprio arquivo da skill (sem campo `license` no frontmatter do `SKILL.md`); licença do repositório como um todo é MIT.

## Relações

- Autor: [zazencodes (Alexander Galea)](../../../../entities/zazencodes.md)
- Repositório-fonte: [zazencodes/skills](../../../../repos/github.com/zazencodes/skills.md)
- Conceitos: [Agent skills](../../../../concepts/agent-skills.md)

## Perguntas abertas

- O que a skill faz quando o método de reconstrução precisa dividir um commit que já foi enviado (`push`) a um branch compartilhado?

## Fontes

- `SKILL.md`: https://raw.githubusercontent.com/zazencodes/skills/9f2d7c8f0e112e03d0e440676afd49fde3c9dff2/skills/git-commit-conventions/SKILL.md (commit `9f2d7c8f0e112e03d0e440676afd49fde3c9dff2`, lido via clone local autorizado, consultado em 2026-10-21).
