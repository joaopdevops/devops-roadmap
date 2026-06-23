---
tipo: conceito
area: Networking
camada-osi: 2
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](LAN.md)

# LAN — Local Area Network

A local network where devices communicate **directly**, without needing a **router**.

All devices share the same **subnet mask** — that is, they are in the same "building".

Communication inside a LAN is handled by the **switch** (Layer 2).

**Examples:**
- Home network
- Office network
- Docker virtual network (docker0)

## Where it was taught
- Lab 1.1 — Networking in the real world

---

## Flashcards

What is a LAN?::Local Area Network — a local network where devices communicate directly, without a router.
What defines that two devices are on the same LAN?::Having the same subnet mask (the same "building").
Who manages communication inside a LAN?::The switch (Layer 2).
Is the docker0 network a LAN?::Yes — it is a virtual LAN created by Docker.
