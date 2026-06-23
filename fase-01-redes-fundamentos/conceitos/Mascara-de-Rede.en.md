---
tipo: conceito
area: Networking
camada-osi: 3
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](Mascara-de-Rede.md)

# Subnet Mask

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

What is the subnet mask for?::To define which part of the IP is the network (building) and which is the host (apartment).
What is /24 in CIDR notation?::Mask 255.255.255.0 — 254 possible hosts.
What is /16?::Mask 255.255.0.0 — 65534 possible hosts.
When do two devices need a router to communicate?::When they are on different networks (masks indicating different "buildings").
In the IP 192.168.1.1/24, which is the network and which is the host?::Network = 192.168.1 (building); Host = .1 (apartment).
What are the 4 uses of the subnet mask?::1) Local route vs gateway; 2) Network address; 3) Broadcast; 4) Network size (how many hosts fit).
In the block 192.168.1.0/24, what is the network address and the broadcast?::Network = 192.168.1.0; Broadcast = 192.168.1.255.
How many usable hosts fit in /25?::126 (2^7 = 128, minus 2 = 126).
What is /30 for?::A point-to-point link — supports only 2 usable hosts.
What is the decimal mask of /26?::255.255.255.192.
What is the decimal mask of /27?::255.255.255.224.
What is the decimal mask of /28?::255.255.255.240.
What is the decimal mask of /29?::255.255.255.248.
What is the master rule for the decimal mask?::Mask = 256 minus the block size. Block = 2 raised to the number of host bits.
How many usable hosts in /27?::30 (2^5 = 32, minus 2 = 30).
In the network 192.168.50.0/27, what is the broadcast address?::192.168.50.31 (network 0 + block 32 minus 1).
What are the values of the 8 bits of an octet, from least to most significant?::1, 2, 4, 8, 16, 32, 64, 128. Sum = 255.
What is the subnet-count formula when splitting a parent network?::2 raised to (new prefix minus old prefix).
Splitting /24 into /27, how many subnets result?::8 (2 to the 3rd, because 27 minus 24 = 3 borrowed bits).
What does each bit borrowed for the network do to the subnet count?::Doubles it. 1 bit = 2 subnets, 2 bits = 4, 3 bits = 8, 4 bits = 16.
What is the RFC 1918 Class A private mask?::/8. Range 10.0.0.0 to 10.255.255.255.
What is the RFC 1918 Class B private mask?::/12. Range 172.16.0.0 to 172.31.255.255.
What is the RFC 1918 Class C private mask?::/16. Range 192.168.0.0 to 192.168.255.255.
Why is 192.168.0.0/24 not the RFC 1918 private range?::Because /24 is a single 256-address network. The full private range is /16 (65k addresses). The /24 is just a piece inside the /16 lot.
