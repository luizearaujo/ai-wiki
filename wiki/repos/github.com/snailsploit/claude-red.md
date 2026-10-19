---
type: repo
url: https://github.com/SnailSploit/Claude-Red
host: github.com
owner: snailsploit
repo: claude-red
commit: a8de813edc9f66f60d44cfe42d47750e89d9930b
license: MIT
language: Python
status: active
created: 2026-10-19
ingested: 2026-10-19
updated: 2026-10-19
tags: [ciberseguranca, red-team, seguranca-ofensiva, skills, agentes, pentest]
---

# SnailSploit/Claude-Red

> Biblioteca curada de 78 skills de segurança ofensiva para o sistema de Skills do Claude, organizadas em 23 categorias e carregadas sob demanda por gatilhos conversacionais.

## O que é

O `claude-red` empacota metodologia de red team em arquivos `SKILL.md`: cada skill cobre uma superfície de ataque específica — injeção de SQL, XSS, SSRF, shellcode, evasão de EDR, abuso de ADCS — e descreve técnicas, ferramentas, casos de borda e caminhos de escalação.

O README posiciona cada skill como um especialista de domínio que o Claude carrega quando o assunto aparece na conversa. Casos de uso declarados: engajamentos autorizados de red team, triagem de bug bounty, pesquisa de segurança, preparação para CTF, treinamento de operadores e exploração metódica de superfície de ataque. O autor mantém um site de pesquisa em [snailsploit.com](https://snailsploit.com).

A biblioteca é explicitamente ofensiva. O README não publica regras de engajamento, aviso legal ou política de uso responsável além da lista de casos de uso; autorização e conformidade ficam por conta do usuário.

## Como funciona

O repositório organiza as skills em `Skills/<categoria>/<slug>/SKILL.md`. O README publica 23 categorias e 78 skills:

| Categoria | Skills | Foco |
|---|---:|---|
| Web Application | 16 | OWASP Top 10, lógica de negócio e classes avançadas de falhas web |
| Wireless | 14 | 802.11, WPA2/3, EAP, WPS, evil twin, BLE, Zigbee, Z-Wave, LoRa e sub-GHz |
| Infrastructure & Red Team | 7 | Acesso inicial, evasão de EDR, operações avançadas e internals do Windows |
| Exploit Development | 6 | Corrupção de pilha/heap, ROP, mitigações, análise de crash e TOCTOU |
| Fuzzing & Vulnerability Research | 4 | libFuzzer, AFL++, fuzzing guiado por cobertura e taxonomia de vulnerabilidades |
| Post-Exploitation | 3 | Movimento lateral, persistência e exfiltração de dados |
| Auth & Identity, API Security, Container & Kubernetes, CI/CD, Cryptography, Privilege Escalation, Forensics & C2, Supply Chain, Social Engineering, Reconnaissance, Utility | 2 cada | JWT/OAuth, APIs, escape de container, pipeline, TLS, privesc, anti-forense/C2, dependências, phishing/SE, OSINT e checklists/report |
| Active Directory, Cloud, Mobile, IoT & Embedded, Network Attacks, AI Security | 1 cada | AD on-prem, multi-cloud, Android/iOS, firmware/ICS, camada 2/3 e segurança de IA |

O carregamento é **sob demanda**: o Claude consulta as descrições das skills e só carrega o conteúdo completo quando o gatilho conversacional corresponde — por exemplo, mencionar SQL injection carrega `offensive-sqli`. Com isso, o README afirma que skills não usadas não ocupam contexto.

O README não detalha a estrutura interna de um `SKILL.md` (frontmatter, seções, scripts auxiliares), o mecanismo exato de descoberta nem como o conjunto foi testado. **A verificar.**

## Instalação e uso rápido

Requisitos: um ambiente compatível com o sistema de Skills do Claude, como Claude Code ou Claude.ai. O README também oferece um instalador interativo.

```bash
# Claude Skills System (recomendado)
git clone https://github.com/SnailSploit/claude-red ~/.claude/skills/claude-red

# Instalar apenas uma categoria
git clone --filter=blob:none --sparse https://github.com/SnailSploit/claude-red
cd claude-red && git sparse-checkout set Skills/web Skills/active-directory

# Instalador
./install.sh                           # interativo
./install.sh --target ~/.claude/skills # destino explícito
./install.sh --category web            # categoria única
```

No Claude Code, o README sugere injetar um `SKILL.md` como system prompt:

```bash
cat Skills/web/offensive-sqli/SKILL.md | claude --system-file -
cat Skills/active-directory/**/SKILL.md | claude --system-file -
```

No Claude.ai, a orientação é colar o conteúdo de um `SKILL.md` no system prompt de um Project ou no início da conversa.

## Exemplos de uso

Exemplos derivados do README, não instruções oficiais:

- **Web:** pedir uma metodologia para testar SQL injection em uma aplicação autorizada; a skill `offensive-sqli` entra com payloads por banco, variações cegas e OOB e CVEs de ORM.
- **Active Directory:** solicitar um roteiro de enumeração e ataque a AD; a skill cobre Kerberoast, AS-REP Roast, ACL abuse, ADCS ESC1–15, delegação e ambientes híbridos.
- **Exploit development:** pedir análise de um crash e avaliação de explorabilidade; as skills de crash analysis, mitigations e ROP organizam o triage e as cadeias de bypass.
- **Wireless:** conduzir um assessment de WPA2/WPA3; as skills separam recon, captura de handshake/PMKID, ataques a SAE e evil twin.

## Quando usar (e quando não usar)

- **Use quando:** você conduz trabalho ofensivo **autorizado** — red team, pentest, bug bounty ou CTF — e quer que o agente carregue um playbook de domínio em vez de improvisar.
- **Use quando:** precisa de cobertura ampla de superfícies e de uma organização por categoria para instalar só o subconjunto relevante.
- **Evite quando:** não há autorização escrita ou escopo definido; a biblioteca documenta técnicas que causam dano real e não fornece controles de escopo.
- **Evite quando:** você espera execução confiável e determinística. O artefato é conhecimento procedural; a execução depende do agente, das ferramentas e do ambiente.
- **Evite quando:** o risco de supply chain de instruções é inaceitável — 78 arquivos de terceiros passam a influenciar o comportamento do agente e não há auditoria publicada.

## Limitações e cuidados

- **Somente o README foi lido.** As 78 skills, o `install.sh`, o `CHANGELOG.md`, o `CONTRIBUTING.md` e a licença não foram inspecionados.
- **Conteúdo ofensivo dual-use.** As categorias incluem evasão de EDR, anti-forense, C2, phishing, keylogging e shellcode. O README não traz aviso legal nem política de uso; a responsabilidade é do operador.
- **Qualidade não uniforme.** São 78 skills de um único autor e colaboradores; não há avaliação publicada de precisão, atualidade ou taxa de erro.
- **Risco de instruções de terceiros.** Instalar o repositório adiciona dezenas de instruções ao contexto do agente; revise o que habilitar e mantenha escopo de autorização explícito.
- **Alguns exemplos parecem perigosos por construção.** As skills de keylogger e de evasão de EDR descrevem arquitetura de captura de entrada e bypass de defesas; não há indicação de controles de segurança embutidos.
- **Contagens do README.** A tabela de categorias soma 78 skills em 23 categorias, consistente com os badges. Não foi verificado se todos os diretórios existem.
- **Idioma.** O conteúdo é em inglês; esta página resume apenas o que o README publica.

## Estado e adoção

- Badges do README: 78 skills, 23 categorias, licença MIT.
- Roadmap declarado no README: fases de expansão para criptografia de identidade em nuvem, IoT e web avançada, com alvo de ~130 skills em 23+ categorias; as fases 3, 7, 8 e 9 aparecem como completas.
- Observado em 2026-10-19: ~7,6 mil stars, ~1,0 mil forks; criado em 2026-03-04; último push em 2026-10-12; branch padrão `main`.
- Licença: MIT. Linguagem principal na API: Python (o README não descreve componentes Python além do instalador).
- Não há releases citadas no README; o histórico está em `CHANGELOG.md`, não consultado.

## Relações

- Mantido por: [SnailSploit](../../../entities/snailsploit.md) — Kai Aizen, pesquisa em segurança de IA generativa.
- Conceitos: [Agent skills](../../../concepts/agent-skills.md), [Cibersegurança com agentes](../../../concepts/ciberseguranca-com-agentes.md), [Evidência e proveniência](../../../concepts/evidencia-e-proveniencia.md).
- Relacionado: [mukul975/Anthropic-Cybersecurity-Skills](../mukul975/anthropic-cybersecurity-skills.md) — catálogo maior e mais amplo, que inclui defesa, DFIR e mapeamentos de framework; [msitarzewski/agency-agents](../msitarzewski/agency-agents.md) — personalidades especializadas em Markdown.
- Alternativas: playbooks internos de red team, documentação de frameworks ofensivos e bibliotecas de skills focadas em defesa.

## Perguntas abertas

- Qual é a qualidade real das 78 skills e como ela varia entre categorias?
- As skills foram testadas em engajamentos reais? Há relatos ou métricas publicadas?
- Como o conjunto lida com atualização de técnicas e CVEs ao longo do tempo?
- Existe revisão de segurança das instruções e scripts de instalação?
- Como garantir que o agente não ultrapasse o escopo autorizado ao carregar uma skill ofensiva?
- O instalador sobrescreve skills existentes ou permite convivência com outras coleções?

## Fontes

- README: https://raw.githubusercontent.com/SnailSploit/Claude-Red/a8de813edc9f66f60d44cfe42d47750e89d9930b/README.md (commit `a8de813edc9f66f60d44cfe42d47750e89d9930b`, consultado em 2026-10-19). Somente o README foi lido; skills, `install.sh`, `CHANGELOG.md`, `CONTRIBUTING.md`, licença e código não foram consultados.
- Metadados: API do GitHub (`/repos/SnailSploit/claude-red`) em 2026-10-19.
