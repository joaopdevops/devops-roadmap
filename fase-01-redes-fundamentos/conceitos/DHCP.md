---
tipo: conceito
area: Redes
camada-osi: 7
protocolo: DHCP
tags: [conceito, flashcards, redes]
primeira-aparicao: 2026-05-15
---

# DHCP — Dynamic Host Configuration Protocol

## Definição rápida

Protocolo que **distribui IP, máscara, gateway e DNS automaticamente** pra dispositivos que entram numa rede. Sem DHCP, cada PC, celular e impressora precisaria ser configurado na mão.

## Analogia

**Hotel que faz seu check-in.** Você chega no hotel sem nada definido. A recepcionista te entrega num pacote só:

- Número do quarto → **IP**
- Chave que abre só seu andar → **máscara de sub-rede**
- Mapa pra saída do prédio → **gateway**
- Senha do Wi-Fi e número da copa → **servidores DNS**

Tudo automático, sem você precisar pedir item por item. E o quarto é **alugado por tempo determinado** (lease) — depois, ou você renova ou devolve a chave.

## Como funciona — as 4 mensagens (DORA)

| # | Sigla | Quem fala | O que diz | Por que broadcast |
|---|---|---|---|---|
| 1 | **D**iscover | Cliente | "Tem algum servidor DHCP aí?" | Cliente nao sabe ainda quem (nem se) vai responder. Sem IP de origem, usa `0.0.0.0`. |
| 2 | **O**ffer | Servidor | "Tenho. Te ofereço IP 192.168.0.19 com máscara /24, gateway .1, DNS 8.8.8.8, lease de 24h" | Cliente ainda nao tem stack IP configurado — sem IP, mascara nem gateway, a pilha TCP/IP nao consegue processar unicast endereçado a um IP que ele nao tem. Servidor usa broadcast pra garantir que o frame chegue na placa. |
| 3 | **R**equest | Cliente | "Aceito a oferta do servidor X (IP 192.168.0.19)" | Avisa os **outros** servidores DHCP que ofereceram e nao foram escolhidos — eles liberam o IP que tinham reservado pro pool. Sem isso, IPs ficariam segurados a toa. |
| 4 | **A**cknowledge | Servidor escolhido | "Confirmado. IP é seu por 24h" | Broadcast ou unicast (depende da implementacao). Lease so fica oficial depois desse ack. |

**Mnemonico mestre:**
- Cliente fala nos passos **impares (1, 3)** — toma a iniciativa.
- Servidor responde nos pares **(2, 4)** — reage.
- Ordem **sempre** D → O → R → A no fluxo inicial. Nunca pula.

Tudo isso acontece em **frações de segundo** quando você liga o Wi-Fi.

## Lease — o "aluguel" do IP

O IP não é seu pra sempre. O servidor DHCP empresta por um tempo (lease) — geralmente algumas horas ou dias. Antes do prazo expirar, o cliente **renova** automaticamente. Se o dispositivo desaparecer (desligado, levou pra outro lugar), o IP volta pro pool e pode ser dado pra outro.

**Por que importa:** sem lease, cada dispositivo que ligasse uma vez consumiria 1 IP pra sempre, mesmo desligado. Pool esgotaria rápido.

## Renovacao do lease — como funciona de verdade

Antes do lease expirar, o cliente **nao faz DORA inteiro de novo**. Ele ja sabe quem foi o servidor que deu o IP — entao otimiza:

1. **~50% do lease decorrido (estado "renewing"):** cliente manda **Request unicast** direto pro servidor que deu o lease. **Pula Discover e Offer.**
2. Se servidor responder Ack → lease renovado, acabou.
3. Se servidor nao responder (caido, p.ex.), em **~87.5% do lease (estado "rebinding"):** cliente manda Request em **broadcast**, perguntando pra qualquer servidor.
4. Se nada responder ate o lease expirar → cliente perde o IP, cai pra **DORA completo** do zero.

**Por que importa:** se renovacao fizesse DORA inteiro toda hora, a rede ficaria saturada de broadcast. O protocolo otimiza pra silencio na rede em estado estavel.

## APIPA (169.254.x.x) — sinal de DORA falhou

Se o DORA nao completar, o sistema operacional auto-atribui um IP da faixa **`169.254.0.0/16`** (APIPA — Automatic Private IP Addressing). E um sinal claro de que algo no fluxo quebrou:

- **D quebrou:** rede nao tem servidor DHCP, ou roteador WiFi esta com DHCP desabilitado/caido. **Caso mais comum no mundo real.**
- **O quebrou:** servidor existe mas nao respondeu Offer (problema de rede, do servidor, ou do roteador).
- **R quebrou:** cliente recebeu Offer mas Request nao chegou no servidor (raro).
- **A quebrou:** servidor recebeu Request mas Ack nao chegou no cliente (lease nao "fecha" oficialmente).

