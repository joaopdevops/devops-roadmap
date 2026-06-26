---
tipo: conceito
area: Redes
camada-osi: 7
protocolo: DNS
tags: [conceito, flashcards, redes]
primeira-aparicao: 2026-05-15
---

# DNS — Domain Name System

## Definição rápida

Sistema que **traduz nome de domínio em IP**. Você pensa em `google.com`, o computador precisa de `142.250.78.78`. DNS faz a tradução.

## Analogia

**Agenda de contatos do celular.** Você liga pra "Mãe", não disca "+55 41 98765-4321". Seu celular consulta a agenda, traduz "Mãe" no número e disca. Você pensa em **nomes**, telefone disca em **números**.

DNS é a agenda de contatos da internet inteira: você pensa em nomes (`google.com`, `youtube.com`, `github.com`), o computador precisa de IPs pra mandar pacote.

## Como funciona — hierarquia mundial

Nenhum servidor DNS sabe TODOS os IPs do mundo. A consulta passa por uma hierarquia:

1. **Você digita `www.google.com`** no navegador.
2. Computador pergunta pro **DNS local** (geralmente do provedor ou `8.8.8.8` do Google): "qual o IP de `www.google.com`?"
3. DNS local não sabe → pergunta pra um **servidor raiz**: "quem cuida do `.com`?"
4. Servidor raiz responde: "fala com os servidores TLD `.com`".
5. DNS local pergunta pros **servidores `.com`**: "quem cuida de `google.com`?"
6. Resposta: "fala com os servidores autoritativos do `google.com`".
7. DNS local pergunta pros **servidores autoritativos da Google**: "qual o IP de `www.google.com`?"
8. Resposta: `142.250.78.78`.
9. DNS local devolve esse IP pro seu computador.

**Tudo isso em frações de segundo.** E com **cache em todo lugar** (cliente, DNS local, servidores intermediários) pra não refazer a viagem inteira toda vez.

## TTL no DNS — mesmo conceito, contexto diferente

Cada resposta DNS vem com um **TTL** (tempo de vida do registro em cache). Diferente do TTL do pacote IP que você já viu (Lab 2.2):

| TTL no IP (pacote) | TTL no DNS (registro) |
|---|---|
| Conta **saltos** (decrementa por roteador) | Conta **segundos** em cache |
| Mata pacote em loop | Define quando re-perguntar pelo registro |
| Carimbado pelo SO da origem (64 ou 128) | Definido pelo dono do domínio (ex: 300s) |

**Mesmo nome, conceitos primos:** ambos são "prazo de validade", mas medem coisas diferentes. Lineu cuida do TTL do pacote; o cache DNS cuida do TTL do registro.

## Tipos de registro (records) — o básico

| Record | O que faz                      | Exemplo                              |
| ------ | ------------------------------ | ------------------------------------ |
| **A**  | Nome → IPv4                    | `google.com` → `142.250.78.78`       |
| AAAA   | Nome → IPv6                    | `google.com` → `2607:f8b0::4004:80a` |
| CNAME  | Apelido → outro nome           | `www.exemplo.com` → `exemplo.com`    |
| MX     | Servidor de email do domínio   | (manda email pra `gmail.com`)        |
| NS     | Quem é o servidor autoritativo | (delega a autoridade do domínio)     |

**No Lab 2.3 você só vai mexer com `A` record.** Os outros entram conforme o curso avança.

## Onde aparece na sua vida

- Toda vez que digita endereço no navegador, **antes** da página abrir, tem DNS lookup acontecendo.
- `nslookup google.com` no terminal = pergunta direta ao DNS, retorna o IP.
- `dig google.com` = versão mais detalhada.
- `/etc/resolv.conf` no Linux = arquivo que diz qual servidor DNS usar (geralmente entregue por DHCP).

## Sem DNS — como seria

Internet vira **lista de IPs decorados**. Você teria que digitar `142.250.78.78` em vez de `google.com`. Cada serviço, cada site, um número diferente pra lembrar. Inviável.

## Por que DevOps importa

- **Service Discovery** em Kubernetes/Docker é DNS: container `frontend` acha o `backend` pelo nome `backend.namespace.svc.cluster.local`.
- **AWS Route53** é serviço de DNS gerenciado.
- **Resolução interna em VPC** (instância EC2 acha outra pelo hostname) usa DNS.
- **Debugging de produção:** 50% dos incidentes "site fora do ar" são DNS quebrado, não a aplicação.

> "**It's always DNS.**" — meme verdadeiro do mundo SRE/DevOps.

## Labs onde foi ensinado

- 2.3-Servicos-de-Rede — primeira aplicação prática (a fazer)

## Relacionado

- [DHCP](DHCP.md) — entrega o IP do servidor DNS pro cliente usar
- [TTL](TTL.md) — mesmo nome, contexto diferente (pacote IP vs cache DNS)
- [NAT](NAT.md) — DNS resolve nome de host externo; NAT permite o pacote sair pra falar com ele

---

## 🇺🇸 English

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

O que e DNS?::A system that translates a domain name (google.com) into an IP (142.250.78.78).
Por que DNS existe?::So humans think in names and machines use numbers — without DNS the internet would be a list of memorized IPs.
Em qual camada OSI o DNS atua?::Layer 7 (Application) — it runs mostly over UDP on port 53.
O que e um servidor DNS recursivo?::A server that walks the whole hierarchy (root, TLD, authoritative) and returns the final IP to the client.
O que e cache DNS?::Temporary memory of recent answers, to avoid redoing the whole hierarchy every time. It has a TTL — after the deadline, it re-asks.
Qual a diferenca entre TTL do pacote IP e TTL do DNS?::The IP TTL counts hops per router (kills a packet in a loop). The DNS TTL counts seconds in cache (defines when to re-ask for the record).
Quem define o TTL de um registro DNS?::The domain owner, when configuring the record on the authoritative server.
O que e um registro tipo A?::A direct mapping of a name to an IPv4 address. E.g. google.com -> 142.250.78.78.
O que e um registro CNAME?::An alias — points one name to another name. E.g. www.example.com -> example.com.
O que e o servidor 8.8.8.8?::Google's public DNS — one of the most used recursive resolvers.
Onde fica configurado o servidor DNS no Linux?::In the /etc/resolv.conf file — usually delivered automatically by DHCP.
Por que o ditado "It's always DNS" existe no DevOps?::Because a large share of "site is down" incidents are caused by a DNS problem, not the application itself.
Na sua casa, quem e o servidor DNS de verdade?::The ISP's DNS (or a public one like 8.8.8.8). The home router is not the contact list — it just forwards the question (forwarder/relay).
Onde existe um servidor DNS dedicado na pratica?::Corporate networks (Windows Server/AD with internal .local names), cloud (AWS Route 53) and Kubernetes (CoreDNS). Homes do not have one — they use the ISP's.
Que comando testa a resolucao de um nome no terminal?::nslookup followed by the name (e.g. nslookup www.lab.local) — asks the DNS server directly and shows the returned IP.
Ao configurar um servidor DNS, o que e adicionar um registro A?::Adding a contact to the address book: linking a name (www.lab.local) to an IPv4 (192.168.10.10).
