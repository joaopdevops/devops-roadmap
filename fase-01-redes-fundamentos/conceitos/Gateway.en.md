---
tipo: conceito
area: Networking
camada-osi: 3
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](Gateway.md)

# Gateway (Default Gateway)

The **exit gate** of a network. When a device wants to communicate with another network, it sends the packet to the gateway.

The gateway is usually the **router** interface inside that network.

**Without a configured gateway:** the device does not know how to leave its local network. It can only communicate with devices on the same LAN.

**Example:**
- PC0 is on network 192.168.1.0/24
- PC0's gateway: 192.168.1.254 (router interface)
- To talk to 192.168.2.x, PC0 sends the packet to 192.168.1.254

## Where it was taught
- Lab 1.2 — Network components
- Essential for: AWS VPC, Docker networking, Kubernetes

---

## Flashcards

What is a Default Gateway?::The exit gate of a network. Usually the IP of the router interface within that network.
What happens if a PC has no gateway configured?::It only talks to devices on the same LAN. It cannot reach other networks.
At which OSI layer does the gateway operate?::Layer 3 (Network).
If PC0 (192.168.1.0/24) wants to talk to 192.168.2.x, where does it send the packet?::To the gateway (the router interface on PC0's network).
