---
tipo: conceito
area: Redes
camada-osi: 3
tags: [conceito, flashcards, redes]
---

# Gateway (Default Gateway)

O **portão de saída** de uma rede. Quando um dispositivo quer se comunicar com outra rede, ele envia o pacote para o gateway.

O gateway é geralmente a interface do [[Conceitos/Roteador]] dentro daquela rede.

**Sem gateway configurado:** o dispositivo não sabe como sair da sua rede local. Só consegue se comunicar com dispositivos da mesma [[Conceitos/LAN]].

**Exemplo:**
- PC0 está na rede 192.168.1.0/24
- Gateway do PC0: 192.168.1.254 (interface do roteador)
- Para falar com 192.168.2.x, o PC0 manda o pacote para 192.168.1.254

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.2-Componentes-de-Rede]]
- Essencial para: AWS VPC, Docker networking, Kubernetes

---

## 🇺🇸 English

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

O que e Default Gateway?::The exit gate of a network. Usually the IP of the router interface within that network.
O que acontece se um PC nao tem gateway configurado?::It only talks to devices on the same LAN. It cannot reach other networks.
Em qual camada OSI o Gateway opera?::Layer 3 (Network).
Se PC0 (192.168.1.0/24) quer falar com 192.168.2.x, para onde manda o pacote?::To the gateway (the router interface on PC0's network).
