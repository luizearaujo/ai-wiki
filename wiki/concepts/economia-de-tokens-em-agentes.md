---
type: concept
aliases: [Token reduction, Token efficiency, Compressão de contexto, Caveman-style output, Economia de contexto]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [tokens, contexto, custo, agentes, compressao, eficiencia]
---

# Economia de tokens em agentes

> Conjunto de técnicas que reduzem o custo de uma sessão de agente — tokens de entrada, de saída ou ambos — sem degradar a qualidade da tarefa.

## Definição

Economia de tokens é o desenho deliberado do que o agente **lê**, do que ele **escreve** e de **qual modelo** usa, com o objetivo de reduzir custo e latência. Distingue-se de otimização de modelo: não altera pesos nem a arquitetura, apenas as informações que entram e saem do contexto e o esforço computacional por solicitação.

A economia aparece em duas frentes:

- **Tokens de entrada:** logs, JSON, CSV, saída de testes, páginas web e arquivos de memória podem ser comprimidos antes de chegar ao modelo.
- **Tokens de saída:** respostas mais curtas, sem preâmbulos, repetições ou conversa entre chamadas de ferramenta.

Em modelos cobrados por token, a redução se converte diretamente em custo. Em planos com preço por solicitação, o efeito é menor ou nulo.

## Como funciona

### Mecanismos observados

| Mecanismo | O que reduz | Exemplo documentado |
|---|---|---|
| **Voz comprimida** | Tokens de saída | Resposta de 63 para 20 tokens; variantes mais agressivas chegam a 13. |
| **Compressão de entrada** | Tokens lidos | 82,4% de redução nos arquivos de teste e 33,2% por sessão completa. |
| **Roteamento de modelo e esforço** | Custo por tarefa | Escolher modelo e nível de esforço por pergunta; 54% mais barato que um modelo forte em esforço máximo. |
| **Code mode / scripts reutilizáveis** | Saída de ferramentas | Um script guardado reduz a leitura de 397 para 76 tokens por execução de testes. |
| **Compressão de páginas web** | Contexto de navegação | Uma tabela de 200 linhas caiu de 15.704 para 121 tokens. |
| **Compressão de arquivos de memória** | Contexto persistente | `CLAUDE.md` e similares reduzidos entre 22,8% e 49,1%, preservando títulos, código e caminhos. |

### Regras que preservam a qualidade

As implementações sérias mantêm restrições explícitas:

- **Payload literal:** código, comandos, caminhos e mensagens de erro não são reescritos.
- **Semântica intacta:** negações, números e unidades permanecem exatos.
- **Exceções de segurança:** avisos de risco, ações irreversíveis e usuários confusos recebem texto completo.
- **Prompt do usuário intocado:** comprimir a pergunta piora a resposta, segundo evidência citada pelo `caveman`.
- **Código inalterado:** a compressão atua na prosa e nas leituras, não no código entregue.

### Evidência externa citada

O README do `caveman` cita três avaliações independentes: Adobe Research (custo 1,4–2,4× menor), JetBrains (sem perda mensurável de qualidade, p = 0,82) e Elastic (63,6% menos tokens de resposta). Esses números são **citados pela fonte e não foram verificados** por esta wiki.

## Onde aparece

- [juliusbrussee/caveman](../repos/github.com/juliusbrussee/caveman.md) — implementação mais completa: voz, compressão de entrada, roteamento, blocks, compressão de memória e browser.
- [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — grafo de código consultável como alternativa a reler arquivos.
- [DeusData/codebase-memory-mcp](../repos/github.com/deusdata/codebase-memory-mcp.md) — servidor MCP que reivindica cerca de 120× menos tokens ao responder perguntas estruturais.
- [Egonex-AI/Understand-Anything](../repos/github.com/egonex-ai/understand-anything.md) — grafo interativo que substitui leitura repetida de código por consultas.
- [Ponytail](../repos/github.com/dietrichgebert/ponytail.md) — reduz tokens como efeito colateral de escrever menos código.

## Trade-offs

- **Vantagens:** menor custo por sessão, menor latência, mais tarefas dentro da janela de contexto, menos ruído para o modelo e possível melhora de foco.
- **Limitações:** compressão agressiva pode remover informação necessária; respostas telegráficas são piores para leitura humana; o ganho depende do modelo de cobrança; medir qualidade exige avaliação pareada; compressão de entrada pode introduzir erros silenciosos.
- **Critério prático:** comprimir primeiro o que é volumoso e redundante — logs, JSON, saída de testes, páginas — e preservar integralmente código, comandos, caminhos e avisos de segurança.

## Relações

- **Relacionado a:** [Grafo de conhecimento de código](grafo-de-conhecimento-de-codigo.md) — consultar um índice estrutural evita reler arquivos; [Atenção esparsa para contexto longo](atencao-esparsa-para-contexto-longo.md) — reduz o custo computacional de contextos longos no lado do modelo; [Agent harness](agent-harness.md) — o harness decide o que entra no contexto e como ferramentas retornam dados; [YAGNI para agentes](yagni-para-agentes.md) — escrever menos código também reduz sessões e custo.
- **Contrasta com:** abordagens que aumentam o contexto para melhorar a resposta, aceitando o custo como necessário.
- **Pré-requisito para:** operar agentes em sessões longas com orçamento limitado e manter a qualidade mensurável.

## Perguntas abertas

- Quanto da redução de tokens se traduz em economia real em planos por assinatura?
- Qual é o limiar de compressão a partir do qual a qualidade cai de forma mensurável?
- Como avaliar perda de informação em logs e JSON comprimidos de forma automática?
- A compressão de arquivos de memória (`CLAUDE.md`) preserva o efeito comportamental das instruções?
- O ganho se sustenta em tarefas de raciocínio longo ou apenas em respostas factuais curtas?

## Fontes

- README de [juliusbrussee/caveman](../repos/github.com/juliusbrussee/caveman.md) no commit `bad48a0e1df55e05e3f52249afa35ecc1909ee76` (consultado em 2026-10-19). Somente o README foi lido.
- README de [dietrichgebert/ponytail](../repos/github.com/dietrichgebert/ponytail.md) no commit `09c434ab73ca43761c5d8b0c5d341926c2fba710` (consultado em 2026-10-19).
- Números de Adobe Research, JetBrains e Elastic conforme citados pelo README do `caveman`; não verificados.
