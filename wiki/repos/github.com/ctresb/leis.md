---
type: repo
url: https://github.com/ctresb/leis
host: github.com
owner: ctresb
repo: leis
commit: c9f21b4ab11aa0d7ca6fe861d75028e94219c2d6
license: MIT
language: desconhecida
status: active
created: 2026-11-05
ingested: 2026-11-05
updated: 2026-11-05
tags: [dados-abertos, legislacao, ocr, portugues-brasileiro]
---

# ctresb/leis

> Acervo de toda a legislação brasileira — Constituição, normas federais, estaduais, distritais e municipais — convertida de fontes oficiais para Markdown com cabeçalho estruturado e link para a origem de cada texto.

**Nota de escopo:** este repositório não é uma ferramenta, modelo ou framework de IA — é um corpus jurídico. Foi ingerido como exceção explícita ao escopo de IA da wiki ([CLAUDE.md](../../../../CLAUDE.md)), confirmada pelo usuário em 2026-11-05, por reunir um pipeline de OCR e normalização em larga escala sobre texto em português que pode interessar como fonte de dados para RAG ou avaliação de LLMs em domínio jurídico brasileiro.

## O que é

Um repositório que publica o ordenamento jurídico brasileiro em texto simples: a Constituição Federal, leis e decretos federais desde 1822, a legislação de todos os estados e do Distrito Federal, e o início de uma cobertura municipal. Cada norma é um arquivo Markdown com cabeçalho YAML (tipo, número, data, ementa, situação, fonte, URN) e o texto abaixo. O objetivo declarado vai além do que já está publicado: cobrir também atos infralegais de agências reguladoras, tratados internalizados e jurisprudência vinculante.

Na base inicial (a maior parte do acervo), **323.849 normas** foram convertidas: 1 Constituição Federal, 29.184 normas federais e 294.664 normas estaduais/distritais, predominantemente leis ordinárias (289.684) e decretos-lei (18.366).

## Como funciona

Scripts em `scripts/estados/<uf>.py` (um por unidade federativa) e `scripts/baixar_federal.py` coletam de fontes oficiais — Planalto, SAPL, APIs e sistemas de legislação de cada Assembleia — respeitando limite de 1–4 requisições por segundo e retomando downloads já feitos. O texto final sai de HTML, PDF ou OCR (framework Vision do macOS para digitalizações; Tesseract 5 com modelo `por.traineddata` para imagem/TIFF), passando por `scripts/normalizar.py` para forçar nomes de pasta e tipos de norma a um vocabulário canônico (`CANONICO`, em `scripts/comum.py`).

O histórico do git da base inicial é a própria linha do tempo: **323.851 commits**, um por norma, em ordem cronológica desde 1822, cada um assinado pelo signatário identificado no texto (ou pela instituição, quando o signatário não é recuperável) — 5.414 autores distintos. Normas datadas antes de 1970 têm a data do commit fixada em 01-01-1970 (limite do epoch do git) com a data real registrada no título e no corpo. Coletas posteriores à base inicial entram em **commits de lote** (um por coleta), não mais um commit por norma — trade-off explícito para não reescrever meio milhão de commits a cada atualização.

`scripts/plano.py` define o escopo completo (o que deve existir, por esfera e tipo); `scripts/progresso.py` mede o acervo contra esse plano e gera `PROGRESSO.md` e `progresso.svg`; `scripts/relatorio.py` gera `COBERTURA.md` com números por estado e lacunas.

## Instalação e uso rápido

**Pré-requisitos:** macOS, Python 3, `pdftotext` (poppler); `pypdf` para diários municipais; `swiftc` para compilar `scripts/ocr.swift` (framework Vision).

```sh
python3 -I scripts/baixar_federal.py             # normas federais
python3 -I scripts/estados/sp.py                 # um estado por script
python3 -I scripts/reconverter.py [UF ...]       # regenera .md a partir de _fonte
python3 -I scripts/normalizar.py                 # aplica vocabulário canônico
python3 -I scripts/montar_repositorio.py --saida /caminho/do/repo   # remonta o histórico git
```

