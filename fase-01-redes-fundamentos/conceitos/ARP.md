---
tipo: conceito
area: Redes
camada-osi: 2
protocolo: ARP
tags: [conceito, flashcards, redes]
---

# ARP — Address Resolution Protocol

Protocolo que descobre o **endereço MAC** de um dispositivo a partir do seu **endereço IP**.

Antes de enviar um pacote, o dispositivo precisa saber o MAC do destino. O ARP resolve isso:

1. Broadcast na rede: *"Quem tem o IP 192.168.1.2? Me diz seu MAC!"*
2. O dono do IP responde com seu MAC.
3. O remetente salva isso na **tabela ARP** (cache) para não perguntar de novo.

**Por que o primeiro ping perde 1 pacote?**
Porque o ARP ainda está descobrindo o MAC. Na segunda tentativa, o MAC já está em cache → 0% loss.

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.2-Componentes-de-Rede]]
- Vai aparecer muito em troubleshooting de redes

---

## 🇺🇸 English

A protocol that discovers a device's **MAC address** from its **IP address**.

Before sending a packet, the device needs to know the destination's MAC. ARP solves this:

1. Broadcast on the network: *"Who has IP 192.168.1.2? Tell me your MAC!"*
2. The owner of that IP replies with its MAC.
3. The sender saves it in the **ARP table** (cache) so it does not have to ask again.

**Why does the first ping drop 1 packet?**
Because ARP is still discovering the MAC. On the second attempt, the MAC is already cached → 0% loss.

## Where it was taught
- Lab 1.2 — Network components
- Will show up a lot in network troubleshooting

---

## Flashcards

O que o ARP descobre?::A device's MAC address from its IP.
Em qual camada OSI o ARP opera?::Layer 2 (Data Link).
Por que o primeiro ping perde 1 pacote?::Because ARP is discovering the destination's MAC. On the second ping, the MAC is already cached.
ARP faz parte do ping?::No. ARP runs BEFORE the ping. The ping itself is just ICMP.
