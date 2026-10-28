---
type: repo
url: https://github.com/Zagitta/gpu-unlock
host: github.com
owner: Zagitta
repo: gpu-unlock
commit: 1fc6d628c49c7fba34ef3a2e7f758700d35ce890
license: desconhecida
language: C
status: active
created: 2026-10-27
ingested: 2026-10-27
updated: 2026-10-27
tags: [gpu, tensor-cores, kernel-module, inferencia-local, treinamento-local, linux, geforce, nvidia]
---

# Zagitta/gpu-unlock

> Módulo de kernel Linux que remove, antes do driver NVIDIA carregar, o limite de metade da taxa de tensor cores que a NVIDIA impõe a placas GeForce em FP16/BF16/TF32 com acumulação FP32.

## O que é

NVIDIA limita por firmware a taxa de tensor cores de placas GeForce (RTX 20/30/40) para FP16, BF16 e TF32 com acumulação FP32 — o formato usado por quase todo treinamento e inferência não quantizada de IA — a metade da taxa que o mesmo silício entrega nas linhas profissionais (RTX A-series/datacenter). O `gpu_unlock` remove esse limite no boot, antes do driver NVIDIA padrão (não modificado) assumir a placa, sem flash de VBIOS e sem precisar ser refeito a cada nova versão do driver.

## Como funciona

O README descreve a técnica como a combinação do método V67/PLM do projeto `cmpunlocker` com o timing pré-driver da abordagem via UEFI. No boot, o módulo roda o unlock, grava os seletores de velocidade (SS0 `0x88888888`, que seleciona a taxa plena de BF16, e o SS1 de 4 bits `0x8`, IMLA4) e executa um FLR (Function-Level Reset) antes do driver NVIDIA binder a placa. Não é uma aplicação UEFI nem um driver NVIDIA modificado.

Os IDs PCI exatos suportados estão em `kernel/gpu_unlock/recipes.c` (não lido — fora do escopo desta ingestão, que cobre apenas o README).

O módulo só age se a linha de comando do kernel tiver `gpu_unlock.targets=all` ou uma lista de endereços PCI (`lspci -D`); um alvo não suportado é logado e ignorado. Os pacotes colocam o módulo e seu firmware gerado no initramfs, antes do módulo `nvidia`, via drop-ins para mkinitcpio, initramfs-tools e dracut. Suspend-to-RAM reseta os seletores de velocidade; um notifier de suspensão reaplica o unlock antes do `nvidia` resumir cada placa (pode ser desativado com `gpu_unlock.resume=0`). Hibernação não é coberta.

## Instalação e uso rápido

```sh
git clone https://github.com/Zagitta/gpu-unlock
cd gpu-unlock
make install
```

Depois, acrescentar `gpu_unlock.targets=all` à linha de comando do kernel (GRUB, grubby, systemd-boot ou UKI, conforme a distribuição) e reiniciar. `make install` detecta a distribuição via `/etc/os-release` e seleciona entre os alvos `install-arch`, `install-deb` e `install-rpm`; o README também documenta alvos de build isolado (`make arch`/`deb`/`rpm`) e cache de insumos NVIDIA em `~/.cache/gpu-unlock/inputs`.

Verificação pós-instalação:

```sh
journalctl -k -b | grep gpu_unlock
lspci -nnk -s 0000:[ID]:00.0
```

## Exemplos de uso

- Treinamento (fine-tuning LoRA ou completo) e inferência não quantizada em BF16/FP16 localmente em uma RTX 3090 ou 4090, para aproveitar o ganho de throughput sem trocar de placa.
- Pipelines de geração de imagem/vídeo (SDXL, SD 1.5, ComfyUI, Wan 2.2) em FP16/BF16 que já seriam candidatos a rodar com [Comfy-Org/ComfyUI](../comfy-org/comfyui.md) ou ferramentas similares de inferência local.

Exemplos derivados do README; não são instruções oficiais além do que ele publica.

## Quando usar (e quando não usar)

