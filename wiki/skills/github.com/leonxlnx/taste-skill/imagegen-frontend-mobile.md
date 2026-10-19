---
type: skill
name: Imagegen Frontend Mobile
slug: imagegen-frontend-mobile
url: https://www.skills.sh/leonxlnx/taste-skill/imagegen-frontend-mobile
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/imagegen-frontend-mobile/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, geracao-de-imagem, mobile, frontend, movida, agent-skills]
---

# Imagegen Frontend Mobile

> Entrada de catálogo movida para outro repositório: a página publica apenas a descrição e o aviso de mudança, sem corpo de `SKILL.md`; o comando de instalação aponta para `Leonxlnx/imagegen-skills`.

## O que é

`imagegen-frontend-mobile` é a variante mobile da família de skills de geração de imagens de referência para frontend. Como [Image to Code](image-to-code.md), ela aparece na listagem do `taste-skill`, mas a página do skills.sh não publica conteúdo renderizado (0 caracteres).

A descrição publicada é: "Moved to github.com/Leonxlnx/imagegen-skills. Runs only when called by name." O comando de instalação já usa o repositório novo:

```bash
npx skills add https://github.com/Leonxlnx/imagegen-skills --skill imagegen-frontend-mobile
```

## Como funciona

**A verificar.** Não há corpo de instruções na fonte consultada. Pelo nome e pela irmã [Imagegen Frontend Web](imagegen-frontend-web.md), a proposta é gerar imagens de referência de telas mobile — provavelmente uma imagem por tela ou seção — antes da implementação. A página não confirma regras, contagem de imagens ou formato de análise.

## Instalação e uso

```bash
npx skills add https://github.com/Leonxlnx/imagegen-skills --skill imagegen-frontend-mobile
```

## Exemplos de uso

**A verificar.** Não há exemplos publicados. Para o fluxo web equivalente, ver [Imagegen Frontend Web](imagegen-frontend-web.md).

## Saídas esperadas

**A verificar.** A descrição não especifica saídas.

## Quando usar (e quando não usar)

- **Use quando:** o projeto tem superfície mobile e o harness permite gerar imagens antes de implementar.
- **Evite quando:** for necessária uma skill do repositório `taste-skill` com conteúdo verificável.

## Limitações e cuidados

- A página de origem está vazia: comportamento e dependências não verificados.
- A entrada pode ficar obsoleta no catálogo antigo após a mudança.
- O caminho `skills/imagegen-frontend-mobile/SKILL.md` consta da árvore do repositório antigo, mas o conteúdo não foi lido.
- Não confundir com [Image Taste Frontend](image-taste-frontend.md), que é específica para tasks web no Codex.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **372.577**, primeira aparição em 25 de abril de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório-fonte atualizado no comando de instalação: `Leonxlnx/imagegen-skills`.
- Repositório da página: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conceito: [Image-to-code](../../../../concepts/image-to-code.md).
- Variantes: [Imagegen Frontend Web](imagegen-frontend-web.md), [Image to Code](image-to-code.md).

## Perguntas abertas

- A skill gera uma imagem por tela ou por seção?
- Ela cobre iOS, Android ou ambos?
- Qual é o conteúdo atual em `Leonxlnx/imagegen-skills`?
- A entrada antiga será removida?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/imagegen-frontend-mobile (consultada em 2026-10-19); a página não publica `SKILL.md` renderizado (0 caracteres).
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
