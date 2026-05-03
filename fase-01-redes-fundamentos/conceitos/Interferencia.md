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

## Flashcards

O que e interferencia em redes?::Degradacao do sinal por fonte externa a midia. O meio fisico esta intacto.
<!--SR:!2026-05-02,1,228-->
Qual a diferenca entre atenuacao e interferencia?::Atenuacao = interno a midia (sinal enfraquece sozinho). Interferencia = externo (campo ou sinal de fora bagunca o sinal).
<!--SR:!2026-05-04,3,268-->
Cabo cortado por caminhao e interferencia?::Nao. E ruptura fisica. Interferencia pressupoe que o meio fisico esta intacto.
<!--SR:!2026-05-03,2,248-->
O que e EMI?::Electromagnetic Interference — campo eletromagnetico de dispositivos eletricos (motor, fluorescente, cabo de energia) induzindo ruido no cobre.
<!--SR:!2026-05-03,2,248-->
Por que o UTP e trancado?::A torcao dos pares faz os campos eletromagneticos induzidos se cancelarem — protecao contra EMI.
<!--SR:!2026-05-02,1,210-->
Por que microondas interfere no Wi-Fi 2.4 GHz?::Microondas opera na mesma frequencia (2.4 GHz) — e RFI direta no mesmo espectro.
<!--SR:!2026-05-03,2,248-->
