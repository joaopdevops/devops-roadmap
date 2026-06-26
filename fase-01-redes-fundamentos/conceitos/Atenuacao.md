---
tipo: conceito
area: Redes
camada-osi: 1
tags: [conceito, flashcards, redes]
---

# Atenuação

Enfraquecimento do sinal à medida que percorre a mídia física. É um fenômeno **interno à mídia** — o próprio meio (cobre, vidro, ar) consome energia do sinal ao longo do caminho.

Começa no metro 0 e é gradual. Não é um evento que acontece num ponto específico.

## Por que UTP tem limite de 100m

O receptor (switch, placa de rede) tem um nível mínimo de sinal que consegue interpretar. Abaixo disso, não distingue 0 de 1 → bits lidos errado → erros → retransmissão.

O 100m do UTP é onde a atenuação acumula o suficiente para o sinal chegar abaixo desse limiar. Não é arbitrário — é física do cobre.

## Atenuação ≠ Interferência

| | O que é | Origem |
|---|---|---|
| Atenuação | sinal enfraquece sozinho | interna à mídia |
| Interferência | sinal externo bagunça | externa à mídia |

Ver [[Conceitos/Interferencia]].

## Ocorre em todas as mídias

- **UTP:** limite 100m. Pulso elétrico no cobre resiste e dissipa em calor.
- **Fibra óptica:** atenuação muito baixa. Luz no vidro quase não perde energia — por isso alcança dezenas de km.
- **Wi-Fi:** atenua com distância e com obstáculos sólidos (parede absorve a onda de rádio).

## Labs onde foi ensinado

- [[Mes-01-Redes-Fundamentos/1.4-Meios-Fisicos-e-Cabos]]

## Relacionado

- [[Conceitos/Interferencia]]
- [[Conceitos/UTP]]
- [[Conceitos/Fibra-Optica]]
- [[Conceitos/Wi-Fi]]

---

## 🇺🇸 English

The weakening of a signal as it travels through the physical medium. It is a phenomenon **internal to the medium** — the medium itself (copper, glass, air) consumes the signal's energy along the way.

It starts at meter 0 and is gradual. It is not an event that happens at a specific point.

## Why UTP has a 100 m limit

The receiver (switch, NIC) has a minimum signal level it can interpret. Below that, it cannot tell a 0 from a 1 → bits read wrong → errors → retransmission.

UTP's 100 m is where attenuation accumulates enough for the signal to fall below that threshold. It is not arbitrary — it is copper physics.

## Attenuation ≠ Interference

| | What it is | Origin |
|---|---|---|
| Attenuation | the signal weakens on its own | internal to the medium |
| Interference | an external signal disrupts it | external to the medium |

See: Interference.

## It happens in every medium

- **UTP:** 100 m limit. The electrical pulse in copper resists and dissipates as heat.
- **Optical fiber:** very low attenuation. Light in glass barely loses energy — that is why it reaches tens of km.
- **Wi-Fi:** attenuates with distance and with solid obstacles (a wall absorbs the radio wave).

## Where it was taught

- Lab 1.4 — Physical media and cabling

## Related

- Interference
- UTP
- Optical Fiber
- Wi-Fi

---

## Flashcards

O que e atenuacao?::The weakening of a signal by means internal to the medium. Gradual, starts at meter 0.
Quando começa a atenuacao em um cabo UTP?::At meter 0. It is gradual — it does not start at 100 m.
Por que UTP tem limite de 100m?::100 m is where attenuation accumulates enough for the signal to fall below the threshold the receiver can interpret.
Atenuacao e o mesmo que interferencia?::No. Attenuation = the medium weakens the signal internally. Interference = an external signal disrupts it.
Atenuacao acontece so no Wi-Fi?::No. It happens in any medium: UTP (copper), optical fiber and Wi-Fi (air).
