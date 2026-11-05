---
type: concept
aliases: [Compliance regulatório com agentes, Regulatory compliance agent skills, LGPD compliance]
status: draft
created: 2026-11-05
updated: 2026-11-05
tags: [compliance, privacidade, juridico, auditoria, agentes]
---

# Conformidade regulatória com agentes

> Skills que conduzem, passo a passo, a conformidade de um projeto com uma lei ou regulação específica — citando artigo e fonte normativa, produzindo artefatos versionados e pausando em pontos que exigem decisão humana ou jurídica.

## Definição

Conformidade regulatória com agentes é o padrão de empacotar o conhecimento de uma legislação (e das normas infralegais que a regulamentam) como instruções que um agente de código executa sobre uma base de software real: mapeiam dados e fluxos, geram documentação exigida por lei (registros, relatórios de impacto, políticas), implementam controles técnicos (consentimento, exclusão, criptografia, retenção) e guiam a resposta a eventos com prazo legal (incidentes de segurança). O resultado não é um relatório de texto solto, mas **artefatos vivos versionados em Git**, revisáveis em PR, que documentam o estado real de conformidade e evoluem com o projeto.

Isso o distingue de:

- **consultoria jurídica tradicional** — opinião e documento produzidos por um advogado, sem vínculo automático com o código;
- **ferramenta de compliance SaaS** — produto fechado que roda fora do repositório, sem artefato versionado junto ao código que gerou o risco;
- **checklist estático** — lista de boas práticas sem orquestração, sem estado, sem distinguir o que já foi feito do que falta.

## Como funciona

O padrão observado no [goul4rt/lgpd-skills](../repos/github.com/goul4rt/lgpd-skills.md):

```text
cenário do projeto (greenfield | legado | híbrido | incidente)
  -> maestro escolhe pipeline e ordem das sub-skills
  -> cada sub-skill: lê código/schema -> aplica norma citada por artigo -> produz artefato em `.lgpd/`
  -> checkpoints pausam o fluxo para revisão humana antes de continuar
  -> disclaimer explícito: não substitui decisão jurídica/do encarregado
```

| Componente | Papel |
|---|---|
| **Maestro** | Orquestra o pipeline, mantém estado (`STATUS.md`) e decide a ordem das sub-skills conforme o cenário |
| **Sub-skills** | Cada uma cobre uma obrigação legal específica (base legal, ROPA, RIPD, DSAR, incidente, DPA, retenção...) e roda isolada ou encadeada |
| **Encode normativo** | Arquivo de referência com o texto/citação das normas, mantido manualmente e sujeito a desatualização quando o regulador publica novas resoluções |
| **Artefatos vivos** | Documentos e schemas versionados em uma pasta dedicada (`.lgpd/`), não conversas efêmeras |
| **Checkpoints** | Pontos do pipeline em que o fluxo pausa para revisão antes de prosseguir, especialmente antes de publicar política ou notificar o regulador |
| **Disclaimer** | Aviso explícito de que a skill não substitui aconselhamento jurídico, repetido nos pontos de maior risco |

Dois elementos sustentam a confiabilidade do padrão: **citação por artigo/norma** em vez de paráfrase genérica de boas práticas, e **separação entre o que a skill produz (rascunho/análise) e o que exige aprovação humana/jurídica** (notificação ao regulador, cláusula contratual negociada, texto final publicado).

## Onde aparece

- [goul4rt/lgpd-skills](../repos/github.com/goul4rt/lgpd-skills.md) — primeiro e único exemplo documentado nesta wiki: 19 skills (1 maestro + 18 sub-skills) para LGPD (Lei 13.709/2018), resoluções da ANPD e ECA Digital (Lei 15.211/2025), com quatro pipelines por cenário e artefatos em `.lgpd/`.

## Trade-offs

- **Vantagens:** artefato de conformidade rastreável junto ao código que ele descreve; citação por artigo torna a recomendação verificável, não apenas plausível; checkpoints reduzem o risco de uma ação de alto custo (notificar o regulador, publicar política) sem revisão humana; cobre tanto documentação legal quanto implementação técnica (schema de consentimento, log imutável, criptografia).
- **Limitações:** o encode normativo é mantido manualmente e envelhece sempre que o regulador publica nova resolução — o próprio projeto pede ajuda da comunidade para isso; assume uma stack específica para os templates de código, que precisam de adaptação fora dela; não substitui avaliação jurídica em decisões de alto risco (comunicação à ANPD, cláusulas contratuais negociadas); depende de o agente interpretar corretamente o estado real do código para preencher mapeamento de dados e ROPA.
- **Critério prático:** vale para organizar e documentar uma auditoria ou retrofit de conformidade com rastreabilidade por commit; não substitui o Encarregado de Dados nem o jurídico em decisões vinculantes.

## Relações

- **Relacionado a:** [Auditoria de mídia paga](auditoria-de-midia-paga.md) — mesmo padrão de achado/artefato versionado aplicado a um domínio diferente; [Cibersegurança com agentes](ciberseguranca-com-agentes.md) — controles técnicos adjacentes (criptografia, logging, retenção) sem o enquadramento jurídico por artigo; [Evidência e proveniência](evidencia-e-proveniencia.md) — artefato como registro canônico, não conversa; [Agent skills](agent-skills.md) — formato de distribuição do método.
- **Contrasta com:** consultoria jurídica sem artefato versionado; ferramentas de compliance SaaS fechadas; checklists estáticos sem orquestração nem estado.
- **Depende de:** um encode normativo mantido e atualizado; checkpoints respeitados pelo operador humano; uma stack de código compatível com os templates, ou adaptação manual quando não é.

## Perguntas abertas

- Como manter o encode normativo atualizado sem reintroduzir o mesmo problema que motiva a skill (conformidade que se desatualiza)?
- O padrão generaliza para outras leis de proteção de dados (GDPR, CCPA) com a mesma arquitetura de maestro + sub-skills, ou cada jurisdição exigiria um pacote próprio?
- Que garantia existe de que os artefatos gerados (ROPA, RIPD) de fato satisfazem um auditor ou a própria ANPD, além de representarem o entendimento da skill sobre a norma?
- Como o padrão lida com conflito entre o que o código realmente faz e o que o desenvolvedor descreve ao agente durante o mapeamento de dados?

## Fontes

- [goul4rt/lgpd-skills](../repos/github.com/goul4rt/lgpd-skills.md) — README no commit `d85d79abeeb37cb99fc0785e735a9ca790698a77` (consultado em 2026-11-05). Somente o README foi lido; os `SKILL.md` individuais e o `normative-reference.md` não foram consultados.
