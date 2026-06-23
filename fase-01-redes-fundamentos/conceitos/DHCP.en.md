---
tipo: conceito
area: Networking
camada-osi: 7
protocolo: DHCP
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](DHCP.md)

# DHCP — Dynamic Host Configuration Protocol

## Quick definition

A protocol that **automatically hands out IP, subnet mask, gateway and DNS** to devices joining a network. Without DHCP, every PC, phone and printer would have to be configured by hand.

## Analogy

**A hotel that does your check-in.** You arrive with nothing set. The receptionist hands you a single bundle:

- Room number → **IP**
- A key that only opens your floor → **subnet mask**
- A map to the building exit → **gateway**
- The Wi-Fi password and the kitchen extension → **DNS servers**

All automatic, without you asking item by item. And the room is **rented for a fixed time** (lease) — afterward you either renew or hand the key back.

## How it works — the 4 messages (DORA)

| # | Name | Who speaks | What it says | Why broadcast |
|---|---|---|---|---|
| 1 | **D**iscover | Client | "Is there a DHCP server out there?" | The client does not yet know who (or whether anyone) will answer. With no source IP, it uses `0.0.0.0`. |
| 2 | **O**ffer | Server | "Yes. I offer you IP 192.168.0.19, mask /24, gateway .1, DNS 8.8.8.8, 24h lease" | The client has no IP stack configured yet — without IP, mask or gateway, the TCP/IP stack cannot process a unicast addressed to an IP it does not have. The server broadcasts so the frame reaches the NIC. |
| 3 | **R**equest | Client | "I accept server X's offer (IP 192.168.0.19)" | Tells the **other** DHCP servers that offered and were not chosen — they release the IP they had reserved back to the pool. Without it, IPs would stay reserved for nothing. |
| 4 | **A**cknowledge | Chosen server | "Confirmed. The IP is yours for 24h" | Broadcast or unicast (implementation dependent). The lease only becomes official after this ack. |

**Master mnemonic:**
- The client speaks on the **odd steps (1, 3)** — it takes the initiative.
- The server answers on the **even steps (2, 4)** — it reacts.
- The order is **always** D → O → R → A in the initial flow. Never skips.

All of this happens in **fractions of a second** when you turn on Wi-Fi.

## Lease — the IP "rental"

The IP is not yours forever. The DHCP server lends it for a while (lease) — usually hours or days. Before the deadline expires, the client **renews** automatically. If the device disappears (off, taken elsewhere), the IP returns to the pool and can be given to another.

**Why it matters:** without a lease, every device that powered on once would consume 1 IP forever, even when off. The pool would run out fast.

## Lease renewal — how it really works

Before the lease expires, the client **does not redo the whole DORA**. It already knows which server gave the IP — so it optimizes:

1. **~50% of the lease elapsed ("renewing" state):** the client sends a **unicast Request** straight to the server that gave the lease. **Skips Discover and Offer.**
2. If the server answers Ack → lease renewed, done.
3. If the server does not answer (down, e.g.), at **~87.5% of the lease ("rebinding" state):** the client sends a **broadcast** Request, asking any server.
4. If nothing answers before the lease expires → the client loses the IP and falls back to a **full DORA** from scratch.

**Why it matters:** if renewal redid the whole DORA all the time, the network would be flooded with broadcasts. The protocol optimizes for silence in steady state.

## APIPA (169.254.x.x) — a sign that DORA failed

If DORA does not complete, the operating system self-assigns an IP from the **`169.254.0.0/16`** range (APIPA — Automatic Private IP Addressing). It is a clear sign that something in the flow broke:

- **D broke:** the network has no DHCP server, or the Wi-Fi router has DHCP disabled/down. **Most common case in the real world.**
- **O broke:** the server exists but did not answer the Offer (network, server, or router problem).
- **R broke:** the client got the Offer but the Request did not reach the server (rare).
- **A broke:** the server got the Request but the Ack did not reach the client (the lease never "closes" officially).

**Practical diagnosis:** seeing a `169.254.x.x` IP in `ip addr show` or `ipconfig` = DHCP failed somewhere. Investigate from the router outward.

