---
tipo: conceito
area: Redes
tags: [conceito, flashcards, redes]
---

# Modelo OSI — Open Systems Interconnection

Modelo de referência com **7 camadas** que descreve como dados viajam pela rede.

| Camada | Nome | O que faz | Exemplo |
|--------|------|-----------|---------|
| 7 | Aplicação | Interface com o usuário | HTTP, DNS, SSH |
| 6 | Apresentação | Formatação, criptografia | SSL/TLS |
| 5 | Sessão | Gerencia conexões | NetBIOS |
| 4 | Transporte | Entrega confiável | TCP, UDP |
| 3 | Rede | Endereçamento e roteamento | IP, [[Conceitos/ICMP]] |
| 2 | Enlace | Comunicação na mesma rede | [[Conceitos/Switch]], [[Conceitos/ARP]], MAC |
| 1 | Física | Cabos, sinais elétricos | Ethernet, Wi-Fi |

**Regra prática para DevOps:**
- Camada 2 → [[Conceitos/Switch]], MAC address, [[Conceitos/LAN]]
- Camada 3 → [[Conceitos/Roteador]], IP, [[Conceitos/Gateway]], [[Conceitos/ICMP]]
- Camada 4 → TCP/UDP (portas — essencial para Docker e Kubernetes)
- Camada 7 → onde vivem suas aplicações

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.1-Redes-no-Mundo-Real]]
- [[Mes-01-Redes-Fundamentos/1.2-Componentes-de-Rede]]
- Aprofundado em: [[Mes-01-Redes-Fundamentos/Indice]] (tópico 1.3)

---

## 🇺🇸 English

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

Quantas camadas tem o modelo OSI?::7.
Em qual camada opera o Switch?::Layer 2 (Data Link).
Em qual camada opera o Roteador?::Layer 3 (Network).
Em qual camada vivem TCP e UDP?::Layer 4 (Transport).
Em qual camada vive o HTTP?::Layer 7 (Application).
Qual a regra pratica para DevOps sobre Camada 4?::It is where the ports are — essential for Docker and Kubernetes.
Camada 2 lida com o que (MAC ou IP)?::MAC.
Camada 3 lida com o que (MAC ou IP)?::IP.
