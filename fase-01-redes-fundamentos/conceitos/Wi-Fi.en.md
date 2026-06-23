---
tipo: conceito
area: Networking
camada-osi: 1
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](Wi-Fi.md)

# Wi-Fi

A wireless physical medium — it transmits the signal as **radio waves** using the air as the medium. "Wireless" is not "no Layer 1": the air is the medium.

## 2.4 GHz vs 5 GHz

| | 2.4 GHz | 5 GHz |
|---|---|---|
| Range | larger | smaller |
| Through walls | passes better | attenuates faster |
| Speed | lower | higher |
| Interference | more (microwaves, more devices) | less |

**Why does 5 GHz attenuate more through a wall?** Higher frequency = shorter wave = a solid obstacle absorbs more energy. See: Attenuation.

**Why does 2.4 GHz have more interference?** Same spectrum as microwave ovens (2.4 GHz) and many other devices. See: Interference.

## Why Wi-Fi is slower than cable

- **Shared medium:** all devices share the same "air"
- **Frequently half-duplex:** it does not transmit and receive at the same time (unlike full-duplex UTP cable)
- **Attenuation and interference:** present in any real environment

## Real home topology (Lab 1.4)

```
[Pole] --(optical fiber)--> [Router] --(Wi-Fi 2.4/5 GHz)--> [PC]
```

Two different Layer 1 media on the same connection.

## Where it was taught

- Lab 1.4 — Physical media and cabling

## Related

- Attenuation — Wi-Fi attenuates with walls and distance
- Interference — susceptible to RFI (microwaves, other Wi-Fi on the same channel)
- Optical Fiber — the medium that reaches the router before Wi-Fi begins

---

## Flashcards

Does Wi-Fi have no Layer 1?::It does. The air is the medium — radio waves are the physical signal.
Why does 5 GHz attenuate more through a wall than 2.4 GHz?::Higher frequency = shorter wave = a solid obstacle absorbs more energy.
Why is Wi-Fi slower than cable?::Shared medium + frequently half-duplex + environmental attenuation and interference.
Why does 2.4 GHz have more interference than 5 GHz?::Same spectrum as microwaves and more devices — more contention for the channel.
What are the two Layer 1 media in a typical home connection?::Optical fiber (from the ISP to the router) and Wi-Fi (from the router to the device).
