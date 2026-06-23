---
tipo: conceito
area: Networking
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](Modelo-OSI.md)

# OSI Model — Open Systems Interconnection

A reference model with **7 layers** that describes how data travels through a network.

| Layer | Name | What it does | Example |
|--------|------|-----------|---------|
| 7 | Application | User interface | HTTP, DNS, SSH |
| 6 | Presentation | Formatting, encryption | SSL/TLS |
| 5 | Session | Manages connections | NetBIOS |
| 4 | Transport | Reliable delivery | TCP, UDP |
| 3 | Network | Addressing and routing | IP, ICMP |
| 2 | Data Link | Communication within the same network | Switch, ARP, MAC |
| 1 | Physical | Cables, electrical signals | Ethernet, Wi-Fi |

**Rule of thumb for DevOps:**
- Layer 2 → Switch, MAC address, LAN
- Layer 3 → Router, IP, Gateway, ICMP
- Layer 4 → TCP/UDP (ports — essential for Docker and Kubernetes)
- Layer 7 → where your applications live

## Where it was taught
- Lab 1.1 — Networking in the real world
- Lab 1.2 — Network components
- Deepened in: lab topic 1.3

---

## Flashcards

How many layers does the OSI model have?::7.
At which layer does the Switch operate?::Layer 2 (Data Link).
At which layer does the Router operate?::Layer 3 (Network).
At which layer do TCP and UDP live?::Layer 4 (Transport).
At which layer does HTTP live?::Layer 7 (Application).
What is the DevOps rule of thumb about Layer 4?::It is where the ports are — essential for Docker and Kubernetes.
Does Layer 2 deal with MAC or IP?::MAC.
Does Layer 3 deal with MAC or IP?::IP.