## Where it shows up in your life

- Your Ubuntu got `192.168.0.19` automatically from the home router when you turned on Wi-Fi. **That was DHCP.**
- You never typed that IP by hand. Check: `ip addr show wlp0s20f3` in the terminal.
- A home router = the DHCP server of the home network. A company = a dedicated DHCP server (Windows Server, isc-dhcp-server on Linux, etc).

## A difference to note

- **DHCP** = you receive an IP automatically
- **Static IP** = you configure it by hand. Used on servers, routers, network printers — things that need a **predictable fixed address**.

## Why it matters for DevOps

- **AWS EC2:** instances get an IP via the VPC's DHCP.
- **Docker:** containers get an IP from the Docker daemon (which plays the DHCP role of the `bridge` network).
- **Kubernetes:** pods get an IP via the CNI plugin (same concept, different scale).

Without understanding DHCP, you do not understand how a container/VM "knows" which IP to use.

## Where it was taught

- Lab 2.3 — Network Services

## Related

- Subnet Mask — one of the 4 things DHCP delivers
- Gateway — another of the 4 things delivered
- DNS — DHCP delivers the DNS server IP for the client to use
- RFC 1918 — IPs handed out by DHCP on a local network are private (10/8, 172.16-31/12, 192.168/16)

---

## Flashcards

What is DHCP?::A protocol that automatically hands out IP, mask, gateway and DNS to devices joining a network.
Which 4 pieces of info does DHCP deliver to the client?::IP, subnet mask, gateway and DNS server addresses.
What does DORA stand for?::Discover, Offer, Request, Acknowledge — the 4 messages exchanged between DHCP client and server.
Who sends the Discover?::The client, as a broadcast, asking "is there a DHCP server here?".
Who answers with the Offer?::The DHCP server, offering an IP and the other parameters.
Why is the Request a broadcast and not unicast?::So other DHCP servers know the client already chose an offer — they then return the offered IP to the pool.
What is a lease in DHCP?::The IP rental time — after that deadline the client renews or the IP returns to the pool.
Why does a lease exist?::To avoid IPs being allocated forever to devices that vanished from the network.
Without DHCP, how would each device be configured?::Manually — IP, mask, gateway and DNS typed into each one.
What is the difference between a DHCP IP and a static IP?::DHCP delivers automatically and the IP can change; static is set by hand and never changes. Servers and network gear use static.
At which OSI layer does DHCP operate?::Layer 7 (Application) — it runs over UDP on ports 67 (server) and 68 (client).
Who plays the DHCP server in your home?::The home router — it hands out IPs from the 192.168.x.x range to the devices.
In DORA, who initiates and who responds?::The client initiates (steps D and R, odd), the server responds (steps O and A, even). The client takes the initiative, the server reacts.
Why is the Offer a broadcast if the server already knows the client's MAC?::The client has no IP stack configured yet (no IP, mask or gateway), so it cannot receive a normal unicast. The server broadcasts to make sure the frame reaches the client's NIC.
How does DHCP lease renewal work?::At ~50% of the lease the client sends a unicast Request straight to the server that gave the lease (skips D and O). If that fails, it falls back to broadcast rebinding at ~87.5%, and only then to a full DORA.
What does a 169.254.x.x (APIPA) IP mean in practice?::DORA failed somewhere — could be no DHCP server, lost Offer, lost Request or lost Ack. A sign the client could not close a lease.
Why exclude an address from the DHCP pool (ip dhcp excluded-address)?::So DHCP does not hand out an IP already used by static gear (router, server, printer) — avoids an IP conflict.
In a DHCP pool, what does the default-router command define?::The gateway given to clients — it is the IP of the router interface that belongs to that same network, not a generic router.
Which command renews a DHCP client's lease?::ipconfig /release then ipconfig /renew (Windows/Packet Tracer); dhclient on Linux. Forces a new DORA.
In the DHCP Offer packet, what is the YOUR CLIENT ADDRESS field?::The IP the server is offering the client to keep (the "O" of DORA written in the packet).
