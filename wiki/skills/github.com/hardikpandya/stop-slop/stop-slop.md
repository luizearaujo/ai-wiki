---
type: skill
name: Stop Slop
slug: stop-slop
url: https://www.skills.sh/hardikpandya/stop-slop/stop-slop
source_url: https://github.com/hardikpandya/stop-slop
source_path: SKILL.md
author: hardikpandya
version: desconhecida
license: MIT
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [escrita, humanizacao, edicao-de-texto, agent-skills]
---

# Stop Slop

> Skill que remove maneirismos previsíveis de escrita gerada por IA com oito regras centrais, listas de checagem e uma nota de 1–10 em cinco dimensões.

## O que é

Stop Slop é uma [agent skill](../../../../concepts/agent-skills.md) publicada por [hardikpandya](../../../../entities/hardikpandya.md) no repositório `hardikpandya/stop-slop` e distribuída pelo catálogo skills.sh. Ela orienta o agente a revisar prosa — ao redigir, editar ou revisar — para eliminar padrões que denunciam geração automática.

Enquanto o [Humanizer](../../blader/humanizer/humanizer.md) organiza um catálogo extenso de 26 padrões, o Stop Slop aposta em **oito regras centrais** e em uma lista curta de checagens antes da entrega. O foco é operacional: cortar enchimento, dar sujeito humano às frases, nomear o concreto, aproximar o leitor e variar o ritmo — e então pontuar o resultado.

O repositório é enxuto: `SKILL.md` na raiz, `README.md`, `CHANGELOG.md`, licença e três referências (`phrases.md`, `structures.md`, `examples.md`). O `SKILL.md` cru e as referências não foram lidos nesta ingestão; o resumo abaixo reflete o que a página do skills.sh publica.

## Como funciona

As oito regras declaradas são:

1. **Cortar frases de enchimento.** Remover abertura protocolar, muletas de ênfase e advérbios.
2. **Quebrar estruturas formulaicas.** Evitar contrastes binários, listas negativas, fragmentação dramática, preparação retórica e falsa agência.
3. **Usar voz ativa.** Dar a cada frase um sujeito humano que pratica a ação; evitar passivas e objetos inanimados executando verbos humanos (por exemplo, "a reclamação vira uma correção").
4. **Ser específico.** Substituir declarações vagas ("as razões são estruturais") pelo concreto; evitar extremos vagos como "todo", "sempre" e "nunca".
5. **Colocar o leitor na sala.** Evitar narrador distante; preferir "você" a "as pessoas" e concretude a abstração.
6. **Variar o ritmo.** Misturar comprimentos de frase, preferir listas de dois itens a tríades, terminar parágrafos de formas diferentes e evitar travessões.
7. **Confiar no leitor.** Dizer o fato direto; dispensar suavização, justificativa e condução pela mão.
8. **Cortar frases citáveis.** Reescrever qualquer trecho com cara de pull-quote.

Antes de entregar, a skill propõe uma lista de checagens: eliminar advérbios; converter passivas; nomear a pessoa quando um inanimado pratica verbo humano; reestruturar frases iniciadas por pronome interrogativo; remover "aqui está o que/isto/aquilo"; trocar "não é X, é Y" por uma afirmação direta de Y; quebrar três frases consecutivas de comprimento igual; variar parágrafos que terminam em frase de efeito; remover travessões; substituir declarações vagas pela implicação específica; colocar o leitor na cena; e apagar meta-conectores como "o resto deste ensaio".

A avaliação usa cinco dimensões, cada uma de 1 a 10:

| Dimensão | Pergunta |
| --- | --- |
| Diretividade (Directness) | O texto afirma ou rodeia? |
| Ritmo (Rhythm) | As frases variam e os parágrafos terminam de formas diferentes? |
| Confiança (Trust) | O texto trata o leitor como capaz de acompanhar? |
| Autenticidade (Authenticity) | A voz parece de uma pessoa, não de um template? |
| Densidade (Density) | Cada frase acrescenta informação? |

Um total abaixo de **35 de 50** indica que o texto precisa de revisão. A skill oferece exemplos de antes e depois em `references/examples.md`.

## Instalação e uso

Comando publicado na página de origem:

```bash
npx skills add https://github.com/hardikpandya/stop-slop --skill stop-slop
```

A instalação é cross-platform; versão e escopo (projeto ou global) não são publicados na página. O comando instala apenas o `SKILL.md` e, presumivelmente, as referências do repositório-fonte — **a verificar**, pois a página não detalha o que o CLI copia.

## Exemplos de uso

Os prompts abaixo são **exemplos derivados da descrição publicada**, não instruções oficiais da skill.

