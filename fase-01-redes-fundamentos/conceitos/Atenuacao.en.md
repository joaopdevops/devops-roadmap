---
tipo: conceito
area: Networking
camada-osi: 1
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](Atenuacao.md)

# Attenuation

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

What is attenuation?::The weakening of a signal by means internal to the medium. Gradual, starts at meter 0.
When does attenuation start in a UTP cable?::At meter 0. It is gradual — it does not start at 100 m.
Why does UTP have a 100 m limit?::100 m is where attenuation accumulates enough for the signal to fall below the threshold the receiver can interpret.
Is attenuation the same as interference?::No. Attenuation = the medium weakens the signal internally. Interference = an external signal disrupts it.
Does attenuation happen only in Wi-Fi?::No. It happens in any medium: UTP (copper), optical fiber and Wi-Fi (air).
