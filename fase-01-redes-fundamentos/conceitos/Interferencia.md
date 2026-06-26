---
tipo: conceito
area: Redes
camada-osi: 1
tags: [conceito, flashcards, redes]
---

# Interferência

Degradação do sinal causada por fonte **externa** à mídia. O meio físico está intacto — o problema é um campo ou sinal externo sobrepondo ruído ao sinal original.

Diferença fundamental com [[Conceitos/Atenuacao]]:

| | Origem | Meio físico |
|---|---|---|
| Atenuação | interna à mídia | intacto |
| Interferência | externa à mídia | intacto |
| Ruptura física | — | danificado/cortado |

Cabo cortado por caminhão = ruptura física, não interferência.

## Tipos

**EMI — Electromagnetic Interference**
Campo eletromagnético de dispositivos elétricos próximos induz ruído no cobre.
Fontes clássicas (CCNA): motor elétrico, luminária fluorescente, cabo de energia correndo em paralelo ao UTP.

**RFI — Radio Frequency Interference**
Sinal de rádio externo no mesmo espectro.
Fontes: outro Wi-Fi no mesmo canal, microondas (opera em 2.4 GHz — mesmo espectro do Wi-Fi 2.4), antenas de TV, rádio AM/FM próximo.

## Como o UTP se protege

Os pares são **trançados** — a torção faz os campos eletromagnéticos induzidos em cada fio se cancelarem mutuamente. Por isso o nome: Unshielded **Twisted** Pair.

Sem torção, o cobre seria uma antena captando EMI de tudo ao redor.

## Labs onde foi ensinado

- [[Mes-01-Redes-Fundamentos/1.4-Meios-Fisicos-e-Cabos]]

## Relacionado

- [[Conceitos/Atenuacao]] — não confundir: interna vs externa
- [[Conceitos/UTP]] — torção como proteção contra EMI
- [[Conceitos/Wi-Fi]] — RFI entre redes Wi-Fi no mesmo canal

---

## 🇺🇸 English

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

O que e interferencia em redes?::Signal degradation by a source external to the medium. The physical medium is intact.
Qual a diferenca entre atenuacao e interferencia?::Attenuation = internal to the medium (signal weakens on its own). Interference = external (a field or signal from outside disrupts the signal).
Cabo cortado por caminhao e interferencia?::No. It is a physical break. Interference assumes the physical medium is intact.
O que e EMI?::Electromagnetic Interference — the electromagnetic field of electrical devices (motor, fluorescent lamp, power cable) inducing noise in the copper.
Por que o UTP e trancado?::The twist of the pairs makes the induced electromagnetic fields cancel out — protection against EMI.
Por que microondas interfere no Wi-Fi 2.4 GHz?::The microwave operates at the same frequency (2.4 GHz) — direct RFI in the same spectrum.
