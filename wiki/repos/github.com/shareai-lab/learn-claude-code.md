---
type: repo
url: https://github.com/shareAI-lab/learn-claude-code
host: github.com
owner: shareai-lab
repo: learn-claude-code
commit: ce8f9f186058939da54c9d6fead78dfb5d0fd6c3
license: MIT
language: Python
status: active
created: 2026-10-23
ingested: 2026-10-23
updated: 2026-10-23
tags: [agent-harness, aprendizado, claude-code, memoria-de-agente, orquestracao-multiagente]
---

# shareAI-lab/learn-claude-code

> Curso de 17 lições progressivas que reconstrói, do zero e em Python runnable, os mecanismos de harness por trás de um agente estilo Claude Code — um tool por vez, até chegar a um loop integrado com equipes, memória, tarefas em background e MCP.

## O que é

O README defende uma tese central antes de qualquer código: **agência — a capacidade de perceber, raciocinar e agir — vem do treinamento do modelo, não da orquestração externa em código**. Um produto de agente, porém, precisa de modelo *e* harness: o modelo decide, o harness executa. O repositório ensina a construir o harness (a "ferramenta"), não o modelo (o "motorista"), usando o Claude Code como estudo de caso por ser, segundo os autores, "a implementação mais elegante e completa de agent harness que já vimos" — justamente por não tentar substituir o julgamento do modelo por árvores de decisão fixas.

O público é quem já usa agentes de código e quer entender *por que* Claude Code funciona como funciona, decompondo-o em: loop do agente, uso de ferramentas, permissões, hooks, planejamento (`TodoWrite`), subagentes, carregamento de skills sob demanda, compactação de contexto, memória, sistema de tarefas, tarefas em background, agendamento (cron), equipes de agentes persistentes, plugins MCP, e finalmente dois exemplos de fechamento: runtime de workflow e "goal loop" (um avaliador independente decide quando o agente pode parar).

## Como funciona

O padrão central do curso é o loop de ferramentas do SDK da Anthropic, reduzido ao essencial:

```python
def agent_loop(messages):
    while True:
        response = client.messages.create(
            model=MODEL, system=SYSTEM,
            messages=messages, tools=TOOLS,
        )
        messages.append({"role": "assistant", "content": response.content})
        tool_calls = [b for b in response.content if b.type == "tool_use"]
        if not tool_calls:
            return
        results = [{"type": "tool_result", "tool_use_id": b.id,
                    "content": TOOL_HANDLERS[b.name](**b.input)} for b in tool_calls]
        messages.append({"role": "user", "content": results})
```

Cada uma das 17 lições (`s01` a `s17`) isola um mecanismo em torno desse loop, com um lema próprio; a tabela abaixo resume a progressão:

| Lição | Tópico | Ideia central |
|---|---|---|
| s01 | Agent Loop | um loop + bash = um agente |
| s02 | Tool Use | adicionar ferramenta = adicionar um handler no dispatch map |
| s03 | Permission | decidir o que pode rodar, o que precisa parar, o que precisa aprovação |
| s04 | Hooks | pontos de extensão em volta do loop, sem reescrevê-lo |
| s05 | TodoWrite | planejar antes de executar dobra a taxa de conclusão |
| s06 | Subagent | `messages[]` isolado por subtarefa; só o texto final retorna |
| s07 | Skill Loading | listar skills primeiro, expandir só quando necessário |
| s08 | Context Compact | quatro passos de compactação, reduzindo resultados de ferramenta antes do histórico |
| s09 | Memory | seleção, extração e consolidação |
| s10 | Task System | grafo de tarefas com dependências, persistido em disco |
| s11 | Background Tasks | threads para operações lentas; notificação ao concluir |
| s12 | Cron Scheduler | disparo por tempo, sem intervenção humana |
| s13 | Agent Teams | colegas persistentes, claim atômico de tarefas, worktrees por tarefa |
| s14 | MCP Plugin | ferramentas externas no mesmo pool |
| s15 | Integrated Harness | todos os mecanismos anteriores em um único loop |
| s16 | Workflow Runtime | orquestração fixa salva em código, com journal retomável |
| s17 | Goal Loop | um avaliador independente decide quando o loop pode parar |

