---
type: repo
url: https://github.com/bilawalsidhu/gods-eye-view
host: github.com
owner: bilawalsidhu
repo: gods-eye-view
commit: 5a1598fd9e5ff707ba73bcb30ba1ae6071a8df68
license: MIT
language: JavaScript
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agentes, voz-em-tempo-real, geoespacial, mcp]
---

# bilawalsidhu/gods-eye-view

> Globo 3D fotorrealista no navegador que junta aviões, navios, satélites, terremotos, trânsito e câmeras públicas ao vivo, controlado por voz através de um agente de IA em tempo real com 30 ferramentas.

## O que é

God's Eye View ("GEV") pega sinais públicos já existentes — transponders de voo, AIS de navios, elementos orbitais, sismógrafos, câmeras de trânsito — e os reúne em um único globo explorável, local-first e com código inspecionável. Nasceu da série "God's Eye View" (antes "WorldView") do próprio autor no YouTube (5M+ de visualizações) e foi aberto depois de uma pesquisa com a audiência sobre abrir o código. O README é explícito sobre o limite do projeto: ele modela eventos, ativos e infraestrutura (aviões, navios, satélites, câmeras, cidades), não construiu busca por pessoa nomeada ou reconhecimento facial, e PRs que cruzem essa linha não são aceitos.

## Como funciona

- **Camada de mapa/dados**: Esri + OSM sem chave; Google Photorealistic 3D Tiles via token Cesium ion (gratuito, uso pessoal) ou chave Google (rota paga e com busca de lugares). Vinte camadas de dados (voos, navios, satélites via SGP4, terremotos USGS, câmeras públicas em ~15 cidades/regiões, rádio, trânsito, ônibus/metrô via GTFS-Realtime, clima NOAA/ECMWF, etc.), 18 delas sem necessidade de chave.
- **Agente de voz em tempo real**: via **OpenAI Realtime API** (padrão) ou Gemini, com 30 ferramentas divididas em quatro famílias — dirigir a câmera, anotar o mundo (desenhar polígonos/rotas reais, não formas genéricas), interrogar as camadas ativas (contagens, filtros, distâncias) e operar o console (trocar camada, estilo visual, iniciar modo cockpit). O agente lê contexto da cena (coordenadas, nomes de rua, camadas ativas, escala) antes de responder, e em modo de rua lê um screenshot do viewport para leitura visual, com instrução explícita de nunca alucinar rótulos.
- **Segurança de chaves**: toda API que toca uma chave privada (OpenAI, AISStream, OpenSky OAuth, frames de câmera) passa por um proxy server-side com proteção SSRF, limites de resposta e erros sanitizados; o navegador só vê as chaves de Google Maps e Cesium ion. A chave OpenAI nunca chega ao navegador — o cliente recebe só um token de sessão de curta duração.
- **Servidor MCP**: o próprio GEV se expõe como servidor MCP, permitindo que Claude Desktop, Codex ou ChatGPT desktop abram o globo ao vivo dentro da própria conversa.
- **Sem framework**: JavaScript vanilla, CesiumJS e Vite.

## Instalação e uso rápido

Três caminhos, todos sem conta ou chave obrigatória:

```bash
# Caminho 2 — terminal / agente de código (Node 24.x ou 26.x)
git clone https://github.com/bilawalsidhu/gods-eye-view.git
cd gods-eye-view
npm ci
npm run doctor
npm run dev   # abre em http://localhost:4173
```

