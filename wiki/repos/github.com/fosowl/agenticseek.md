---
type: repo
url: https://github.com/Fosowl/agenticSeek
host: github.com
owner: fosowl
repo: agenticseek
commit: 4f5f924c1eb326b4163d3bf942954dcc7dd7875b
license: GPL-3.0
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-23
updated: 2026-10-23
tags: [agentes, harness, navegacao-web, codigo, voz, local, llm]
---

# Fosowl/agenticSeek

> Alternativa 100% local ao Manus AI: assistente de voz que navega na web, escreve e executa código e planeja tarefas, selecionando automaticamente o agente certo para cada pedido, sem depender de nuvem.

## O que é

AgenticSeek é um assistente de IA autônomo pensado para rodar inteiramente no hardware do usuário. O problema que ataca é a dependência de serviços cloud — custo de API e exposição de dados — em agentes autônomos do tipo Manus AI. Em vez de um único prompt, o projeto expõe vários agentes especializados (navegação web, código, planejamento) e um roteador que escolhe qual usar.

O README é explícito sobre a origem: "started as a side-project" sem roadmap nem funding formal, criado por um engenheiro de ML/AI e dois colaboradores.

## Como funciona

- **Seleção automática de agente:** a cada pedido, o sistema decide qual agente atende melhor — navegação, codificação ou planejamento de tarefas longas.
- **Navegação web autônoma:** busca, leitura, extração e preenchimento de formulários via browser automatizado, com `undetected_chromedriver` em modo stealth opcional.
- **Agente de código:** escreve, depura e executa Python, C, Go, Java e outras linguagens sem supervisão direta.
- **Planejamento:** decompõe tarefas complexas em passos executados por múltiplos agentes.
- **Execução:** Docker Compose orquestra SearxNG (busca), Redis (suporte ao SearxNG), frontend e backend; há um modo CLI alternativo (`uv run cli.py`) que roda o backend no host.
- **Provedores de LLM:** locais (Ollama, LM Studio, servidor OpenAI-compatible como llama.cpp) ou em nuvem (OpenAI, Google, Deepseek, Hugging Face, TogetherAI, OpenRouter, MiniMax, e desde a reingestão de 2026-10-23 também TrustedRouter), configurados em `config.ini`.
- **Voz:** texto-para-fala e fala-para-texto, com palavra de ativação (nome do agente); listado como funcionalidade em progresso e só disponível no modo CLI, em inglês.
- **Importação de sessão do browser:** pode copiar cookies, logins e dados salvos do navegador do próprio usuário para o navegador do agente — o README avisa que isso dá ao agente acesso às mesmas contas autenticadas (e-mail, banco).

### Modelo de segurança declarado

- A API do backend exige token (`AGENTICSEEK_API_TOKEN`, gerado automaticamente se ausente); só `/health` é público.
- O backend só responde a `localhost`/`127.0.0.1`, salvo hosts adicionados em `AGENTICSEEK_ALLOWED_HOSTS`.
- Em Docker, o código do agente roda como usuário sem privilégio, sem acesso a chaves de API via ambiente.
- O contêiner do backend precisa da capability `NET_ADMIN` para bloquear o loopback; sem ela, o agente pode alcançar o ChromeDriver/DevTools do Chrome.
- `safe_mode` (ligado por padrão) é descrito como um filtro de comandos "best-effort", **não um sandbox**.

## Instalação e uso rápido

```sh
git clone https://github.com/Fosowl/agenticSeek.git
cd agenticSeek
mv .env.example .env
# editar .env e config.ini com provider, modelo e portas
./start_services.sh full   # Docker completo, interface web em localhost:3000
```

Modo CLI alternativo (backend no host):

```sh
./install.sh
uv run cli.py
```

## Exemplos de uso

Exemplos do README:

> *Make a snake game in python!*

> *Search the web for top cafes in Rennes, France, and save a list of three with their addresses in rennes_cafes.txt.*

