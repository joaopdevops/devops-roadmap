---
tipo: conceito
area: Redes
camada-osi: 1
tags: [conceito, flashcards, redes]
---

# Wi-Fi

Mídia física sem fio — transmite sinal por **ondas de rádio** usando o ar como meio. "Sem fio" não é "sem Camada 1": o ar é a mídia.

## 2.4 GHz vs 5 GHz

| | 2.4 GHz | 5 GHz |
|---|---|---|
| Alcance | maior | menor |
| Parede | atravessa melhor | atenua mais rápido |
| Velocidade | menor | maior |
| Interferência | mais (microondas, mais dispositivos) | menos |

**Por que 5 GHz atenua mais em parede?** Frequência mais alta = onda mais curta = obstáculo sólido absorve mais energia. Ver [[Conceitos/Atenuacao]].

**Por que 2.4 GHz tem mais interferência?** Mesmo espectro do microondas (2.4 GHz) e de muitos outros dispositivos. Ver [[Conceitos/Interferencia]].

## Por que Wi-Fi é mais lento que cabo

- **Meio compartilhado:** todos os dispositivos dividem o mesmo "ar"
- **Half-duplex frequente:** não transmite e recebe ao mesmo tempo (diferente do cabo UTP full-duplex)
- **Atenuação e interferência:** presentes em qualquer ambiente real

## Topologia da casa real (Lab 1.4)

```
[Poste] --(fibra óptica)--> [Roteador] --(Wi-Fi 2.4/5 GHz)--> [PC]
```

Duas mídias Camada 1 diferentes na mesma conexão.

## Labs onde foi ensinado

- [[Mes-01-Redes-Fundamentos/1.4-Meios-Fisicos-e-Cabos]]

## Relacionado

- [[Conceitos/Atenuacao]] — Wi-Fi atenua com paredes e distância
- [[Conceitos/Interferencia]] — suscetível a RFI (microondas, outros Wi-Fi no mesmo canal)
- [[Conceitos/Fibra-Optica]] — mídia que chega ao roteador antes do Wi-Fi começar

---

## 🇺🇸 English

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

Wi-Fi nao tem Camada 1?::It does. The air is the medium — radio waves are the physical signal.
Por que 5 GHz atenua mais em parede que 2.4 GHz?::Higher frequency = shorter wave = a solid obstacle absorbs more energy.
Por que Wi-Fi e mais lento que cabo?::Shared medium + frequently half-duplex + environmental attenuation and interference.
Por que 2.4 GHz tem mais interferencia que 5 GHz?::Same spectrum as microwaves and more devices — more contention for the channel.
Quais sao as duas midias Camada 1 na conexao de casa tipica?::Optical fiber (from the ISP to the router) and Wi-Fi (from the router to the device).
