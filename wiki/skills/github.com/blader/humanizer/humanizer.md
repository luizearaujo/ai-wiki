---
type: skill
name: Humanizer
slug: humanizer
url: https://www.skills.sh/blader/humanizer/humanizer
source_url: https://github.com/blader/humanizer
source_path: SKILL.md
author: blader
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [escrita, humanizacao, edicao-de-texto, agent-skills, claude-code]
---

# Humanizer

> Skill que reescreve texto com marcas de escrita gerada por IA para que ele soe como o autor, sem alterar o conteúdo — usando um catálogo de 26 padrões organizados em seis famílias.

## O que é

Humanizer é uma [agent skill](../../../../concepts/agent-skills.md) publicada por [blader](../../../../entities/blader.md) no repositório `blader/humanizer` e distribuída pelo catálogo skills.sh. Ela resolve um problema específico de edição: texto produzido por LLM costuma carregar maneirismos reconhecíveis — contrastes "não é X, é Y", frases de efeito isoladas, tríades forçadas, inflação de importância, palavras de estoque e formatação decorativa — que fazem o leitor perceber o gerador antes do argumento.

O objetivo declarado é **remover os sinais sem mudar o que o texto diz**: reescrever para que pareça escrito por uma pessoa para um leitor e um assunto, não gerado por previsão estatística. A skill não é um detector de IA nem um reescritor genérico; é um procedimento de edição com critérios explícitos para decidir o que cortar.

A página de origem apresenta o material como o conteúdo do `SKILL.md`; o arquivo cru não foi lido nesta ingestão e o repositório não foi clonado.

## Como funciona

O método se apoia em uma distinção: um modelo escreve o que é mais provável em seguida; um autor humano escolhe para **um leitor e um assunto**. O teste central é "toda frase mantida precisa acrescentar algo que o leitor ainda não tinha". Um padrão pesa mais quando um escritor cuidadoso raramente o usaria de propósito.

O fluxo tem quatro etapas:

1. **Marcar os sinais** no texto inteiro, incluindo repetição no nível do parágrafo.
2. **Rascunhar a reescrita**, preservando toda afirmação sustentada. Não introduzir fatos, nomes, números, datas, citações ou referências ausentes da fonte ou do usuário; ficção é exceção.
3. **Conferir o rascunho** lendo em voz alta, procurando afirmações adicionadas ou perdidas e sinais sobreviventes — com atenção especial aos padrões mais fortes.
4. **Escrever a versão final**, variando o comprimento das frases e reescrevendo o parágrafo se alguma frase continuar desajeitada.

O catálogo de padrões é organizado em seis famílias:

| Família | Padrões | Exemplos |
| --- | --- | --- |
| A. Encenação | §1–§5 | "não X, mas Y"; frases de efeito isoladas; ditos pseudo-profundos; preparação dramática; discussão com interlocutor inexistente. |
| B. Ritmo | §6–§11 | tríades forçadas; aberturas de frase repetidas; excesso de travessões; qualificadores empilhados; pares hifenizados desnecessários; voz passiva e sujeitos ausentes. |
| C. Inflação | §12–§18 | palavras de estoque de IA; importância inflada; associação vaga; orações "-ando/-endo" rasas; linguagem de vendas; autoridade emprestada; evitar "é", "são" e "tem". |
| D. Formatação | §19–§21 | negrito decorativo; títulos decorativos; aspas curvas. |
| E. Resíduos | §22–§25 | resíduo de chatbot; ressalvas sobre limite de conhecimento e suposições; título repetido na primeira frase; texto sobre o documento em vez do assunto. |
| F. Leitor errado | §26 | reexplicar contexto que o leitor já tem. |

Os padrões §1 a §5 e §6 justificam uma edição com uma única ocorrência; os marcados como "fracos sozinhos" precisam de apoio de outros sinais próximos. A skill inclui limites: não alterar frases observadas em citações, títulos, nomes próprios ou passagens que discutem a própria frase; saudação e despedida são aceitáveis; texto anterior a 30 de novembro de 2022 é tratado como não gerado por IA. Detalhes que carregam voz — especificidades incomuns, sentimentos mistos, referências datadas, escolhas em primeira pessoa e apartes genuínos — devem ser preservados.

Há três modos de saída: **texto colado** (rascunho, padrões restantes e reescrita final), **arquivo** (somente a prosa final, preservando código, comandos, caminhos, metadados YAML, dados e alvos de link) e **embutido** (apenas o texto final). Se o usuário fornecer uma amostra de escrita, ela vence as regras: a skill deve imitar comprimento de frase, vocabulário, pontuação, aberturas e transições, inclusive a restrição a travessões.

## Instalação e uso

Comando publicado na página de origem:

```bash
npx skills add https://github.com/blader/humanizer --skill humanizer
```

A página também oferece uma invocação sem instalação permanente, via `npx skills use`. A instalação é cross-platform; não há versão publicada nem instruções separadas de escopo por projeto ou global na página.

## Exemplos de uso

Os prompts abaixo são **exemplos derivados da descrição publicada**, não instruções oficiais da skill.

