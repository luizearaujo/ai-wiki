---
type: concept
aliases: [Agent Skills, Skills para agentes, SKILL.md]
status: draft
created: 2026-10-17
updated: 2026-10-17
tags: [agentes, skills, claude-code, distribuicao]
---

# Agent skills

> Instruções empacotadas em um diretório com `SKILL.md` que ensinam um agente a executar um tipo de tarefa, distribuídas e instaladas como artefatos versionáveis.

## Definição

Uma agent skill é um pacote de conhecimento procedural para um agente: um diretório com um arquivo `SKILL.md` — descrição, quando usar e instruções — e, opcionalmente, referências, scripts e outros recursos. Em vez de repetir um prompt longo em cada sessão, o usuário instala a skill e o agente carrega as instruções quando a tarefa corresponde.

A diferença central em relação a um prompt avulso é a **distribuição**: a skill tem repositório-fonte, caminho, versão, licença e um comando de instalação. Isso a torna um artefato que pode ser compartilhado, auditado e atualizado.

## Como funciona

O padrão observado no ecossistema:

1. A skill vive em um repositório-fonte, tipicamente em `skills/<slug>/SKILL.md`.
2. Um CLI — como o `skills`, usado pelo claudemarketplaces.com — instala a skill no agente escolhido, por projeto ou globalmente.
3. O agente decide quando aplicar a skill a partir da descrição publicada.
4. O comportamento de carregamento de referências adicionais depende do agente e do formato; nesta wiki isso ainda não foi verificado.

Instalação típica observada:

```bash
npx -y skills add owner/repo --skill <slug> --agent claude-code
```

## Onde aparece

- [UX Audit Rethink](../skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — skill de auditoria de UX instalada pelo CLI `skills`, com `SKILL.md` em `skills/ux-audit-rethink/`.

## Trade-offs

- **Vantagens:** reutilização de instruções complexas; versionamento e fonte rastreável; instalação em um comando; possibilidade de distribuir conhecimento especializado sem escrever código.
- **Limitações:** a skill é texto executado pelo agente, não um sandbox — instruções de terceiros podem ser maliciosas ou simplesmente ruins; a qualidade e a manutenção variam; atualizações podem mudar o comportamento sem aviso; o formato ainda não é padronizado entre fornecedores.

## Relações

- **Relacionado a:** [Model Context Protocol](../concepts/model-context-protocol.md) — camada complementar: skills empacotam *instruções*, MCP expõe *ferramentas e dados* em runtime.
- **Distingue-se de:** [CLAUDE.md](../concepts/claude-md.md) — instruções persistentes do projeto, carregadas em toda sessão; skills são acionadas por tarefa e distribuídas como pacote.
- **Contrasta com:** prompts avulsos copiados entre sessões e plugins específicos de um único cliente.
- **Pré-requisito para:** usar skills de catálogo com segurança — revisar fonte, licença, conteúdo e permissões antes da instalação.

## Perguntas abertas

- Qual é o modelo exato de carregamento e de uso de contexto das skills em cada agente?
- Como o `skills` CLI resolve conflitos de nome, versões e atualizações?
- Que garantias de segurança existem além da revisão manual do `SKILL.md`?
- Como skills e servidores MCP se combinam na prática — instruções que chamam ferramentas?

## Fontes

- [UX Audit Rethink](../skills/github.com/mastepanoski/claude-skills/ux-audit-rethink.md) — comandos de instalação e caminho do `SKILL.md` publicados no catálogo (consultado em 2026-10-17).
- https://github.com/mastepanoski/claude-skills — árvore do repositório com `skills/<slug>/SKILL.md` (consultada em 2026-10-17).
