---
tipo: conceito
area: Networking
camada-osi: 1
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](Fibra-Optica.md)

# Optical Fiber

A physical medium that transmits the signal as a **pulse of light** inside a glass (or plastic) core. It does not use electricity.

The thin black cable that enters your home from the pole = the ISP's optical fiber.

## Why it reaches tens of kilometers

The attenuation of light in pure glass is hundreds of times lower than the attenuation of the electrical pulse in copper. The signal travels tens of km before needing amplification.

- **UTP:** 100 m without a repeater
- **Single-mode fiber:** tens of km without an amplifier

## Speed of light in glass

~200,000 km/s (two hundred thousand kilometers per **second**, not per hour).

Practical consequence: **São Paulo → Virginia ≈ 120 ms** because it is ~10,000 km of undersea fiber. It is not software slowness — it is the physical limit of the speed of light. No code optimization changes that.

## Immune to EMI

It does not conduct electricity → an external electromagnetic field cannot induce noise. It can run next to an electric motor without a problem. See: Interference.

## Where it was taught

- Lab 1.4 — Physical media and cabling

## Related

- Attenuation — very low attenuation is what allows long distance
- UTP — comparison: copper vs glass, 100 m vs tens of km
- Interference — immune to EMI because it does not conduct electricity

---

## Flashcards

What does optical fiber transmit?::A pulse of light inside glass. It does not use electricity.
Why does fiber reach tens of km and UTP only 100 m?::The attenuation of light in glass is hundreds of times lower than the attenuation of the electrical pulse in copper.
What is the speed of light in glass?::~200,000 km/s (two hundred thousand kilometers per second).
Why is the SP-Virginia latency ~120 ms even with fiber?::It is ~10,000 km of undersea fiber. The speed of light in glass has a physical limit — it is not a software bug.
Why is fiber immune to EMI?::It does not conduct electricity — an external electromagnetic field has no way to induce noise into the light signal.
What is the thin black cable from the ISP that enters your home?::Optical fiber — it transmits light, not electricity.
