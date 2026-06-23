---
tipo: conceito
area: Networking
camada-osi: 7
protocolo: DNS
tags: [conceito, flashcards, redes, en]
---

> 🇧🇷 [Versão em Português](DNS.md)

# DNS — Domain Name System

## Quick definition

A system that **translates a domain name into an IP**. You think of `google.com`, the computer needs `142.250.78.78`. DNS does the translation.

## Analogy

**Your phone's contact list.** You call "Mom", you do not dial "+55 41 98765-4321". Your phone checks the contacts, translates "Mom" into the number and dials. You think in **names**, the phone dials in **numbers**.

DNS is the contact list of the whole internet: you think in names (`google.com`, `youtube.com`, `github.com`), the computer needs IPs to send packets.

## How it works — a worldwide hierarchy

No single DNS server knows ALL the IPs in the world. The query walks a hierarchy:

1. **You type `www.google.com`** in the browser.
2. The computer asks the **local DNS** (usually the ISP's or Google's `8.8.8.8`): "what is the IP of `www.google.com`?"
3. The local DNS does not know → asks a **root server**: "who handles `.com`?"
4. The root server answers: "talk to the `.com` TLD servers".
5. The local DNS asks the **`.com` servers**: "who handles `google.com`?"
6. Answer: "talk to `google.com`'s authoritative servers".
7. The local DNS asks **Google's authoritative servers**: "what is the IP of `www.google.com`?"
8. Answer: `142.250.78.78`.
9. The local DNS returns that IP to your computer.

**All in fractions of a second.** And with **caching everywhere** (client, local DNS, intermediate servers) so it does not redo the whole trip every time.

## TTL in DNS — same word, different context

Each DNS answer comes with a **TTL** (the record's cache lifetime). Different from the IP packet TTL you already saw (Lab 2.2):

| TTL in IP (packet) | TTL in DNS (record) |
|---|---|
| Counts **hops** (decremented per router) | Counts **seconds** in cache |
| Kills a packet in a loop | Defines when to re-ask for the record |
| Stamped by the source OS (64 or 128) | Set by the domain owner (e.g. 300s) |

**Same name, cousin concepts:** both are an "expiration date", but they measure different things. The router handles the packet's TTL; the DNS cache handles the record's TTL.

## Record types — the basics

| Record | What it does                  | Example                              |
| ------ | ----------------------------- | ------------------------------------ |
| **A**  | Name → IPv4                   | `google.com` → `142.250.78.78`       |
| AAAA   | Name → IPv6                   | `google.com` → `2607:f8b0::4004:80a` |
| CNAME  | Alias → another name          | `www.example.com` → `example.com`    |
| MX     | The domain's mail server      | (sends email to `gmail.com`)         |
| NS     | Who the authoritative server is | (delegates the domain's authority) |

**In Lab 2.3 you only touch the `A` record.** The others come as the course advances.

## Where it shows up in your life

- Every time you type an address in the browser, **before** the page opens, a DNS lookup is happening.
- `nslookup google.com` in the terminal = a direct question to DNS, returns the IP.
- `dig google.com` = a more detailed version.
- `/etc/resolv.conf` on Linux = the file that says which DNS server to use (usually delivered by DHCP).

## Without DNS — what it would be like

The internet becomes a **list of memorized IPs**. You would have to type `142.250.78.78` instead of `google.com`. Each service, each site, a different number to remember. Unworkable.

## Why it matters for DevOps

- **Service Discovery** in Kubernetes/Docker is DNS: the `frontend` container finds the `backend` by the name `backend.namespace.svc.cluster.local`.
- **AWS Route 53** is a managed DNS service.
- **Internal resolution in a VPC** (an EC2 instance finds another by hostname) uses DNS.
- **Production debugging:** 50% of "site is down" incidents are broken DNS, not the application.

> "**It's always DNS.**" — a true meme from the SRE/DevOps world.

## Where it was taught

- Lab 2.3 — Network Services

## Related

- DHCP — delivers the DNS server IP for the client to use
- TTL — same word, different context (IP packet vs DNS cache)
- NAT — DNS resolves an external host name; NAT lets the packet go out to reach it

---

## Flashcards

What is DNS?::A system that translates a domain name (google.com) into an IP (142.250.78.78).
Why does DNS exist?::So humans think in names and machines use numbers — without DNS the internet would be a list of memorized IPs.
At which OSI layer does DNS operate?::Layer 7 (Application) — it runs mostly over UDP on port 53.
What is a recursive DNS server?::A server that walks the whole hierarchy (root, TLD, authoritative) and returns the final IP to the client.
What is a DNS cache?::Temporary memory of recent answers, to avoid redoing the whole hierarchy every time. It has a TTL — after the deadline, it re-asks.
What is the difference between the IP packet TTL and the DNS TTL?::The IP TTL counts hops per router (kills a packet in a loop). The DNS TTL counts seconds in cache (defines when to re-ask for the record).
Who sets a DNS record's TTL?::The domain owner, when configuring the record on the authoritative server.
What is an A record?::A direct mapping of a name to an IPv4 address. E.g. google.com -> 142.250.78.78.
What is a CNAME record?::An alias — points one name to another name. E.g. www.example.com -> example.com.
What is the 8.8.8.8 server?::Google's public DNS — one of the most used recursive resolvers.
Where is the DNS server configured on Linux?::In the /etc/resolv.conf file — usually delivered automatically by DHCP.
Why does the saying "It's always DNS" exist in DevOps?::Because a large share of "site is down" incidents are caused by a DNS problem, not the application itself.
At home, who is the real DNS server?::The ISP's DNS (or a public one like 8.8.8.8). The home router is not the contact list — it just forwards the question (forwarder/relay).
Where does a dedicated DNS server exist in practice?::Corporate networks (Windows Server/AD with internal .local names), cloud (AWS Route 53) and Kubernetes (CoreDNS). Homes do not have one — they use the ISP's.
Which command tests name resolution in the terminal?::nslookup followed by the name (e.g. nslookup www.lab.local) — asks the DNS server directly and shows the returned IP.
When configuring a DNS server, what is adding an A record?::Adding a contact to the address book: linking a name (www.lab.local) to an IPv4 (192.168.10.10).
