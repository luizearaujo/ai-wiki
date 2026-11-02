---
type: repo
url: https://github.com/amosblomqvist/learnharness
host: github.com
owner: amosblomqvist
repo: learnharness
commit: e69e85269c064c6c9c49a8b06ae78c06e79c4a63
license: AGPL-3.0
language: TypeScript
status: active
created: 2026-11-02
ingested: 2026-11-02
updated: 2026-11-02
tags: [harness, educacao, aprendizado, grafo-de-conhecimento, tutoria, on-device]
---

# amosblomqvist/learnharness

> Harness de agente para aprender assuntos difíceis: avalia o conhecimento atual do usuário, mapeia o caminho até o objetivo, ensina em etapas incrementais e reforça com exercícios adaptativos — tudo persistido em grafo de conhecimento local.

## O que é

LearnHarness é uma plataforma educacional orientada por agentes que personaliza o aprendizado a partir do estado atual do usuário. A proposta é tratar o processo de aprender como um problema de planejamento agêntico: o agente não entrega um currículo fixo, mas traça a rota mínima do ponto atual ao objetivo declarado.

O README descreve quatro fases:

| Fase | O que acontece |
|---|---|
| **Measurement** | O agente avalia o conhecimento existente antes de qualquer instrução |
| **Planning** | Cria um mapa de dependências mostrando o caminho do estado atual ao objetivo |
| **Teaching** | Cada etapa da lição constrói sobre a anterior, com explicações e verificações de compreensão |
| **Practice** | Exercícios adaptativos reforçam o conhecimento sem prompt explícito do usuário |

O diferencial em relação a tutores LLM convencionais é o **grafo de conhecimento persistente**: proposições aprendidas e cadeias de raciocínio ficam armazenados entre sessões, permitindo que futuras interações partam do que já foi consolidado, não do zero.

O usuário pode "pensar em voz alta" — por digitação ou dictation — para que o agente entenda o raciocínio por trás de cada resposta, e não apenas se a resposta está certa ou errada.

## Como funciona

A arquitetura é orientada por agente: não há currículo pré-fabricado. O mapa de dependências é gerado sob medida para cada objetivo e estado inicial. A persistência é em grafo local (não em nuvem do fornecedor), armazenado como arquivos inspecionáveis — proposições e cadeias de raciocínio são entidades do grafo, não logs de conversa.

O modelo de IA é **configurado pelo próprio usuário**, sem markup ou assinatura do LearnHarness:
- Claude
- Endpoints compatíveis com OpenAI
- Modelos locais
- Integração por CLI

## Instalação e uso rápido

Disponível para download direto em [learnharness.ai](https://learnharness.ai):

- macOS (Apple Silicon)
- Windows (x64)
- Linux (x64)

**A verificar:** instrução de instalação via linha de comando, formatos de exportação do grafo e suporte a múltiplos objetivos em paralelo — o README não cobre esses detalhes.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é aprender um assunto técnico difícil de forma sistemática; você prefere usar seu próprio provider de modelo (Claude, OpenAI-compatible, local) sem custo adicional de plataforma; quer que o progresso persista entre sessões sem depender de nuvem de terceiro.
- **Evite quando:** o objetivo é aprender fazendo (project-based learning) em vez de conceitos sequenciais; o fluxo de trabalho exige integração direta com IDEs ou pipelines de código — o LearnHarness é um harness de aprendizado, não de desenvolvimento.

## Limitações e cuidados

- Somente o README foi lido; código-fonte, documentação interna e formatos do grafo de conhecimento não foram verificados.
- **A verificar:** como o grafo lida com conceitos contraditórios ou atualizações de conteúdo após o modelo de IA mudar de opinião; capacidade de exportar ou auditar o grafo acumulado.
- Licença AGPL-3.0: qualquer software derivado ou que use o código como biblioteca precisa ser aberto sob a mesma licença.
- Projeto recente (criado em 2026-10-16); a estabilidade das APIs internas e o ritmo de manutenção ainda são desconhecidos.

## Estado e adoção

- Último push: 2026-10-31.
- Observado em 2026-11-02: ~4.913 stars, ~759 forks, ~358 issues abertas; criado em 2026-10-16.
- Licença: AGPL-3.0.
- Linguagem principal: TypeScript.

## Relações

- Mantido por: [amosblomqvist](../../../entities/amosblomqvist.md)
- Conceitos: [Agent harness](../../../concepts/agent-harness.md), [Memória de agente](../../../concepts/memoria-de-agente.md)

## Fontes

- README: https://raw.githubusercontent.com/amosblomqvist/learnharness/e69e85269c064c6c9c49a8b06ae78c06e79c4a63/README.md (commit `e69e85269c064c6c9c49a8b06ae78c06e79c4a63`, consultado em 2026-11-02). Somente o README foi lido.
- Metadados: API do GitHub em 2026-11-02.
