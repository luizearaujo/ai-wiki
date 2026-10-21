---
type: repo
url: https://github.com/virgiliojr94/book-to-skill
host: github.com
owner: virgiliojr94
repo: book-to-skill
commit: a24e62f4d8caf2ee433f6e48d9073800f56f906e
license: MIT
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, economia-de-tokens, rag, estudo]
---

# virgiliojr94/book-to-skill

> Converte um livro técnico, pasta de documentos ou coleção de fontes em uma Agent Skill unificada — capítulos sob demanda, glossário, padrões e cheatsheet — carregada pelo agente só quando o tópico é perguntado, com 24×–51× menos tokens do que despejar o livro inteiro no contexto.

## O que é

Resolve um problema específico: ler um livro técnico uma vez e não conseguir voltar a um capítulo específico meses depois sem reler o PDF inteiro ou arriscar o agente alucinar sobre o conteúdo. A skill gerada funciona em qualquer host que suporte o padrão aberto [Agent Skills](https://github.com/agentskills/agentskills) — GitHub Copilot CLI, Amp, Claude Code, Codex, Hermes Agent, OpenCode e OpenClaw todos leem o mesmo formato `SKILL.md`.

## Como funciona

Duas metades: um **extrator Python determinístico** (documento → texto limpo + metadados) e um **gerador guiado por spec** (o próprio agente segue o `SKILL.md` do conversor para estruturar esse texto em skill). Rodar `/book-to-skill ./meu-livro.pdf` gera, em `~/.agents/skills/<slug>/` (ou equivalente por host):

| Arquivo | Propósito | Tamanho |
|---|---|---|
| `SKILL.md` | Modelos mentais centrais + índice de capítulos | ~4.000 tokens |
| `chapters/ch01-*.md` … | Um arquivo por capítulo, carregado sob demanda | ~1.000 tokens cada |
| `glossary.md` | Todo termo-chave, alfabético, com referência ao capítulo | ~1.500 tokens |
| `patterns.md` | Técnicas, algoritmos e padrões de design | ~2.000 tokens |
| `cheatsheet.md` | Tabelas de decisão e referência rápida | ~1.000 tokens |

Os arquivos de capítulo só contam contra o orçamento de contexto quando o tópico é perguntado — a estruturação (o "discovery loop" de reler sumário, retroceder, reprocessar que um agente faria em um PDF cru) é pago uma vez, na conversão, não em toda consulta. O extrator escolhe a ferramenta certa por formato e tipo de livro (`pdftotext`/`pypdf`/`pdfminer.six` para prosa; `docling` para livros técnicos com tabelas e código), com um modo `--check` que lista o que está instalado. PDFs escaneados sem camada de texto são detectados e recusados antes de processar o livro inteiro.

Além de livros, o mesmo mecanismo serve documentação interna, guias de marca/voz, clusters de papers de pesquisa e specs/RFCs — qualquer prosa estruturada que o usuário reabre com frequência.

## Instalação e uso rápido

```bash
npx skills add virgiliojr94/book-to-skill
# ou manualmente:
git clone https://github.com/virgiliojr94/book-to-skill.git ~/.claude/skills/book-to-skill
```

```
/book-to-skill ./meu-livro.pdf
/meu-livro-slug replication   # pergunta sobre um capítulo específico
```

Também tem modos apenas-análise, geração-a-partir-de-análise e atualização/fold-in de material novo no mesmo skill.

## Quando usar (e quando não usar)

- **Use quando:** tem um livro técnico, pasta de documentação ou cluster de papers que reabre com frequência e quer que o agente responda do conteúdo real, sem reler o PDF em cada sessão.
- **Evite quando:** o material é lido uma única vez ou raramente reconsultado — o custo de conversão (análise completa do livro) não se paga em consultas únicas.

## Limitações e cuidados

- **Direitos de autor**: a ferramenta não distribui nenhum conteúdo do livro — o README é explícito que a skill gerada é "nota de estudo" derivada (nomes de framework, definições, conclusões), nunca cópia de trechos brutos, e recomenda não redistribuir uma skill gerada de um livro de terceiros protegido por direitos autorais.
- Processamento é local; nada é enviado pela própria ferramenta — mas se o agente do usuário rodar na nuvem, o texto segue os termos de dados desse provedor, como qualquer prompt.
- EPUB/DOCX/HTML/RTF/MOBI dependem de bibliotecas opcionais com qualidade variável; PDFs tecnicamente densos (tabelas, código) exigem `docling`, mais lento (~1,5s/página).

## Estado e adoção

- 35.564 estrelas, 3.758 forks, 25 issues abertas — observado em 2026-10-21.
- Repositório criado em 2026-05-01, com push mais recente em 2026-10-18 — observado em 2026-10-21.
- Licença: MIT (aplica-se ao conversor — código e definição da skill —, não a nenhum livro ou documento processado com ele).

## Relações

- Mantido por: [Virgilio Junior (virgiliojr94)](../../../entities/virgiliojr94.md)
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [Economia de tokens em agentes](../../../concepts/economia-de-tokens-em-agentes.md) — carregamento sob demanda por capítulo como técnica central de economia.

## Perguntas abertas

- Como o modo de atualização/fold-in resolve conflitos quando o livro tem uma nova edição com capítulos reorganizados?

## Fontes

- README: https://raw.githubusercontent.com/virgiliojr94/book-to-skill/a24e62f4d8caf2ee433f6e48d9073800f56f906e/README.md (commit `a24e62f4d8caf2ee433f6e48d9073800f56f906e`, consultado em 2026-10-21). Somente o README foi lido; `SKILL.md` e o extrator não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/virgiliojr94/book-to-skill`), consultada em 2026-10-21.
