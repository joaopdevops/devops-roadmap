---
tipo: conceito
area: Redes
camada-osi: 3
tags: [conceito, flashcards, redes]
primeira-aparicao: 2026-05-15
---

> 🇺🇸 [English version](NAT.en.md)
nat
# NAT — Network Address Translation

## Definição rápida

Técnica que **troca o IP privado por IP público** quando um pacote sai da rede local pra internet — e faz o caminho inverso na volta. Permite **vários dispositivos compartilharem 1 IP público**.

## Analogia

**Síndico no portão que reescreve o remetente das cartas e mantém uma planilha de despacho.**

Você (apartamento 305) escreve uma carta. Remetente: "Apto 305, Bloco B, Condomínio Y" (endereço interno, que ninguém na rua reconhece).

A carta passa pelo **portão** antes de ir aos Correios. O **síndico** está lá e faz três coisas:

1. **Apaga o remetente interno** ("Apto 305")
2. **Escreve um remetente oficial do prédio inteiro** ("Rua X, número 100")
3. **Anota na planilha do portão**: "carta com nº de protocolo 54321 saiu pro Apto 305"

Quando a resposta volta endereçada à "Rua X, 100, protocolo 54321", o síndico **consulta a planilha** e entrega no Apto 305 certo. **Mundo externo nunca sabe que existe um Apto 305 — só sabe do prédio.**

**Diferença pro porteiro (ARP):** porteiro fica na portaria interna, pergunta "quem mora aqui?". Síndico fica no portão de saída, representa o prédio pro mundo externo e mantém os registros. Funções e localizações distintas.

> **A planilha do síndico = tabela NAT.** É o coração do mecanismo. Sem ela, a resposta voltaria pro prédio e ninguém saberia em qual apto entregar.

## Como funciona — passo a passo

Roteador da sua casa tem **2 IPs**:
- **Privado** (lado interno, ex: `192.168.0.1`) — falado com seus dispositivos
- **Público** (lado da operadora, ex: `189.34.78.12`) — falado com a internet

**Quando seu PC acessa o Google:**
1. Ubuntu (`192.168.0.19`) monta pacote pra `142.250.78.78` (Google).
2. Pacote vai pro gateway (`192.168.0.1` = roteador).
3. Roteador **troca o IP de origem** do pacote: `192.168.0.19` → `189.34.78.12`.
4. Roteador **anota numa tabela**: "essa conversa (essa porta TCP/UDP) é do .19".
5. Pacote vai pra internet com origem `189.34.78.12`.
6. Google responde pra `189.34.78.12`.
7. Roteador recebe, **consulta a tabela**, descobre que era pro .19.
8. Roteador **troca o IP de destino** de volta: `189.34.78.12` → `192.168.0.19`.
9. Entrega pro Ubuntu.

**Resultado:** Google nunca soube que existia um `192.168.0.19`. Só viu `189.34.78.12`.

## Por que NAT existe — a história curta

IPv4 tem **~4 bilhões de endereços**. Em 1990 já se sabia que ia acabar (hoje tem 8 bilhões de pessoas + bilhões de dispositivos por pessoa).

**Solução criada nos anos 90:**
1. **RFC 1918** reservou faixas privadas (10/8, 172.16-31/12, 192.168/16) que **se repetem** entre redes locais sem conflito.
2. **NAT** traduz essas faixas privadas em IPs públicos na hora de sair pra internet.

Sem NAT, o IPv4 teria acabado nos anos 2000. Com NAT, dá pra ter 1 IP público por **rede inteira** (casa, empresa, prédio) em vez de 1 por dispositivo.

## Tipos de NAT — o básico

| Tipo | O que faz | Onde aparece |
|---|---|---|
| **NAT estático** | 1 IP privado fixo ↔ 1 IP público fixo | Servidor que precisa ser acessado de fora |
| **NAT dinâmico** | Pool de IPs públicos rotativo entre clientes | Empresas com poucos IPs públicos |
| **PAT (NAT overload)** | **Vários IPs privados → 1 IP público**, separados por porta | **Sua casa.** O mais comum. |

PAT é o que **realmente** roda no seu roteador doméstico. A "tabela" do roteador não usa só IP, usa **IP + porta** pra distinguir conversas.

