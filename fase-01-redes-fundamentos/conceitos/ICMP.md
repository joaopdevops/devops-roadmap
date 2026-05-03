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

## Flashcards

Para que serve o ICMP?::Testar conectividade. Nao transfere dados, so verifica se o caminho esta aberto.
<!--SR:!2026-05-02,2,210-->
Qual comando usa ICMP?::ping.
<!--SR:!2026-05-03,3,268-->
Echo Request vs Echo Reply?::Request = "voce esta ai?"; Reply = "estou sim!".
<!--SR:!2026-05-02,2,228-->
O que significa 0% packet loss?::Todos os pacotes enviados foram respondidos — comunicacao perfeita.
<!--SR:!2026-05-03,3,268-->
Em qual camada OSI o ICMP opera?::Camada 3 (Rede).
<!--SR:!2026-05-02,2,228-->
