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

## Flashcards

Quantas camadas tem o modelo OSI?::7.
<!--SR:!2026-05-10,10,288-->
Em qual camada opera o Switch?::Camada 2 (Enlace).
<!--SR:!2026-05-12,12,288-->
Em qual camada opera o Roteador?::Camada 3 (Rede).
<!--SR:!2026-05-11,11,288-->
Em qual camada vivem TCP e UDP?::Camada 4 (Transporte).
<!--SR:!2026-05-03,3,248-->
Em qual camada vive o HTTP?::Camada 7 (Aplicacao).
<!--SR:!2026-05-10,10,288-->
Qual a regra pratica para DevOps sobre Camada 4?::E onde estao as portas — essencial para Docker e Kubernetes.
<!--SR:!2026-05-03,3,230-->
Camada 2 lida com o que (MAC ou IP)?::MAC.
<!--SR:!2026-05-06,11,270-->
Camada 3 lida com o que (MAC ou IP)?::IP.
<!--SR:!2026-05-11,11,288-->
