---
tipo: conceito
area: Redes
camada-osi: 3
protocolo: ICMP
tags: [conceito, flashcards, redes]
primeira-aparicao: 2026-06-10
---
mtu fragmentacao
# MTU e Fragmentação

## Definição rápida

**MTU (Maximum Transmission Unit)** = o **tamanho máximo** de um pacote que uma interface de rede aceita transmitir, em bytes. Padrão da Ethernet/Wi-Fi: **1500**. Se um pacote passa do MTU, ele precisa ser **fragmentado** (quebrado em pedaços menores) — ou é **recusado**, se estiver marcado pra não fragmentar.

## Analogia

**MTU = tamanho máximo da caixa que cabe no caminhão dos Correios.**

A encomenda (teus dados) tem que caber numa caixa padrão. Se ela é maior que a caixa:
- ou os Correios **dividem em caixas menores** (fragmentação) e remontam no destino;
- ou, se a encomenda está carimbada **"NÃO PODE DIVIDIR"** (o **DF bit** = *Don't Fragment*), os Correios **devolvem um bilhete**: *"não coube, manda menor"*. Esse bilhete é uma mensagem **ICMP**.

## A conta — por que 1472 é o número mágico

O MTU de 1500 é o tamanho do **pacote IP inteiro**, e dentro dele já vão etiquetas obrigatórias antes do teu recheio:

| Parte | Bytes | O que é |
|---|---|---|
| Cabeçalho **IP** | 20 | endereço de origem/destino (a etiqueta) |
| Cabeçalho **ICMP** | 8 | o tipo do ping |
| **Recheio** (o teu `-s`) | o resto | os dados |
| **TOTAL máximo** | **1500** | o MTU |

Então: `1500 − 20 − 8 =` **`1472`** bytes de recheio máximo num ping.

- **1472** + 28 = 1500 → cabe na caixa, **passa**
- **1473** + 28 = 1501 → 1 byte além, **estoura**

## Vendo ao vivo no Linux (o que eu fiz)

```bash
ip link show wlp0s20f3        # acha o MTU da placa Wi-Fi -> mtu 1500
ping -c 2 -M do -s 1472 8.8.8.8   # cabe exato -> passa, 0% loss
ping -c 2 -M do -s 1473 8.8.8.8   # 1 byte alem -> "Message too long"
```

- `-s 1472` = **s**ize: tamanho do recheio, em bytes
- `-M do` = **do**n't fragment: carimba o pacote como "PROIBIDO partir" (liga o DF bit)
- `lo` (loopback) tem MTU 65536 porque é virtual, não tem meio físico — não serve pro teste

## Quem avisa quando não cabe

Quando o pacote excede o MTU **e** o DF bit está ligado:
- Se o gargalo é a **própria placa de saída**, a máquina barra local (foi o "Message too long" que vi — o pacote nem saiu).
- Se o gargalo é um **roteador no meio do caminho** (link menor lá na frente), esse roteador devolve um **ICMP Tipo 3, Código 4** ("Fragmentation Needed but DF set") pra origem.

Esse ICMP Tipo 3/4 é a base do **Path MTU Discovery** — como a origem descobre o menor MTU do caminho inteiro e ajusta o tamanho dos pacotes.

> ICMP de novo: ele não é só o "tá vivo?" do ping — é o **mensageiro de erros da rede**.

## Por que DevOps importa

Uma das causas **mais traiçoeiras** de bug em produção:

- **Kubernetes:** redes overlay (Flannel, Calico, VXLAN) **reduzem o MTU** dos pods abaixo de 1500. Se não ajustado, pacote grande estoura no encapsulamento.
- **VPN / túneis (IPsec, GRE, WireGuard):** o encapsulamento come bytes do MTU. App conecta, faz ping, parece tudo bem — mas **trava ao transferir arquivo grande**.
- Sintoma clássico: "conexão abre mas congela em transferências grandes". Quem sabe de MTU resolve em minutos; quem não sabe perde dias caçando fantasma.

## Relacionado

- [[Conceitos/ICMP]] — quem entrega o aviso de "não coube" (Tipo 3 Código 4)
- [[Conceitos/TTL]] — outro campo do cabeçalho IP, mesma lógica de "limite no pacote"
- [[Conceitos/Roteador]] — quem fragmenta ou gera o ICMP no meio do caminho

---

## Flashcards

O que e MTU?::Maximum Transmission Unit — tamanho maximo em bytes de um pacote que uma interface aceita transmitir. Padrao Ethernet/Wi-Fi e 1500.
Por que o recheio maximo de um ping e 1472 e nao 1500?::Porque 1500 e o pacote IP inteiro; 20 bytes vao no cabecalho IP e 8 no cabecalho ICMP. 1500 - 20 - 8 = 1472.
O que e o DF bit?::Don't Fragment — marca no pacote que proibe fragmentacao. Se o pacote nao cabe no MTU e o DF esta ligado, ele e recusado em vez de dividido.
O que acontece com um pacote maior que o MTU sem o DF bit?::Ele e fragmentado (dividido em pedacos menores) e remontado no destino.
Quem avisa a origem que um pacote nao coube e o DF estava ligado?::Um ICMP Tipo 3 (Destination Unreachable) Codigo 4 (Fragmentation Needed) enviado pelo roteador do gargalo.
O que e Path MTU Discovery?::Mecanismo onde a origem descobre o menor MTU do caminho inteiro usando os ICMP Tipo 3/4, e ajusta o tamanho dos pacotes pra nao fragmentar.
Por que a interface loopback tem MTU 65536?::Porque e virtual, nao passa por meio fisico, entao nao tem limite fisico real de tamanho de quadro.
Por que MTU importa em Kubernetes e VPN?::Redes overlay e tuneis reduzem o MTU pelo encapsulamento. Se nao ajustado, pacotes grandes estouram e a conexao trava em transferencias grandes.
