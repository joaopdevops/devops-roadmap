---
tags: [resumo, redes, ccna]
periodo: 2026-05-04 a 2026-06-11
---

# Resumo — Redes Fundamentos (Semanas 02 a 04)

Consolidado do que estudei no período: subnetting, serviços de rede (DHCP/DNS/NAT) e ICMP/fragmentação.

---

## Tópicos cobertos

- **Subnetting prático** — escolha de prefixo, faixa útil, contagem de sub-redes.
- **DHCP / DNS / NAT** — serviços de rede, com prática no Linux real.
- **ICMP / Fragmentação (Etapa 1)** — MTU, DF bit, Path MTU Discovery, vistos ao vivo no Linux.

## Conceitos novos

- **DHCP** — DORA (Discover / Offer / Request / Ack); renovação unicast (~50%), rebinding broadcast (~87,5%); APIPA `169.254.x.x` = DORA falhou.
- **DNS** — resolução nome → IP; TTL de registro DNS ≠ TTL de pacote IP.
- **NAT / PAT (`overload`)** — tradução privado ↔ público na fronteira; a porta desempata dois hosts atrás de um único IP público.
- **MTU / Fragmentação** — `1500 − 20 (IP) − 8 (ICMP) = 1472` de recheio; DF bit; Path MTU Discovery via ICMP Tipo 3 Código 4.

## Analogias que uso pra fixar

- **NAT = síndico no portão** — a planilha do síndico é a tabela NAT; em PAT, a porta é o "protocolo" que identifica cada apartamento.
- **MTU / Fragmentação = caixa do caminhão dos Correios** — encomenda grande é dividida em caixas; se marcada "não dividir" (DF bit), volta um bilhete ICMP "manda menor".

## Erros que cometi e corrigi (registro honesto)

| Erro | Correção |
|------|----------|
| Achei que o DHCP "resolve o esgotamento de IPs do mundo" | DHCP gerencia config local; quem resolve o esgotamento do IPv4 é o **NAT** |
| Contei `/24 → /27` como 5 sub-redes | São **8** — `2^(27-24)` = 2³ bits emprestados. Fórmula internalizada |
| Invertia a notação da máscara na escrita (`8-256` em vez de `256-8`) | A cabeça acerta o valor; passei a escrever a ordem `256 − bloco` explícita em todo drill |
| Li `lo` (MTU 65536) como interface física | Loopback é virtual, sem limite físico; a interface real (`wlp0s20f3`) tem MTU 1500 |

## Nível de domínio ao fim do período

| Tópico | Confiança (1-3) |
|--------|:---:|
| Subnetting / máscaras | 3 (reforçar notação `256-bloco` na escrita) |
| DHCP / DORA | 2-3 |
| DNS | 3 |
| NAT / PAT | 3 |
| MTU / Fragmentação | 2 (forte) — falta Etapa 2 + retestes pra fechar em 3 |

## Próxima etapa

- Fechar o **Lab 2.4** (Etapa 2 — fragmentação real, sem `-M do` + retestes), depois **Lab 2.5 (Roteamento Básico)**.
- Revisar antes: notação `256 − bloco` e a fórmula `2^(bits emprestados)`.
