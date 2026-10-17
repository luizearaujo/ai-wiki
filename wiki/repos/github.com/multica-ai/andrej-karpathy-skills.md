---
type: repo
url: https://github.com/multica-ai/andrej-karpathy-skills
host: github.com
owner: multica-ai
repo: andrej-karpathy-skills
commit: 2c606141936f1eeef17fa3043a72095b4765b9c2
license: MIT
language: desconhecida
status: unknown
created: 2026-10-17
ingested: 2026-10-17
updated: 2026-10-17
tags: [agentes, claude-code, diretrizes, comportamento-de-agentes, cursor]
---

# multica-ai/andrej-karpathy-skills

> Um único arquivo `CLAUDE.md` com quatro princípios de comportamento para agentes de código, derivados das observações de Andrej Karpathy sobre falhas recorrentes de LLMs ao programar.

## O que é

O repositório empacota diretrizes de comportamento para agentes de código em um só arquivo `CLAUDE.md`, endereçando três problemas descritos por Andrej Karpathy: suposições erradas assumidas sem verificação, código e abstrações inflados para tarefas simples, e mudanças ortogonais em código que o agente não entende o suficiente.

O público é quem usa Claude Code — e, por extensão, outros agentes que aceitem instruções persistentes — em projetos existentes, e quer reduzir diffs desnecessários, overengineering e implementações feitas sobre premissas não confirmadas. O README promete melhorar o comportamento do agente sem instalar ferramentas: o artefato é texto de instrução, não código executável.

O README é publicado em inglês e chinês, e o repositório também inclui uma regra de projeto para o Cursor (`.cursor/rules/karpathy-guidelines.mdc`), descrita em `CURSOR.md`. Nenhum desses arquivos internos foi lido nesta ingestão.

## Como funciona

O conteúdo é organizado em quatro princípios, cada um associado a uma falha observada:

| Princípio | Falha que endereça | O que exige |
| --- | --- | --- |
| **Think Before Coding** | Suposições silenciosas, confusão oculta, trade-offs ausentes | Declarar premissas; apresentar interpretações concorrentes; pedir esclarecimento; discordar quando houver opção mais simples |
| **Simplicity First** | Overcomplicação, abstrações infladas | Código mínimo para o problema; nada especulativo; sem features, flexibilidade ou tratamento de erros não pedidos |
| **Surgical Changes** | Edições ortogonais ao pedido | Tocar apenas o necessário; seguir o estilo existente; remover somente órfãos criados pela própria mudança; apontar dead code preexistente sem apagá-lo |
| **Goal-Driven Execution** | Critérios de sucesso fracos | Converter tarefas imperativas em metas verificáveis e iterar até a verificação passar |

A ideia central do quarto princípio é que LLMs são bons em repetir até atingir um objetivo específico. Transformar "corrija o bug" em "escreva um teste que o reproduza e faça-o passar" dá ao agente um critério objetivo de parada; "faça funcionar" exige esclarecimento constante.

Dois testes propostos no README resumem os princípios de simplicidade e escopo: perguntar se um engenheiro sênior consideraria o código complicado demais e verificar se cada linha alterada remete diretamente ao pedido do usuário.

## Instalação e uso rápido

O README oferece três caminhos, todos reproduzidos com os caminhos que ele publica:

**Plugin do Claude Code (recomendado):**

```text
/plugin marketplace add forrestchang/andrej-karpathy-skills
/plugin install andrej-karpathy-skills@karpathy-skills
```

