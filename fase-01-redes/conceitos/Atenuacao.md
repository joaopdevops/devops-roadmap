---
tipo: conceito
area: Redes
camada-osi: 1
tags: [conceito, flashcards, redes]
---

# Atenuação

Enfraquecimento do sinal à medida que percorre a mídia física. É um fenômeno **interno à mídia** — o próprio meio (cobre, vidro, ar) consome energia do sinal ao longo do caminho.

Começa no metro 0 e é gradual. Não é um evento que acontece num ponto específico.

## Por que UTP tem limite de 100m

O receptor (switch, placa de rede) tem um nível mínimo de sinal que consegue interpretar. Abaixo disso, não distingue 0 de 1 → bits lidos errado → erros → retransmissão.

O 100m do UTP é onde a atenuação acumula o suficiente para o sinal chegar abaixo desse limiar. Não é arbitrário — é física do cobre.

## Atenuação ≠ Interferência

| | O que é | Origem |
|---|---|---|
| Atenuação | sinal enfraquece sozinho | interna à mídia |
| Interferência | sinal externo bagunça | externa à mídia |

Ver [[Conceitos/Interferencia]].

## Ocorre em todas as mídias

- **UTP:** limite 100m. Pulso elétrico no cobre resiste e dissipa em calor.
- **Fibra óptica:** atenuação muito baixa. Luz no vidro quase não perde energia — por isso alcança dezenas de km.
- **Wi-Fi:** atenua com distância e com obstáculos sólidos (parede absorve a onda de rádio).

## Labs onde foi ensinado

- [[Mes-01-Redes-Fundamentos/1.4-Meios-Fisicos-e-Cabos]]

## Relacionado

- [[Conceitos/Interferencia]]
- [[Conceitos/UTP]]
- [[Conceitos/Fibra-Optica]]
- [[Conceitos/Wi-Fi]]

---

## Flashcards

O que e atenuacao?::Enfraquecimento do sinal por meios internos a midia. Gradual, começa no metro 0.
<!--SR:!2026-05-04,3,250-->
Quando começa a atenuacao em um cabo UTP?::No metro 0. E gradual — nao começa em 100m.
<!--SR:!2026-05-04,3,250-->
Por que UTP tem limite de 100m?::100m e onde a atenuacao acumula o suficiente para o sinal chegar abaixo do limiar que o receptor consegue interpretar.
<!--SR:!2026-05-02,1,230-->
Atenuacao e o mesmo que interferencia?::Nao. Atenuacao = enfraquecimento interno da midia. Interferencia = sinal externo bagunçando.
<!--SR:!2026-05-05,4,270-->
Atenuacao acontece so no Wi-Fi?::Nao. Acontece em qualquer midia: UTP (cobre), fibra optica e Wi-Fi (ar).
<!--SR:!2026-05-05,4,270-->
