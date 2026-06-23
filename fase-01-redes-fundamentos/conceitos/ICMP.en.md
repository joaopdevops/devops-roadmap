---
tipo: conceito
area: Networking
camada-osi: 3
protocolo: ICMP
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](ICMP.md)

# ICMP — Internet Control Message Protocol

A protocol used to **test connectivity**. It does not transfer data — it only checks whether the path is open.

Used by the `ping` command.

**How it works:**
- **Echo Request:** "hey, are you there?"
- **Echo Reply:** "yes, I am!"
- **0% packet loss** = perfect communication

**On Linux:**
```bash
ping 192.168.1.2        # continuous ping
ping -c 4 192.168.1.2   # send 4 packets and stop
```

## Where it was taught
- Lab 1.1 — Networking in the real world
- Lab 1.2 — Network components

---

## Flashcards

What is ICMP used for?::Testing connectivity. It does not transfer data, only checks whether the path is open.
Which command uses ICMP?::ping.
Echo Request vs Echo Reply?::Request = "are you there?"; Reply = "yes, I am!".
What does 0% packet loss mean?::Every packet sent was answered — perfect communication.
At which OSI layer does ICMP operate?::Layer 3 (Network).
