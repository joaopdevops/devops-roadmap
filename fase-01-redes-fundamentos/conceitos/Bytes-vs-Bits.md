---
tipo: conceito
area: Redes
camada-osi: 1
tags: [conceito, flashcards, redes]
primeira-aparicao: 2026-06-30
---

bytes vs bits
# Bytes ≠ Bits

## Definição rápida

Duas unidades parecidas que **não** são a mesma coisa:

- **bit** = `b` minúsculo = o tijolinho. A menor unidade de dado. Um `0` ou um `1`.
- **byte** = `B` maiúsculo = um pacote de **8 bits**. `1 Byte = 8 bits`.

O fator entre as duas é **8**. Esquecer esse ×8 é o erro nº1 de quem mede rede.

## Analogia

🏢 Nos Correios: o **bit é um tijolo solto**; o **byte é um palete com 8 tijolos** amarrados.

A **estrada** (o link de rede) conta **tijolos por segundo**. O **arquivo** é medido em **paletes de 8**. Pra calcular tempo, os dois lados precisam falar a mesma língua — converter palete em tijolo (**× 8**) ou tijolo em palete (**÷ 8**).

## A pegadinha do marketing

| Coisa | Medida em | Por quê |
|---|---|---|
| **Velocidade de internet** (500 **Mbps**) | **bits** (`b` minúsculo) | número fica 8× maior → vende melhor |
| **Tamanho de arquivo** / download real (500 **MB**, 60 **MB/s**) | **bytes** (`B` maiúsculo) | é como o disco e o navegador contam |

Provedor **sempre** anuncia em **Mbps** (bits). Nunca em MB/s.

## A conta — quando as unidades NÃO casam

Arquivo de 100 MB num link de 100 Mbps:

```
Arquivo:    100 MB  →  100 × 8 = 800 Megabits   (paletes viram tijolos)
Velocidade: 100 Mbps = 100 Megabits POR SEGUNDO

Tempo = 800 Mb ÷ 100 Mb/s = 8 segundos
```

**Não é 1 segundo** porque o arquivo (bytes) tem 8× mais tijolos do que o número da velocidade (bits) faz parecer.

## A conta — quando as unidades JÁ casam

Mesmo arquivo, mas link em 100 **MB/s** (bytes):

```
Tempo = 100 MB ÷ 100 MB/s = 1 segundo
```

Aqui dá 1 segundo porque os dois lados já estão em bytes — **byte com byte, não tem ×8**.

> Regra de ouro: **antes de dividir, cheque se as unidades casam.** Os dois em bits, ou os dois em bytes → divide direto. Um em bit e outro em byte → converte primeiro pelo `1 Byte = 8 bits`.

## Por que DevOps / vida real importa

- **Plano "500 mega" → download a ~60 MB/s.** Não foi roubo: `500 ÷ 8 = 62,5 MB/s`. É a mesma internet em duas línguas.
- **Regra de bolso:** pega o "mega" do plano e **divide por 8** → é o MB/s que você vê baixando. Serve pra checar se a operadora entrega o contratado.
- Em troubleshooting de banda, comparar **MB/s** (real) com **Mbps** (contratado) explica 90% das brigas de "internet lenta".

## Relacionado

- [[Conceitos/MTU-Fragmentacao]] — MTU é medida em **bytes** (tamanho do pacote), banda em **bits/s**

---

## 🇺🇸 English

## Quick definition

Two units that look alike but are **not** the same:

- **bit** = lowercase `b` = the single brick. The smallest unit of data, a `0` or a `1`.
- **byte** = uppercase `B` = a bundle of **8 bits**. `1 Byte = 8 bits`.

The factor between them is **8**. Forgetting that ×8 is the #1 mistake when measuring networks.

## Analogy

🏢 At the post office: the **bit is a single brick**; the **byte is a pallet of 8 bricks**. The road (the network link) counts **bricks per second**; the file is measured in **pallets of 8**. To compute time, both sides must speak the same language — convert pallet to brick (**× 8**) or brick to pallet (**÷ 8**).

## The marketing trap

ISPs **always** advertise in **Mbps** (bits) because the number is 8× bigger. Files and real downloads are in **bytes** (MB, MB/s).

## The math

```
File:  100 MB  -> 100 x 8 = 800 Megabits
Link:  100 Mbps = 100 Megabits per second
Time = 800 / 100 = 8 seconds   (units do NOT match -> x8 first)

If the link were 100 MB/s (bytes):
Time = 100 MB / 100 MB/s = 1 second   (units match -> divide directly)
```

Rule of thumb: a "500 mega" plan downloads at ~`500 / 8 = 62.5 MB/s`. Same internet, two languages.

---

## Flashcards

Quantos bits tem 1 byte?::8 bits. 1 Byte = 8 bits.
Qual a diferenca entre bit e byte na escrita?::bit = lowercase b (a single brick); byte = uppercase B (a bundle of 8 bits).
Provedores de internet vendem a velocidade em MB/s ou Mbps?::Mbps (megabits per second, lowercase b). The number is 8x bigger, so it sells better. Never MB/s.
Um plano de 500 Mbps baixa a quantos MB/s na vida real?::About 62.5 MB/s. 500 / 8 = 62.5. Divide the advertised "mega" by 8 to get the real MB/s.
Quanto tempo leva baixar 100 MB num link de 100 Mbps?::8 seconds. 100 MB = 800 megabits; 800 / 100 = 8. The units do not match, so convert with x8 first.
Quanto tempo leva baixar 100 MB num link de 100 MB/s?::1 second. Both sides are in bytes, so divide directly: 100 / 100 = 1. No x8.
Qual a regra antes de dividir tamanho por velocidade?::Check that the units match. Both in bits or both in bytes -> divide directly. One in bits and the other in bytes -> convert first using 1 Byte = 8 bits.
Por que um arquivo de 100 MB nao baixa em 1 segundo num link de 100 Mbps?::Because the file is in bytes and the link speed is in bits; the file has 8x more bricks than the speed number suggests, so it takes 8 seconds, not 1.
