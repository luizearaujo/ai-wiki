---
type: repo
url: https://github.com/mukul975/Anthropic-Cybersecurity-Skills
host: github.com
owner: mukul975
repo: anthropic-cybersecurity-skills
commit: 54a798831d2266a3ca61ce68a7acb80b81160d57
license: Apache-2.0
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [ciberseguranca, agentes, skills, mitre-attack, nist, red-team, blue-team, defesa, dfir]
---

# mukul975/Anthropic-Cybersecurity-Skills

> Biblioteca de skills de cibersegurança para agentes de IA, organizada em 34 domínios e mapeada a seis frameworks — MITRE ATT&CK, NIST CSF 2.0, MITRE ATLAS, D3FEND, NIST AI RMF e MITRE F3.

## O que é

O projeto entrega conhecimento operacional de segurança em um formato que agentes conseguem carregar sob demanda: cada skill é um diretório com `SKILL.md`, referências, scripts e templates. O README posiciona a biblioteca como uma **base de conhecimento AI-native**, não como uma coleção de scripts ou checklists, e diz que as skills codificam fluxos de trabalho de analistas reais.

O alvo declarado é reduzir a lacuna de mão de obra em segurança: o agente recebe o playbook que transforma um LLM genérico em um analista capaz de escolher a técnica, verificar pré-requisitos, executar passos e validar resultados.

Apesar do nome, o README afirma explicitamente que o projeto é **independente e não afiliado à Anthropic PBC**. Também restringe o uso a testes de penetração autorizados, pesquisa, defesa e educação, e responsabiliza o usuário pelo cumprimento de leis e regras de engajamento.

## Como funciona

Cada skill segue a anatomia:

```
skills/<nome>/
├── SKILL.md              # frontmatter YAML + workflow em Markdown
├── references/
│   ├── standards.md      # mapeamentos MITRE/NIST
│   └── workflows.md      # procedimento técnico detalhado
├── scripts/
│   └── process.py        # scripts auxiliares
└── assets/
    └── template.md       # checklists e relatórios
```

O frontmatter traz `name`, `description`, `domain`, `subdomain`, `tags`, `atlas_techniques`, `d3fend_techniques`, `nist_ai_rmf`, `nist_csf`, autor, versão e licença. Os mapeamentos ATT&CK ficam em `references/standards.md` e em uma camada do ATT&CK Navigator incluída nos releases.

O carregamento é **progressivo**: o agente varre os frontmatters por cerca de 30 tokens por skill, seleciona as candidatas e carrega o workflow completo (estimado em 500–2.000 tokens). Com isso, a biblioteca inteira pode ser pesquisada em uma passada sem ocupar toda a janela de contexto.

### Seis frameworks

| Framework | Versão | Escopo | O que mapeia |
|---|---|---|---|
| MITRE ATT&CK | v19.1 | 15 táticas · Enterprise/Mobile/ICS | Comportamentos e TTPs de adversários |
| NIST CSF 2.0 | 2.0 | 6 funções · 22 categorias · 106 subcategorias | Postura organizacional de segurança |
| MITRE ATLAS | 2026.07 | 101 técnicas · 77 sub-técnicas | Ameaças adversariais a IA/ML |
| MITRE D3FEND | v1.4.0 | 270 técnicas | Contramedidas defensivas |
| NIST AI RMF | 1.0 | 4 funções | Gestão de risco de IA |
| MITRE F3 | v1.1 | 8 táticas · 123 técnicas | Fraude financeira habilitada por computador |

O README publica a cobertura por framework: MITRE ATT&CK 805 skills, NIST CSF 2.0 804, D3FEND 139, NIST AI RMF 97, MITRE F3 94 e ATLAS 93. Cada skill recebe apenas os frameworks relevantes ao seu tema.

### Domínios

| Domínio | Skills | Domínio | Skills |
|---|---:|---|---:|
| Cloud Security | 66 | Identity & Access Management | 40 |
| SOC Operations | 63 | Malware Analysis | 39 |
| Threat Hunting | 58 | Red Teaming | 35 |
| Threat Intelligence | 52 | Container Security | 33 |
| Web Application Security | 46 | OT/ICS Security | 29 |
| Network Security | 43 | API Security | 28 |
| Digital Forensics | 41 | Incident Response | 26 |
| Vulnerability Management | 25 | Ransomware Defense | 13 |
| Penetration Testing | 23 | Mobile Security | 13 |
| DevSecOps | 18 | Compliance & Governance | 10 |
| Zero Trust Architecture | 18 | Supply Chain Security | 8 |
| Endpoint Security | 17 | Threat Detection | 7 |
| Phishing Defense | 16 | Hardware & Firmware Security | 6 |
| Cryptography | 16 | Deception Technology | 6 |
| AI Security | 14 | Blockchain Security | 2 |
| Wireless Security | 2 | Privacy Compliance | 2 |
| Data Protection | 1 | Purple Team | 1 |

## Instalação e uso rápido