- **Use quando:** a carga é FP16/BF16/TF32 com acumulação FP32 (prefill de LLM, fine-tuning, geração de imagem/vídeo, FlashAttention/SDPA) em uma GeForce RTX série 20/30/40 sob Linux, e o usuário aceita rodar um módulo de kernel de terceiros não assinado pela NVIDIA.
- **Evite quando:** a carga é decode de LLM (memory-bound), INT8/FP8/INT4 quantizado, jogos ou CUDA FP32 — o README declara "sem mudança" nesses casos. Também evite em Blackwell (RTX 50, não suportado) e em notebooks cuja GPU dedicada é desligada quando ociosa, o que reseta o unlock silenciosamente.

## Limitações e cuidados

- Linux apenas; o README não mantém porte para Windows, apontando para um fork de terceiros (`impacifist/Windows-GPU-UNLOCK`) sem endosso de manutenção.
- Suporte a Ampere (RTX 30) é descrito como "estável, 100+ relatos de usuário"; Ada Lovelace (RTX 40) e Turing (RTX 20) são "experimentais"; Blackwell (RTX 50) não é suportado e "improvável de acontecer".
- O README alerta explicitamente contra sites, instaladores e criptomoedas associados ao projeto além do próprio repositório GitHub — não há "o" instalador ou moeda oficial.
- Risco de dano declarado pelo autor como "muito improvável", já que o throttling e a gestão de energia padrão permanecem intactos; não verificado de forma independente nesta ingestão.
- Cada build baixa insumos NVIDIA/CachyOS via HTTPS e gera firmware apenas no diretório de build e no pacote binário; o pacote fonte Debian e o `.nosrc.rpm` não contêm esses arquivos.
- **A verificar:** a licença. O badge e o texto do README afirmam que o módulo de kernel e o empacotamento local são GPL-2.0-only (com o firmware gerado sob os termos da NVIDIA, ver `firmware/NOTICE.md` e `licenses/`), mas a API do GitHub não detecta nenhum arquivo `LICENSE` reconhecido (`license: null`). Não há arquivo de licença formal confirmado nesta ingestão.
- Esta página documenta apenas o conteúdo do `README.md`; `recipes.c`, scripts de build e demais arquivos do repositório não foram lidos.

## Estado e adoção

- Versão: `2.0.0` (badge do README).
- Repositório criado em 2026-10-18 e com push mais recente em 2026-10-27; 11.402 estrelas, 1.118 forks e 78 issues abertas observadas em 2026-10-27 — crescimento muito rápido para um repositório de ~9 dias, registrado apenas como observação datada.
- Licença: GPL-2.0-only declarada no README para o módulo/empacotamento; não confirmada por arquivo `LICENSE` detectável pela API do GitHub (ver Limitações).

## Relações

- Mantido por: [Zagitta (Simon)](../../../entities/zagitta.md).
- Conceitos: nenhum conceito dedicado nesta wiki cobre "cap de hardware por segmentação de mercado" ou "unlock de tensor cores"; a página fica listada na categoria [Inferência local e runtime de modelos](../../../categorias.md#inferência-local-e-runtime-de-modelos).
- Alternativas: nenhuma alternativa de software é citada no README; o próprio README é a única fonte "oficial", conforme sua seção de FAQ.

## Perguntas abertas

- Qual é de fato a licença formal do repositório, já que a API do GitHub não a detecta apesar do badge/texto declararem GPL-2.0-only?
- Como o projeto se comporta em kernels e versões de driver NVIDIA futuras, já que depende de timing pré-driver e de firmware extraído de uma versão de driver pinada (`610.43.03`, apenas para extração, segundo o FAQ)?

## Fontes

- README: https://raw.githubusercontent.com/Zagitta/gpu-unlock/1fc6d628c49c7fba34ef3a2e7f758700d35ce890/README.md (commit `1fc6d628c49c7fba34ef3a2e7f758700d35ce890`, consultado em 2026-10-27). Somente o README foi lido; os demais arquivos do repositório não foram consultados.
- Metadados: API do GitHub (`api.github.com/repos/Zagitta/gpu-unlock`), consultada em 2026-10-27.
