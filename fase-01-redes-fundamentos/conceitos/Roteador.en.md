---
tipo: conceito
area: Networking
camada-osi: 3
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](Roteador.md)

# Router

Operates at **Layer 3** of the OSI model.

Connects **different networks**. It receives packets and decides which path to take based on the destination IP address.

**Analogy:** the post office. It links one building to another — it knows the path between neighborhoods.

**Difference from the switch:** the switch works within one network. The router works between networks.

Each router interface belongs to a different network and acts as the **gateway** for the devices on that network.

## Where it was taught
- Lab 1.2 — Network components
- Will be essential in: Docker networking, AWS VPC, Kubernetes

---

## Flashcards

What does the router do?::Connects different networks. Operates at Layer 3.
What is the difference between a switch and a router?::A switch works WITHIN a network (Layer 2). A router connects DIFFERENT networks (Layer 3).
What does each router interface belong to?::A different network. And it acts as the gateway for the devices on that network.
What is the router analogy?::The post office — links one building to another.
