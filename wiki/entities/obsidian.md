---
type: entity
kind: project
url: https://obsidian.md
created: 2026-10-19
updated: 2026-10-19
tags: [notas, markdown, grafo-de-conhecimento, pkm]
---

# Obsidian

> App de notas pessoais em Markdown local, com links bidirecionais e grafo visual entre notas; software proprietário mas gratuito para uso pessoal e comercial, com arquivos em formato aberto.

## O que é

Obsidian é um app de gerenciamento de conhecimento pessoal ("The free and flexible app for your private thoughts"). Guarda notas como arquivos Markdown simples, locais, dentro de uma pasta chamada "vault" — sem lock-in de formato proprietário. É mantido pela Obsidian.md (antes Dynalist Inc.), fundada por Shida Li e Erica Xu; o modelo de negócio é "100% sustentado por usuários, não investidores", com serviços opcionais pagos (Sync, Publish) sobre um núcleo gratuito.

**A verificar:** sede da empresa e papéis exatos dos fundadores — fontes consultadas (Wikipédia, fórum) divergem e não foram confirmadas por uma página oficial da empresa.

## Como funciona

- **Vault:** uma pasta no sistema de arquivos do usuário, com subpastas; pode ficar em qualquer lugar permitido pelo SO. Por ser texto puro, os arquivos podem ser editados por outros programas, e o Obsidian detecta mudanças externas automaticamente.
- **Links bidirecionais:** notas se conectam por `[[wikilinks]]`, formando uma wiki pessoal de ideias, pessoas e tópicos interligados.
- **Grafo visual:** visualização interativa de como as notas se relacionam (grafo global e grafo local por nota), útil para identificar padrões — mas é uma representação dos links já existentes nos arquivos, não uma camada de inferência própria.
- **Canvas:** espaço livre para brainstorming e diagramação.
- **Configuração por vault:** cada vault tem uma pasta oculta `.obsidian` com atalhos, temas e plugins da comunidade; configurações globais ficam em outro local do sistema, fora do vault.
- **Sincronização:** Obsidian Sync (serviço pago, ponta a ponta) ou serviços de terceiros (Dropbox, iCloud, OneDrive, Git, entre outros).
- **Plugins:** milhares de plugins e temas da comunidade sobre uma API aberta (exemplos citados: Calendar, Kanban, Dataview, Outliner, Tasks).
- **Recomendação oficial:** não criar vaults dentro de outros vaults — links internos são locais ao vault e podem não se atualizar corretamente entre eles; também recomenda não colocar um vault dentro da pasta de configurações do sistema.

## Relações

- Integra com: [Graphify-Labs/graphify](../repos/github.com/graphify-labs/graphify.md) — exporta o grafo de conhecimento gerado pelo Graphify como notas e links compatíveis com um vault do Obsidian (`graphify export obsidian`), preservando notas e configuração `.obsidian` já existentes, segundo a documentação do Graphify.
- Citado em: [Workflow Claude Code + Graphify + Obsidian](../analyses/claude-code-graphify-obsidian.md).
- Conceitos: [Wiki pessoal com LLMs](../concepts/wiki-pessoal-com-llms.md) — o gist original de Karpathy já cita o Obsidian como a "IDE" de navegação da wiki pessoal.

## Fontes

- https://obsidian.md/ (consultado em 2026-10-19).
- https://obsidian.md/help/data-storage (consultado em 2026-10-19).
- https://obsidian.md/help/links (consultado em 2026-10-19).
- Wikipédia, "Obsidian (software)" (consultado em 2026-10-19) — fundadores e licença proprietária; fonte secundária, não oficial.
