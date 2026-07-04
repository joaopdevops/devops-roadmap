---
tipo: conceito
area: Redes
camada-osi: 3
tags: [conceito, flashcards, redes, roteamento]
primeira-aparicao: 2026-06-28
consolidada: 2026-07-03
---

# Tabela de Rotas (decisão de rota)

## Definição rápida

A tabela de rotas é a **lista de instruções escritas** que o roteador (ou seu PC) consulta pra decidir o que fazer com cada pacote. Cada linha é uma regra **SE → ENTÃO**:

```
10.0.0.0/8  via  192.168.0.1
└── SE ──┘       └── ENTÃO ──┘
"SE o destino     "despacha pro
começa com 10."    192.168.0.1"
```

O roteador é **burro de propósito**: só executa o que está escrito. Regra não escrita = ação não executada. Ele nunca deduz "deve ser pra fora" — roteador que chuta espalharia pacote errado pelo mundo.

## Analogia

🏢 **Roteador = agência dos Correios; tabela de rotas = painel de triagem.** O funcionário lê o painel de cima a baixo: "SE o endereço é da Rua das Flores → porta 3. SE é do bairro Centro → caminhão 2. QUALQUER outra coisa → central." Encomenda que não casa com nenhuma linha do painel e sem regra "qualquer outra coisa"? **Devolve ao remetente com bilhete** — o funcionário não inventa destino.

## Como ler o SE (casar prefixo com destino) — A MECÂNICA

O número depois da barra diz **quantos números do começo do endereço estão travados**:

| Prefixo | Octetos travados | Significa "SE o destino..." |
|---|---|---|
| `10.0.0.0/8` | 1º | começa com **10.** |
| `172.16.0.0/16` | 1º e 2º | começa com **172.16.** |
| `192.168.0.0/24` | 1º, 2º e 3º | começa com **192.168.0.** |
| `0.0.0.0/0` | **nenhum** | **qualquer coisa** (é a default) |

**Teste na prática: compara só os números travados, um a um.**

```
8.8.8.8  casa com 10.0.0.0/8?    1º octeto: 8 ≠ 10   → NÃO casa
10.5.5.5 casa com 10.0.0.0/8?    1º octeto: 10 = 10  → CASA
172.16.3.3 casa com 172.16.0.0/16?  172=172, 16=16   → CASA
```

*(Prefixos que não caem na fronteira do octeto — /26, /29 etc. — travam "pedaços" do último número: é o mesmo bloco do subnetting. `192.168.0.64/26` = "começa com 192.168.0. E o último número está na faixa 64-127".)*

## A regra de ouro — longest prefix match

Se o destino casa com **mais de uma linha**, ganha a **mais específica** = a de **prefixo mais longo** = a com **mais números travados**. Faz sentido literal: mais números travados = endereço mais detalhado.

A default `/0` casa com TUDO, mas tem **zero números travados** — é a MENOS específica. Só ganha quando nenhuma outra casou. É o **último recurso**.

## O `via` — entrega direta vs intermediário

**TODA linha da tabela é rota conhecida.** A pergunta que cada linha responde não é "conheço?" — é "**entrego COMO?**":

| Linha | Tradução | Correios |
|---|---|---|
| `192.168.0.0/24 dev wlp0s20f3` (**sem** via) | rota **CONECTADA**: é vizinho meu, **entrego eu mesmo** | carta pro apto do lado: desço e entrego na porta |
| `default via 192.168.0.1` (**com** via) | entrego **POR VIA DE** (através de) alguém | carta pra outra cidade: levo na agência |

Grava pelo português: **"via" = "por via de / através de"**. Não é sobre conhecer — é sobre **precisar ou não de intermediário**.

## Quando NENHUMA linha casa

Sem linha que case (e sem default): o roteador **descarta o pacote** e devolve **ICMP Destination Unreachable** pra origem. Carta sem endereço no painel e sem regra geral → volta com bilhete.

**A default é a intuição "manda pro gateway de qualquer jeito" — POR ESCRITO.** A diferença entre "vai pro gateway" e "pacote morre" é uma linha escrita ou não escrita na tabela.

## O algoritmo completo (3 passos)

