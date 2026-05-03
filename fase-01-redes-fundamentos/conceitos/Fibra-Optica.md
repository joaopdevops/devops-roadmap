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

## Flashcards

O que a fibra optica transmite?::Pulso de luz dentro de vidro. Nao usa eletricidade.
Por que fibra alcanca dezenas de km e UTP so 100m?::A atenuacao da luz no vidro e centenas de vezes menor que a atenuacao do pulso eletrico no cobre.
Qual a velocidade da luz no vidro?::~200.000 km/s (duzentos mil quilometros por segundo).
Por que a latencia SP-Virginia e ~120ms mesmo com fibra?::Sao ~10.000 km de fibra submarina. A velocidade da luz no vidro tem limite fisico — nao e bug de software.
Por que fibra e imune a EMI?::Nao conduz eletricidade — campo eletromagnetico externo nao tem como induzir ruido no sinal de luz.
O cabo fino preto que entra na sua casa da operadora e o que?::Fibra optica — transmite luz, nao eletricidade.
