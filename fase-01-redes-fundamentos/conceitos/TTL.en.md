---
tipo: conceito
area: Networking
camada-osi: 3
protocolo: IP
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](TTL.md)

# TTL (Time To Live)

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

What is TTL?::Time To Live — a field in the IP header that limits how many routers a packet can cross.
Who decrements the TTL?::Each router that forwards the packet subtracts 1 from the TTL.
What happens when the TTL reaches zero?::The router drops the packet and sends an ICMP Time Exceeded back to the source.
What is the default initial TTL on Windows?::128.
What is the default initial TTL on Linux?::64.
Why does TTL exist?::To prevent packets from circling forever in routing loops.
If a packet leaves with TTL=128 and arrives with TTL=125, how many routers did it cross?::3 routers (128 − 125 = 3).
In an intra-subnet ping from Windows, which TTL do you expect in the reply?::128, because the packet does not pass through a router.
In an inter-subnet ping via 1 router from Windows, which TTL do you expect in the reply?::127, because the router decremented 1.
Which tool uses TTL to map a packet's path?::traceroute (Linux) or tracert (Windows).
