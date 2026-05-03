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

## Flashcards

O que e Default Gateway?::O portao de saida de uma rede. Geralmente o IP da interface do roteador dentro daquela rede.
<!--SR:!2026-05-02,2,210-->
O que acontece se um PC nao tem gateway configurado?::Ele so fala com dispositivos da mesma LAN. Nao sai para outras redes.
<!--SR:!2026-05-03,3,250-->
Em qual camada OSI o Gateway opera?::Camada 3 (Rede).
<!--SR:!2026-05-03,3,250-->
Se PC0 (192.168.1.0/24) quer falar com 192.168.2.x, para onde manda o pacote?::Para o gateway (a interface do roteador na rede do PC0).
<!--SR:!2026-05-03,3,250-->