**`CLAUDE.md` por projeto (novo arquivo):**

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md
```

**`CLAUDE.md` existente (acrescentar):**

```bash
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md >> CLAUDE.md
```

O README recomenda mesclar as diretrizes com instruções específicas do projeto, em vez de substituí-las. Para o Cursor, o repositório já traz uma regra de projeto; o README remete a `CURSOR.md` para instalação e para a relação com o Claude Code.

**Atenção:** os comandos acima usam `forrestchang/andrej-karpathy-skills`, mas o repositório hoje é `multica-ai/andrej-karpathy-skills`. A API do GitHub responde com redirecionamento 301 do caminho antigo para o novo, então os links devem continuar resolvendo; o funcionamento do marketplace de plugins e do download `raw` com o owner antigo não foi testado nesta ingestão. **A verificar.**

## Exemplos de uso

Exemplos derivados do README — não são instruções oficiais além do que ele publica.

- **Validação:** em vez de "adicione validação", pedir "escreva testes para entradas inválidas e faça-os passar".
- **Correção de bug:** em vez de "corrija o bug", pedir "escreva um teste que reproduza o bug e faça-o passar".
- **Refatoração:** em vez de "refatore X", pedir "garanta que os testes passem antes e depois".
- **Tarefa multi-etapa:** listar as etapas com um critério de verificação por etapa, para que o agente possa iterar sem novas perguntas.
- **Regras do projeto:** acrescentar ao mesmo `CLAUDE.md` seções como "use TypeScript em modo estrito", "todo endpoint de API tem testes" e "siga o tratamento de erros existente em `src/utils/errors.ts`".

## Quando usar (e quando não usar)

- **Use quando:** o agente tende a assumir premissas sem confirmar, complicar implementações simples, alterar código fora do escopo ou parar sem um critério de sucesso verificável.
- **Use quando:** você quer um conjunto curto de diretrizes reutilizável em vários projetos e agentes compatíveis com instruções persistentes.
- **Evite quando:** a tarefa é trivial — o próprio README recomenda bom senso para correções de typo e one-liners, em vez de aplicar toda a disciplina.
- **Evite quando:** você precisa de conhecimento de domínio ou de ferramentas em runtime; isso é escopo de uma [agent skill](../../../concepts/agent-skills.md) ou de um servidor [MCP](../../../concepts/model-context-protocol.md), não de diretrizes gerais.
- **Evite quando:** você espera garantia ou enforcement. O README não descreve nenhum mecanismo que force o agente a cumprir as regras; são instruções textuais sujeitas à interpretação do modelo.

## Limitações e cuidados

- **Somente o README foi lido nesta ingestão.** O conteúdo real de `CLAUDE.md`, a regra de Cursor e `CURSOR.md` não foram consultados; a descrição acima reflete o que o README publica sobre eles.
- **Caminho antigo nos comandos.** O README ainda aponta para `forrestchang/andrej-karpathy-skills`; o redirecionamento do GitHub foi observado, mas o plugin marketplace e o download `raw` pelo caminho antigo não foram verificados.
- **Licença inconsistente.** O README declara MIT, mas a API do GitHub não detecta licença (`license: null`; endpoint de licença retorna 404). A ausência de arquivo `LICENSE` no repositório é **A verificar** — a página registra MIT conforme o README.
- **Sem releases.** A API não reporta nenhuma release; a distribuição é feita pelo arquivo e pelo plugin.
- **Atividade incerta.** O último push observado foi em 2026-04-20 e o repositório não está arquivado; o README não declara política de manutenção. Por isso o status é `unknown`.
- **Efeito não medido.** O README descreve sinais qualitativos de que as diretrizes funcionam (menos mudanças desnecessárias, menos reescritas, perguntas antes da implementação, PRs menores), mas não apresenta benchmarks ou avaliação controlada.
- **Promoção cruzada.** O README divulga o projeto `multica-ai/multica`, da mesma organização, e o perfil do mantenedor no X.

## Estado e adoção

- **Versão:** nenhuma versão ou release publicada; o README não fixa versão.
- **Popularidade (observada em 2026-10-17):** ~220,6 mil estrelas e ~22,2 mil forks. Números voláteis; registrados apenas como observação datada.
- **Atividade:** criado em 2026-01-27; último push em 2026-04-20, no commit `2c606141936f1eeef17fa3043a72095b4765b9c2` (sync do README chinês, PR #95). Sem commits nos seis meses anteriores à observação.
- **Licença:** MIT segundo o README; não detectada pela API do GitHub.
- **Origem do caminho:** `forrestchang/andrej-karpathy-skills` redireciona (301) para `multica-ai/andrej-karpathy-skills`; a transferência não é mencionada no README.

## Relações

- **Mantido por:** [multica-ai](../../../entities/multica-ai.md).
- **Inspiração:** post de Andrej Karpathy no X sobre falhas de LLMs ao programar — https://x.com/karpathy/status/2015883857489522876 (não consultado; citado pelo README).
- **Conceitos:** [CLAUDE.md](../../../concepts/claude-md.md) — artefato usado para instruções persistentes; [Agent skills](../../../concepts/agent-skills.md) — formato vizinho, mas com instruções carregadas por tarefa e distribuídas como pacote `SKILL.md`.
- **Projeto relacionado:** `multica-ai/multica`, plataforma open-source para executar e gerenciar agentes de código com skills reutilizáveis, promovida no README.
- **Alternativas:** outros conjuntos de diretrizes para agentes e arquivos `CLAUDE.md` específicos de projeto; não comparados nesta ingestão.

## Perguntas abertas

- O texto real de `CLAUDE.md` corresponde ao resumo do README? (arquivo não lido)
- Os comandos de instalação com o owner antigo continuam funcionando no marketplace de plugins e no download `raw`?
- Como a regra de Cursor difere do arquivo `CLAUDE.md` em conteúdo e precedência? (ver `CURSOR.md`, não lido)
- Existe arquivo `LICENSE` no repositório, apesar de a API não detectar licença?
- Como as diretrizes se comportam quando entram em conflito com instruções específicas do projeto?
- Há alguma avaliação quantitativa do efeito das diretrizes no comportamento de agentes?

## Fontes

- README: https://raw.githubusercontent.com/multica-ai/andrej-karpathy-skills/2c606141936f1eeef17fa3043a72095b4765b9c2/README.md (commit `2c606141936f1eeef17fa3043a72095b4765b9c2`, consultado em 2026-10-17). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados do GitHub API: repositório `multica-ai/andrej-karpathy-skills`, commits recentes, releases, endpoint de licença e redirecionamento de `forrestchang/andrej-karpathy-skills`, consultados em 2026-10-17.