Também há instalação de um clique via [Pinokio](https://pinokio.co/apps/github-com-bilawalsidhu-gods-eye-view) (Windows/macOS/Linux) e um caminho via `docker compose up`. Chaves (Cesium ion, Google Maps, OpenAI, AISStream, NASA FIRMS, TomTom, Mapillary) são adicionadas depois, dentro do app, pelo painel **POWER UP**, nunca em arquivo editado à mão por padrão.

## Exemplos de uso

Exemplos abaixo vêm do "tool playbook" descrito no próprio README, não são instruções oficiais do projeto além do que ele documenta:

- *"Take me to Tokyo."* / *"Orbit around this area slowly."* — comandos de câmera.
- *"Outline the state of Texas."* — desenha o contorno real, não uma forma genérica.
- *"How many flights are over Texas right now?"* — consulta analítica sobre a camada ativa.
- *"Switch to night vision and turn on the flights layer."* — operação do console por voz.

## Quando usar (e quando não usar)

- **Use quando:** o interesse é explorar dados geoespaciais públicos ao vivo com controle por voz, prototipar camadas sobre fontes OSINT abertas, ou testar um agente de voz em tempo real com grounding visual e de cena sobre um domínio concreto.
- **Evite quando:** o objetivo envolve rastreamento de pessoas identificadas — o próprio projeto recusa esse uso — ou quando é necessário dado de navegação crítico: o README avisa que os dados podem estar atrasados, incompletos, modelados ou errados, e não devem ser usados para navegação aérea/marítima, resposta a emergência, decisões médicas ou de investimento.

## Limitações e cuidados

- Vários feeds são estimativas ou simulações declaradas: trânsito fora de áreas com TomTom é simulado sobre vias OSM; poses de câmeras de CCTV são "priors estimados" calibráveis manualmente; relançamentos de foguete são rotulados "RECONSTRUCTED ESTIMATE".
- A licença detectada pela API do GitHub é `other`/`NOASSERTION`, mas o README afirma explicitamente "Released under the **MIT License**" com link para `LICENSE` — **a verificar**: há uma divergência entre a classificação automática do GitHub e o texto do README; este registro segue o README.
- Compartilhar a instância na LAN expõe as chaves configuradas a qualquer um que alcance o servidor; o README pede configurar cotas/alertas de billing antes de ampliar o acesso.
- O caminho OAuth do ChatGPT para voz é descrito como experimental, sem confirmação de um contrato comercial de terceiro para reuso de tokens do Codex.
- Vídeo ao vivo (HLS) não é suportado sob Docker, nem o servidor MCP local.
- Somente o README foi lido; não há leitura de `docs/`, código-fonte ou issues além do que ele descreve.

## Estado e adoção

- Alcançou #1 no GitHub Trending (diário e semanal) e #8 Product of the Day no Product Hunt, em agosto de 2026, segundo o próprio README.
- Release mais recente no GitHub: `v0.2.1`, publicada em 2026-10-03 — observado em 2026-10-21.
- Repositório criado em 2026-06-22, com push mais recente em 2026-10-21 (mesmo dia da ingestão) — observado em 2026-10-21.
- README anuncia uma versão hospedada futura em Halfpixel, mantendo este repositório como o cliente open source.
- Licença: MIT (conforme README; ver nota em Limitações sobre a divergência com a classificação automática do GitHub).

## Relações

- Mantido por: [Bilawal Sidhu (bilawalsidhu)](../../../entities/bilawalsidhu.md), com Sameh Khamis, na Halfpixel.
- Conceitos: [Model Context Protocol (MCP)](../../../concepts/model-context-protocol.md)

## Perguntas abertas

- Qual é de fato o modelo de negócio da versão hospedada anunciada pela Halfpixel, e o que muda para o repositório open source quando ela sair?
- A divergência de licença (API do GitHub vs. README) tem origem em algum detalhe de formatação do arquivo `LICENSE`?

## Fontes

- README: https://raw.githubusercontent.com/bilawalsidhu/gods-eye-view/5a1598fd9e5ff707ba73bcb30ba1ae6071a8df68/README.md (commit `5a1598fd9e5ff707ba73bcb30ba1ae6071a8df68`, consultado em 2026-10-21). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/bilawalsidhu/gods-eye-view`), consultada em 2026-10-21.
