---
type: repo
url: https://github.com/littledivy/mimic
host: github.com
owner: littledivy
repo: mimic
commit: 8cf998ac0b365806d8e522d34107cc504ecaa345
license: MIT
language: Python
status: active
created: 2026-10-18
ingested: 2026-10-18
updated: 2026-10-18
tags: [agentes, engenharia-reversa, mitmproxy, code-generation, claude, api-client]
---

# littledivy/mimic

> Captura o tráfego de qualquer app iOS ou web, extrai as credenciais de autenticação e usa Claude para gerar automaticamente um cliente Python chamável como biblioteca.

## O que é

mimic transforma qualquer app móvel ou web em uma biblioteca Python sem escrever uma linha de código HTTP. O fluxo é: captura de tráfego → extração de auth → geração de cliente por IA. O cliente gerado é Python puro sobre `mimic.App` e pode ser editado como qualquer outro arquivo.

```python
from hinge_client import Hinge

acc = Hinge()                          # reutiliza a sessão capturada
recs = acc.get_recommendations()
acc.like(subject_id, comment="hi lol")
```

O arquivo `hinge_client.py` não é escrito manualmente — Claude lê os endpoints capturados e gera o cliente.

## Como funciona

A maioria dos apps autentica cada requisição com o mesmo conjunto de valores: bearer token, device IDs, session ID, cookies. Esses valores são estáveis entre chamadas. Capturar uma vez e reutilizar é suficiente para replay.

```
captura de tráfego  →  extração de auth  →  geração de cliente
   (mitmproxy)          (mimic.Session)      (Claude lê os endpoints
                                              capturados e gera Python)
```

O cliente gerado inclui métodos nomeados, templates de body e encadeamento multi-step (ex.: buscar um token em uma chamada e gastá-lo na próxima — padrão comum em APIs mobile).

## Instalação e uso rápido

```bash
sh install.sh          # instala uv se necessário, depois mimic em env isolado
mimic doctor           # confirma que proxy + claude estão prontos
```

**Fluxo para iPhone:**

```bash
mimic record           # inicia o proxy, imprime os passos para iPhone

# Configurar no iPhone:
# Wi-Fi → Configure Proxy → Manual → <ip-do-mac>:8080
# Safari → http://mitm.it → instalar perfil Apple
# Ajustes → Geral → Sobre → Definições de Confiança de Certificado → ativar mitmproxy

mimic hosts                           # lista os hosts capturados
mimic learn  prod-api.exemplo.com     # inspeciona os endpoints
mimic gen    prod-api.exemplo.com     # gera o_cliente.py via Claude
```

## Backends de captura

| Backend | Quando usar | Comando |
|---------|-------------|---------|
| mitmproxy | Apps iOS (padrão) | `mimic record` |
| cURL/paste | Apps web ("Copy as cURL" no devtools) | `Session.from_curl(text)` |
| HAR file | Apps web (exportar do Network tab do browser) | `mimic gen api.ex.com --har traffic.har` |

## API Python (`mimic.Session`)

Três formas de construir uma sessão manualmente, sem codegen:

```python
from mimic import Session

Session.from_mitm("api.exemplo.com")          # pull auth do mitmweb
Session.from_curl(open("copied.txt").read())  # colar "Copy as cURL"
Session(base_url="https://x.com", headers={}) # explícito

sess.get("/path")
sess.post("/path", json={...})
```

`.get`, `.post` e outros verbos retornam JSON parseado e levantam `requests.HTTPError` em erros. Se o token rotar, um `401` em requisição idempotente dispara um re-pull do mitmweb e retry automático.

## Limitações

- **Certificate pinning** (apps bancários, Instagram): o app rejeita o cert do mitmproxy, nada aparece em `mimic hosts`. Bloqueia a *captura*, não o replay. Workaround: `mimic unpin <ipa|bundle-id>` — bypass baseado em Frida, documentado em `docs/pinning.md`. **A verificar:** quais versões de iOS e quais apps são suportados.
- **DPoP / sender-constrained tokens**: cada requisição carrega uma prova assinada por chave privada que nunca sai do dispositivo, então requisições capturadas não fazem replay. Derrota o modelo central, sem workaround limpo. Documentado em `docs/dpop.md`.
- mitmproxy é lançado via `uvx` (não é dependência separada), mas requer que a ferramenta esteja disponível no ambiente.
- O conteúdo de `docs/pinning.md` e `docs/dpop.md` não foi lido; detalhes técnicos do bypass de pinning e das restrições DPoP são a verificar.

## Quando usar (e quando não usar)

- **Use quando:** quiser automatizar interações com um app móvel ou web que não tem API pública; para scraping de dados da sua própria conta; para testes de regressão de fluxos mobile.
- **Evite quando:** o app usa certificate pinning forte sem IPA acessível; quando o token é DPoP/sender-constrained; quando os termos de serviço do app proíbem acesso automatizado.
- **Ética declarada pelo projeto:** somente na própria conta e dados. O replay de sessão não acessa dados de terceiros.

## Estado e adoção

- Último push: 2026-07-26.
- Observado em 2026-10-18: ~2.848 stars, ~336 forks, ~6 issues abertas.
- Licença: MIT. Fornecido sem garantias.

## Relações

- Mantido por: [littledivy](../../../entities/littledivy.md)
- Conceitos: [Engenharia reversa agêntica](../../../concepts/engenharia-reversa-agentica.md)
- Relacionado: [morluto/rea](../morluto/rea.md) — engenharia reversa de binários via MCP; abordagem complementar (rede vs binário).

## Perguntas abertas

- Qual modelo Claude é usado para gerar o cliente e como o prompt é estruturado?
- O `mimic unpin` suporta apps Android além de iOS?
- Há suporte para fluxos OAuth onde o token inicial requer interação humana (login)?
- Como o projeto lida com apps que mudam a estrutura da API frequentemente?

## Fontes

- README: https://raw.githubusercontent.com/littledivy/mimic/8cf998ac0b365806d8e522d34107cc504ecaa345/README.md (commit `8cf998ac0b365806d8e522d34107cc504ecaa345`, consultado em 2026-10-18). Somente o README foi lido; `docs/pinning.md`, `docs/dpop.md`, código-fonte e scripts não foram consultados.
- Metadados: API do GitHub em 2026-10-18.
