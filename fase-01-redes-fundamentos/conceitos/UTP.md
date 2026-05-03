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

## Flashcards

O que significa UTP?::Unshielded Twisted Pair — cabo de cobre sem blindagem, com pares trancados.
Por que os pares do UTP sao trancados?::A torcao cancela interferencia eletromagnetica (EMI) — sem torcao, o cobre captaria ruido de tudo ao redor.
Qual o limite de distancia do UTP e por que?::100m — a atenuacao do cobre derruba o sinal abaixo do limiar interpretavel pelo receptor.
Qual categoria UTP e o padrao atual?::Cat6 — suporta 10 Gbps em curtas distancias.
Conexao PC-Switch usa cabo direto ou crossover?::Direto — classes diferentes de dispositivo.
Conexao Switch-Switch usa cabo direto ou crossover?::Crossover — mesma classe de dispositivo.
O que e Auto-MDIX?::Recurso de equipamentos modernos que detecta e cruza o cabo por software — torna o crossover obsoleto na pratica.