O repositório mantém duas trilhas: a atual, de 17 lições na raiz (`s01_*` a `s17_*`), e uma trilha legada de 12 lições em `docs/`/`agents/`, preservada para links antigos durante a migração — o README avisa que a numeração dos capítulos não coincide entre as duas trilhas.

## Instalação e uso rápido

```bash
git clone https://github.com/shareAI-lab/learn-claude-code
cd learn-claude-code
pip install -r requirements.txt
cp .env.example .env   # configurar ANTHROPIC_API_KEY

python s01_agent_loop/code.py        # começar aqui
python s08_context_compact/code.py   # compactação de contexto (complexo)
python s17_goal_loop/code.py         # ponto final: continuação até uma meta verificável
```

Há também uma trilha legada (`python agents/s01_agent_loop.py` etc.) e uma web app (`cd web && npm install && npm run dev`) que expõe o curso com visualizações de leitura, código-fonte, simulador e arquitetura.

## Exemplos de uso

Exemplo de leitura de um capítulo, conforme a estrutura declarada no README:

```text
s08_context_compact/
  README.md       # inglês, narrativa completa
  README.zh.md     # tradução em chinês
  README.ja.md     # tradução em japonês
  code.py          # implementação runnable isolada
  images/          # diagramas SVG (quando necessário)
```

## Quando usar (e quando não usar)

- **Use quando:** você quer entender os mecanismos internos de um harness de agente de código construindo-os você mesmo, capítulo por capítulo, em vez de ler apenas a documentação de um produto fechado.
- **Evite quando:** você quer um harness pronto para produção — o próprio README enfatiza "isto não é 'copie o código-fonte', isto é 'entenda os designs-chave e construa você mesmo'"; para instalar componentes prontos, os próprios autores apontam para seus projetos irmãos `Kode-CLI` e `kode-agent-sdk`.

## Limitações e cuidados

- **Curso, não produto.** O README é explícito: o objetivo é entender e reconstruir mecanismos, não reaproveitar o código como biblioteca de produção.
- **Duas trilhas coexistindo.** A numeração de capítulos diverge entre a trilha legada (12 lições) e a atual (17 lições); o README publica uma tabela de mapeamento para evitar confusão, mas isso é uma fonte comum de erro para quem segue links antigos.
- Apenas o README foi lido: o código de cada capítulo (`code.py`), os diagramas e a web app não foram consultados nesta ingestão.

## Estado e adoção

- Observado em 2026-10-23: 79.092 estrelas, 12.644 forks, 69 issues abertas; criado em 2025-06-29; último push em 2026-09-28.
- Licença: MIT.
- Linguagem principal na API: Python.
- Projetos irmãos citados no README: `shareAI-lab/Kode-CLI` (CLI de agente de código open source) e `shareAI-lab/kode-agent-sdk` (SDK para embutir capacidades de agente); e `shareAI-lab/claw0`, curso irmão sobre harnesses "always-on" (heartbeat, cron, IM, memória, personalidade) — nenhum ingerido nesta wiki.

## Relações

- Mantido por: [shareAI-lab](../../../entities/shareai-lab.md)
- Conceitos: [Agent harness](../../../concepts/agent-harness.md), [Memória de agente](../../../concepts/memoria-de-agente.md), [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md)
- Contrasta com: ferramentas de orquestração "no-code"/drag-and-drop, que o README rejeita explicitamente como "Rube Goldberg machines" sem agência real.

## Perguntas abertas

- Como os mecanismos ensinados aqui se comparam, na prática, com a implementação real do Claude Code (não apenas com a descrição pública)?
- O curso legado de 12 lições será removido ou mantido indefinidamente para compatibilidade de links?
- Qual é a relação de propriedade/afiliação entre este curso e o produto comercial `Kode-CLI`/`kode-agent-sdk` dos mesmos autores?

## Fontes

- README: https://raw.githubusercontent.com/shareAI-lab/learn-claude-code/ce8f9f186058939da54c9d6fead78dfb5d0fd6c3/README.md (commit `ce8f9f186058939da54c9d6fead78dfb5d0fd6c3`, consultado em 2026-10-23). Somente o README foi lido; o código de cada capítulo, diagramas e a web app não foram consultados.
- Metadados: API do GitHub (`/repos/shareAI-lab/learn-claude-code`) em 2026-10-23.
