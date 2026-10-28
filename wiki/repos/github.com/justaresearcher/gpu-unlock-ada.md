---
type: repo
url: https://github.com/JustAResearcher/gpu-unlock-ada
host: github.com
owner: JustAResearcher
repo: gpu-unlock-ada
commit: d28c485418c3d9d034cd4bac19200bc33dd3453b
license: GPL-2.0
language: C
status: active
created: 2026-10-27
ingested: 2026-10-27
updated: 2026-10-27
tags: [gpu, tensor-cores, kernel-module, inferencia-local, treinamento-local, linux, geforce, nvidia, ada-lovelace, rtx-40]
---

# JustAResearcher/gpu-unlock-ada

> Fork de [Zagitta/gpu-unlock](../zagitta/gpu-unlock.md) que estende o desbloqueio de tensor cores para a RTX 4090 (suporte principal) e uma lista crescente de GPUs Ada Lovelace (RTX 40) experimentais, com flag de opt-in por chip.

## O que é

O `gpu-unlock-ada` integra o payload de desbloqueio AD102 (extraído do trabalho publicado por [TOTORONG/AD103_win_unlocker](https://huggingface.co/TOTORONG/AD103_win_unlocker)) ao módulo de kernel, geração de firmware e empacotamento de boot do `Zagitta/gpu-unlock`. O resultado é o mesmo efeito — remover o cap de metade da taxa de tensor cores em FP16/BF16/TF32 com acumulação FP32 — mas com suporte dedicado à RTX 4090 (AD102) como caminho principal, e uma tabela de IDs PCI "experimentais" da geração Ada (AD102/AD103/AD104/AD106/AD107, incluindo variantes de notebook) que exigem cada uma sua própria flag de opt-in.

## Como funciona

O caminho da RTX 4090 roda o firmware assinado, verifica o marcador de conclusão do payload e as permissões exigidas, grava os seletores de velocidade SS0 `0x88888888` e SS1 `0x8`, e executa um FLR (Function-Level Reset) antes do driver NVIDIA (não modificado) assumir a placa — mesmo mecanismo do repositório-base. Para as demais GPUs Ada da tabela "Experimental Ada targets", o módulo reaproveita o firmware/payload da família AD102 pinado, mas só age se o usuário passar, além do endereço PCI exato, uma flag específica do chip (ex.: `gpu_unlock.ad103_experimental=1`, `gpu_unlock.ad107_experimental=1`). `targets=all` nunca seleciona esses IDs experimentais — cada um precisa ser nomeado explicitamente.

O README documenta, linha a linha, o PCI ID, o die, a flag de opt-in e o grau de teste (de "oito placas em um host" a "um relato de proprietário") para cada um dos 16 IDs Ada cobertos, incluindo três variantes de notebook (`2757` RTX 4090 Laptop, `28a0`/`28e0` RTX 4060 Laptop, `28e1` RTX 4050 Laptop). O suporte legado GA102/GA104/GA103/GA106 do repositório-base é mantido sem revalidação de cada placa.

Uma contribuição experimental separada (`windows/ad104-msi/`) documenta um boot manual único em Windows via UEFI para uma RTX 4070 Ti (AD104) em uma placa MSI específica; o README deixa explícito que isso **não** adiciona suporte a AD104 ao módulo Linux.

## Instalação e uso rápido

```sh
git clone https://github.com/JustAResearcher/gpu-unlock-ada.git
cd gpu-unlock-ada
make install
```

`make install` detecta a distribuição e expõe os mesmos alvos do repositório-base (`install-arch`, `install-deb`, `install-rpm`); builds isolados via `make arch`/`deb`/`rpm`. Depois, a linha de comando do kernel precisa de `gpu_unlock.targets=<endereço PCI ou all>` e, para qualquer ID da tabela experimental, da flag de opt-in correspondente, por exemplo:

```text
gpu_unlock.targets=0000:01:00.0 gpu_unlock.ad107_experimental=1
```

O README recomenda ligar a máquina "do zero" (power off completo) para a primeira tentativa, já que um reboot a quente não garante o estado de firmware necessário; verificação via `journalctl -k -b | grep gpu_unlock` e `lspci -nnk`.

## Exemplos de uso

- RTX 4090 em treinamento/inferência BF16/FP16 local, como caminho principal e mais testado do fork.
- GPUs Ada de notebook (RTX 4050/4060/4090 Laptop) cuja compatibilidade não está no repositório-base `Zagitta/gpu-unlock`, mas aparece aqui como experimental com relatos pontuais (ex.: `28a0`, o mesmo PCI ID da RTX 4060 Laptop/Max-Q discutido na consulta anterior desta wiki).

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** a placa é uma RTX 4090 (caminho validado) ou um dos IDs da tabela experimental, e o usuário aceita o risco de um caminho com teste de "uma ou poucas placas" por ID, exigindo a flag de opt-in exata.
- **Evite quando:** a placa é um ID Ada não listado na tabela, uma RTX A-series/datacenter, ou se o usuário precisa de uma solução validada e não experimental — nesse caso a RTX 3090/3080 etc. no `Zagitta/gpu-unlock` têm mais relatos de confirmação.

## Limitações e cuidados

- O README é explícito: "resultados vêm de uma ou poucas placas por ID; outras placas, configurações de memória e modelos de notebook permanecem não verificados" e "firmware compartilhado entre chips Ada não estabelece suporte para placas não testadas".
- Notebooks variam em exposição de VBIOS, trilhos de energia do controlador embarcado e tratamento de FLR — um resultado em um modelo não se transfere para outro.
- Qualquer reload do driver, ou RTD3 (desligamento da GPU dedicada em notebook quando ociosa), reseta os seletores de velocidade; o módulo não consegue re-desbloquear em runtime.
- O número de FP8 é descrito como "variável" e dependente da forma do kernel usado; o próprio README mostra um caso onde o ganho de FP8 não aparece numa GEMM CUTLASS que usa apenas ~17% do pico da placa.
- Uma carga de inferência MoE quantizada em uma RTX 4090 modificada mostrou ganho zero (0,983×), consistente com o unlock não afetar o caminho de matmul quantizado.
- Licença GPL-2.0-only para módulo, empacotamento e integração do payload (confirmada pela API do GitHub nesta ingestão); firmware NVIDIA permanece sob termos próprios.
- Esta página documenta apenas o conteúdo do `README.md`; os relatórios individuais em `docs/`, `docs/evidence/`, scripts e demais arquivos do repositório não foram lidos.

## Estado e adoção

- Versão citada no título do README: `1.1.1`.
- Repositório criado em 2026-10-23 e com push mais recente em 2026-10-26; 4.284 estrelas, 557 forks e 43 issues abertas observadas em 2026-10-27 — crescimento rápido para ~4 dias de existência, registrado apenas como observação datada.
- Licença: GPL-2.0, confirmada pela API do GitHub.

## Relações

- Mantido por: [JustAResearcher (Tim)](../../../entities/justaresearcher.md).
- Repositório-base: [Zagitta/gpu-unlock](../zagitta/gpu-unlock.md) — este fork deriva o módulo Linux, geração de firmware e empacotamento de boot diretamente dele, adicionando o payload Ada.
- Conceitos: nenhum conceito dedicado nesta wiki cobre "cap de hardware por segmentação de mercado" ou "unlock de tensor cores"; a página fica na categoria [Inferência local e runtime de modelos](../../../categorias.md#inferência-local-e-runtime-de-modelos).
- Alternativas citadas no README: [goldlionren/gpu-unlock-4080s](https://github.com/Goldlionren/gpu-unlock-4080s) (medição de FP8 em RTX 4080 SUPER) e [A-XIANGQAQ/rtx4070tis-ad103-tensor-unlock](https://github.com/A-XIANGQAQ/rtx4070tis-ad103-tensor-unlock), citados como fontes de dados cruzados, não como projetos documentados nesta wiki.

## Perguntas abertas

- Qual a taxa real de confirmação por chip da tabela experimental, já que a maioria dos IDs tem apenas "uma placa" testada?
- Como o projeto absorve novas IDs Ada enviadas pela comunidade (ex.: PR #24, #34) e qual o processo de promoção de "experimental" para suporte confirmado?

## Fontes

- README: https://raw.githubusercontent.com/JustAResearcher/gpu-unlock-ada/d28c485418c3d9d034cd4bac19200bc33dd3453b/README.md (commit `d28c485418c3d9d034cd4bac19200bc33dd3453b`, consultado em 2026-10-27). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/JustAResearcher/gpu-unlock-ada`), consultada em 2026-10-27.
