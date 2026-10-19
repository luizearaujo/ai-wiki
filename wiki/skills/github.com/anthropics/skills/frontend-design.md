---
type: skill
name: Frontend Design
slug: frontend-design
url: https://github.com/anthropics/skills/tree/main/skills/frontend-design
source_url: https://github.com/anthropics/skills
source_path: skills/frontend-design
author: anthropics
version: desconhecida
license: Apache-2.0
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [agent-skills, design-taste, frontend]
---

# Frontend Design

> Skill da Anthropic para orientar design visual distinto e deliberado em UIs novas ou existentes, cobrindo direção estética, tipografia e escolhas que evitam o aspecto genérico e templado.

## O que é

Skill de exemplo do repositório oficial [anthropics/skills](../../../../repos/github.com/anthropics/skills.md), categoria Criativo & Design. Ajuda quem constrói interfaces a produzir identidade visual distinta em vez de padrões default repetidos entre projetos.

## Como funciona

Workflow descrito no `SKILL.md`, em duas passagens:

1. **Fundamentar o design no assunto:** identificar produto, público e função principal, confirmando com o cliente se o briefing for ambíguo; tirar pistas de paleta, tipografia e layout do setor e do vocabulário visual do assunto.
2. **Planejar o hero:** abrir com o elemento mais característico do universo do assunto; o hero padrão de "estatística + gradiente" só deve ser usado quando for genuinamente a melhor escolha.
3. **Definir tipografia:** usar uma ou duas famílias claramente distintas, uma escala tipográfica deliberada, e tratar a tipografia como elemento ativo de design — evitando acentos de uma palavra em títulos, rótulos em caixa alta e rótulos decorativos acima de headings; manter linhas com menos de 80 caracteres e dar mais entrelinha a corpo de texto serifado do que sans-serif.
4. **Dar significado à estrutura:** bordas, divisores e numeração devem codificar informação; usar marcadores numerados só para sequências reais.
5. **Usar movimento com parcimônia:** preferir um momento de animação orquestrado, e ligar outros movimentos a ações do usuário.
6. **Escrever copy centrada no usuário:** linguagem simples, ativa e consistente; estados de erro e vazio específicos e úteis.
7. **Trabalhar em duas passagens:** primeiro escrever um plano de tokens compacto (4–6 cores nomeadas, papéis de tipografia, layout com wireframes ASCII, alinhamento e princípios); depois revisar o plano contra o briefing, corrigir escolhas genéricas, e só então construir — observando especificidade de CSS, especialmente em espaçamento de seção.
8. **Atingir um piso de qualidade e autocriticar:** cobrir layouts responsivos, estados de foco visíveis, `prefers-reduced-motion`, acessibilidade e harmonia de cor; revisar screenshots e remover decoração desnecessária.

A skill lista clichês de design gerado por IA a evitar: fundos creme com acentos terracota, quase-preto com acentos neon, hairlines de jornal, cards SaaS arredondados idênticos, strings de metadado separadas por ponto médio, rótulos de dados em monospace e setas anexadas a links.

## Instalação e uso

Via marketplace de plugins do Claude Code:
```
/plugin marketplace add anthropics/skills
/plugin install example-skills@anthropic-agent-skills
```
ou em Claude.ai/Claude API conforme descrito na página do repositório [anthropics/skills](../../../../repos/github.com/anthropics/skills.md).

## Exemplos de uso

> Exemplos derivados da descrição publicada, não são instruções oficiais da skill.

- Redesenhar a home de um produto evitando o hero padrão de estatística com gradiente, partindo do vocabulário visual do setor do cliente.
- Revisar um plano de tokens de cor e tipografia antes de implementar, para eliminar escolhas genéricas antes de qualquer linha de CSS.

## Saídas esperadas

Um plano de tokens de design (cores nomeadas, papéis de tipografia, wireframes ASCII) revisado contra o briefing, seguido de uma implementação que atende a um piso de qualidade (responsividade, foco visível, acessibilidade, redução de movimento) e evita os clichês listados.

## Quando usar (e quando não usar)

- **Use quando:** quiser uma direção visual deliberada e ancorada no domínio do produto, com processo de duas passagens (planejar tokens, depois construir).
- **Evite quando:** precisar de um sistema de regras mais prescritivo e sorteado automaticamente — nesse caso, a família [taste-skill](../../../../repos/github.com/leonxlnx/taste-skill.md) (ex.: [Design Taste Frontend](../../leonxlnx/taste-skill/design-taste-frontend.md)) cobre esse caso com direção de arte sorteada e inspeção por screenshot.

## Limitações e cuidados

- `SKILL.md` cru foi lido via URL raw no commit registrado, mas o frontmatter indica uma licença própria em `LICENSE.txt` dentro da pasta da skill, não verificada diretamente nesta ingestão.
- Não há scripts ou recursos auxiliares listados além do próprio `SKILL.md` e do `LICENSE.txt`.

## Estado e adoção

- Versão: desconhecida.
- Preço/licença: Apache-2.0 (licença geral do repositório); a skill referencia um `LICENSE.txt` próprio não lido nesta ingestão.

## Relações

- Autor: [Anthropic (anthropics)](../../../../entities/anthropics.md).
- Conceitos: [Design taste para agentes](../../../../concepts/design-taste-para-agentes.md).
- Alternativas: [Design Taste Frontend](../../leonxlnx/taste-skill/design-taste-frontend.md) e demais skills da família [taste-skill](../../../../repos/github.com/leonxlnx/taste-skill.md); [pbakaus/impeccable](../../../../repos/github.com/pbakaus/impeccable.md).

## Perguntas abertas

- O que o `LICENSE.txt` específico da skill adiciona ou restringe em relação à licença Apache-2.0 geral do repositório?

## Fontes

- Página de origem: https://github.com/anthropics/skills/tree/main/skills/frontend-design (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/anthropics/skills, `SKILL.md` lido em https://raw.githubusercontent.com/anthropics/skills/dbd4588f9e1033efb41dad4bef2f7947c8993d44/skills/frontend-design/SKILL.md (commit `dbd4588f9e1033efb41dad4bef2f7947c8993d44`, consultado em 2026-10-19).