Requisitos: um agente compatível com o padrão [agentskills.io](https://agentskills.io); nenhuma dependência de build é mencionada.

```bash
# Opção recomendada pelo README
npx skills add mukul975/Anthropic-Cybersecurity-Skills

# Alternativa
git clone https://github.com/mukul975/Anthropic-Cybersecurity-Skills.git
cd Anthropic-Cybersecurity-Skills
```

O README lista compatibilidade com Claude Code, GitHub Copilot, Codex CLI, Cursor, Gemini CLI, Windsurf, Cline, Aider, Continue, Roo Code, Amazon Q Developer, Devin, Replit Agent, SWE-agent, OpenHands e frameworks como LangChain, CrewAI e AutoGen — 26+ plataformas no total.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais:

- **DFIR:** pedir ao agente que analise um dump de memória suspeito; ele seleciona skills de Volatility3, hunting de credential dumping e análise de event logs, executa o workflow e valida os IOCs contra ATT&CK T1003.
- **Detecção:** pedir regras Sigma para Kerberoasting e o mapeamento correspondente em ATT&CK e NIST CSF.
- **Cloud:** delimitar o escopo de um incidente que atravessa AWS, Azure e GCP usando as skills de Cloud Security e Cloud Forensics.
- **Compliance:** mapear controles e evidências para NIST CSF 2.0 ou NIST AI RMF.
- **Red team autorizado:** conduzir enumeração de Active Directory, BloodHound ou simulação de C2 dentro de um engajamento com permissão escrita.

## Quando usar (e quando não usar)

- **Use quando:** você quer dar a um agente conhecimento estruturado de segurança para trabalho autorizado — pentest, red team, blue team, DFIR, threat hunting, análise de malware ou compliance.
- **Use quando:** precisa de mapeamentos prontos entre técnicas e frameworks e de um formato de skills que vários clientes carregam.
- **Evite quando:** não há autorização escrita ou o alvo está fora do escopo legal — a biblioteca inclui técnicas ofensivas e dual-use.
- **Evite quando:** você precisa de uma ferramenta que execute exploração de forma confiável; aqui o artefato é conhecimento procedural, e a execução depende do agente e do ambiente.
- **Evite quando:** decisões de produção exigem validação humana e auditoria; trate a saída do agente como rascunho a revisar.

## Limitações e cuidados

- **Somente o README foi lido.** As 818 skills, os scripts, as referências, o `SECURITY.md` e as releases não foram inspecionados.
- **Contagem inconsistente.** O README alterna entre 817 e 818 skills; a descrição da API do GitHub informa 817, e a tabela de domínios soma 817. O badge e o texto principal dizem 818.
- **Projeto comunitário, não Anthropic.** O nome pode sugerir afiliação; o README nega isso explicitamente.
- **Superfície ofensiva.** Red-team, C2, phishing simulado e exploração são documentados como casos de uso. O próprio README exige autorização escrita e responsabiliza o usuário.
- **Qualidade não uniforme.** São centenas de contribuições comunitárias; não há auditoria pública do conteúdo nem taxa de erro dos workflows documentada.
- **Supply chain de instruções.** Instalar a biblioteca adiciona centenas de arquivos Markdown e scripts ao contexto potencial do agente; revise as skills que habilitar.
- **Mapeamentos podem envelhecer.** O README referencia ATT&CK v19.1 e diz que atualizações futuras serão feitas em release; a sincronia com os frameworks upstream não é garantida.
- **Promoção comercial.** O README promove Casky.ai, o GARS-2026 e tokens de acesso; separe conteúdo técnico de marketing.
- **Licença.** Apache-2.0 segundo o README e a API; a licença de contribuições individuais não foi verificada.

## Estado e adoção

- Releases citadas: v1.0.0 em 11/03/2026, com 734 skills, 26 domínios e mapeamento ATT&CK + NIST CSF; a `main` cresceu depois disso para 818 skills e seis frameworks.
- Observado em 2026-10-19: ~34,7 mil stars, ~4,2 mil forks, 63 issues abertas; criado em 2026-02-25; último push em 2026-08-31; branch padrão `main`.
- Licença: Apache-2.0. Linguagem principal na API: Python.
- Site: [mahipal.engineer/Anthropic-Cybersecurity-Skills](https://mahipal.engineer/Anthropic-Cybersecurity-Skills/).

## Relações

- Mantido por: [mukul975](../../../entities/mukul975.md) — Mahipal Jangra, também ligado ao Casky.ai e ao GARS-2026.
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [Cibersegurança com agentes](../../../concepts/ciberseguranca-com-agentes.md), [Evidência e proveniência](../../../concepts/evidencia-e-proveniencia.md).
- Relacionado: [morluto/rea](../morluto/rea.md) — engenharia reversa e análise de binários; [affaan-m/ECC](../affaan-m/ecc.md) — outro catálogo grande de skills; [msitarzewski/agency-agents](../msitarzewski/agency-agents.md) — personalidades de agente por especialidade; [SnailSploit/Claude-Red](../snailsploit/claude-red.md) — recorte exclusivamente ofensivo, sem mapeamento de frameworks.
- Alternativas: playbooks internos de SOC/DFIR, documentação oficial do MITRE/NIST e plataformas de segurança que embutem automação.

## Perguntas abertas

- Qual é a qualidade real das 818 skills e como ela varia entre domínios?
- Como os mapeamentos de framework são validados e atualizados quando ATT&CK, ATLAS ou D3FEND mudam?
- Como o agente escolhe entre centenas de skills sem duplicar trabalho ou carregar contexto demais?
- Os scripts auxiliares são seguros e mantidos, ou são exemplos?
- Existe auditoria independente do conteúdo e das instruções de terceiros?
- Qual é a relação entre a biblioteca, o Casky.ai e o GARS-2026 — dependência, patrocínio ou apenas divulgação?
- A contagem oficial é 817 ou 818 skills?

## Fontes

- README: https://raw.githubusercontent.com/mukul975/Anthropic-Cybersecurity-Skills/54a798831d2266a3ca61ce68a7acb80b81160d57/README.md (commit `54a798831d2266a3ca61ce68a7acb80b81160d57`, consultado em 2026-10-19). Somente o README foi lido; skills, scripts, `SECURITY.md`, docs e releases não foram consultados.
- Metadados: API do GitHub (`/repos/mukul975/Anthropic-Cybersecurity-Skills`) em 2026-10-19.
