---
tipo: conceito
area: Redes
camada-osi: 3
tags: [conceito, flashcards, redes]
---

# Máscara de Rede (Subnet Mask)

Define qual parte do endereço IP é a **rede** e qual é o **dispositivo** (host).

**Analogia:** o "prédio" do endereço. Dispositivos no mesmo prédio se comunicam direto. Se o prédio for diferente, precisa do [[Conceitos/Roteador]].

**Exemplo:**
- IP: `192.168.1.1`
- Máscara: `255.255.255.0` (equivalente a `/24`)
- Rede: `192.168.1` → o "prédio"
- Host: `.1` → o "apartamento"

**Dispositivos que se comunicam diretamente:** mesma rede (mesmo prédio)
**Dispositivos que precisam de roteador:** redes diferentes (prédios diferentes)

**Notação CIDR:**
- `/24` = 255.255.255.0 → 254 hosts
- `/16` = 255.255.0.0 → 65534 hosts
- `/8`  = 255.0.0.0 → 16 milhões de hosts

## 4 funções da máscara

**1. Rota local vs gateway**
Determina se o destino está no mesmo prédio (comunicação direta) ou em prédio diferente (precisa passar pelo [[Conceitos/Gateway|gateway]]). É a decisão fundamental de roteamento local.

**2. Endereço de rede**
Primeiro endereço do bloco — identifica o "prédio". Não pode ser atribuído a host.
Exemplo em `/24`: `192.168.1.0` → endereço da rede.

**3. Broadcast**
Último endereço do bloco — pacote enviado para todos os hosts da rede. Não pode ser atribuído a host.
Exemplo em `/24`: `192.168.1.255` → broadcast da rede.

**4. Tamanho da rede**
Define quantos hosts cabem no bloco. Fórmula: 2^(bits de host) − 2 (desconta rede e broadcast).

| Máscara | Hosts úteis |
|---|---|
| /24 | 254 |
| /25 | 126 |
| /26 | 62 |
| /29 | 6 (sub-rede pequena, 2-4 hosts + gateway) |
| /30 | 2 (enlaces ponto a ponto) |

## Labs onde foi ensinado
- `1.1-Redes-no-Mundo-Real.md` — primeiro contato (`/24`)
- `2.1-Enderecamento-IPv4.md` — fórmula `2^h − 2` e tabela CIDR
- `2.2-Subnetting-Pratico.md` — `/29` aplicado em topologia real (4 sub-redes)

## Conceito relacionado
- `Subnetting.md` — o ato de dividir uma rede em sub-redes estendendo a máscara
- `TTL.md` — prova material de que o pacote atravessou o gateway

---

## 🇺🇸 English

Defines which part of the IP address is the **network** and which is the **device** (host).

**Analogy:** the "building" of the address. Devices in the same building talk directly. If the building is different, a router is needed.

**Example:**
- IP: `192.168.1.1`
- Mask: `255.255.255.0` (equivalent to `/24`)
- Network: `192.168.1` → the "building"
- Host: `.1` → the "apartment"

**Devices that communicate directly:** same network (same building)
**Devices that need a router:** different networks (different buildings)

**CIDR notation:**
- `/24` = 255.255.255.0 → 254 hosts
- `/16` = 255.255.0.0 → 65534 hosts
- `/8`  = 255.0.0.0 → 16 million hosts

## The 4 functions of the mask

**1. Local route vs gateway** — decides whether the destination is in the same building (direct communication) or a different building (must go through the gateway). The fundamental local routing decision.

**2. Network address** — the first address of the block, identifies the "building". Cannot be assigned to a host. In `/24`: `192.168.1.0`.

**3. Broadcast** — the last address of the block, a packet sent to all hosts on the network. Cannot be assigned to a host. In `/24`: `192.168.1.255`.

**4. Network size** — how many hosts fit in the block. Formula: 2^(host bits) − 2 (minus network and broadcast).

## Canonical table /24 to /30 (memorize)