Os quatro scripts de manutenção (`reconverter`, `normalizar`, `corrigir_ocr`, `corrigir_datas_invalidas`) rodam em simulação por padrão; só gravam com `--aplicar`.

## Exemplos de uso

- Consultar o texto vigente de uma lei específica por caminho (`federal/leis-ordinarias/2002/*.md` para o Código Civil) em vez de acessar o portal oficial.
- Usar o acervo como corpus de domínio jurídico brasileiro para RAG ou fine-tuning, com proveniência (`fonte`, `baixado_em`) por documento — exemplo derivado da estrutura publicada, não uma instrução oficial do projeto.
- Auditar quais normas de um estado ainda faltam ou têm texto não digitalizado, via `COBERTURA.md`.

## Quando usar (e quando não usar)

- **Use quando:** precisar de texto legal brasileiro em Markdown, com fonte rastreável, para leitura, indexação ou experimentação com LLMs — sempre conferindo a fonte oficial antes de citar.
- **Evite quando:** precisar de valor jurídico certificado (publicação em Diário Oficial) ou de cobertura de atos infralegais e jurisprudência, que o README declara como lacunas em andamento (fases 2 e 3 do plano).

## Limitações e cuidados

- O próprio README avisa: os textos são conversões automáticas e OCR de documentos escaneados, **não substituem a publicação no Diário Oficial**.
- OCR com dois problemas conhecidos: ordem de leitura trocada em PDFs de duas colunas (corrigido parcialmente, sem reprocessamento integral do acervo) e ordinais confundidos tipo "Art. 19" por "Art. 1º" (corrigido em 1.509 arquivos, com regra conservadora).
- Pendências declaradas por estado: RJ sem coleta (timeout do Lotus Notes da ALERJ), AC e TO com corte de data por limite do SAPL, RS com 5.569 leis sem texto digitalizado na fonte, MG sem atualização desde que o serviço de dados abertos da ALMG parou de responder.
- `raw/fonte/` (27 GB de HTML/PDF originais) e índices não são versionados; apenas os `.md` convertidos e os logs de falha (`_falhas.jsonl`).
- Licença mista: os textos das normas são atos oficiais, não protegidos por direito de autor (art. 8º, I, da Lei nº 9.610/98); os scripts do repositório estão sob MIT.
- **A verificar:** apenas o `README.md` foi lido; não foram verificados `scripts/plano.py`, `PROGRESSO.md`, `COBERTURA.md` nem o código dos coletores.

## Estado e adoção

- Sem releases ou versionamento semântico citado no README; o histórico de commits é o próprio mecanismo de versionamento do conteúdo.
- Atividade observada em 2026-11-05: último push em 2026-11-02; 2.550 estrelas; 429 forks; 23 issues abertas (API do GitHub, não um fato estável — sujeito a mudar).
- Pasta local do projeto citada em 133,8 GB (1º de novembro de 2026), fora do git (`_fonte/`).
- Licença: MIT para os scripts; textos sem proteção autoral (LICENSE no repositório).

## Relações

- Mantido por: [ctresb](https://github.com/ctresb) (perfil "C3B", bio mínima — sem página de entidade própria por falta de contexto suficiente).
- Conceitos: nenhum conceito existente na wiki cobre corpus jurídico ou pipeline de OCR para dados abertos; ver nota de escopo acima.
- Alternativas: portais oficiais por esfera (Planalto, normas.leg.br, portais de cada Assembleia Legislativa), sem a conversão unificada para Markdown.

## Perguntas abertas

- Se a wiki passar a ingerir mais corpora de dados abertos como este, vale criar um conceito dedicado (ex.: "corpora de dados abertos para IA") e uma categoria própria em `categorias.md`.
- Não há informação, no README, sobre uso real do acervo em pipelines de RAG ou fine-tuning — é uma possibilidade inferida, não um fato documentado pela fonte.

## Fontes

- README: https://raw.githubusercontent.com/ctresb/leis/c9f21b4ab11aa0d7ca6fe861d75028e94219c2d6/README.md (commit `c9f21b4ab11aa0d7ca6fe861d75028e94219c2d6`, consultado em 2026-11-05). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/ctresb/leis`, `api.github.com/users/ctresb`), consultada em 2026-11-05.
