---
tipo: conceito
area: Networking
camada-osi: 1
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](UTP.md)

# UTP — Unshielded Twisted Pair

The most common network cable. Transmits the signal as an **electrical pulse in copper**. Connector: RJ-45.

**Unshielded** = no metallic shielding (unlike STP — Shielded Twisted Pair).
**Twisted** = twisted pairs — the twist cancels electromagnetic interference (EMI).
**Pair** = 4 pairs of wires (8 wires total).

## The 100 m limit

Defined by copper's attenuation. The electrical pulse weakens continuously from meter 0 — at 100 m it falls below the threshold the receiver can interpret.

## Categories

| Category | Max speed | Typical use |
|---|---|---|
| Cat5e | 1 Gbps | older networks, still common |
| Cat6 | 10 Gbps (short distances) | current standard |
| Cat6a | 10 Gbps over 100 m | data center |

## Straight-through vs crossover

| Connection | Cable |
|---|---|
| PC ↔ Switch | straight-through |
| Switch ↔ Router | straight-through |
| PC ↔ PC | crossover |
| Switch ↔ Switch | crossover |
| Router ↔ Router | crossover |

**Mnemonic:** same device class = crossover. Different classes = straight-through.

**In practice:** Auto-MDIX on modern gear detects and crosses over in software. Crossover became a museum piece — but the CCNA tests the theory.

## Where it was taught

- Lab 1.4 — Physical media and cabling

## Related

- Attenuation — the 100 m limit comes from copper's attenuation
- Interference — the pair twist protects against EMI
- Optical Fiber — the alternative for long distances

---

## Flashcards

What does UTP stand for?::Unshielded Twisted Pair — an unshielded copper cable with twisted pairs.
Why are the UTP pairs twisted?::The twist cancels electromagnetic interference (EMI) — without it, the copper would pick up noise from everything around.
What is UTP's distance limit and why?::100 m — copper's attenuation drops the signal below the receiver's interpretable threshold.
Which UTP category is the current standard?::Cat6 — supports 10 Gbps over short distances.
Does a PC-Switch connection use straight-through or crossover?::Straight-through — different device classes.
Does a Switch-Switch connection use straight-through or crossover?::Crossover — same device class.
What is Auto-MDIX?::A feature on modern gear that detects and crosses the cable in software — makes crossover obsolete in practice.
