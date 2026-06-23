---
tipo: conceito
area: Networking
camada-osi: 3
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](NAT.md)

# NAT — Network Address Translation

## Quick definition

A technique that **swaps the private IP for a public IP** when a packet leaves the local network for the internet — and does the reverse on the way back. It lets **many devices share 1 public IP**.

## Analogy

**A building manager at the gate who rewrites the sender of the letters and keeps a dispatch log.**

You (apartment 305) write a letter. Sender: "Apt 305, Block B, Condo Y" (an internal address nobody on the street recognizes).

The letter passes the **gate** before going to the post office. The **building manager** is there and does three things:

1. **Erases the internal sender** ("Apt 305")
2. **Writes an official sender for the whole building** ("123 X Street")
3. **Notes in the gate log**: "letter with protocol no. 54321 went out for Apt 305"

When the reply comes back addressed to "123 X Street, protocol 54321", the manager **checks the log** and delivers it to the right Apt 305. **The outside world never knows an Apt 305 exists — it only knows the building.**

**Difference from the doorman (ARP):** the doorman stays at the internal lobby, asking "who lives here?". The manager stays at the exit gate, represents the building to the outside world and keeps the records. Different roles and locations.

> **The manager's log = the NAT table.** It is the heart of the mechanism. Without it, the reply would come back to the building and nobody would know which apartment to deliver to.

## How it works — step by step

Your home router has **2 IPs**:
- **Private** (inside, e.g. `192.168.0.1`) — speaks to your devices
- **Public** (ISP side, e.g. `189.34.78.12`) — speaks to the internet

**When your PC accesses Google:**
1. Ubuntu (`192.168.0.19`) builds a packet for `142.250.78.78` (Google).
2. The packet goes to the gateway (`192.168.0.1` = router).
3. The router **swaps the source IP**: `192.168.0.19` → `189.34.78.12`.
4. The router **notes in a table**: "this conversation (this TCP/UDP port) belongs to .19".
5. The packet goes to the internet with source `189.34.78.12`.
6. Google replies to `189.34.78.12`.
7. The router receives it, **checks the table**, finds it was for .19.
8. The router **swaps the destination IP** back: `189.34.78.12` → `192.168.0.19`.
9. Delivers it to Ubuntu.

**Result:** Google never knew a `192.168.0.19` existed. It only saw `189.34.78.12`.

## Why NAT exists — the short story

IPv4 has **~4 billion addresses**. By 1990 it was clear they would run out (today there are 8 billion people + billions of devices). 

**The solution created in the 90s:**
1. **RFC 1918** reserved private ranges (10/8, 172.16-31/12, 192.168/16) that **repeat** across local networks without conflict.
2. **NAT** translates those private ranges into public IPs at the moment of leaving for the internet.

Without NAT, IPv4 would have run out in the 2000s. With NAT, you can have 1 public IP per **whole network** (home, company, building) instead of 1 per device.

## NAT types — the basics

| Type | What it does | Where it shows up |
|---|---|---|
| **Static NAT** | 1 fixed private IP ↔ 1 fixed public IP | A server that must be reachable from outside |
| **Dynamic NAT** | A pool of public IPs rotated among clients | Companies with few public IPs |
| **PAT (NAT overload)** | **Many private IPs → 1 public IP**, separated by port | **Your home.** The most common. |

PAT is what **actually** runs on your home router. The router's "table" does not use only IP, it uses **IP + port** to tell conversations apart.

## How to see NAT happening

- `whatismyip` on Google → shows your **public IP** (the router's NAT)
- `ip addr show wlp0s20f3` on Linux → shows your **private IP** (behind NAT)
- **They are different.** That difference IS the NAT.

## Connection to RFC 1918

Remember the 3 private ranges (Lab 2.1)?
- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

**They only work because NAT exists.** Private = valid inside the home, **invalid on the internet**. The router MUST translate before sending out — otherwise the packet would be dropped by any internet router.

## Why it matters for DevOps

- **AWS NAT Gateway:** instances in a private subnet (no public IP) use a NAT Gateway to reach the internet (apt update, pulling Docker images).
- **Docker:** containers on the `bridge` network get a private IP from `172.17.0.0/16`. When a container runs `curl google.com`, the Docker daemon does NAT to the host IP.
- **Kubernetes:** SNAT on pods leaving the cluster for the internet.

NAT is everywhere a private network needs to talk to the outside world.

## NAT limitations

- **Breaks inbound connections:** an external server cannot start a connection to a device behind NAT (no way to know which private IP to send to). That is why online games, P2P and VoIP need tricks (port forwarding, STUN, UPnP).
- **Performance:** the router must keep a table and process every packet. At large scale it becomes a bottleneck.
- **IPv6 removes the need for NAT** (enough addresses for every device to have a public IP), but adoption is slow.

## Where it was taught

- Lab 2.3 — Network Services

## Related

- RFC 1918 — the private ranges that exist BECAUSE of NAT
- Router — who performs the NAT
- Gateway — the exit door where NAT happens
- DHCP — hands out the private IPs that NAT will translate

---

## Flashcards

What is NAT?::Network Address Translation — a technique that swaps a private IP for a public IP when leaving the local network, and does the reverse on the way back.
Why does NAT exist?::IPv4 has only 4 billion addresses, not enough for 1 public IP per device. NAT lets many devices share 1 public IP.
Who performs NAT in your home?::The home router — it has a private IP on one side (192.168.x.x) and a public one on the other (assigned by the ISP).
What is PAT?::Port Address Translation — a NAT variant where many private IPs share 1 public IP, told apart by TCP/UDP port. It is the most common NAT type in home networks.
How does the router know which internal IP to deliver the internet's reply to?::It keeps a translation table with the IP+port of each ongoing conversation. When the reply comes back, it checks the table.
What is the relationship between NAT and RFC 1918?::RFC 1918 ranges are private and do not route on the internet. NAT is what lets those ranges work — it translates to a public IP on the way out.
At which OSI layer does NAT operate?::Layer 3 (Network) — it manipulates IP addresses. When doing PAT it also touches Layer 4 (the port).
What shows up in whatismyip — your private or public IP?::Public. It is the router's IP assigned by the ISP — NAT masked your real private IP.
Why are inbound connections (an outside server starting the conversation) problematic with NAT?::The router does not know which private IP to deliver to — the table only has entries for connections that left the local network. Solutions: port forwarding, STUN, UPnP.
Does NAT exist in IPv6?::Generally no — IPv6 has enough addresses for each device to have a public IP. NAT was a temporary fix for IPv4 scarcity.
Does Docker use NAT?::Yes — containers have a private IP from the bridge network (172.17.0.0/16). The Docker daemon does NAT to the host IP when a container accesses the internet.
