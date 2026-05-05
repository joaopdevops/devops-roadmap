# Fase 01 — Redes Fundamentos

Fundamentos de redes (CCNA 1). Foco em entender o que está sendo abstraído nas camadas que DevOps usa (cloud, containers, Kubernetes).

## Estrutura

- `labs/` — labs práticos (Packet Tracer + Linux real)
- `conceitos/` — notas atômicas com flashcards (Spaced Repetition)
- `resumos/` — resumos semanais consolidados
- `projeto-integrador/` — projeto final da fase (a definir)

## Labs

1. **1.1 Redes no Mundo Real** — LAN, Switch, IP, ping, ICMP
2. **1.2 Componentes de Rede** — Roteador, Gateway, ARP, primeiro ping
3. **1.3 Modelos OSI e TCP/IP** — camadas, encapsulamento, PDU
4. **1.4 Meios Físicos e Cabos** — UTP, fibra, Wi-Fi, atenuação
5. **2.1 Endereçamento IPv4** — 32 bits, classes, RFC 1918, subnetting `2^n − 2`

## Conceitos atômicos

ARP · Atenuação · Fibra Óptica · Gateway · ICMP · Interferência · LAN · Máscara de Rede · Modelo OSI · RFC 1918 · Roteador · Switch · UTP · Wi-Fi

Cada nota tem:
- Conceito + analogia canônica
- Exemplos concretos
- Seção "Por que DevOps importa" (Docker / Kubernetes / AWS / Terraform)
- Flashcards no formato `Pergunta?::Resposta.`

## Por que isso importa

Cloud abstrai a rede física. Você precisa saber o que está sendo abstraído pra debugar quando quebra.

Cada conceito aqui aparece direto no dia a dia DevOps:
- ARP → tabelas CAM em switches gerenciados
- RFC 1918 → VPCs AWS, redes Docker, Kubernetes pods
- Gateway → default route em containers e nodes
- Subnetting → planejamento de VPCs e service CIDRs
- OSI → debug de comunicação em service mesh