- **Revisão antes de publicar:** "Revise este artigo com o Stop Slop, aplique as oito regras e dê uma nota de 1 a 10 em diretividade, ritmo, confiança, autenticidade e densidade. Se o total ficar abaixo de 35, mostre o que revisar."
- **Rascunho:** "Escreva a introdução deste relatório e depois passe o Stop Slop: sem enchimento, sem tríades forçadas, sem travessões, voz ativa e exemplos concretos."
- **Diagnóstico:** "Aponte os trechos que soam gerados por IA e explique qual regra cada um viola antes de reescrever."

## Saídas esperadas

- prosa revisada segundo as oito regras;
- lista de violações ou de mudanças aplicadas, quando solicitada;
- pontuação nas cinco dimensões e decisão de revisar se o total for menor que 35;
- exemplos antes/depois quando o material de referência é acionado.

**A verificar:** o texto integral do `SKILL.md`, o conteúdo de `phrases.md` e `structures.md`, e se a skill sempre aplica a pontuação ou apenas quando pedida.

## Quando usar (e quando não usar)

- **Use quando:** você quer uma revisão rápida e opinativa de prosa com critérios claros e uma nota final.
- **Use quando:** o texto é um rascunho e você quer enxugar enchimento, passivas e estruturas formulaicas antes de editar a fundo.
- **Evite quando:** o texto é jurídico, técnico ou factual e a reescrita pode alterar precisão; a skill corta agressivamente e não promete preservação literal.
- **Evite quando:** você precisa de um catálogo detalhado de padrões com análise de força por ocorrência — o Humanizer cobre isso com mais granularidade.
- **Evite quando:** o objetivo é burlar detecção de IA; a skill é de edição de estilo, não de atribuição de autoria.

## Limitações e cuidados

- **Reescrita agressiva.** Regras como "eliminar advérbios" e "cortar frases citáveis" podem remover nuance legítima; a aplicação literal empobrece texto que já era bom.
- **Pontuação subjetiva.** As cinco dimensões não têm rubrica pública detalhada; dois revisores podem chegar a notas diferentes para o mesmo texto.
- **Preferências estilísticas apresentadas como regra.** "Evitar travessões", "preferir listas de dois itens" e "não terminar com frase de efeito" são escolhas de estilo, não consensos editoriais.
- **Referências não verificadas.** `phrases.md`, `structures.md` e `examples.md` existem na árvore do repositório, mas não foram lidos; a lista de frases e estruturas pode ser mais ampla do que a página resume.
- **Sem versão publicada.** A página não informa versão da skill; o `CHANGELOG.md` do repositório não foi lido.
- **Supply chain.** Instalar a skill adiciona instruções de terceiros ao agente; revise o conteúdo antes de usar em contexto sensível.

## Estado e adoção

- **Versão da skill:** não publicada na página de origem (observada em 2026-10-19).
- **Catálogo:** 17,5 mil instalações (17.456 nos dados estruturados), 18,1 mil estrelas, primeira aparição em 2026-01-20 (observado em 2026-10-19).
- **Auditorias de terceiros:** Gen Agent Trust Hub, Socket e Snyk com resultado "Pass" (observado em 2026-10-19); critérios não verificados nesta wiki.
- **Repositório-fonte:** MIT, ~18,1 mil estrelas e ~1,3 mil forks na API do GitHub; criado em 2026-01-11, último push em 2026-03-17, no commit `8da1f030185bdfe8471220585162991eaeb970e9`. A API não informa linguagem principal.
- **Preço:** gratuito.

## Relações

- **Autor:** [hardikpandya](../../../../entities/hardikpandya.md) — Hardik Pandya, Head of Design na Atlassian.
- **Repositório-fonte:** [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop).
- **Conceitos:** [Agent skills](../../../../concepts/agent-skills.md) — formato de distribuição; [Humanização de texto gerado por IA](../../../../concepts/humanizacao-de-texto-por-ia.md) — prática que a skill operacionaliza.
- **Alternativas:** [Humanizer](../../blader/humanizer/humanizer.md) — catálogo de 26 padrões com três modos de saída; estilos de guia editorial tradicionais (por exemplo, manuais de redação), que não são skills.

## Perguntas abertas

- A pontuação de 1–10 por dimensão tem rubrica objetiva, ou é calibrada pelo modelo?
- Como a skill equilibra "cortar agressivamente" com "preservar afirmações" em textos factuais?
- As listas `phrases.md` e `structures.md` são mais extensas que as oito regras e os exemplos resumidos?
- Qual é a diferença prática entre Stop Slop e Humanizer em um mesmo texto — velocidade, agressividade, preservação de voz?
- A skill foi pensada para prosa em inglês; como se comporta em português?

## Fontes

- Página de origem: https://www.skills.sh/hardikpandya/stop-slop/stop-slop (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/hardikpandya/stop-slop (metadados e árvore consultados via API do GitHub em 2026-10-19; commit `8da1f030185bdfe8471220585162991eaeb970e9`). O repositório não foi clonado e o `SKILL.md` cru não foi lido.
