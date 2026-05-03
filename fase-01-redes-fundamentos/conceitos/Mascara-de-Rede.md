---
tipo: conceito
area: Redes
camada-osi: 3
tags: [conceito, flashcards, redes]
---

# Máscara de Rede (Subnet Mask)

Define qual parte do endereço IP é a **rede** e qual é o **dispositivo** (host).

**Analogia:** o "prédio" do endereço. Dispositivos no mesmo prédio se comunicam direto. Se o prédio for diferente, precisa do [[Conceitos/Roteador]].

**Exemplo:**
- IP: `192.168.1.1`
- Máscara: `255.255.255.0` (equivalente a `/24`)
- Rede: `192.168.1` → o "prédio"
- Host: `.1` → o "apartamento"

**Dispositivos que se comunicam diretamente:** mesma rede (mesmo prédio)
**Dispositivos que precisam de roteador:** redes diferentes (prédios diferentes)

**Notação CIDR:**
- `/24` = 255.255.255.0 → 254 hosts
- `/16` = 255.255.0.0 → 65534 hosts
- `/8`  = 255.0.0.0 → 16 milhões de hosts

## 4 funções da máscara

**1. Rota local vs gateway**
Determina se o destino está no mesmo prédio (comunicação direta) ou em prédio diferente (precisa passar pelo [[Conceitos/Gateway|gateway]]). É a decisão fundamental de roteamento local.

**2. Endereço de rede**
Primeiro endereço do bloco — identifica o "prédio". Não pode ser atribuído a host.
Exemplo em `/24`: `192.168.1.0` → endereço da rede.

**3. Broadcast**
Último endereço do bloco — pacote enviado para todos os hosts da rede. Não pode ser atribuído a host.
Exemplo em `/24`: `192.168.1.255` → broadcast da rede.

**4. Tamanho da rede**
Define quantos hosts cabem no bloco. Fórmula: 2^(bits de host) − 2 (desconta rede e broadcast).

| Máscara | Hosts úteis |
|---|---|
| /24 | 254 |
| /25 | 126 |
| /26 | 62 |
| /30 | 2 (enlaces ponto a ponto) |

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.1-Redes-no-Mundo-Real]]
- Aprofundado em: [[Mes-01-Redes-Fundamentos/Indice]] (tópico 2.2 - Subnetting)

---

## Flashcards

Para que serve a mascara de rede?::Definir qual parte do IP e a rede (predio) e qual e o host (apartamento).
<!--SR:!2026-05-02,1,190-->
O que e /24 em notacao CIDR?::Mascara 255.255.255.0 — 254 hosts possiveis.
<!--SR:!2026-05-03,2,210-->
O que e /16?::Mascara 255.255.0.0 — 65534 hosts possiveis.
<!--SR:!2026-05-02,1,190-->
Quando dois dispositivos precisam de roteador para se comunicar?::Quando estao em redes diferentes (mascaras indicando "predios" diferentes).
<!--SR:!2026-05-04,4,270-->
No IP 192.168.1.1/24, qual e a rede e qual e o host?::Rede = 192.168.1 (predio); Host = .1 (apartamento).
<!--SR:!2026-05-03,3,250-->
Quais sao os 4 usos da mascara de rede?::1) Rota local vs gateway; 2) Endereco de rede; 3) Broadcast; 4) Tamanho da rede (quantos hosts cabem).
No bloco 192.168.1.0/24, qual e o endereco de rede e o broadcast?::Rede = 192.168.1.0; Broadcast = 192.168.1.255.
Quantos hosts uteis cabem em /25?::126 (2^7 = 128, menos 2 = 126).
Para que serve o /30?::Enlace ponto a ponto — suporta apenas 2 hosts uteis.
