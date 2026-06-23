---
tipo: conceito
area: Networking
camada-osi: 3
protocolo: ICMP
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](MTU-Fragmentacao.md)

# MTU and Fragmentation

## Quick definition

**MTU (Maximum Transmission Unit)** = the **maximum size** of a packet that a network interface will transmit, in bytes. Ethernet/Wi-Fi default: **1500**. If a packet exceeds the MTU, it must be **fragmented** (split into smaller pieces) — or **refused**, if it is marked do-not-fragment.

> ## 🎯 What is on the CCNA (study focus)
>
> **On the CCNA 200-301 (understand well):**
> - The **concept** of MTU and fragmentation (the truck's box).
> - The **DF bit** and ICMP Type 3 Code 4 ("did not fit, send smaller").
> - **Path MTU Discovery** (how the source finds the smallest MTU on the path).
> - **Jumbo frames** (MTU 9000) — shows up in switching.
> - The **bug signature**: "small passes, large stalls = MTU".
>
> **NOT on the CCNA (Linux/DevOps — look it up, do not memorize):**
> - The commands `ping -M do`, `ip link set ... mtu`, `iptables ... TCPMSS`.
> - On Cisco the equivalent fix is **one line**: `ip tcp adjust-mss 1452` on an interface (tunnel/WAN). That is all.
>
> Summary: **understand the "concept" column, look up the "command" column.**

## Analogy

**MTU = the size of the box that fits in the mail truck.**

The parcel (your data) has to fit in a standard box. If it is bigger than the box:
- either the post office **splits it into smaller boxes** (fragmentation) and reassembles at the destination;
- or, if the parcel is stamped **"DO NOT SPLIT"** (the **DF bit** = *Don't Fragment*), the post office **sends back a note**: *"did not fit, send smaller"*. That note is an **ICMP** message.

## The math — why 1472 is the magic number

The 1500 MTU is the size of the **whole IP packet**, and mandatory labels already go inside it before your payload:

| Part | Bytes | What it is |
|---|---|---|
| **IP** header | 20 | source/destination address (the label) |
| **ICMP** header | 8 | the ping type |
| **Payload** (your `-s`) | the rest | the data |
| **MAX TOTAL** | **1500** | the MTU |

So: `1500 − 20 − 8 =` **`1472`** bytes of maximum payload in a ping.

- **1472** + 28 = 1500 → fits in the box, **passes**
- **1473** + 28 = 1501 → 1 byte too far, **overflows**

## Seeing it live on Linux (what I did)

```bash
ip link show wlp0s20f3        # find the Wi-Fi card's MTU -> mtu 1500
ping -c 2 -M do -s 1472 8.8.8.8   # fits exactly -> passes, 0% loss
ping -c 2 -M do -s 1473 8.8.8.8   # 1 byte over -> "Message too long"
```

- `-s 1472` = **s**ize: the payload size, in bytes
- `-M do` = **do**n't fragment: stamps the packet as "FORBIDDEN to split" (sets the DF bit)
- `lo` (loopback) has MTU 65536 because it is virtual, it has no physical medium — not useful for this test

## Who warns when it does not fit

When the packet exceeds the MTU **and** the DF bit is set:
- If the bottleneck is the **outgoing card itself**, the machine blocks it locally (that was the "Message too long" I saw — the packet never even left).
- If the bottleneck is a **router along the path** (a smaller link further ahead), that router sends an **ICMP Type 3, Code 4** ("Fragmentation Needed but DF set") back to the source.

That ICMP Type 3/4 is the basis of **Path MTU Discovery** — how the source finds the smallest MTU of the whole path and adjusts the packet size.

> ICMP again: it is not just the ping's "are you alive?" — it is the **network's error messenger**.

## How to fix an MTU problem — the 3 ways

> ⚠️ **This section is Linux/DevOps — NOT on the CCNA.** Look it up, do not memorize. On Cisco the equivalent is one line (`ip tcp adjust-mss 1452`). Read it to know it exists; come back when you need to use it.

The symptom that triggers all this: **"connects but stalls on large transfers"** — a small packet passes, a large packet vanishes. An MTU signature (it is not a wrong password, otherwise it would not even connect; it is not a down network, otherwise not even the small one would pass).

### Way 1 — Diagnose (find the right truck)

Same `-M do` tool, now as diagnosis: keep lowering `-s` until it stops failing. The largest payload that passes **+ 28** = the path's real MTU.

```bash
ping -M do -s 1472 8.8.8.8   # failed? lower it
ping -M do -s 1400 8.8.8.8   # passed? this one fits
```

### Way 2 — Lower the interface MTU (the blunt way)

```bash
sudo ip link set dev wlp0s20f3 mtu 1400
ip a                                    # check: shows mtu 1400
```

- `ip link set dev wlp0s20f3` — touches that card.
- `mtu 1400` — shrinks the truck to 1400.

**Translation:** you buy a smaller truck, so every box that leaves already fits further ahead. Simple, but **blunt** — it affects *everything* leaving that card. Good for a one-off test on your Linux.

### Way 3 — MSS clamping (the professional way, at the gateway)

In the TCP handshake both sides agree on the maximum size of each chunk (**MSS** = Maximum Segment Size, the TCP payload). MSS clamping = a gateway in the middle **rewrites** that agreement to a smaller value, at the SYN.

```bash
sudo iptables -t mangle -A FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu
```

- `iptables` — Linux packet manipulation tool.
- `-t mangle` — the table that **alters** packet fields (patches, does not block).
- `-A FORWARD` — only packets that **cross** the machine (routing) — gateway behavior.
- `-p tcp` — only TCP (MSS only exists in TCP).
- `--tcp-flags SYN,RST SYN` — only the **SYN**, the handshake, where MSS is negotiated.
- `-j TCPMSS --clamp-mss-to-pmtu` — clamps the MSS to the path's MTU, **automatically**.

**Why it is the right fix at a VPN gateway:** it is surgical (only that connection's TCP), automatic (no hardcoding the number), and — most importantly — **it adjusts at a single point and fixes it for all the clients** behind the gateway. That is why VPN, a gateway and the Kubernetes CNI do MSS clamping on their own.

> **The opposite — jumbo frames:** in the data center (the Equinix world), for performance, you *increase* the MTU: `sudo ip link set dev eth0 mtu 9000`. A giant truck to move a lot of data at once (storage, backup). Not a stall fix — an optimization.

## Why it matters for DevOps

One of the **most treacherous** causes of production bugs:

- **Kubernetes:** overlay networks (Flannel, Calico, VXLAN) **lower the pods' MTU** below 1500. If not adjusted, a large packet overflows in the encapsulation.
- **VPN / tunnels (IPsec, GRE, WireGuard):** the encapsulation eats bytes from the MTU. The app connects, pings, everything seems fine — but it **stalls when transferring a large file**.
- Classic symptom: "the connection opens but freezes on large transfers". Someone who knows MTU solves it in minutes; someone who does not loses days chasing a ghost.

## Related

- ICMP — who delivers the "did not fit" notice (Type 3 Code 4)
- TTL — another IP header field, same "limit on the packet" logic
- Router — who fragments or generates the ICMP along the path

---

## Flashcards

What is MTU?::Maximum Transmission Unit — the maximum size in bytes of a packet an interface will transmit. Ethernet/Wi-Fi default is 1500.
Why is the maximum ping payload 1472 and not 1500?::Because 1500 is the whole IP packet; 20 bytes go in the IP header and 8 in the ICMP header. 1500 - 20 - 8 = 1472.
What is the DF bit?::Don't Fragment — a mark on the packet that forbids fragmentation. If the packet does not fit the MTU and DF is set, it is refused instead of split.
What happens to a packet larger than the MTU without the DF bit?::It is fragmented (split into smaller pieces) and reassembled at the destination.
Who tells the source that a packet did not fit and DF was set?::An ICMP Type 3 (Destination Unreachable) Code 4 (Fragmentation Needed) sent by the bottleneck router.
What is Path MTU Discovery?::A mechanism where the source finds the smallest MTU of the whole path using the ICMP Type 3/4 messages, and adjusts packet size to avoid fragmentation.
Why does the loopback interface have MTU 65536?::Because it is virtual, it does not cross a physical medium, so it has no real physical frame-size limit.
Why does MTU matter in Kubernetes and VPN?::Overlay networks and tunnels lower the MTU through encapsulation. If not adjusted, large packets overflow and the connection stalls on large transfers.
What is the signature of an MTU problem?::Connects but stalls on large transfers — a small packet passes, a large packet vanishes. Not a password (it would not connect) nor a down network (not even the small one would pass).
How do you find a path's real MTU?::With ping -M do -s, lowering the size until it stops failing; the largest payload that passes + 28 = the MTU.
How do you lower an interface's MTU on Linux?::sudo ip link set dev <interface> mtu 1400 — affects everything leaving that card (blunt, good for testing).
What is MSS clamping?::A gateway rewrites the MSS (TCP payload size) to a smaller value at the handshake (SYN), automatically. Command: iptables -t mangle -A FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu.
Why is MSS clamping the right fix at a VPN gateway?::It is surgical (only that connection's TCP), automatic, and adjusts at a single point fixing it for all clients behind the gateway. That is why VPN and the Kubernetes CNI do it on their own.
What are jumbo frames?::An increased MTU (e.g. 9000) in the data center for performance — a giant truck to move a lot of data at once. An optimization, not a stall fix.