- **Texto colado:** "Reescreva este post removendo os sinais de escrita por IA. Mantenha todas as afirmações, não invente fatos e mostre o rascunho, os padrões que restaram e a versão final."
- **Arquivo de documentação:** "Edite `README.md` no modo arquivo: devolva só a prosa final e preserve blocos de código, caminhos e metadados."
- **Com amostra de voz:** "Use os três textos anteriores como amostra de estilo e reescreva este e-mail no mesmo ritmo e vocabulário, sem mudar o conteúdo."

## Saídas esperadas

- texto reescrito sem os padrões catalogados;
- preservação das afirmações, dos dados e da intenção do original;
- no modo colado, visibilidade dos padrões encontrados e do que restou;
- no modo arquivo, apenas a prosa alterada, com código e metadados intactos.

A página alerta que "remover os sinais é metade do trabalho": o resultado precisa continuar soando como uma pessoa. **A verificar:** o texto integral do `SKILL.md`, os critérios exatos de cada um dos 26 padrões e como a skill lida com textos longos.

## Quando usar (e quando não usar)

- **Use quando:** você tem um texto funcional e quer remover maneirismos de IA mantendo o conteúdo — posts, ensaios, documentação, e-mails.
- **Use quando:** existe uma amostra de escrita do autor e o objetivo é aproximar o texto dessa voz.
- **Evite quando:** o objetivo é burlar detecção de IA ou atribuir autoria humana a conteúdo gerado — a skill edita estilo, não resolve questões de integridade.
- **Evite quando:** o texto é jurídico, técnico ou factual e qualquer reescrita pode alterar precisão; nesses casos, revise manualmente ou use o modo arquivo com revisão linha a linha.
- **Evite quando:** você espera um detector de IA; a skill produz uma reescrita, não um veredito de autoria.

## Limitações e cuidados

- **Preservação de sentido depende do modelo.** A instrução de não inventar fatos é explícita, mas a reescrita ainda pode perder nuances, ironia ou incerteza epistêmica.
- **Risco de uniformizar a voz.** Aplicar as regras sem amostra pode produzir outro estilo padronizado — o oposto do objetivo. A própria skill reconhece que a amostra deve vencer as regras.
- **Heurística temporal.** "Texto anterior a 30 de novembro de 2022 não é de IA" vale para o ChatGPT público, não para todos os geradores; é um atalho, não uma prova.
- **Origem dos padrões.** O catálogo deriva da página "Signs of AI writing" da Wikipédia e de revisões de texto gerado por IA; é uma lista empírica e evolutiva, não uma taxonomia científica.
- **Conteúdo não verificado.** O `SKILL.md` cru e o validador `scripts/validate-package.py` não foram lidos; regras internas podem divergir do resumo publicado.
- **Supply chain.** Instalar a skill coloca instruções de terceiros no agente; revise o conteúdo antes de usar em contexto sensível.

## Estado e adoção

- **Versão da skill:** não publicada na página de origem (observada em 2026-10-19).
- **Catálogo:** 9,8 mil instalações (9.831 nos dados estruturados), 58,1 mil estrelas, primeira aparição em 2026-01-20 (observado em 2026-10-19).
- **Auditorias de terceiros:** Gen Agent Trust Hub, Socket e Snyk com resultado "Pass" (observado em 2026-10-19); critérios não verificados nesta wiki.
- **Repositório-fonte:** MIT, linguagem principal Python, ~58,3 mil estrelas e ~4,6 mil forks na API do GitHub; último push em 2026-10-16, no commit `8c307f367c91bd974002f10f2be2965d642c13df`.
- **Preço:** gratuito.

## Relações

- **Autor:** [blader](../../../../entities/blader.md) — Siqi Chen.
- **Repositório-fonte:** [blader/humanizer](https://github.com/blader/humanizer), com `SKILL.md` na raiz e empacotamento para plugins de Claude e Cursor.
- **Conceitos:** [Agent skills](../../../../concepts/agent-skills.md) — formato de distribuição; [Humanização de texto gerado por IA](../../../../concepts/humanizacao-de-texto-por-ia.md) — prática que a skill operacionaliza.
- **Alternativas:** Stop Slop (`hardikpandya/stop-slop`) — abordagem próxima com regras centrais, referências e pontuação de 1–10 por dimensão.

## Perguntas abertas

- Como a skill decide entre os modos colado, arquivo e embutido quando a instrução não é explícita?
- Os 26 padrões têm pesos diferentes na prática, ou todos entram como lista de verificação?
- Como a skill evita introduzir fatos ao reescrever textos densos em dados?
- A amostra de voz realmente sobrepõe todas as regras, inclusive quando contém padrões catalogados?
- Qual é a taxa de preservação de sentido observada em avaliações independentes?

## Fontes

- Página de origem: https://www.skills.sh/blader/humanizer/humanizer (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/blader/humanizer (metadados e árvore consultados via API do GitHub em 2026-10-19; commit `8c307f367c91bd974002f10f2be2965d642c13df`). O repositório não foi clonado e o `SKILL.md` cru não foi lido.
