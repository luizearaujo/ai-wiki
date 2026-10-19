---
type: concept
aliases: [Produção de vídeo agêntica, Agentic video production, Vídeo com agentes]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [agentes, video, producao, pipelines, skills]
---

# Produção de vídeo agêntica

> Uso de um agente de IA para conduzir o processo completo de produção de vídeo — pesquisa, roteiro, geração de ativos, edição, trilha, legendas e composição — em vez de gerar um clipe isolado a partir de um prompt.

## Definição

Produção de vídeo agêntica é a aplicação de um agente a um **processo de produção**, não a uma única chamada de modelo. O agente precisa decompor o pedido, escolher um pipeline, pesquisar o tema, escrever e revisar o roteiro, planejar cenas, selecionar ou gerar ativos, montar uma timeline, validar o resultado e prestar contas de custo e decisões.

Isso a distingue de:

- **geração de clipe** — um modelo texto-para-vídeo ou imagem-para-vídeo produz um trecho;
- **edição assistida** — o humano opera a timeline e a IA sugere cortes;
- **slideshow automatizado** — imagens estáticas animadas sem intenção de movimento real.

## Como funciona

O padrão observado no [calesthio/OpenMontage](../repos/github.com/calesthio/openmontage.md):

```text
pesquisa -> proposta -> roteiro -> plano de cenas -> ativos -> edição -> composição
```

Componentes típicos:

| Componente | Papel |
|---|---|
| **Pipeline** | Manifesto com etapas, ferramentas, critérios de revisão e gates |
| **Skills de direção** | Instruções por etapa — como pesquisar, escrever, planejar, editar |
| **Registro de ferramentas** | Geração de vídeo/imagem, TTS, música, análise, legendas, composição |
| **Seleção de provedor** | Escolha pontuada por adequação, qualidade, controle, custo, latência etc. |
| **Checkpoints** | Estado resumível, log de decisões e custo por produção |
| **Gates de qualidade** | Aprovação humana, validação pré-composição, auto-revisão pós-render |
| **Renderizador** | Remotion, HyperFrames, FFmpeg ou equivalente |

O custo e a qualidade dependem de uma decisão central: **gerar** ativos (modelos de imagem/vídeo, APIs pagas) ou **recuperar** filmagem real de acervos livres e editá-la. A segunda rota reduz custo e alucinação visual, mas exige busca semântica, indexação e critérios de direitos.

## Onde aparece

- [calesthio/OpenMontage](../repos/github.com/calesthio/openmontage.md) — sistema agent-first com 10+ pipelines, 100+ ferramentas, 60+ provedores, pesquisa web obrigatória e gates de qualidade; o assistente de código é o orquestrador.
- [graphify-labs/graphify](../repos/github.com/graphify-labs/graphify.md) — não produz vídeo, mas o mesmo padrão de skill + pipeline determinístico + verificação aparece na indexação de código.
- [SynkraAI/aiox-core](../repos/github.com/synkraai/aiox-core.md) — orquestração por artefatos e etapas, análoga ao encadeamento de um pipeline de produção.

## Trade-offs

- **Vantagens:** processo reproduzível; cobertura de etapas que um clipe isolado não resolve; possibilidade de usar acervos livres e modelos locais; auditoria de custo e decisão; qualidade verificável por gates.
- **Limitações:** custo e latência altos; muitas integrações e credenciais; direitos autorais e atribuição de mídia; qualidade depende de modelos externos; gates automatizados não substituem julgamento criativo; prompts e pipelines envelhecem rápido.
- **Critério prático:** vale quando o vídeo é um artefato recorrente e o processo importa; para um clipe único, uma chamada de modelo ou um editor manual pode ser mais barato.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — instruções por etapa; [Agent harness](agent-harness.md) — runtime que instala o processo; [Orquestração multiagente](orquestracao-multiagente.md) — quando etapas são delegadas a subagentes.
- **Depende de:** modelos de imagem/vídeo, TTS, música, análise de mídia e renderização programática.
- **Contrasta com:** geração de um único clipe; edição manual em timeline; templates de slideshow.

## Perguntas abertas

- Como medir qualidade de vídeo de forma objetiva, além de checks técnicos de áudio, frames e duração?
- Qual é o custo real de um minuto de vídeo em cada rota (geração, acervo, híbrido)?
- Como garantir direitos e atribuição ao usar acervos e conteúdo de referência?
- Gates de qualidade são aplicados por código, por hooks ou por convenção do agente?
- Como o processo lida com revisões humanas e com a preservação de decisões entre versões?

## Fontes

- [calesthio/OpenMontage](../repos/github.com/calesthio/openmontage.md) — README no commit `c8066452325cb57c8fc1ba8c2a71b6e8842e6b65` (consultado em 2026-10-19).
