---
type: skill
name: Agent DX CLI Scale
slug: agent-dx-cli-scale
url: https://www.skills.sh/google-labs-code/design.md/agent-dx-cli-scale
source_url: https://github.com/google-labs-code/design.md
source_path: .agents/skills/agent-dx-cli-scale/SKILL.md
author: google-labs-code
version: desconhecida
license: Apache-2.0
status: active
created: 2026-10-19
updated: 2026-10-19
tags: [cli, agent-dx, avaliacao, design-de-ferramentas, seguranca, agent-skills]
---

# Agent DX CLI Scale

> Skill que avalia qualquer CLI em sete eixos de design agent-first, com pontuação de 0 a 3 por eixo e um total de 0 a 21 que classifica a ferramenta de "human-only" a "agent-first".

## O que é

Agent DX CLI Scale é uma [agent skill](../../../../concepts/agent-skills.md) publicada por [google-labs-code](../../../../entities/google-labs-code.md) no repositório `google-labs-code/design.md` e distribuída pelo catálogo skills.sh. Ela entrega ao agente um **instrumento de avaliação**: em vez de reescrever uma CLI por intuição, o agente percorre sete critérios objetivos e atribui notas com critérios de aceitação para cada nível.

A tese publicada separa duas otimizações: *human DX* prioriza descoberta e tolerância a erro; *agent DX* prioriza **previsibilidade e defesa em profundidade**. A skill cita "You Need to Rewrite Your CLI for AI Agents" como origem da distinção.

O conteúdo desta página vem do `SKILL.md` renderizado na página do skills.sh. O arquivo cru no repositório não foi buscado e o repositório não foi clonado. O README de `design.md` não menciona a skill; o diretório correspondente é `.agents/skills/agent-dx-cli-scale/`.

## Como funciona

Sete eixos recebem nota de 0 a 3:

| Eixo | Pergunta central | Nível 3 (resumo) |
| --- | --- | --- |
| **1. Saída legível por máquina** | O agente consegue parsear a saída sem heurísticas? | NDJSON para resultados paginados; saída estruturada por padrão fora de TTY. |
| **2. Entrada de payload cru** | O agente consegue enviar o payload da API sem tradução? | Payload cru é cidadão de primeira classe ao lado de flags; o schema da API serve de documentação. |
| **3. Introspecção de schema** | O agente descobre o que a CLI aceita em runtime? | Schemas resolvidos em runtime, incluindo escopos, enums e tipos aninhados. |
| **4. Disciplina de contexto** | A CLI ajuda a limitar o tamanho da resposta? | Paginação por stream em NDJSON e orientação explícita sobre field masks. |
| **5. Endurecimento de entrada** | A CLI defende contra falhas típicas de agentes — alucinação, não erro de digitação? | Rejeita caracteres de controle, `../`, `%2e`, `?` e `#`; sandbox de caminho de saída; postura "o agente não é um operador confiável". |
| **6. Trilhos de segurança** | O agente consegue validar antes de agir? As respostas são sanitizadas? | `--dry-run` em todas as mutações e sanitização de resposta contra prompt injection embutida em dados. |
| **7. Empacotamento de conhecimento** | A CLI entrega conhecimento em formato consumível pelo agente? | Biblioteca de skills com guardrails, versionada e descoberta por padrão como OpenClaw. |

O total é interpretado em quatro faixas:

| Faixa | Classificação | Leitura |
| --- | --- | --- |
| 0–5 | Human-only | Agentes terão dificuldade de parsear, alucinarão entradas e não terão trilhos de segurança. |
| 6–10 | Agent-tolerant | Funciona, mas desperdiça tokens, comete erros evitáveis e exige muito prompt engineering. |
| 11–15 | Agent-ready | I/O estruturado, validação e alguma introspecção; restam lacunas. |
| 16–21 | Agent-first | Introspecção completa, endurecimento, trilhos de segurança e conhecimento empacotado. |

Além da nota, a skill pede uma observação qualitativa de **prontidão multi-superfície**, não pontuada: MCP via stdio JSON-RPC, instalação como extensão/plugin e autenticação headless por variáveis de ambiente. São sinais de que a mesma CLI serve o agente por mais de um caminho.

## Instalação e uso

Comando publicado na página de origem:

```bash
npx skills add https://github.com/google-labs-code/design.md --skill agent-dx-cli-scale
```

A página também oferece invocação sem instalação permanente, via `npx skills use`. A skill não requer dependências além do acesso ao código ou à documentação da CLI avaliada.

## Exemplos de uso

Os prompts abaixo são **exemplos derivados da descrição publicada**, não instruções oficiais da skill.

