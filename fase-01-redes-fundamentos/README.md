# Fase 01 — Redes Fundamentos (CCNA)

Primeira fase do roadmap. Foco: dominar os fundamentos de redes que sustentam tudo no DevOps/Cloud.

## Status

🔄 **Em andamento** — Mai/2026

| Lab | Tema | Status |
|---|---|:---:|
| 1.1 | Redes no Mundo Real (LAN, switch, IP, ping, ICMP) | ✅ |
| 1.2 | Componentes de Rede (roteador, gateway, ARP) | ✅ |
| 1.3 | Modelos OSI e TCP/IP | ✅ |
| 1.4 | Meios Físicos e Cabos | ✅ |
| 2.1 | Endereçamento IPv4 e Subnetting | ✅ |
| 2.2 | Subnetting avançado (cálculo de range) | ⏳ |
| 2.3 | Serviços de Rede (DHCP, DNS, NAT) | ⏳ |
| 2.4 | ICMP e Fragmentação | ⏳ |
| 2.5 | Roteamento Básico | ⏳ |

## Estrutura

- `labs/` — labs numerados com objetivo, mecanismo, exemplos e ponte para DevOps
- `conceitos/` — notas atômicas (1 conceito por arquivo) com flashcards no formato `Pergunta?::Resposta`
- `resumos/` — resumo semanal da fase
- `projeto-integrador/` — projeto final aplicando o que foi aprendido

## Conceitos cobertos até agora

13 notas atômicas: ARP, Gateway, ICMP, LAN, Máscara de Rede, Modelo OSI, Roteador, Switch, Atenuação, Interferência, UTP, Fibra Óptica, Wi-Fi.

## Método

- 1 lab por dia útil
- Cada conceito novo vira nota atômica em `conceitos/`
- Cada lab termina com **ponte para DevOps** (datacenter, cloud, K8s, AWS)
- Critério de avanço: confiança 3 + reteste 24h + reteste 72h surpresa

## Ferramentas

- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) para simulação
- Linux real (Ubuntu) para amarrar conceitos no terminal (`ip addr`, `ping`, `traceroute`)
