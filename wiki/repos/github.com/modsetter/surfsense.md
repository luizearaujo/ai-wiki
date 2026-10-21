---
type: repo
url: https://github.com/MODSetter/SurfSense
host: github.com
owner: MODSetter
repo: SurfSense
commit: e3de9e0d293b2ebb1fb813628ecc1d6f26909396
license: Apache-2.0
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [pesquisa-pessoal, notebooklm, self-hosted, mcp]
---

# MODSetter/SurfSense

> App desktop air-gapped, alternativa ao Notebook LM, que não só responde sobre os documentos do usuário como os edita — preenche e assina PDFs, mantém controle de alterações em Word, recalcula fórmulas em Excel — sempre em uma cópia nova, nunca sobrescrevendo o original.

## O que é

SurfSense se posiciona para "documentos que você não pode subir" — o índice fica no disco do usuário, o modelo é escolhido (local ou remoto) e não há conta. O README está passando por uma transição: a versão web hospedada anterior está sendo descontinuada (export de workspaces até 18/10/2026), com o app desktop como caminho principal daqui para frente.

## Como funciona

A tabela de formatos no README detalha quatro capacidades por tipo de arquivo:

| Formato | Pesquisa (resposta citada) | Criar | Editar (como cópia) | Transformar |
|---|---|---|---|---|
| PDF | sim, inclusive páginas escaneadas (OCR) | sim | preencher/achatar formulários; marca d'água, numeração, cabeçalho/rodapé | mesclar, dividir, extrair, rotacionar, reordenar páginas |
| Word (.docx) | sim | sim, ou a partir do próprio `.docx` como modelo | corpo do texto, como alterações rastreadas e comentários | para PDF |
| Excel (.xlsx) | sim, lê fórmulas | sim, com fórmulas e gráficos nativos | valores e fórmulas de célula | análise com pandas, gráficos dos resultados |
| PowerPoint (.pptx) | sim | sim, ou a partir de modelo próprio | substituir texto em slides/notas; apagar/duplicar slides | para PDF |
| Imagens, gravações, podcast, mapas mentais/flashcards/quizzes | parcial (OCR, transcrição) | parcial | — | — |

Conversões para PDF dependem de suporte de Office (LibreOffice), opcional e nunca incluído no instalador. Edições sempre geram um arquivo novo.

- **Plugins da SurfSense**: Google Search, Web Crawl, YouTube, TikTok, Google Maps, Amazon, Walmart, Indeed — leem páginas públicas sem contas próprias, exigem licença da SurfSense (download do app + e-mail dá 30 dias grátis).
- **Plugins de terceiros**: servidores MCP do registro de plugins (DeepWiki, Notion, ou qualquer um por URL) — não precisam de licença, ficam desativados até o usuário permitir.
- Modelos: qualquer API compatível com OpenAI, ou um modelo local.

## Instalação e uso rápido

Instaladores por plataforma em `github.com/MODSetter/SurfSense/releases/latest`: `SurfSense-Setup.exe` (Windows x64), `SurfSense-arm64.dmg` (macOS Apple Silicon), `.AppImage`/`.deb` (Linux x64). Depois do onboarding inicial: soltar arquivos ou pastas nas fontes, e pedir ao agente para buscar, extrair ou editar.

## Quando usar (e quando não usar)

- **Use quando:** tem documentos sensíveis que não quer subir a lugar nenhum, e quer que o agente não só responda sobre eles, mas também os edite (preencher formulário, rastrear mudança, recalcular planilha).
- **Evite quando:** usava a versão web hospedada anterior e depende de acesso multiusuário/nuvem — essa versão está sendo descontinuada; é preciso exportar workspaces e migrar para o app desktop antes do prazo do README.

## Limitações e cuidados

- Documento interno do repositório (comentário HTML no topo do README) menciona um "sunset callout" com data para remover, confirmando que a transição da versão web é temporária e documentada só até certa data — tratado aqui como dado do próprio repositório, não como instrução.
- OCR cobre script latino, chinês e japonês — não universal.
- Geração de imagem/infográfico via "Create" em imagens precisa de um modelo de imagem configurado (local ou remoto); nenhum vem escolhido por padrão.

## Estado e adoção

- 16.555 estrelas, 1.590 forks, 68 issues abertas — observado em 2026-10-21.
- Repositório criado em 2024-07-30, com push mais recente em 2026-10-21 — observado em 2026-10-21.
- Licença: Apache-2.0.

## Relações

- Mantido por: [Rohan Verma (MODSetter)](../../../entities/modsetter.md)
- Alternativa comparável (também NotebookLM-like, documentada nesta mesma ingestão): [lfnovo/open-notebook](../lfnovo/open-notebook.md) — Open Notebook é self-hosted via Docker com foco em notebooks de pesquisa e podcast; SurfSense é um app desktop air-gapped com foco em editar os próprios documentos.

## Perguntas abertas

- O que muda tecnicamente para quem migra da versão web hospedada para o app desktop, além do processo de export/import de workspace citado no README?

## Fontes

- README: https://raw.githubusercontent.com/MODSetter/SurfSense/e3de9e0d293b2ebb1fb813628ecc1d6f26909396/README.md (commit `e3de9e0d293b2ebb1fb813628ecc1d6f26909396`, consultado em 2026-10-21). Somente o README foi lido; `docs/`, `CONTRIBUTING.md` e o código-fonte não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/MODSetter/SurfSense`), consultada em 2026-10-21.
