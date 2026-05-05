---
tags: [resumo-curso, meta]
semana: 01
periodo: 2026-04-15 a 2026-05-03
---

# Resumo do Curso — Semana 01

> Primeiro resumo do curso. Cobre todo o conteúdo desde o Dia 01 até a revisão de domingo 03/05. Inclui o gap de 6 dias (22-28/04) por desânimo. A partir da Semana 02, o resumo vira incremental (segunda a domingo).

---

## Tópicos cobertos esta semana

- **1.1 Redes no Mundo Real** (15/04) — LAN, Switch, IP, máscara, ping, ICMP. Lab: 2 PCs + 1 switch no Packet Tracer, ping 0% loss.
- **1.2 Componentes de Rede** (16/04) — Roteador, Gateway, ARP, primeiro ping perde 1 pacote. Lab: 2 redes diferentes ligadas via roteador, configuração CLI inicial.
- **1.3 Modelos OSI e TCP/IP** (18/04, retomado 28/04) — 7 camadas OSI, 4 camadas TCP/IP, simulação Packet Tracer com PDU camada por camada. Confiança 2.
- **1.4 Meios Físicos e Cabos** (28/04) — UTP Cat5e/6, fibra, Wi-Fi 2.4 vs 5 GHz, limites de distância, atenuação, interferência, Auto-MDIX. Confiança 3 efetivo (reteste 72h sólido em 01/05).
- **2.1 Endereçamento IPv4** (01/05 parte 1 + 02/05 parte 2) — 32 bits, octeto, classes A/B/C/D/E, conversão binário ↔ decimal, RFC 1918, endereços especiais, subnetting matemático `2^n − 2`, /24 a /30, /30 ponto a ponto.

## Conceitos novos introduzidos

- Camada 2 (Enlace, MAC, switch) vs Camada 3 (Rede, IP, roteador) vs Camada 4 (Transporte, TCP/UDP) vs Camada 7 (Aplicação, navegador)
- ARP (resolução IP → MAC) e cache ARP
- Gateway como saída do "condomínio"
- udev nomeando interfaces Linux (`wlp0s20f3`)
- Atenuação (perda com distância) vs Interferência (sinal externo)
- Velocidade da luz em fibra (~200.000 km/s)
- Tabela mestra de pesos binários: 128 64 32 16 8 4 2 1
- Classes IPv4 + identificação por 1º octeto e bits iniciais
- RFC 1918 (10/8, 172.16-31/12, 192.168/16) — privado vs público
- NAT (mencionado como sementinha, fica pra 2.3)
- Endereços especiais: 0.0.0.0 (rota default), 127.0.0.1 (loopback), 169.254.x.x (APIPA), 255.255.255.255 (broadcast limitado), x.x.x.255 em /24 (broadcast da rede)
- Fórmula universal de hosts úteis: `2^(bits de host) − 2` (desconta rede + broadcast)
- /30 = enlace ponto a ponto (2 IPs úteis)
- Subnet sizing: "menor máscara que comporta o requisito"

## Analogias canônicas criadas ou reforçadas

(Família travada no syllabus — não inventar novas sem registrar.)

- **Switch** = carteiro do prédio (Camada 2, mesma rede)
- **Roteador** = agência dos Correios (Camada 3, entre redes)
- **IP** = número do apartamento
- **Máscara /24** = define qual é o "prédio"
- **Gateway** = portão de saída do condomínio
- **ARP** = porteiro perguntando o nome do morador
- **TTL** = prazo de validade do pacote
- **Interfaces Linux** = crachás com nome completo baseado na posição física
- **ARP no primeiro ping** = primeiro dia de trabalho (segundo dia já sabe onde fica a impressora)

## Erros conceituais que JP cometeu e foram corrigidos

| Erro | Correção |
|------|----------|
| Máscara "conecta PCs" (15/04) | Define qual parte do IP é rede, qual é host |
| ARP como parte do ping (15/04) | ARP é chamado ANTES; ping em si só usa ICMP |
| Camadas OSI invertidas (16/04) | C2 Enlace (MAC, switch), C3 Rede (IP, roteador), C4 Transporte (TCP/UDP) |
| Porteiro (ARP) confundido com portão (gateway) (28/04) | Porteiro PERGUNTA o MAC; portão é o LUGAR físico de saída |
| Navegador HTTPS = Camada 4 (28/04) | É Camada 7; navegador USA TCP, nao E TCP |
| Atenuação confundida com interferência (29/04) | Atenuação = perda com distância no próprio meio; interferência = sinal externo |
| Velocidade da luz "200.000 km/h" (28/04) | km/s — corrigido e consolidado em 29/04 |
| 172.20.5.10 sem flag privado (01/05) | Faixa privada 172.16-31/12 — fragilidade ainda ativa em 03/05 |
| Fórmula `2^n` sem o `−2` (02/05) | Desconta endereço de rede + broadcast |
| Justificar /24 "porque é Classe C" (02/05) | Mecanismo é `2^n − 2` independente de classe |

