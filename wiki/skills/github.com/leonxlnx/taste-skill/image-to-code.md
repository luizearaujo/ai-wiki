---
type: skill
name: Image to Code
slug: image-to-code
url: https://www.skills.sh/leonxlnx/taste-skill/image-to-code
source_url: https://github.com/leonxlnx/taste-skill
source_path: skills/image-to-code-skill/SKILL.md
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [design-ui, image-to-code, geracao-de-imagem, frontend, movida, agent-skills]
---

# Image to Code

> Entrada de catálogo movida para outro repositório: a página publica apenas a descrição e o aviso de mudança, sem corpo de `SKILL.md`; o comando de instalação já aponta para `Leonxlnx/imagegen-skills`.

## O que é

`image-to-code` aparece na listagem do `leonxlnx/taste-skill`, mas a página do skills.sh não publica conteúdo renderizado (0 caracteres). A descrição diz apenas: "Moved to github.com/Leonxlnx/imagegen-skills. Runs only when called by name."

O comando de instalação confirma a mudança:

```bash
npx skills add https://github.com/leonxlnx/imagegen-skills --skill image-to-code
```

Não há, portanto, corpo de instruções a documentar a partir da fonte consultada. O que se sabe é o posicionamento declarado: uma skill de image-to-code, opt-in, hoje mantida em outro repositório.

## Como funciona

**A verificar.** O conteúdo não está disponível na página de origem. A função inferível a partir do nome e do ecossistema é gerar uma imagem de referência e então implementar o frontend correspondente — o mesmo padrão descrito em [Image Taste Frontend](image-taste-frontend.md) e [Imagegen Frontend Web](imagegen-frontend-web.md), que permanecem no repositório `taste-skill`.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/imagegen-skills --skill image-to-code
```

## Exemplos de uso

**A verificar.** Não há exemplos publicados na página consultada. Para um fluxo equivalente documentado, ver [Image Taste Frontend](image-taste-frontend.md).

## Saídas esperadas

**A verificar.** A descrição não especifica saídas.

## Quando usar (e quando não usar)

- **Use quando:** o harness permite gerar imagens antes de codificar e o repositório `imagegen-skills` é aceitável como fonte.
- **Evite quando:** for necessária uma skill mantida no repositório `taste-skill`; nesse caso, usar as alternativas com conteúdo publicado.

## Limitações e cuidados

- A página de origem está vazia: não é possível verificar regras, dependências ou comportamento.
- A skill foi movida; a entrada no catálogo antigo pode ficar obsoleta.
- A auditoria Socket está publicada como "Warn" (as demais, "Pass"), sem motivo detalhado na página.
- O caminho `skills/image-to-code-skill/SKILL.md` consta da árvore do repositório antigo, mas o conteúdo não foi lido.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **384.653**, primeira aparição em 24 de abril de 2026.
- Auditorias publicadas: Gen Agent Trust Hub "Pass", Socket "Warn", Snyk "Pass".
- Repositório-fonte atualizado no comando de instalação: `Leonxlnx/imagegen-skills`.
- Repositório da página: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conceito: [Image-to-code](../../../../concepts/image-to-code.md).
- Equivalentes no repositório antigo: [Image Taste Frontend](image-taste-frontend.md), [Imagegen Frontend Web](imagegen-frontend-web.md), [Imagegen Frontend Mobile](imagegen-frontend-mobile.md).

## Perguntas abertas

- Qual é o conteúdo atual da skill em `Leonxlnx/imagegen-skills`?
- A entrada antiga será removida do catálogo?
- Por que a auditoria Socket é "Warn"?
- A skill difere funcionalmente de `image-taste-frontend`?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/image-to-code (consultada em 2026-10-19); a página não publica `SKILL.md` renderizado (0 caracteres).
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
