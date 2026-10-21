---
type: repo
url: https://github.com/petergyang/no-ai-slop
host: github.com
owner: petergyang
repo: no-ai-slop
commit: 000650b156983f5159695b441477f4e63b25dc85
license: MIT
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agent-skills, humanizacao, escrita]
---

# petergyang/no-ai-slop

> Skill que remove mais de 20 padrões de escrita por IA (contrastes binários, "o que ninguém te conta", finais de falso-profundo) preservando a voz do autor, com um modo de detecção que só cita os padrões encontrados e um modo satírico que gera "slop" de propósito.

## O que é

Resolve o problema de texto gerado ou editado por IA que soa genérico — mesmo os melhores modelos reproduzem certas construções ("Não é X. É Y.", "O melhor de tudo: aprende sozinho.") que soam reconhecivelmente artificiais e apagam vocabulário, cadência e humor pessoais. A skill é instalável globalmente em ChatGPT, Claude Code, Codex ou outro agente de código, e também existe como plugin do ChatGPT.

## Como funciona

- **`/no-ai-slop (texto)`**: remove os padrões de slop, preserva a voz pessoal e lista o que mudou.
- **`/no-ai-slop is this slop? (texto)`**: só cita cada padrão de slop encontrado, sem tentar adivinhar se o texto foi escrito por IA.
- **Modo satírico**: gera o "slop" mais exagerado possível como piada, a partir de um pedido como "Draft an AI slop post about (tópico)".
- Dez dos mais de 20 padrões catalogados, segundo o README: contrastes binários, aberturas de "deixa eu limpar a garganta", falsos insights ("o que ninguém te conta"), revelações por dois-pontos, fragmentos dramáticos, análise superficial, exagero de importância ("marca um momento decisivo"), atribuição vaga ("especialistas concordam"), sinonímia cíclica e finais de falso-profundo ("o futuro não está chegando. Já chegou.").
- Também verifica fundamentos de escrita: liderar com o ponto principal, voz ativa, destrinchar frases difíceis e preferir detalhes concretos a abstrações.
- Arquivos do repositório: `SKILL.md` (regras e workflow), `eval.md` (checagens que a skill roda sobre o próprio trabalho), `.codex-plugin/plugin.json` (metadados de plugin ChatGPT/Codex) e `scripts/build_plugin.py` (builda e valida o pacote de plugin).

## Instalação e uso

```text
Install the /no-ai-slop skill globally from https://github.com/petergyang/no-ai-slop
```

```bash
npx skills add petergyang/no-ai-slop --skill no-ai-slop --global --yes
```

## Quando usar (e quando não usar)

- **Use quando:** quer revisar texto editado ou escrito por IA sem perder a voz pessoal, ou quer detectar padrões de slop sem alterar o texto.
- **Evite quando:** o objetivo é confirmar com certeza se um texto *foi* escrito por IA — a própria skill, no modo de detecção, só cita os padrões encontrados e explicitamente não tenta adivinhar a origem do texto.

## Limitações e cuidados

- Detecção é por padrão de estilo, não forense: o modo "is this slop?" não afirma autoria, só aponta construções.
- `eval.md` descreve checagens que a skill roda sobre o próprio trabalho, mas o conteúdo exato não foi lido nesta ingestão.

## Estado e adoção

- 12.651 estrelas, 880 forks, 23 issues abertas — observado em 2026-10-21.
- Repositório criado em 2026-07-07, com push mais recente em 2026-09-02 — observado em 2026-10-21.
- Licença: MIT.

## Relações

- Mantido por: [Peter Yang (petergyang)](../../../entities/petergyang.md)
- Conceitos: [Humanização de texto gerado por IA](../../../concepts/humanizacao-de-texto-por-ia.md), [Agent skills](../../../concepts/agent-skills.md).
- Alternativas já documentadas (mesmo conceito): [Humanizer](../../../skills/github.com/blader/humanizer/humanizer.md) (26 padrões em seis famílias, quatro etapas) e [Stop Slop](../../../skills/github.com/hardikpandya/stop-slop/stop-slop.md) (oito regras centrais, nota 1–10) — No AI Slop soma mais de 20 padrões específicos e um modo de detecção que só cita, sem veredito de autoria.

## Perguntas abertas

- Como o modo satírico evita que o slop gerado de propósito seja reaproveitado fora do contexto de piada?

## Fontes

- README: https://raw.githubusercontent.com/petergyang/no-ai-slop/000650b156983f5159695b441477f4e63b25dc85/README.md (commit `000650b156983f5159695b441477f4e63b25dc85`, consultado em 2026-10-21). Somente o README foi lido; `SKILL.md` e `eval.md` não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/petergyang/no-ai-slop`), consultada em 2026-10-21.