## Como ver NAT acontecendo

- `whatismyip` no Google → mostra seu **IP público** (NAT do roteador)
- `ip addr show wlp0s20f3` no Linux → mostra seu **IP privado** (atrás do NAT)
- **São diferentes.** Essa diferença É o NAT.

## Conexão com RFC 1918

Lembra das 3 faixas privadas (Lab 2.1)?
- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

**Elas só funcionam porque NAT existe.** Privadas = válidas dentro de casa, **inválidas na internet**. Roteador OBRIGATORIAMENTE traduz antes de mandar pra fora — caso contrário, o pacote seria descartado por qualquer roteador da internet.

## Por que DevOps importa

- **AWS NAT Gateway:** instâncias em sub-rede privada (sem IP público) usam NAT Gateway pra acessar internet (apt update, baixar imagens Docker).
- **Docker:** containers em rede `bridge` recebem IP privado da rede `172.17.0.0/16`. Quando container faz `curl google.com`, daemon Docker faz NAT pra IP do host.
- **Kubernetes:** SNAT em pods saindo do cluster pra internet.

NAT está em todo lugar onde uma rede privada precisa falar com o mundo externo.

## Limitações do NAT

- **Quebra conexão entrante:** servidor externo não consegue iniciar conexão pra dispositivo atrás do NAT (não tem como saber pra qual IP privado mandar). Por isso jogos online, P2P e VoIP precisam de truques (port forwarding, STUN, UPnP).
- **Performance:** roteador precisa manter tabela e processar cada pacote. Em escala grande, vira gargalo.
- **IPv6 elimina a necessidade de NAT** (endereços suficientes pra todo dispositivo ter IP público), mas adoção tá lenta.

## Labs onde foi ensinado

- 2.3-Servicos-de-Rede — primeira aplicação prática (a fazer)

## Relacionado

- [RFC-1918](RFC-1918.md) — faixas privadas que existem POR CAUSA do NAT
- [Roteador](Roteador.md) — quem executa o NAT
- [Gateway](Gateway.md) — porta de saída onde NAT acontece
- [DHCP](DHCP.md) — distribui IPs privados que vão ser traduzidos pelo NAT

---

## Flashcards

O que e NAT?::Network Address Translation — tecnica que troca IP privado por IP publico ao sair da rede local, e faz o inverso na volta.
Por que NAT existe?::IPv4 tem so 4 bilhoes de enderecos, insuficiente para 1 IP publico por dispositivo. NAT permite vario dispositivos compartilharem 1 IP publico.
Quem executa o NAT na sua casa?::O roteador domestico — tem IP privado de um lado (192.168.x.x) e publico do outro (atribuido pela operadora).
O que e PAT?::Port Address Translation — variante do NAT onde varios IPs privados compartilham 1 IP publico, distinguidos por porta TCP/UDP. E o tipo de NAT mais comum em redes domesticas.
Como o roteador sabe pra qual IP interno entregar a resposta da internet?::Mantem uma tabela de traducao com IP+porta de cada conversa em andamento. Quando volta resposta, consulta a tabela.
Qual a relacao entre NAT e RFC 1918?::Faixas RFC 1918 sao privadas e nao roteiam na internet. NAT e o que permite essas faixas funcionarem — traduz para IP publico na saida.
Em qual camada OSI o NAT atua?::Camada 3 (Rede) — manipula enderecos IP. Quando faz PAT, toca tambem na Camada 4 (porta).
O que aparece no whatismyip — seu IP privado ou publico?::Publico. E o IP do roteador atribuido pela operadora — o NAT mascarou seu IP privado real.
Por que conexoes entrantes (servidor de fora iniciando conversa) sao problematicas com NAT?::O roteador nao sabe pra qual IP privado entregar — a tabela so tem entradas de conexoes que saiarem da rede local. Solucoes: port forwarding, STUN, UPnP.
NAT existe no IPv6?::Geralmente nao — IPv6 tem enderecos suficientes para cada dispositivo ter IP publico. NAT foi solucao temporaria para escassez do IPv4.
O Docker usa NAT?::Sim — containers tem IP privado da rede bridge (172.17.0.0/16). Daemon Docker faz NAT para o IP do host quando container acessa internet.
