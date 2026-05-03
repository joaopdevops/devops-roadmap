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

## Flashcards

O que e uma LAN?::Local Area Network — rede local onde dispositivos se comunicam diretamente, sem roteador.
<!--SR:!2026-05-03,2,230-->
O que define que dois dispositivos estao na mesma LAN?::Ter a mesma mascara de rede (mesmo "predio").
<!--SR:!2026-05-02,2,230-->
Quem gerencia a comunicacao dentro de uma LAN?::O switch (Camada 2).
<!--SR:!2026-05-04,4,270-->
A rede docker0 e uma LAN?::Sim — e uma LAN virtual criada pelo Docker.
<!--SR:!2026-05-02,2,230-->