| Mask | Block | Usable hosts | Last octet | Where it shows up |
|---|---|---|---|---|
| /24 | 256 | 254 | **0**   (256-256) | Default home network |
| /25 | 128 | 126 | **128** (256-128) | Split a /24 in 2 |
| /26 | 64  | 62  | **192** (256-64)  | Split a /24 in 4 |
| /27 | 32  | 30  | **224** (256-32)  | Medium subnet |
| /28 | 16  | 14  | **240** (256-16)  | Small subnet |
| /29 | 8   | 6   | **248** (256-8)   | Lab 2.2 — 4 subnets |
| /30 | 4   | 2   | **252** (256-4)   | Point-to-point router-to-router link |

**Master rule (memorize this, end of story):**
```
mask in decimal = 256 - block_size
block_size      = 2^(host bits) = 2^(32 - prefix)
usable hosts    = block_size - 2
```

**Anti-drift rule (full subnetting):**
```
broadcast    = network address + block − 1
next subnet  = network address + block
```

## Daily drill — practice EVERY day until it is automatic

1. Say out loud: `/24=0, /25=128, /26=192, /27=224, /28=240, /29=248, /30=252`
2. Reverse: given the decimal mask, give the prefix. E.g. 224 → /27
3. Usable hosts: given the prefix, give the hosts. E.g. /27 → 30 hosts
4. Given a network `192.168.50.0/27`, state: network `.0`, broadcast `.31`, first usable `.1`, last usable `.30`, next subnet starts at `.32`
5. Subnet count: given the parent network and the new prefix, state how many subnets. E.g. `/24 → /27` = 2³ = **8** subnets.

## Common pitfalls to drill

**1. Adjacent-answer drift on the mask.** When asked for the mask of prefix X, do not return the mask of the lab you just finished. E.g. just finished with /29 (248); if asked for /28, it is **240**, not 248.
**Antidote:** apply the rule `mask = 256 − block` **mentally** before answering. For /28: host bits = 32-28 = 4 → block = 2⁴ = 16 → mask = 256-16 = **240**. Without the math, you return the neighbor.

**2. Subnet count on division.** When asked "how many subnets result from splitting X into Y", do not estimate — use the formula.
- **Canonical formula:** `number of subnets = 2^(new prefix − old prefix)`. E.g. `/24 → /27` = 2^(27-24) = 2³ = **8**.
- **Alternative check:** `parent network total ÷ subnet block` = 256 ÷ 32 = **8**.
- Each bit borrowed for the network **doubles** the number of subnets (1 bit = 2, 2 bits = 4, 3 bits = 8, 4 bits = 16...).

## Two layers of mask — do not confuse

**1. The mask of the RFC 1918 "lot"** = the size of the available private space. **Fixed** by the standard:

| Range | RFC mask | Lot size |
|---|---|---|
| `10.0.0.0/8` | /8 | 16.7 million addresses |
| `172.16.0.0/12` | /12 | 1 million addresses (172.16.0.0 to 172.31.255.255) |
| `192.168.0.0/16` | /16 | 65,536 addresses (192.168.0.0 to 192.168.255.255) |

**2. The mask of the subnets YOU create inside the lot** = how you cut the land. **Free** — it is normal subnetting (/24, /27, /28...).

**Analogy:** the RFC gives you 3 plots of different sizes. The **plot size** is fixed, not negotiable. **Inside the plot**, you divide into as many lots as you want, of whatever size you want.

**Trap:** writing `192.168.0.0/24` as "the private Class C range" is wrong. /24 is just **one street** inside the `192.168.0.0/16` plot. The whole plot is /16.

## Why memorizing this table matters

Subnetting is foundational. It shows up in:
- **CCNA exam:** manual calculation questions under a timer
- **AWS VPC:** designing subnets in a `10.0.0.0/16` VPC requires knowing how many /24 fit (256), how many /28 (4096), etc
- **Docker/Kubernetes:** defining a container/pod network CIDR
- **Troubleshooting:** "why can't this IP reach that one?" → almost always a wrong mask

An online calculator is a crutch — in the exam you do not have one; in a 3 a.m. production incident you want it automatic.

