---
tipo: conceito
area: Networking
camada-osi: 2
protocolo: ARP
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](ARP.md)

# ARP — Address Resolution Protocol

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

What does ARP discover?::A device's MAC address from its IP.
At which OSI layer does ARP operate?::Layer 2 (Data Link).
Why does the first ping drop 1 packet?::Because ARP is discovering the destination's MAC. On the second ping, the MAC is already cached.
Is ARP part of the ping?::No. ARP runs BEFORE the ping. The ping itself is just ICMP.
