---
tipo: conceito
area: Redes
camada-osi: 1
tags: [conceito, flashcards, redes]
---

# Fibra Óptica

Mídia física que transmite sinal por **pulso de luz** dentro de um núcleo de vidro (ou plástico). Não usa eletricidade.

O cabo fino preto que entra na sua casa vindo do poste = fibra óptica da operadora.

## Por que alcança dezenas de quilômetros

A [[Conceitos/Atenuacao|atenuação]] da luz no vidro puro é centenas de vezes menor que a atenuação do pulso elétrico no cobre. O sinal percorre dezenas de km antes de precisar de amplificação.

- **UTP:** 100m sem repetidor
- **Fibra single-mode:** dezenas de km sem amplificador

## Velocidade da luz no vidro

~200.000 km/s (duzentos mil quilômetros por **segundo**, não por hora).

Consequência prática: **São Paulo → Virgínia ≈ 120ms** porque são ~10.000 km de fibra submarina. Não é lentidão de software — é o limite físico da velocidade da luz. Nenhuma otimização de código muda isso.

## Imune a EMI

Não conduz eletricidade → campo eletromagnético externo não induz ruído. Pode passar ao lado de motor elétrico sem problema. Ver [[Conceitos/Interferencia]].

## Labs onde foi ensinado

- [[Mes-01-Redes-Fundamentos/1.4-Meios-Fisicos-e-Cabos]]

## Relacionado

- [[Conceitos/Atenuacao]] — atenuação muito baixa é o que permite longa distância
- [[Conceitos/UTP]] — comparação: cobre vs vidro, 100m vs dezenas de km
- [[Conceitos/Interferencia]] — imune a EMI por não conduzir eletricidade

---

## 🇺🇸 English

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

O que a fibra optica transmite?::A pulse of light inside glass. It does not use electricity.
Por que fibra alcanca dezenas de km e UTP so 100m?::The attenuation of light in glass is hundreds of times lower than the attenuation of the electrical pulse in copper.
Qual a velocidade da luz no vidro?::~200,000 km/s (two hundred thousand kilometers per second).
Por que a latencia SP-Virginia e ~120ms mesmo com fibra?::It is ~10,000 km of undersea fiber. The speed of light in glass has a physical limit — it is not a software bug.
Por que fibra e imune a EMI?::It does not conduct electricity — an external electromagnetic field has no way to induce noise into the light signal.
O cabo fino preto que entra na sua casa da operadora e o que?::Optical fiber — it transmits light, not electricity.
