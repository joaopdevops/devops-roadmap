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

## 🇺🇸 English

## Quick definition

A field in the IP header that limits **how many routers** a packet can pass through. It starts at an initial value and each router decrements it by 1 when forwarding. When it reaches zero, the router drops the packet.

## Analogy

**The packet's expiration date.** Each router "stamps" the packet by subtracting 1 from the deadline. If the deadline expires before the destination, the packet dies on the way — exactly like spoiled milk goes to the trash, it never reaches the consumer.

**Why it exists:** it prevents a packet from circling forever in routing loops (a misconfigured route that loops back to the same router). Without TTL, a loop would flood the network with zombie packets.

## How it works

1. The operating system sets the **initial TTL** when sending the packet.
   - Windows: 128
   - Linux: 64
   - macOS: 64
2. At each router on the path, **TTL = TTL − 1**.
3. If TTL = 0 before the destination, the router drops the packet and sends an **ICMP Time Exceeded** back to the source.

## How to read it in ping

The TTL in the `Reply from` shows **how many hops** the packet took:
- TTL = 128 → 0 routers (same subnet, Windows source)
- TTL = 127 → 1 router
- TTL = 126 → 2 routers
- ...

**It is material proof of routing.** Without comparing TTL, "the ping worked" is just faith. With a different TTL between source and destination, the difference tells you how many routers the packet crossed.

## Where it shows up

- **`traceroute` / `tracert`:** an entire tool **based on TTL**. It sends packets with TTL=1, TTL=2, TTL=3... and uses the ICMP Time Exceeded messages to map the path router by router.
- **Troubleshooting:** if ping returns `TTL expired in transit`, there is a routing loop or the initial TTL is too low for the path.
- **Security:** TTL can hint at the source OS (128 = Windows, 64 = Linux/Unix). Footprinting uses this.

## Where it was taught

- Lab 2.2 — Practical Subnetting (first appearance in action: PC0 → PC3 returned TTL=127, proof it crossed 1 router)

## Related

- ICMP — Time Exceeded packets are ICMP
- Router — who decrements TTL
- Gateway — the first stop where TTL is decremented

---

## Flashcards

O que e TTL?::Time To Live — a field in the IP header that limits how many routers a packet can cross.
Quem decrementa o TTL?::Each router that forwards the packet subtracts 1 from the TTL.
O que acontece quando o TTL chega a zero?::The router drops the packet and sends an ICMP Time Exceeded back to the source.
Qual o TTL inicial padrao do Windows?::128.
Qual o TTL inicial padrao do Linux?::64.
Por que TTL existe?::To prevent packets from circling forever in routing loops.
Se um pacote sai com TTL=128 e chega com TTL=125, quantos roteadores ele atravessou?::3 routers (128 − 125 = 3).
Em ping intra-sub-rede de Windows, qual TTL voce espera no reply?::128, because the packet does not pass through a router.
Em ping inter-sub-rede via 1 roteador de Windows, qual TTL voce espera no reply?::127, because the router decremented 1.
Qual ferramenta usa TTL para mapear o caminho de um pacote?::traceroute (Linux) or tracert (Windows).