## Nível de domínio dos tópicos da semana

| Tópico | Confiança (1-3) | Precisa reforço? |
|--------|-----------------|------------------|
| 1.1 Redes no Mundo Real | 3 | Não |
| 1.2 Componentes de Rede | 3 | Analogia porteiro/portão monitorada (reapareceu 28/04) |
| 1.3 OSI e TCP/IP | 2 | Sim — papel da camada (Aplicação vs Transporte), conceito de "escopo" |
| 1.4 Meios Físicos | 3 efetivo | Não — atenuação consolidada em reteste 72h (01/05) |
| 2.1 Endereçamento IPv4 | 3 (1ª declaração) | **SIM** — falhou reteste 24h em RFC 1918 (Classe B faixa privada). Não avança pro 2.2 antes de quitar |

## Decisões pedagógicas novas

- **Reteste 24h + 72h obrigatório** (24h consolida, 72h surpresa testa contra padrão de "aceita correção rápido demais").
- **Critério de avanço entre labs:** confiança 3 em 2 check-ins consecutivos + reteste 24h passar + reteste 72h passar. Falha em qualquer = não avança.
- **Camadas paralelas:** Packet Tracer + Linux real (`ip addr show`, `ping -c 4`) ao final de cada lab.
- **Comando nunca é colado sem explicação linha a linha.**
- **Cada lab termina com "Por que isso importa pra DevOps"** ancorado em Docker/K8s/AWS.
- **Migração de ambiente (02/05):** terminal integrado do VS Code. Sem mudança técnica.
- **Estratégia GitHub revisada (02/05):** conteúdo técnico (lab + conceitos) vai DIRETO do vault pro repo `devops-roadmap`, sem destilação. Check-ins ficam fora até criar `Template-Checkin-Publico.md`. Regra "ler memória antes de propor ação em sistema externo" virou feedback registrado.
- **Padrão observado em JP — "cobro conceito que passei rápido":** pendente discutir hoje (item 7 da pauta). Único exemplo concreto: faixa 172.16-31 em tabela densa sem destaque antes do mini-teste.

## Próxima semana — o que vem

- **Tópico principal:** fechar fragilidade RFC 1918 + Lab 2.2 Subnetting prático (cenários multi-rede).
- **Pré-requisito a revisar antes:** segunda 04/05 — 3 perguntas RFC 1918 (Classe A, B, C) ANTES de qualquer outra coisa. Se passar, retoma reteste 72h do 2.1 normalmente.
- **Meta de lab:** 2.2 Subnetting prático na semana. Se o ritmo aguentar, abrir 2.3 (DHCP/DNS/NAT) na sexta.

## Observações do instrutor

Ritmo real: 5 labs em 19 dias civis (não 5 dias). Distribuição: 3 labs nos primeiros 4 dias úteis (15-21/04), gap de 6 dias por desânimo puro, retomada em 28/04 com 2 labs nos 6 dias seguintes. Sustentável **se** o gap não virar padrão — ponto a discutir hoje na pauta de "lab mínimo viável".

Padrões cognitivos firmes:
- Aceita correção rápido demais → mitigado por reteste 72h surpresa.
- Responde escrita enxuta vs oral detalhada → cobrar elaboração escrita.
- Pede pra avançar rápido → resistir, ritmo é 1 lab/dia.

Vitória da semana: **atenuação consolidada em 4 dias** (introduzida 28/04 confusa, sólida em 01/05 no Pi-hole na garagem). Mostra que o reteste 72h funciona quando JP processa o feedback do reteste 24h.

Risco da semana: 5 N seguidos no tracker S1 (28-29-30-01-02). Plano de sono Fase 1 não fechou. Item 4 e 5 da pauta de hoje.

Risco pedagógico: **fragilidade RFC 1918 não cedeu de 01/05 pra 03/05**. JP foi de "esqueci de mencionar" pra "não lembro" — piorou em 48h. Não é só leitura de enunciado, é buraco conceitual. Memorização das 3 faixas é pré-requisito não-negociável pro Lab 2.2.

---

## Checklist de atualização

- [x] Este arquivo salvo em `Resumos-do-Curso/Semana-01.md`
- [x] Syllabus vivo (`project_curso_syllabus.md`) atualizado com o que mudou
- [x] MEMORY.md ainda reflete o estado correto (sem mudança de índice)
