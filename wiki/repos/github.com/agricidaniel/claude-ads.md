---
type: repo
url: https://github.com/AgriciDaniel/claude-ads
host: github.com
owner: agricidaniel
repo: claude-ads
commit: fc3908e786c318776df89a3a098333da377364be
license: MIT
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [marketing, publicidade, auditoria, evidencia, skills, agentes, claude-code, midia-paga]
---

# AgriciDaniel/claude-ads

> Skill de operações de mídia paga para Claude Code que audita contas em 12 plataformas de anúncios com achados rastreáveis, relatórios JSON versionados e alterações gated por capacidade.

## O que é

Claude Ads é uma skill gratuita e open source (MIT) para Claude Code, voltada a agências, consultores e times de marketing in-house. O usuário entrega dados de conta — exportação CSV ou JSON, screenshots ou um resumo colado com período, moeda e fuso — e a skill responde o que está funcionando, o que está quebrado e o que corrigir primeiro, em 12 plataformas: Google, Meta, YouTube, LinkedIn, TikTok, Microsoft, Apple, Amazon, Reddit, Pinterest, Snapchat e X.

A promessa central é de **leitura e relatório**: "it reads your data and reports back. It does not change your accounts on its own." O README posiciona o produto pela confiabilidade — evidência por achado, honestidade sobre lacunas e dados que permanecem do cliente — e não pela automação de campanhas.

## Como funciona

A arquitetura declarada é **um condutor e vários workers**:

- um conductor centraliza escopo, política, agregação e artefatos finais;
- workers analisam fatias limitadas e devolvem achados validados por schema;
- falha de um worker obrigatório torna a execução **parcial**, nunca um audit completo apresentado como íntegro.

O resultado canônico é um **JSON versionado**; Markdown, HTML e PDF são renderizações do mesmo bundle validado. Cada plataforma tem skill própria, worker de auditoria, referência de controles e declaração de capacidade; o manifesto de capacidades é a fonte autoritativa sobre o que pode ser lido ou alterado ao vivo.

### Quatro resultados e cobertura de evidência

Todo controle termina em `pass`, `fail`, `unknown` ou `not_applicable`. `unknown` é uma resposta legítima: significa dado ausente e nunca é adivinhado.

- Saúde, cobertura de evidência, exposição regulatória e oportunidades são dimensões separadas.
- Cobertura ≥ 80% é "graded", 60–79% é "provisional" e abaixo de 60% é "insufficient evidence".
- Uma plataforma com falha é excluída do score de portfólio e torna a execução parcial.
- **Os 12 perfis de saúde estão desativados** — nenhum health score é produzido; o audit reporta achados, desconhecidos e cobertura.

### Segurança de escrita

Todos os adapters são read-only por padrão. Aplicar uma mudança exige seis condições:

1. capacidade testada e habilitada para a operação exata;
2. IDs explícitos de conta e objeto;
3. diff antes/depois legível, com raio de impacto;
4. aprovação do dono dentro de limites definidos por conta;
5. chave de idempotência, destino de auditoria, rollback e janela de verificação;
6. verificação de que o estado remoto ainda satisfaz a pré-condição.

Sem limites definidos, não há escrita. Exclusão permanente não é suportada na v2. Credenciais ficam em variáveis de ambiente, keychain do sistema ou cofre aprovado — nunca em perfis, relatórios, logs ou no repositório.

## Instalação e uso rápido

O runtime canônico é Claude Code; Codex, Gemini, Cursor, Windsurf, Goose e hosts compatíveis com Agent Skills podem consumir os mesmos arquivos, em caráter **experimental**.

```text
/plugin marketplace add agricidaniel/claude-ads
/plugin install claude-ads@ai-marketing-hub-claude-ads
```

Instalação a partir de clone local:

```bash
git clone https://github.com/AgriciDaniel/claude-ads.git
cd claude-ads
bash install.sh --source=local
```

Outros hosts, com targets explícitos:

```bash
bash install.sh --target=codex --source=local
bash install.sh --target=gemini --source=local --no-deps
```

Pré-requisitos: CPython 3.11 ou 3.12 para dependências gerenciadas; Linux x86_64 com glibc 2.28+ (musl não suportado); Playwright instalado pelo operador para captura de navegador; WeasyPrint e Pango para PDF. `--no-deps` faz instalação apenas da skill.

Releases publicam zip, `release-manifest.json`, `sbom.cdx.json` e `SHA256SUMS`. O README recomenda verificar com `sha256sum -c SHA256SUMS` antes de instalar, e avisa que os artefatos são **checksummed, not signed**. O instalador `--source=git` aceita `--ref` para pinar tag, branch ou commit e imprime o SHA resolvido.

## Exemplos de uso

Comandos publicados no README (standalone usam `/ads`; plugin usa `/claude-ads:ads`):

| Comando | Resultado |
| --- | --- |
| `/ads setup` | Salva perfil de cliente, conta, objetivo, privacidade e guardrails |
| `/ads audit google` ou `/ads audit all` | Auditoria completa ou por escopo, com evidência |
| `/ads plan` | Planos de canal, campanha, orçamento, concorrente e mensuração |
| `/ads create` | Copy, imagem, vídeo e briefs de foto de produto |
| `/ads launch --draft` | Plano de mudança em rascunho, sem tocar na conta |
| `/ads monitor` | Ritmo de gasto, entrega, tracking, fadiga, política e performance |
| `/ads optimize --draft` | Melhorias sugeridas e escritas como rascunho |
| `/ads experiment` | Desenho de teste controlado ou leitura de resultado |
| `/ads report` | Renderiza execução salva em Markdown, HTML ou PDF |
| `/ads research refresh` | Atualiza evidência de plataforma, política, API e benchmarks |
| `/ads validate` | Verifica contratos, execuções, capacidades ou prontidão de release |
| `/ads status` e `/ads next` | Situação atual e o bloqueador mais importante |

