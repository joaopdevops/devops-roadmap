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

## Flashcards

O que e DHCP?::Protocolo que distribui IP, mascara, gateway e DNS automaticamente para dispositivos que entram numa rede.
Quais 4 informacoes o DHCP entrega ao cliente?::IP, mascara de sub-rede, gateway e enderecos de servidores DNS.
O que significa DORA?::Discover, Offer, Request, Acknowledge — as 4 mensagens trocadas entre cliente e servidor DHCP.
Quem manda o Discover?::O cliente, em broadcast, perguntando "tem algum servidor DHCP aqui?".
Quem responde com o Offer?::O servidor DHCP, oferecendo um IP e os outros parametros.
Por que o Request e em broadcast e nao unicast?::Para outros servidores DHCP saberem que o cliente ja escolheu uma oferta — assim eles devolvem o IP oferecido para o pool.
O que e lease no DHCP?::O tempo de aluguel do IP — depois desse prazo, o cliente renova ou o IP volta para o pool.
Por que existe lease?::Para evitar que IPs fiquem alocados eternamente em dispositivos que sumiram da rede.
Sem DHCP, como cada dispositivo seria configurado?::Manualmente — IP, mascara, gateway e DNS digitados em cada um.
Qual a diferenca entre IP por DHCP e IP estatico?::DHCP entrega automaticamente e o IP pode mudar; estatico e configurado na mao e nunca muda. Servidores e equipamentos de rede usam estatico.
Em qual camada OSI o DHCP atua?::Camada 7 (Aplicacao) — roda sobre UDP nas portas 67 (servidor) e 68 (cliente).
Quem faz papel de servidor DHCP na sua casa?::O roteador domestico — distribui IPs da faixa 192.168.x.x para os dispositivos.
No DORA, quem inicia e quem responde?::Cliente inicia (passos D e R, impares), servidor responde (passos O e A, pares). Cliente toma a iniciativa, servidor reage.
Por que o Offer e broadcast se o servidor ja sabe o MAC do cliente?::Cliente ainda nao tem stack IP configurado (sem IP, mascara nem gateway), entao nao consegue receber unicast normal. Servidor usa broadcast pra garantir que o frame chegue na placa do cliente.
Como funciona a renovacao do lease no DHCP?::A ~50% do lease, cliente manda Request unicast direto pro servidor que deu o lease (pula D e O). Se falhar, cai pra rebinding em broadcast a ~87.5%, e so depois pra DORA completo.
O que significa um IP 169.254.x.x (APIPA) na pratica?::DORA falhou em algum ponto — pode ser sem servidor DHCP, Offer perdido, Request perdido ou Ack perdido. Sinal de que o cliente nao conseguiu fechar lease.
Por que excluir um endereco do pool DHCP (ip dhcp excluded-address)?::Para o DHCP nao distribuir um IP ja usado por equipamento estatico (roteador, servidor, impressora) — evita conflito de IP.
No pool DHCP, o que o comando default-router define?::O gateway entregue aos clientes — e o IP da interface do roteador que pertence aquela mesma rede, nao um roteador generico.
Que comando renova o lease de um cliente DHCP?::ipconfig /release e depois ipconfig /renew (Windows/Packet Tracer); dhclient no Linux. Forca um novo DORA.
No pacote DHCP Offer, o que e o campo YOUR CLIENT ADDRESS?::O IP que o servidor esta oferecendo ao cliente ficar (o "O" do DORA escrito no pacote).
