---
tipo: conceito
area: Redes
camada-osi: 3
protocolo: IP
tags: [conceito, flashcards, redes]
---

# TTL (Time To Live)

## Definição rápida

Campo do cabeçalho IP que limita por **quantos roteadores** um pacote pode passar. Começa com um valor inicial e cada roteador decrementa 1 ao reencaminhar. Chega a zero, o roteador descarta o pacote.

## Analogia

**Prazo de validade do pacote.** Cada roteador "carimba" o pacote subtraindo 1 do prazo. Se o prazo expirar antes do destino, o pacote morre no caminho — exatamente como leite vencido vai pro lixo, não chega ao consumidor.

**Por que existe:** evita pacote girando eternamente em loops de roteamento (rota mal configurada que volta no mesmo roteador). Sem TTL, um loop encheria a rede de pacotes-zumbi.

## Como funciona

1. Sistema operacional define **TTL inicial** ao mandar o pacote.
   - Windows: 128
   - Linux: 64
   - macOS: 64
2. A cada roteador no caminho, **TTL = TTL − 1**.
3. Se TTL = 0 antes do destino, o roteador descarta o pacote e manda **ICMP Time Exceeded** de volta pra origem.

## Como ler em ping

TTL no `Reply from` indica **quantos saltos** o pacote deu:
- TTL = 128 → 0 roteadores (mesma sub-rede, origem Windows)
- TTL = 127 → 1 roteador
- TTL = 126 → 2 roteadores
- ...

**É evidência material de roteamento.** Sem comparar TTL, "ping passou" é só fé. Com TTL diferente entre origem e destino, dá pra saber pela diferença quantos roteadores o pacote atravessou.

## Onde aparece

- **`traceroute` / `tracert`:** ferramenta inteira **baseada em TTL**. Manda pacotes com TTL=1, TTL=2, TTL=3... e usa os ICMP Time Exceeded pra mapear o caminho roteador por roteador.
- **Troubleshooting:** se ping retorna `TTL expired in transit`, há loop de roteamento ou TTL inicial muito baixo pro caminho.
- **Segurança:** TTL pode indicar SO da origem (128 = Windows, 64 = Linux/Unix). Footprinting usa isso.

## Labs onde foi ensinado

- `2.2-Subnetting-Pratico.md` — primeira aparição em ação (PC0 → PC3 retornou TTL=127, prova que atravessou 1 roteador)

## Conceito relacionado

- `ICMP.md` — pacotes Time Exceeded são ICMP
- `Roteador.md` — quem decrementa TTL
- `Gateway.md` — primeira parada onde TTL é decrementado

---

## Flashcards

O que e TTL?::Time To Live — campo do cabecalho IP que limita quantos roteadores um pacote pode atravessar.
Quem decrementa o TTL?::Cada roteador que reencaminha o pacote subtrai 1 do TTL.
O que acontece quando o TTL chega a zero?::O roteador descarta o pacote e envia ICMP Time Exceeded de volta pra origem.
Qual o TTL inicial padrao do Windows?::128.
Qual o TTL inicial padrao do Linux?::64.
Por que TTL existe?::Para evitar pacotes girando eternamente em loops de roteamento.
Se um pacote sai com TTL=128 e chega com TTL=125, quantos roteadores ele atravessou?::3 roteadores (128 − 125 = 3).
Em ping intra-sub-rede de Windows, qual TTL voce espera no reply?::128, porque o pacote nao passa por roteador.
Em ping inter-sub-rede via 1 roteador de Windows, qual TTL voce espera no reply?::127, porque o roteador decrementou 1.
Qual ferramenta usa TTL para mapear o caminho de um pacote?::traceroute (Linux) ou tracert (Windows).