Atalhos como `/ads meta`, `/ads amazon` e `/ads reddit` vão direto à auditoria daquela plataforma. O fluxo do quickstart é: configurar, trazer evidência, auditar, reler o relatório e checar o próximo bloqueador.

## Quando usar (e quando não usar)

- **Use quando:** você precisa de uma auditoria de conta de anúncios reproduzível, com achado e evidência separados de recomendação.
- **Use quando:** o trabalho é multi-plataforma e a saída precisa ser comparável entre contas e execuções.
- **Use quando:** a organização exige que o agente **não** altere contas sem aprovação e diff.
- **Evite quando:** você quer automação de lances ou mudanças de campanha em produção. A escrita está atrás de gates e os perfis de saúde estão desativados.
- **Evite quando:** o ambiente não pode instalar Python 3.11/3.12, Playwright ou as bibliotecas de PDF.
- **Evite quando:** você espera hosts além de Claude Code com paridade — o README marca os demais como experimentais.

## Limitações e cuidados

- **Somente o README foi lido.** Código, `ads/`, `skills/`, `agents/`, `control-plane/`, `claude_ads_core/`, testes, evals e Cockpit não foram consultados. Capacidades, gates e cobertura são afirmações do projeto.
- **Status declarado: development candidate.** O próprio README diz que o projeto não está pronto para release enquanto todos os gates de `RELEASE_REQUIREMENTS.md` não passarem em contexto de verificação novo.
- **Sem health score.** Os 12 perfis de pontuação estão desativados; a saída é achado + evidência + cobertura, não uma nota. Isso limita comparação entre contas.
- **Cobertura baixa não é falha.** Abaixo de 60% a execução é classificada como evidência insuficiente, mas o README não define como o usuário deve obter os dados faltantes.
- **Distribuição dupla.** Existe um espelho comunitário em `AI-Marketing-Hub/claude-ads` para membros do AI Marketing Hub Pro; a fronteira entre release público e desenvolvimento privado não é detalhada.
- **Verificação de integridade parcial.** Releases têm checksum e SBOM, não assinatura; um checksum confirma correspondência com o publicado, não a origem.
- **Dependências externas de runtime.** Captura de navegador e PDF dependem de bibliotecas do host, fora do contrato de dependências gerenciadas.
- **Marketing no README.** O projeto promove o Skool "AI Marketing Hub Pro" e mantém um espelho pago para acesso antecipado; separe conteúdo técnico de promoção.
- **Dados sensíveis.** Exportações de conta, prompts, transcrições e credenciais não devem entrar em Git, relatórios ou arquivos de release — orientação do próprio README.

## Estado e adoção

- **Versão citada:** v2.x; a instalação alerta sobre o alias obsoleto `agricidaniel-claude-ads` anterior à v2.0.0. Cockpit é um complemento opcional na versão 0.1.0.
- **Atividade e popularidade observadas em 2026-10-19:** ~10,1 mil estrelas, ~1,5 mil forks, 3 issues abertas; criado em 2026-02-11 e último push em 2026-10-17.
- **Licença:** MIT para código e documentação originais; APIs, marcas e artefatos de terceiros seguem seus próprios termos.
- **Linguagem principal:** Python.
- **Commit de referência:** `fc3908e786c318776df89a3a098333da377364be`.

## Relações

- **Mantido por:** [AgriciDaniel](../../../entities/agricidaniel.md).
- **Conceitos:** [Auditoria de mídia paga](../../../concepts/auditoria-de-midia-paga.md) — achado, evidência e cobertura; [Agent skills](../../../concepts/agent-skills.md) — skill instalada por plugin e por instalador; [Evidência e proveniência](../../../concepts/evidencia-e-proveniencia.md) — quatro estados de controle e cobertura; [CLI agent-first](../../../concepts/cli-agent-first.md) — comandos com saída estruturada e validação; [Saída completa de agente](../../../concepts/saida-completa-de-agente.md) — execução parcial declarada em vez de relatório incompleto.
- **Alternativas:** [msitarzewski/agency-agents](../msitarzewski/agency-agents.md) — inclui personalidades de marketing e um fluxo de takeover de mídia paga, mas sem auditoria executável por plataforma. Ferramentas de mídia paga convencionais não estão documentadas na wiki.

## Perguntas abertas

- Quais controles compõem os 12 perfis de saúde e o que falta para habilitá-los?
- Como o condutor decide que um dado ausente é `unknown` e não um `fail`?
- O manifesto de capacidades descreve APIs oficiais de cada plataforma ou há scraping/captura de navegador?
- A confirmação de escrita é imposta por código, por hook ou apenas por instrução da skill?
- Como os 12 workers lidam com limites de rate e com dados desatualizados?
- Qual é a diferença prática entre a distribuição MIT e o espelho para membros?
- Como o audit se comporta em contas com múltiplas moedas e fusos?

## Fontes

- README: https://github.com/AgriciDaniel/claude-ads/blob/main/README.md (commit `fc3908e786c318776df89a3a098333da377364be`, consultado em 2026-10-19). Somente o README foi lido; código, skills internas, `control-plane/`, testes e documentação não foram consultados.
- Metadados do repositório e do perfil: API do GitHub em 2026-10-19 (licença, linguagem, estrelas, forks, issues e datas).