## Where it was taught
- Lab 1.1 — Networking in the real world (introduction)
- Lab 2.1 — IPv4 Addressing (manual calculation)
- Lab 2.2 — Practical Subnetting (/29 applied to a real topology, 4 subnets)

---

## Flashcards

Para que serve a mascara de rede?::To define which part of the IP is the network (building) and which is the host (apartment).
O que e /24 em notacao CIDR?::Mask 255.255.255.0 — 254 possible hosts.
O que e /16?::Mask 255.255.0.0 — 65534 possible hosts.
Quando dois dispositivos precisam de roteador para se comunicar?::When they are on different networks (masks indicating different "buildings").
No IP 192.168.1.1/24, qual e a rede e qual e o host?::Network = 192.168.1 (building); Host = .1 (apartment).
Quais sao os 4 usos da mascara de rede?::1) Local route vs gateway; 2) Network address; 3) Broadcast; 4) Network size (how many hosts fit).
No bloco 192.168.1.0/24, qual e o endereco de rede e o broadcast?::Network = 192.168.1.0; Broadcast = 192.168.1.255.
Quantos hosts uteis cabem em /25?::126 (2^7 = 128, minus 2 = 126).
Para que serve o /30?::A point-to-point link — supports only 2 usable hosts.
Qual a mascara em decimal de /25?::255.255.255.128.
Qual a mascara em decimal de /26?::255.255.255.192.
Qual a mascara em decimal de /27?::255.255.255.224.
Qual a mascara em decimal de /28?::255.255.255.240.
Qual a mascara em decimal de /29?::255.255.255.248.
Qual a mascara em decimal de /30?::255.255.255.252.
Qual a regra mestra para mascara em decimal?::Mask = 256 minus the block size. Block = 2 raised to the number of host bits.
Quantos hosts uteis em /27?::30 (2^5 = 32, minus 2 = 30).
Quantos hosts uteis em /28?::14 (2^4 = 16, minus 2 = 14).
Na rede 192.168.50.0/27, qual o endereco de broadcast?::192.168.50.31 (network 0 + block 32 minus 1).
Na rede 192.168.50.0/27, onde comeca a proxima sub-rede?::At 192.168.50.32.
Quais sao os valores dos 8 bits de um octeto, do menos significativo ao maior?::1, 2, 4, 8, 16, 32, 64, 128. Sum = 255.
Por que devolver a mascara do lab anterior quando perguntam outra?::Adjacent-deviation pattern — returning the fresh calculation instead of the one asked. Watch out.
Qual a regra anti-desvio para broadcast em subnetting?::Broadcast = network address plus block minus 1.
Qual a formula da contagem de sub-redes ao dividir uma rede mae?::2 raised to (new prefix minus old prefix).
Dividindo /24 em /27, quantas sub-redes saem?::8 (2 to the 3rd, because 27 minus 24 = 3 borrowed bits).
Qual a verificacao alternativa da contagem de sub-redes?::Parent network total divided by the subnet block size. E.g. 256 divided by 32 = 8.
O que cada bit emprestado pra rede faz na contagem de sub-redes?::Doubles it. 1 bit = 2 subnets, 2 bits = 4, 3 bits = 8, 4 bits = 16.
Antes de devolver mascara em decimal, qual passo nao pular?::Compute 256 minus block. Block = 2 raised to (32 minus prefix). Without this step, I return the neighbor.
Mascara da rede privada Classe A da RFC 1918?::/8. Range 10.0.0.0 to 10.255.255.255.
Mascara da rede privada Classe B da RFC 1918?::/12. Range 172.16.0.0 to 172.31.255.255.
Mascara da rede privada Classe C da RFC 1918?::/16. Range 192.168.0.0 to 192.168.255.255.
Por que 192.168.0.0/24 nao e a faixa privada da RFC 1918?::Because /24 is a single 256-address network. The full private range is /16 (65k addresses). The /24 is just a piece inside the /16 lot.
Qual a diferenca entre mascara da RFC 1918 e mascara de sub-rede?::RFC mask = size of the whole lot (fixed: /8, /12, /16). Subnet mask = how I split the lot internally (free, I do subnetting). They are different layers.
