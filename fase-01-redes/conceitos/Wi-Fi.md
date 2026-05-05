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

## Flashcards

Wi-Fi nao tem Camada 1?::Tem. O ar e a midia — onda de radio e o sinal fisico.
Por que 5 GHz atenua mais em parede que 2.4 GHz?::Frequencia mais alta = onda mais curta = obstaculo solido absorve mais energia.
Por que Wi-Fi e mais lento que cabo?::Meio compartilhado + half-duplex frequente + atenuacao e interferencia do ambiente.
Por que 2.4 GHz tem mais interferencia que 5 GHz?::Mesmo espectro do microondas e de mais dispositivos — mais disputa pelo canal.
Quais sao as duas midias Camada 1 na conexao de casa tipica?::Fibra optica (da operadora ate o roteador) e Wi-Fi (do roteador ate o dispositivo).
