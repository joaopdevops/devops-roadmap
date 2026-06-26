---
tipo: conceito
area: Redes
camada-osi: 2
tags: [conceito, flashcards, redes]
---

# LAN — Local Area Network

Rede local onde dispositivos se comunicam **diretamente**, sem precisar de [[Conceitos/Roteador]].

Todos os dispositivos compartilham a mesma [[Conceitos/Mascara-de-Rede]], ou seja, estão no mesmo "prédio".

A comunicação dentro de uma LAN é gerenciada pelo [[Conceitos/Switch]] (Camada 2).

**Exemplos:**
- Rede doméstica
- Rede de escritório
- Rede virtual do Docker (docker0)

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.1-Redes-no-Mundo-Real]]

---

## 🇺🇸 English

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

O que e uma LAN?::Local Area Network — a local network where devices communicate directly, without a router.
O que define que dois dispositivos estao na mesma LAN?::Having the same subnet mask (the same "building").
Quem gerencia a comunicacao dentro de uma LAN?::The switch (Layer 2).
A rede docker0 e uma LAN?::Yes — it is a virtual LAN created by Docker.