- **Auditoria de CLI:** "Avalie esta CLI nos sete eixos, cite a evidência de cada nota e calcule o total."
- **Plano de melhoria:** "Com base no score, proponha as três mudanças de maior impacto para levar a CLI de agent-tolerant a agent-ready."
- **Comparação:** "Aplique a mesma escala a `gh`, `aws` e `kubectl` e compare os totais por eixo."
- **Revisão de PR:** "Verifique se o novo comando aceita payload cru, retorna JSON consistente e tem `--dry-run`."

## Saídas esperadas

- uma nota de 0 a 3 por eixo, com evidência observável;
- total de 0 a 21 e classificação correspondente;
- lista de lacunas priorizadas;
- observação separada sobre MCP, extensão/plugin e autenticação headless.

## Quando usar (e quando não usar)

- **Use quando:** você está desenhando ou revisando uma CLI que agentes vão operar.
- **Use quando:** precisa comparar ferramentas concorrentes com critérios explícitos em vez de impressões.
- **Use quando:** quer transformar "boa para agentes" em requisitos verificáveis de produto.
- **Evite quando:** a ferramenta não é uma CLI ou não será consumida por agentes; a escala mede uma superfície específica.
- **Evite quando:** você não tem acesso ao comportamento real da ferramenta; notas sem evidência viram opinião.
- **Evite quando:** espera uma avaliação de UX humana; os eixos são deliberadamente outros.

## Limitações e cuidados

- **Escala de julgamento.** Os critérios de cada nível são descritivos, mas a atribuição de nota ainda depende de interpretação; dois avaliadores podem divergir.
- **Pesos iguais.** Os sete eixos valem o mesmo, embora saída legível e hardening tenham impactos diferentes conforme o caso de uso.
- **Parcialmente normativa.** A referência a "OpenClaw" no nível 3 do eixo 7 pressupõe um padrão externo que pode não ser universal.
- **Foco em CLI.** MCP, SDKs e APIs HTTP ficam de fora da pontuação; a prontidão multi-superfície é um bônus qualitativo.
- **Sem validação empírica publicada.** A skill não apresenta estudos correlacionando score com sucesso de agentes em tarefas reais.
- **Superfície de supply chain.** Instalar a skill adiciona instruções de terceiros ao agente; revise o `SKILL.md` antes de usar em contexto sensível.

## Estado e adoção

- **Versão da skill:** não publicada na página de origem (observado em 2026-10-19).
- **Catálogo:** 166 instalações, primeira aparição em 2026-04-22 (observado em 2026-10-19).
- **Auditorias de terceiros:** Gen Agent Trust Hub, Socket e Snyk com resultado "Pass" (observado em 2026-10-19); critérios não verificados nesta wiki.
- **Repositório-fonte:** Apache-2.0, TypeScript, ~28,4 mil estrelas e ~2,3 mil forks na API do GitHub; último push em 2026-10-16, no commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`. A licença é do repositório; a página da skill não declara licença própria.
- **Preço:** gratuito.

## Relações

- **Autor:** [google-labs-code](../../../../entities/google-labs-code.md) — organização Google Labs Code.
- **Repositório-fonte:** [google-labs-code/design.md](https://github.com/google-labs-code/design.md) — esta skill fica em `.agents/skills/agent-dx-cli-scale/`.
- **Conceitos:** [CLI agent-first](../../../../concepts/cli-agent-first.md) — tese que a escala operacionaliza; [Contratos tipados de serviço](../../../../concepts/contratos-tipados-de-servico.md) — entrada/saída estruturadas no nível do código; [TDD para agentes](../../../../concepts/tdd-para-agentes.md) — verificação como contrapressão.
- **Skills irmãs:** [Typed Service Contracts](typed-service-contracts.md), [TDD Red-Green-Refactor](tdd-red-green-refactor.md) e [Ink](ink.md).

## Perguntas abertas

- A escala foi aplicada publicamente a alguma CLI real? Quais foram as notas?
- Como ponderar os eixos por tipo de ferramenta (leitura vs. mutação, local vs. remota)?
- O nível 3 de hardening é viável para CLIs que operam caminhos fora do CWD por design?
- Como medir "sanitização contra prompt injection" sem um benchmark comum?
- "OpenClaw" é um padrão estabelecido ou uma referência interna do autor?

## Fontes

- Página de origem: https://www.skills.sh/google-labs-code/design.md/agent-dx-cli-scale (consultada em 2026-10-19).
- Repositório-fonte: https://github.com/google-labs-code/design.md (metadados e árvore consultados via API do GitHub em 2026-10-19; commit `6e5da5382f41edbba9d73b2c62f33f32e9971f15`). O repositório não foi clonado; o `SKILL.md` foi lido conforme renderizado na página do skills.sh, não como arquivo cru no repositório.