1. Pega o IP de destino do pacote.
2. Acha **todas** as linhas cujo SE casa; escolhe a de **prefixo mais longo**.
3. Nenhuma casou? Usa a **default**. Não tem default? **Descarta + ICMP Destination Unreachable.**

## Lab — veja na sua máquina (feito ao vivo em 03/07)

```bash
ip route                      # a lista de instruções inteira
ip route get 192.168.0.50     # "pra ESTE destino, qual linha ganha?" → sem via (vizinho, entrega direta)
ip route get 8.8.8.8          # → "via 192.168.0.1" (só a default casou → gateway)
```

`ip route get` = a decisão de rota acontecendo ao vivo.

## Por que importa pra DevOps

- "Rota errada / falta de rota" é causa nº 1 de "container não alcança o serviço X". `ip route get <ip-do-serviço>` responde em 1 segundo se a rota existe e por onde sai.
- Kubernetes/VPN/Docker criam e apagam rotas o tempo todo — ler a tabela é habilidade diária.

## Relacionado

- [[Conceitos/Roteador]] — quem executa a tabela
- [[Conceitos/Gateway]] — o intermediário do `via`
- [[Conceitos/Mascara-de-Rede]] — a mesma máscara: lá constrói o prédio, aqui filtra destinos
- [[Conceitos/ICMP]] — o bilhete Destination Unreachable

---

## 🇺🇸 English

## Quick definition

The routing table is the **written instruction list** a router (or your PC) checks for every packet. Each line is an **IF → THEN** rule: `10.0.0.0/8 via 192.168.0.1` = "IF the destination starts with **10.** THEN hand it to 192.168.0.1". The router is **dumb on purpose**: no written rule = no action. It never guesses.

## Reading the IF (prefix matching)

The number after the slash says **how many leading numbers of the address are locked**: `/8` = first octet ("starts with 10."), `/16` = first two, `/24` = first three, `/0` = none (matches anything — the default). To test a match, **compare only the locked numbers**: `8.8.8.8` vs `10.0.0.0/8` → 8 ≠ 10 → no match.

## Golden rule — longest prefix match

If a destination matches several lines, the **most specific** one wins (longest prefix = most locked numbers). The default `/0` matches everything but locks nothing — it is the **last resort**.

## `via` — direct vs middleman

**Every line in the table is a known route.** The question is not "do I know it?" but "**how do I deliver?**": no `via` = **connected route**, neighbor, deliver it myself; with `via` = hand it to the **gateway** (middleman). If **no line matches** (and there is no default), the router **drops the packet and sends ICMP Destination Unreachable** back.

## See it live

```bash
ip route get 8.8.8.8    # shows which line wins and whether a gateway (via) is used
```

## Why it matters for DevOps

"Wrong/missing route" is the #1 cause of "my container can't reach service X". `ip route get` answers it in one second.

---

## Flashcards

O que é cada linha da tabela de rotas?::A written IF-THEN rule: IF the destination matches the prefix, THEN deliver as instructed (directly or via a gateway).
O que significa o /8 em 10.0.0.0/8 na leitura da rota?::The first octet is locked: the rule matches any destination that starts with 10. — compare only the locked numbers to test a match.
8.8.8.8 casa com a rota 10.0.0.0/8? Por que?::No. The first octet is locked: 8 is not 10, so the rule does not match.
Qual a regra de ouro quando o destino casa com mais de uma linha?::Longest prefix match: the most specific line (most locked numbers) wins.
Por que a rota default 0.0.0.0/0 e o ultimo recurso?::It matches everything but locks nothing, so it is the least specific line — it only wins when no other line matches.
O que significa via numa linha da rota?::Deliver THROUGH a middleman (the gateway). It does NOT mean unknown route — every line in the table is a known route.
O que significa uma rota SEM via?::A connected route: the destination is a neighbor on my own network, so I deliver it myself, directly.
O que faz o roteador quando NENHUMA linha casa e nao ha default?::It drops the packet and sends ICMP Destination Unreachable back to the source. Routers never guess.
Qual comando mostra qual rota ganha para um destino especifico?::ip route get <destination> — it shows the route decision live, including the gateway (via) if one is used.
Por que o roteador nao manda pro gateway mesmo sem regra escrita?::Because routers are dumb on purpose: unwritten rule means no action. The default route IS that intuition, written down.