**Diagnostico pratico:** ver IP `169.254.x.x` no `ip addr show` ou `ipconfig` = DHCP falhou em algum ponto. Investigar do roteador pra fora.

## Onde aparece na sua vida

- Seu Ubuntu pegou `192.168.0.19` automaticamente do roteador de casa quando ligou o Wi-Fi. **Foi DHCP.**
- Você nunca digitou esse IP na mão. Conferir: `ip addr show wlp0s20f3` no terminal.
- Roteador doméstico = servidor DHCP da rede de casa. Empresa = servidor DHCP dedicado (Windows Server, isc-dhcp-server no Linux, etc).

## Diferença pra notar

- **DHCP** = você recebe IP automaticamente
- **IP estático** = você configura na mão. Usado em servidores, roteadores, impressoras de rede — coisas que precisam de **endereço fixo previsível**.

## Por que DevOps importa

- **AWS EC2:** instâncias recebem IP via DHCP do VPC.
- **Docker:** containers recebem IP do daemon Docker (que faz papel de DHCP da rede `bridge`).
- **Kubernetes:** pods recebem IP via plugin CNI (mesmo conceito, escala diferente).

Sem entender DHCP, você não entende como container/VM "sabe" qual IP usar.

## Labs onde foi ensinado

- 2.3-Servicos-de-Rede — primeira aplicação prática (a fazer)

## Relacionado

- [Mascara-de-Rede](Mascara-de-Rede.md) — uma das 4 coisas entregues pelo DHCP
- [Gateway](Gateway.md) — outra das 4 coisas entregues
- [DNS](DNS.md) — DHCP entrega o IP do servidor DNS pro cliente usar
- [RFC-1918](RFC-1918.md) — IPs distribuídos por DHCP em rede local são privados (10/8, 172.16-31/12, 192.168/16)

---

## 🇺🇸 English

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

O que e DHCP?::A protocol that automatically hands out IP, mask, gateway and DNS to devices joining a network.
Quais 4 informacoes o DHCP entrega ao cliente?::IP, subnet mask, gateway and DNS server addresses.
O que significa DORA?::Discover, Offer, Request, Acknowledge — the 4 messages exchanged between DHCP client and server.
Quem manda o Discover?::The client, as a broadcast, asking "is there a DHCP server here?".
Quem responde com o Offer?::The DHCP server, offering an IP and the other parameters.
Por que o Request e em broadcast e nao unicast?::So other DHCP servers know the client already chose an offer — they then return the offered IP to the pool.
O que e lease no DHCP?::The IP rental time — after that deadline the client renews or the IP returns to the pool.
Por que existe lease?::To avoid IPs being allocated forever to devices that vanished from the network.
Sem DHCP, como cada dispositivo seria configurado?::Manually — IP, mask, gateway and DNS typed into each one.
Qual a diferenca entre IP por DHCP e IP estatico?::DHCP delivers automatically and the IP can change; static is set by hand and never changes. Servers and network gear use static.
Em qual camada OSI o DHCP atua?::Layer 7 (Application) — it runs over UDP on ports 67 (server) and 68 (client).
Quem faz papel de servidor DHCP na sua casa?::The home router — it hands out IPs from the 192.168.x.x range to the devices.
No DORA, quem inicia e quem responde?::The client initiates (steps D and R, odd), the server responds (steps O and A, even). The client takes the initiative, the server reacts.
Por que o Offer e broadcast se o servidor ja sabe o MAC do cliente?::The client has no IP stack configured yet (no IP, mask or gateway), so it cannot receive a normal unicast. The server broadcasts to make sure the frame reaches the client's NIC.
Como funciona a renovacao do lease no DHCP?::At ~50% of the lease the client sends a unicast Request straight to the server that gave the lease (skips D and O). If that fails, it falls back to broadcast rebinding at ~87.5%, and only then to a full DORA.
O que significa um IP 169.254.x.x (APIPA) na pratica?::DORA failed somewhere — could be no DHCP server, lost Offer, lost Request or lost Ack. A sign the client could not close a lease.
Por que excluir um endereco do pool DHCP (ip dhcp excluded-address)?::So DHCP does not hand out an IP already used by static gear (router, server, printer) — avoids an IP conflict.
No pool DHCP, o que o comando default-router define?::The gateway given to clients — it is the IP of the router interface that belongs to that same network, not a generic router.
Que comando renova o lease de um cliente DHCP?::ipconfig /release then ipconfig /renew (Windows/Packet Tracer); dhclient on Linux. Forces a new DORA.
No pacote DHCP Offer, o que e o campo YOUR CLIENT ADDRESS?::The IP the server is offering the client to keep (the "O" of DORA written in the packet).
