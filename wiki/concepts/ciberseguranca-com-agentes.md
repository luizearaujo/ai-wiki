---
type: concept
aliases: [Cibersegurança com agentes, Agentic cybersecurity, Segurança ofensiva e defensiva com agentes, AI security agents]
status: draft
created: 2026-10-19
updated: 2026-10-19
tags: [ciberseguranca, agentes, red-team, blue-team, dfir, skills]
---

# Cibersegurança com agentes

> Uso de agentes de IA para executar trabalho de segurança — defesa, resposta a incidentes, threat hunting e testes ofensivos autorizados — com conhecimento estruturado, ferramentas locais e supervisão humana.

## Definição

Cibersegurança com agentes é a aplicação de agentes a tarefas de segurança: analisar tráfego e artefatos, investigar incidentes, correlacionar evidências, mapear técnicas a frameworks, executar verificações de configuração e conduzir exercícios ofensivos dentro de escopo autorizado.

O conceito não descreve **segurança de agentes** (proteger o próprio agente contra prompt injection, vazamento de credenciais ou ações indevidas), embora os dois se cruzem. Aqui o agente é o operador; a segurança é o domínio de aplicação.

## Como funciona

Os padrões observados:

1. **Conhecimento procedural empacotado.** Skills descrevem quando usar uma técnica, pré-requisitos, workflow, verificação e referências — em vez de esperar que o modelo saiba o procedimento de memória.
2. **Descoberta progressiva.** O agente varre descrições curtas, seleciona poucas skills relevantes e só então carrega o workflow completo. Isso permite catálogos grandes sem inflar o contexto.
3. **Mapeamento de frameworks.** Técnicas viram metadados (ATT&CK, NIST CSF, ATLAS, D3FEND, AI RMF, F3), o que permite consulta, cobertura e relatórios.
4. **Ferramentas locais ou MCP.** O agente executa binários, consulta APIs ou usa um servidor local; a análise pode ficar na máquina, mas o conteúdo enviado ao modelo depende da configuração.
5. **Escopo e autorização.** O trabalho ofensivo exige alvo, permissão escrita e regras de engajamento; a evidência do que foi executado precisa ser registrada.

## Onde aparece

- [mukul975/Anthropic-Cybersecurity-Skills](../repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — biblioteca de 818 skills em 34 domínios, com mapeamento a seis frameworks e carregamento progressivo.
- [SnailSploit/Claude-Red](../repos/github.com/snailsploit/claude-red.md) — recorte exclusivamente ofensivo: 78 skills em 23 categorias, carregadas por gatilho conversacional e instaladas como skills do Claude.
- [morluto/rea](../repos/github.com/morluto/rea.md) — engenharia reversa de binários e análise em runtime com agentes, incluindo evidência estruturada.
- [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — AgentShield e agentes de segurança que auditam hooks, MCP e permissões da configuração do agente.
- [littledivy/mimic](../repos/github.com/littledivy/mimic.md) — captura de tráfego autenticado e geração de cliente, com atenção a certificate pinning e DPoP.

## Trade-offs

- **Vantagens:** acesso a playbooks consistentes; cobertura de muitos domínios; mapeamento automático a frameworks; velocidade em triagem e documentação; possibilidade de operar localmente.
- **Limitações:** o agente pode alucinar comandos ou conclusões; a qualidade das skills varia; técnicas ofensivas exigem autorização e podem causar dano; a execução depende de ferramentas e ambiente; auditoria e responsabilidade continuam humanas.
- **Critério prático:** use o agente para acelerar análise, hipóteses e relatórios, mas exija validação humana antes de ações destrutivas ou decisões de produção.

## Relações

- **Relacionado a:** [Agent skills](agent-skills.md) — formato de distribuição do conhecimento; [Engenharia reversa agêntica](engenharia-reversa-agentica.md) — subconjunto voltado a artefatos sem código-fonte; [Evidência e proveniência](evidencia-e-proveniencia.md) — requisito para que a saída seja auditável; [Model Context Protocol](model-context-protocol.md) — integração com ferramentas.
- **Contrasta com:** automação determinística de SIEM/SOAR, que executa regras fixas sem julgamento do modelo.
- **Pré-requisito para:** usar agentes em red team, blue team ou DFIR com escopo e evidência.

## Perguntas abertas

- Como medir a qualidade de uma skill de segurança e a taxa de erro do agente que a executa?
- Como garantir que o agente não ultrapasse o escopo autorizado?
- Quais tarefas de segurança realmente se beneficiam de um LLM e quais exigem automação determinística?
- Como auditar instruções e scripts de terceiros antes de instalá-los?
- Como conciliar análise local com o envio de conteúdo sensível ao provedor do modelo?

## Fontes

- [mukul975/Anthropic-Cybersecurity-Skills](../repos/github.com/mukul975/anthropic-cybersecurity-skills.md) — README no commit `54a798831d2266a3ca61ce68a7acb80b81160d57` (consultado em 2026-10-19).
- [SnailSploit/Claude-Red](../repos/github.com/snailsploit/claude-red.md) — README no commit `a8de813edc9f66f60d44cfe42d47750e89d9930b` (consultado em 2026-10-19).
- [morluto/rea](../repos/github.com/morluto/rea.md) e [affaan-m/ECC](../repos/github.com/affaan-m/ecc.md) — páginas existentes da wiki, usadas como comparação.
- [littledivy/mimic](../repos/github.com/littledivy/mimic.md) — página existente da wiki, usada como exemplo de captura de tráfego.
