---
tipo: conceito
area: Redes
camada-osi: 2
protocolo: ARP
tags: [conceito, flashcards, redes]
---

# ARP — Address Resolution Protocol

Protocolo que descobre o **endereço MAC** de um dispositivo a partir do seu **endereço IP**.

Antes de enviar um pacote, o dispositivo precisa saber o MAC do destino. O ARP resolve isso:

1. Broadcast na rede: *"Quem tem o IP 192.168.1.2? Me diz seu MAC!"*
2. O dono do IP responde com seu MAC.
3. O remetente salva isso na **tabela ARP** (cache) para não perguntar de novo.

**Por que o primeiro ping perde 1 pacote?**
Porque o ARP ainda está descobrindo o MAC. Na segunda tentativa, o MAC já está em cache → 0% loss.

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.2-Componentes-de-Rede]]
- Vai aparecer muito em troubleshooting de redes

---

## Flashcards

O que o ARP descobre?::O endereco MAC de um dispositivo a partir do seu IP.
<!--SR:!2026-05-03,2,210-->
Em qual camada OSI o ARP opera?::Camada 2 (Enlace).
<!--SR:!2026-05-03,3,250-->
Por que o primeiro ping perde 1 pacote?::Porque o ARP esta descobrindo o MAC do destino. No segundo ping, o MAC ja esta em cache.
<!--SR:!2026-05-02,1,170-->
ARP faz parte do ping?::Nao. ARP roda ANTES do ping. O ping em si e so ICMP.
<!--SR:!2026-05-03,3,250-->
