---
tipo: conceito
area: Redes
camada-osi: 3
protocolo: ICMP
tags: [conceito, flashcards, redes]
---

# ICMP — Internet Control Message Protocol

Protocolo usado para **testar conectividade**. Não transfere dados — só verifica se o caminho está aberto.

Usado pelo comando `ping`.

**Funcionamento:**
- **Echo Request:** "ei, você está aí?"
- **Echo Reply:** "estou sim!"
- **0% packet loss** = comunicação perfeita

**No Linux:**
```bash
ping 192.168.1.2        # ping contínuo
ping -c 4 192.168.1.2   # envia 4 pacotes e para
```

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.1-Redes-no-Mundo-Real]]
- [[Mes-01-Redes-Fundamentos/1.2-Componentes-de-Rede]]

---

## 🇺🇸 English

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

Para que serve o ICMP?::Testing connectivity. It does not transfer data, only checks whether the path is open.
Qual comando usa ICMP?::ping.
Echo Request vs Echo Reply?::Request = "are you there?"; Reply = "yes, I am!".
O que significa 0% packet loss?::Every packet sent was answered — perfect communication.
Em qual camada OSI o ICMP opera?::Layer 3 (Network).
