---
type: skill
name: Full-Output Enforcement
slug: full-output-enforcement
url: https://www.skills.sh/leonxlnx/taste-skill/full-output-enforcement
source_url: https://github.com/leonxlnx/taste-skill
source_path: não localizado na árvore atual do repositório
author: leonxlnx
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [engenharia-de-agentes, completude, output, truncamento, agent-skills]
---

# Full-Output Enforcement

> Skill de comportamento que substitui a tendência de modelos a truncar respostas: exige entrega completa, proíbe placeholders e define como pausar e retomar quando o limite de tokens é atingido.

## O que é

`full-output-enforcement` não é uma skill de design. É uma instrução de processo para agentes, publicada no mesmo catálogo do pacote `taste-skill`, que trata toda tarefa como crítica de produção: uma saída parcial é uma saída quebrada.

O texto é curto (cerca de 2,3 mil caracteres) e tem quatro blocos: baseline, padrões de saída banidos, processo de execução e tratamento de saídas longas. A página o descreve como aplicável a "qualquer tarefa que exija saída exaustiva e integral".

## Como funciona

A skill define:

- **Baseline** — otimizar para completude, não brevidade. Se o pedido é um arquivo inteiro, entregar o arquivo inteiro; se são cinco componentes, entregar cinco.
- **Padrões banidos em código** — `// ...`, `// rest of code`, `// implement here`, `// TODO`, `/* ... */`, `// similar to above`, `// continue pattern`, `// add more as needed` e reticências soltas representando código omitido.
- **Padrões banidos em prosa** — "Let me know if you want me to continue", "for brevity", "the rest follows the same pattern", "and so on" no lugar de conteúdo real.
- **Atalhos estruturais banidos** — entregar esqueleto quando o pedido era implementação completa, mostrar só a primeira e a última seção, substituir lógica repetida por um exemplo e uma descrição, ou descrever o que o código deveria fazer em vez de escrevê-lo.
- **Processo** — escopar e contar os entregáveis, construir todos, e recontar antes de responder.
- **Saídas longas** — não comprimir nem pular para a conclusão; escrever com qualidade total até um ponto de corte limpo e encerrar com `[PAUSED — X of Y complete. Send "continue" to resume from: <seção>]`. Ao receber "continue", retomar exatamente de onde parou, sem recapitular.
- **Quick check** — confirmar ausência de padrões banidos, presença de todos os itens, código executável e nada encurtado para economizar espaço.

## Instalação e uso

```bash
npx skills add https://github.com/leonxlnx/taste-skill --skill full-output-enforcement
```

## Exemplos de uso

Exemplos derivados do conteúdo publicado, não instruções oficiais:

- **Geração de múltiplos arquivos:** contar os arquivos pedidos, entregar todos e conferir a contagem no final.
- **Resposta que atinge o limite:** parar no fim de uma função ou seção e emitir o marcador `[PAUSED — ...]`.
- **Revisão de código:** não substituir trechos repetidos por "(mesma lógica acima)".

## Saídas esperadas

Respostas completas, código executável sem placeholders e, quando necessário, uma pausa explícita com contagem de progresso e instrução de retomada.

## Quando usar (e quando não usar)

- **Use quando:** a tarefa exige saída integral e o modelo tende a resumir, elidir ou entregar esqueleto.
- **Evite quando:** o usuário pediu explicitamente um resumo, um recorte ou apenas as mudanças relevantes; a regra não deve transformar pedidos curtos em despejos.

## Limitações e cuidados

- Não foi possível localizar um `SKILL.md` correspondente na árvore atual do repositório, embora a página do catálogo publique o conteúdo; a origem exata do arquivo é **A verificar**.
- A skill não controla o limite de tokens do harness: o marcador de pausa depende de o agente reconhecer o limite antes de truncar.
- Pode conflitar com instruções de concisão do sistema ou do usuário.
- O comando de instalação publicado continua apontando para `leonxlnx/taste-skill`.

## Estado e adoção

- Versão: **desconhecida**.
- Instalações observadas em 2026-10-19: **401.008**, primeira aparição em 1º de março de 2026.
- Auditorias publicadas: Gen Agent Trust Hub, Socket e Snyk com "Pass".
- Repositório: 99.159 estrelas, 6.743 forks, 2 issues abertas; licença MIT; JavaScript.

## Relações

- Autor: [Leon Lin](../../../../entities/leonxlnx.md).
- Conceito: [Saída completa de agente](../../../../concepts/saida-completa-de-agente.md).
- Família de publicação: [Design Taste Frontend](design-taste-frontend.md) (mesmo catálogo, domínio diferente).

## Perguntas abertas

- Onde está o `SKILL.md` desta skill no repositório atual?
- O marcador de pausa é reconhecido automaticamente por algum harness?
- A regra tem efeito mensurável na taxa de truncamento?
- Como reconciliar a exigência de completude com limites de contexto?

## Fontes

- Página de origem: https://www.skills.sh/leonxlnx/taste-skill/full-output-enforcement (consultada em 2026-10-19); `SKILL.md` renderizado na página.
- Repositório-fonte: https://github.com/leonxlnx/taste-skill (metadados e árvore via API do GitHub, commit `b9ca2fd8047f4c72d7da90ebc1c1203e57c72cd2`, consultados em 2026-10-19); o repositório não foi clonado e o `SKILL.md` cru não foi lido.
