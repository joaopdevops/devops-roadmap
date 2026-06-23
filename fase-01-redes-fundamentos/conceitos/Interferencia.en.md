---
tipo: conceito
area: Networking
camada-osi: 1
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](Interferencia.md)

# Interference

Signal degradation caused by a source **external** to the medium. The physical medium is intact — the problem is an external field or signal adding noise on top of the original.

Fundamental difference from Attenuation:

| | Origin | Physical medium |
|---|---|---|
| Attenuation | internal to the medium | intact |
| Interference | external to the medium | intact |
| Physical break | — | damaged/cut |

A cable cut by a truck = a physical break, not interference.

## Types

**EMI — Electromagnetic Interference**
The electromagnetic field of nearby electrical devices induces noise in the copper.
Classic sources (CCNA): an electric motor, a fluorescent lamp, a power cable running parallel to the UTP.

**RFI — Radio Frequency Interference**
An external radio signal in the same spectrum.
Sources: another Wi-Fi on the same channel, a microwave oven (operates at 2.4 GHz — same spectrum as 2.4 Wi-Fi), TV antennas, a nearby AM/FM radio.

## How UTP protects itself

The pairs are **twisted** — the twist makes the electromagnetic fields induced in each wire cancel each other out. Hence the name: Unshielded **Twisted** Pair.

Without the twist, copper would be an antenna picking up EMI from everything around it.

## Where it was taught

- Lab 1.4 — Physical media and cabling

## Related

- Attenuation — do not confuse: internal vs external
- UTP — the twist as protection against EMI
- Wi-Fi — RFI between Wi-Fi networks on the same channel

---

## Flashcards

What is interference in networking?::Signal degradation by a source external to the medium. The physical medium is intact.
What is the difference between attenuation and interference?::Attenuation = internal to the medium (signal weakens on its own). Interference = external (a field or signal from outside disrupts the signal).
Is a cable cut by a truck interference?::No. It is a physical break. Interference assumes the physical medium is intact.
What is EMI?::Electromagnetic Interference — the electromagnetic field of electrical devices (motor, fluorescent lamp, power cable) inducing noise in the copper.
Why is UTP twisted?::The twist of the pairs makes the induced electromagnetic fields cancel out — protection against EMI.
Why does a microwave oven interfere with 2.4 GHz Wi-Fi?::The microwave operates at the same frequency (2.4 GHz) — direct RFI in the same spectrum.