> *Search the web for the latest AI news articles from 2025, select three, and write a Python script to scrape their titles and summaries.*

O README recomenda pedidos explícitos sobre a ação desejada (ex.: "do a web search and find..."), porque o roteamento de agente ainda erra em pedidos ambíguos.

## Quando usar (e quando não usar)

- **Use quando:** o objetivo é um assistente autônomo rodando localmente, com controle total sobre os dados, e há hardware para um modelo de raciocínio de 14B+ (idealmente 70B+).
- **Evite quando:** a tarefa exige confiabilidade de produção — é projeto hobby, sem roadmap nem funding declarado —, o hardware é limitado (7B não é recomendado pelo próprio README) ou a segurança de execução de código precisa ser garantida além de um filtro best-effort.

## Limitações e cuidados

- **Somente o README foi lido.** Código do roteador de agentes, dos agentes individuais e dos prompts não foi inspecionado.
- `safe_mode` é um filtro de comandos, não isolamento real; a contenção de rede depende de `NET_ADMIN` estar configurada corretamente.
- Preenchimento de formulários web é "ainda experimental e pode falhar", segundo o README.
- Voz (fala-para-texto) só funciona em inglês e apenas no modo CLI.
- Um servidor LLM legado próprio (`llm_server/`, `provider_name = server`) é declarado deprecated: sem streaming, sem autenticação, atende uma requisição por vez.
- Importar a sessão do browser do usuário é descrito como dar ao agente as mesmas credenciais e cookies — inclusive de bancos e e-mail — com `is_local = False` enviando o conteúdo lido ao provedor de nuvem.

## Estado e adoção

- **Atividade observada em 2026-10-19:** ~27,5 mil estrelas, ~3,2 mil forks, 30 issues abertas; criado em 2025-02-19, último push em 2026-10-15.
- **Reingestão em 2026-10-23:** novo commit `4f5f924c1eb326b4163d3bf942954dcc7dd7875b`. Mudanças no README: adição do provedor TrustedRouter à tabela de provedores de LLM e atualização dos créditos (frontend atribuído a Tanvir Ahamed). Sem mudança de propósito, arquitetura ou modelo de segurança.
- **Licença:** GPL-3.0, conforme a API do GitHub.
- **Linguagem principal:** Python.
- Mantido pelo criador e dois colaboradores da comunidade; sem afiliação a empresa ou startup, segundo o README.

## Relações

- **Mantido por:** [Fosowl](../../../entities/fosowl.md) (Martin Legrand).
- **Conceitos:** [Agent harness](../../../concepts/agent-harness.md) — roteamento entre agentes especializados sobre um runtime único; [Navegação web agêntica](../../../concepts/navegacao-web-agentica.md) — browser automatizado com modo stealth como ferramenta do agente.
- **Alternativas:** Manus AI (proprietário, cloud) — a comparação central do próprio README; outros harnesses locais documentados nesta wiki, como [bytedance/deer-flow](../bytedance/deer-flow.md).

## Perguntas abertas

- Qual a taxa real de sucesso do roteamento automático de agente e do preenchimento de formulários?
- O `safe_mode` e o isolamento de rede via `NET_ADMIN` resistem a um agente de código adversarial ou mal instruído?
- Como o projeto pretende sustentar manutenção sem roadmap nem funding formais?

## Fontes

- README: https://raw.githubusercontent.com/Fosowl/agenticSeek/4f5f924c1eb326b4163d3bf942954dcc7dd7875b/README.md (commit `4f5f924c1eb326b4163d3bf942954dcc7dd7875b`, consultado em 2026-10-23; reingestão do commit anterior `b46bcca482218643236999221720586e7f410e04`, lido em 2026-10-19). Somente o README foi lido; código-fonte, `docs/CONTRIBUTING.md` e scripts não foram consultados.
- Metadados do repositório: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues, datas).
- Perfil do mantenedor: API do GitHub (`users/Fosowl`) em 2026-10-19.
