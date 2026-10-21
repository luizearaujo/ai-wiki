---
type: concept
aliases: [Humanização de texto por IA, Remoção de sinais de IA, AI writing tells, Humanizer]
status: draft
created: 2026-10-19
updated: 2026-10-21
tags: [escrita, edicao-de-texto, agent-skills, llm, humanizacao]
---

# Humanização de texto gerado por IA

> Prática de editar prosa gerada por LLM para remover maneirismos reconhecíveis — contrastes formulaicos, tríades forçadas, inflação de importância, resíduos de chatbot — preservando o conteúdo e aproximando o texto da voz do autor.

## Definição

Humanização de texto gerado por IA é a **edição de estilo** de um texto produzido por modelo para que ele não carregue os sinais que um leitor associa a geração automática. Não é detecção de autoria, não é reescrita livre e não é uma garantia de que o texto "pareça humano": é um procedimento de revisão com critérios explícitos sobre o que cortar, o que preservar e o que não inventar.

O conceito se distingue de **detecção de IA**. Detectores tentam estimar probabilidade de autoria; a humanização parte do texto e melhora sua legibilidade, ritmo e especificidade. A confusão entre os dois usos é relevante: a mesma técnica pode servir para melhorar prosa ou para contornar políticas de atribuição, e a wiki trata a primeira finalidade como a documentada.

## Como funciona

Os métodos observados compartilham quatro movimentos:

1. **Inventariar.** Marcar no texto inteiro os padrões suspeitos, inclusive repetição entre parágrafos e não só dentro de frases.
2. **Classificar por força.** Alguns padrões justificam edição com uma ocorrência; outros, marcados como fracos isoladamente, só contam quando acompanhados de outros sinais. Isso evita caça às bruxas estilística.
3. **Reescrever preservando afirmações.** Nenhum fato, nome, número, data ou citação pode ser acrescentado. A regra vale para o texto e para a amostra de voz.
4. **Verificar.** Ler em voz alta, comparar com o original para detectar perda ou invenção e procurar padrões sobreviventes.

Os catálogos convergem em famílias de problemas:

| Família | O que aparece | Por que soa artificial |
| --- | --- | --- |
| Encenação | "não X, mas Y"; frases de efeito isoladas; preparação dramática | Cria tensão sem conteúdo novo, como um texto que se apresenta em vez de dizer. |
| Ritmo | tríades forçadas; aberturas repetidas; travessões em excesso; qualificadores empilhados | Uniformidade métrica e pontuação decorativa denunciam geração por probabilidade. |
| Inflação | palavras de estoque; importância inflada; autoridade emprestada; linguagem de vendas | Amplia a significance sem evidência proporcional. |
| Formatação | negrito decorativo; títulos a cada parágrafo; aspas curvas | Trata estrutura visual como substituto de hierarquia de ideias. |
| Resíduos | ressalvas de limite de conhecimento; menção ao próprio documento; repetição do título | Explicita o processo do modelo em vez do assunto. |
| Leitor errado | reexplicar o que o leitor já sabe; narrador distante | Assume um leitor genérico, não o leitor real. |

A noção de **amostra de voz** é central: quando existe texto do próprio autor, ele deve sobrepor as regras gerais. Sem amostra, o risco é trocar um padrão por outro — o "texto humanizado" vira um novo registro uniforme.

As três skills documentadas mostram variantes do mesmo método: o Humanizer enumera 26 padrões, atribui força a cada um e oferece modos de saída distintos; o Stop Slop reduz tudo a oito regras centrais, uma lista de checagens e uma nota de 1–10 em cinco dimensões, com corte em 35 de 50; o No AI Slop soma mais de 20 padrões específicos (contrastes binários, revelações por dois-pontos, finais de falso-profundo) e acrescenta um modo de detecção que só cita os padrões encontrados, sem veredito de autoria, e um modo satírico que gera slop de propósito como piada. O Humanizer é mais granular e conservador na decisão de editar; o Stop Slop é mais operacional e agressivo; o No AI Slop separa explicitamente "editar" de "detectar" como dois comandos distintos.

## Onde aparece

- [Humanizer](../skills/github.com/blader/humanizer/humanizer.md) — catálogo de 26 padrões em seis famílias, fluxo de quatro etapas e três modos de saída; deriva da página "Signs of AI writing" da Wikipédia.
- [Stop Slop](../skills/github.com/hardikpandya/stop-slop/stop-slop.md) — oito regras centrais, lista de checagens e pontuação de 1–10 em cinco dimensões, com corte em 35 de 50.
- [petergyang/no-ai-slop](../repos/github.com/petergyang/no-ai-slop.md) — mais de 20 padrões, com comando de edição, comando de detecção (só cita, não atribui autoria) e modo satírico; também disponível como plugin do ChatGPT.

## Trade-offs

- **Vantagens:** melhora legibilidade, ritmo e especificidade; remove muletas que escondem falta de conteúdo; dá ao autor um procedimento repetível em vez de intuição vaga; pode preservar voz quando há amostra.
- **Limitações:** a reescrita pode perder nuance, ironia ou incerteza; aplicar regras sem amostra pode uniformizar o estilo; heurísticas temporais ("texto anterior a 2022") não provam autoria; catálogos são empíricos e evoluem.
- **Risco de uso:** usar a técnica para burlar detecção ou atribuir autoria humana a conteúdo gerado desloca o problema de estilo para o de integridade. A wiki documenta o método, não endossa esse uso.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — formato de distribuição dos dois métodos; [CLAUDE.md](claude-md.md) — instruções persistentes de estilo podem cumprir papel semelhante, mas por sessão, não por tarefa.
- **Contrasta com:** detecção de texto gerado por IA, que produz um escore de autoria; e com edição livre, que não tem catálogo nem verificação de preservação de sentido.
- **Pré-requisito para:** usar skills de humanização em texto factual sem alterar afirmações — exige revisão humana do diff.

## Perguntas abertas

- Os catálogos de padrões são estáveis o suficiente para virar critério de qualidade editorial, ou envelhecem junto com os modelos?
- Como medir preservação de sentido e de voz sem uma avaliação humana cega?
- Qual é a diferença observável entre texto editado por skill e texto escrito por uma pessoa?
- Quando a humanização melhora a prosa e quando apenas troca um maneirismo por outro?
- Como conciliar a promessa de "não inventar fatos" com reescritas que reorganizam parágrafos inteiros?

## Fontes

- [Humanizer](../skills/github.com/blader/humanizer/humanizer.md) — página do skills.sh consultada em 2026-10-19 e metadados do repositório `blader/humanizer` no commit `8c307f367c91bd974002f10f2be2965d642c13df`. O `SKILL.md` cru não foi lido.
- [Stop Slop](../skills/github.com/hardikpandya/stop-slop/stop-slop.md) — página do skills.sh consultada em 2026-10-19 e metadados do repositório `hardikpandya/stop-slop` no commit `8da1f030185bdfe8471220585162991eaeb970e9`. O `SKILL.md` cru não foi lido.
- [petergyang/no-ai-slop](../repos/github.com/petergyang/no-ai-slop.md) — README no commit `000650b156983f5159695b441477f4e63b25dc85` (consultado em 2026-10-21). `SKILL.md` e `eval.md` não foram lidos.
- Wikipedia, "Signs of AI writing" — citada pelo Humanizer como origem do catálogo de padrões (não consultada diretamente nesta ingestão).
