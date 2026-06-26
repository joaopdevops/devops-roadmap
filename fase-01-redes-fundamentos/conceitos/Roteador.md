---
tipo: conceito
area: Redes
camada-osi: 3
tags: [conceito, flashcards, redes]
---

# Roteador

Opera na **Camada 3** do [[Conceitos/Modelo-OSI]].

Conecta **redes diferentes**. Recebe pacotes e decide qual caminho seguir baseado no endereço IP de destino.

**Analogia:** agência dos Correios. Liga um prédio ao outro — sabe o caminho entre bairros.

**Diferença do [[Conceitos/Switch]]:** o switch opera dentro de uma rede. O roteador opera entre redes.

Cada interface do roteador pertence a uma rede diferente e atua como [[Conceitos/Gateway]] para os dispositivos daquela rede.

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.2-Componentes-de-Rede]]
- Será essencial em: Docker networking, AWS VPC, Kubernetes

---

## 🇺🇸 English

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

O que o roteador faz?::Connects different networks. Operates at Layer 3.
Qual a diferenca entre switch e roteador?::A switch works WITHIN a network (Layer 2). A router connects DIFFERENT networks (Layer 3).
Cada interface de um roteador pertence a que?::A different network. And it acts as the gateway for the devices on that network.
Analogia do roteador?::The post office — links one building to another.
