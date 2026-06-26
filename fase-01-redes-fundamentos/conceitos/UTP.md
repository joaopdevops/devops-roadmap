---
tipo: conceito
area: Redes
camada-osi: 1
tags: [conceito, flashcards, redes]
---

# UTP — Unshielded Twisted Pair

Cabo de rede mais comum. Transmite sinal por **pulso elétrico no cobre**. Conector: RJ-45.

**Unshielded** = sem blindagem metálica (diferente do STP — Shielded Twisted Pair).
**Twisted** = pares trançados — a torção cancela [[Conceitos/Interferencia|interferência eletromagnética (EMI)]].
**Pair** = 4 pares de fios (8 fios no total).

## Limite de 100m

Definido pela [[Conceitos/Atenuacao|atenuação]] do cobre. O pulso elétrico enfraquece continuamente desde o metro 0 — aos 100m, chega abaixo do limiar que o receptor consegue interpretar.

## Categorias

| Categoria | Velocidade máx | Uso típico |
|---|---|---|
| Cat5e | 1 Gbps | redes antigas, ainda comum |
| Cat6 | 10 Gbps (curtas distâncias) | padrão atual |
| Cat6a | 10 Gbps em 100m | datacenter |

## Cabo direto vs crossover

| Conexão | Cabo |
|---|---|
| PC ↔ Switch | direto |
| Switch ↔ Roteador | direto |
| PC ↔ PC | crossover |
| Switch ↔ Switch | crossover |
| Roteador ↔ Roteador | crossover |

**Mnemônico:** mesma classe de dispositivo = crossover. Classes diferentes = direto.

**Prática:** Auto-MDIX em equipamento moderno detecta e cruza por software. Crossover virou peça de museu — mas CCNA cobra a teoria.

## Labs onde foi ensinado

- [[Mes-01-Redes-Fundamentos/1.4-Meios-Fisicos-e-Cabos]]

## Relacionado

- [[Conceitos/Atenuacao]] — limite de 100m vem da atenuação do cobre
- [[Conceitos/Interferencia]] — torção dos pares protege contra EMI
- [[Conceitos/Fibra-Optica]] — alternativa pra longas distâncias

---

## 🇺🇸 English

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

O que significa UTP?::Unshielded Twisted Pair — an unshielded copper cable with twisted pairs.
Por que os pares do UTP sao trancados?::The twist cancels electromagnetic interference (EMI) — without it, the copper would pick up noise from everything around.
Qual o limite de distancia do UTP e por que?::100 m — copper's attenuation drops the signal below the receiver's interpretable threshold.
Qual categoria UTP e o padrao atual?::Cat6 — supports 10 Gbps over short distances.
Conexao PC-Switch usa cabo direto ou crossover?::Straight-through — different device classes.
Conexao Switch-Switch usa cabo direto ou crossover?::Crossover — same device class.
O que e Auto-MDIX?::A feature on modern gear that detects and crosses the cable in software — makes crossover obsolete in practice.
