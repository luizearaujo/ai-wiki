---
type: repo
url: https://github.com/MadsLorentzen/ai-job-search
host: github.com
owner: MadsLorentzen
repo: ai-job-search
commit: e16acee3abdaae57f8026789338a3c6eebf4608b
license: MIT
language: Python
status: active
created: 2026-10-21
ingested: 2026-10-21
updated: 2026-10-21
tags: [agentes, agent-skills, orquestracao-multiagente, claude-code]
---

# MadsLorentzen/ai-job-search

> Framework de busca de emprego que transforma o Claude Code em um assistente completo de candidatura: avalia vagas, redige CV e carta em LaTeX, revisa com um segundo agente e prepara para a entrevista — criado pelo autor para a própria busca de emprego, que resultou em contrato.

## O que é

O autor, geofísico, foi demitido no fim de 2025 e construiu este framework para rodar a própria busca de emprego: 69 candidaturas, 20 primeiras entrevistas e um contrato assinado depois, começou como engenheiro de IA em junho de 2026. O workflow central (`/setup`, `/scrape`, `/apply`) é descrito como independente de idioma e país; as skills de busca em portais (Jobindex, Jobnet, Akademikernes Jobbank) são do mercado dinamarquês, pensadas para serem substituídas pelo portal local do usuário.

## Como funciona

- **`/setup`** lê uma pasta `documents/` (CV em PDF, exportação do LinkedIn, diplomas), importa um CV colado ou conduz uma entrevista — idempotente, pode ser reexecutado conforme mais material é adicionado.
- **`/scrape`** busca em vários portais, deduplica e ordena por aderência; **`/rank`** pontua em lote contra uma rubrica de cinco dimensões antes de decidir o que candidatar.
- **`/apply <url>`** roda um workflow **drafter-reviewer**: avalia aderência, redige CV e carta em LaTeX, um segundo agente (contexto novo) pesquisa a empresa e critica os rascunhos, revisa, compila e inspeciona visualmente os PDFs (CV em exatamente 2 páginas, carta em 1), e faz uma checagem de ATS extraindo a camada de texto do PDF compilado (`pdftotext`) para verificar se o parser vê os dados de contato e a cobertura de palavras-chave da vaga.
- A vaga passa por um **gate de integridade determinístico** antes de qualquer agente processá-la (texto oculto, caracteres invisíveis, linhas em formato de instrução); os agentes tratam o conteúdo da vaga como entrada não confiável e não seguem instruções embutidas nela.
- Dez comandos adicionais estendem o núcleo: `/interview` (pacote de preparo por estágio e simulação de entrevista), `/outcome` (registra resultado, arquiva materiais, sugere follow-up nunca enviado automaticamente), `/notion-sync` e `/gmail-sync` (via MCP/conector oficial, só leitura ou proposta em lote para aprovação), `/expand` (enriquece o perfil a partir de GitHub/portfólio), `/upskill` (mapa de lacunas de skill), `/html-report` (dashboard offline autocontido), `/add-template` e `/add-portal` (extensibilidade sem tocar o upstream).
- Corte de CV que excede 2 páginas é ponderado por relevância à vaga, unicidade no documento e dependência da carta — não corta mecanicamente a seção "mais antiga".

## Instalação e uso rápido

```bash
gh repo fork MadsLorentzen/ai-job-search --clone
cd ai-job-search
python3 tools/install_portal_clis.py
claude
# dentro do Claude Code:
/setup
/scrape
/apply https://jobindex.dk/job/1234567
```

Pré-requisitos: Claude Code (assinatura Pro/Max/Team ou créditos de API — sem tier gratuito), Python 3.10+, Bun, distribuição LaTeX com `lualatex` e `xelatex`. Um fork público grava dados pessoais em arquivos rastreados — o README recomenda um repositório **privado** com este como `upstream` para quem não vai contribuir de volta.

## Quando usar (e quando não usar)

- **Use quando:** já usa Claude Code e quer automatizar o funil de candidatura inteiro — busca, avaliação, redação e preparo de entrevista — mantendo verificação determinística (compilação de PDF, checagem de ATS) sobre o que o agente produz.
- **Evite quando:** não tem assinatura ou crédito de API do Claude Code (não há tier gratuito), ou o mercado de trabalho alvo não tem portal compatível e não há tempo para gerar um via `/add-portal`.

## Limitações e cuidados

- Defesas contra conteúdo malicioso na vaga são em nível de instrução, não um sandbox — o README recomenda revisar o que foi buscado e escrito antes de enviar em um portal desconhecido.
- `/outcome followup` só rascunha, nunca envia, e no máximo duas vezes por candidatura; `/gmail-sync` propõe mudanças em lote para aprovação, nunca grava direto.
- As quatro skills de portal dinamarquesas são exemplo de padrão, não solução pronta para outros mercados; portais com autenticação são recusados pelo gerador `/add-portal`.
- Projeto não afiliado à Anthropic; sem token, criptomoeda ou patrocínio pago associado, segundo o próprio README.

## Estado e adoção

- 62.458 estrelas, 19.288 forks, 49 issues abertas — observado em 2026-10-21.
- Repositório criado em 2026-03-18, com push mais recente em 2026-10-21 — observado em 2026-10-21.
- Atualizações recomendadas via release tagueada (não `master` direto), com ferramentas próprias para prever o que uma atualização upstream toca nos arquivos personalizados.
- Licença: MIT.

## Relações

- Conceitos: [Agent skills](../../../concepts/agent-skills.md) — contrato de skill de portal (`search`/`detail` CLI, flag `enabled:`, testes próprios); [Orquestração multiagente](../../../concepts/orquestracao-multiagente.md) — separação drafter-reviewer com contexto novo; [CLAUDE.md](../../../concepts/claude-md.md) — perfil do candidato vive em `CLAUDE.md`.
- Agradecimento do autor: skills de busca de vaga originadas do repositório de [Mikkel Krogholm](https://github.com/mikkelkrogsholm/skills) (não documentado nesta wiki).

## Perguntas abertas

- Que proporção dos "community forks" por mercado (citados no README) estão ativamente mantidos?

## Fontes

- README: https://raw.githubusercontent.com/MadsLorentzen/ai-job-search/e16acee3abdaae57f8026789338a3c6eebf4608b/README.md (commit `e16acee3abdaae57f8026789338a3c6eebf4608b`, consultado em 2026-10-21). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/MadsLorentzen/ai-job-search`), consultada em 2026-10-21.
