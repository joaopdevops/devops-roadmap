---
tipo: conceito
area: Redes
camada-osi: 3
tags: [conceito, flashcards, redes, subnetting]
---

# Subnetting

Ato de dividir uma rede maior em sub-redes menores, **estendendo a máscara** pra recortar o bloco original em pedaços com identidade própria.

## Distinção fundamental

- **Rede** vs **sub-rede** = mesma natureza estrutural. Uma sub-rede é uma rede; "sub" é só posição na hierarquia (recortada de outra).
- **Máscara da sub-rede ≠ máscara da rede mãe.** Sempre **maior** (mais bits de rede). Nunca igual, nunca menor — igual seria a própria rede mãe; menor seria uma rede maior englobando.

## Analogia — andares do prédio

- **Prédio** = rede mãe (ex: `192.168.1.0/24`).
- **Andar** = sub-rede (ex: `192.168.1.0/29`).
- Subnetting = pegar o prédio e dividir em andares numerados, cada um com sua própria faixa de apartamentos.

## Mecânica — estender a máscara

Subnetting é literalmente **roubar bits da parte de host pra virarem bits de rede**. Cada bit roubado:

- **Dobra** o número de sub-redes
- **Divide pela metade** o número de IPs por sub-rede

| Bits roubados (de `/24`) | Conta | Sub-redes | IPs por sub-rede | Hosts úteis |
|---|---|---|---|---|
| 1 | 2¹ | 2 (`/25`) | 128 | 126 |
| 2 | 2² | 4 (`/26`) | 64 | 62 |
| 3 | 2³ | 8 (`/27`) | 32 | 30 |
| 4 | 2⁴ | 16 (`/28`) | 16 | 14 |
| 5 | 2⁵ | 32 (`/29`) | 8 | 6 |
| 6 | 2⁶ | 64 (`/30`) | 4 | 2 |

## Duas fórmulas, dois expoentes

| O que calcular | Fórmula | Expoente é... |
|---|---|---|
| Quantas sub-redes criei | `2^(bits roubados)` | `N_novo − N_mãe` |
| Quantos hosts úteis por sub-rede | `2^(bits de host) − 2` | `32 − N_novo` |

**Trava mental:** ao ler "X bits", nunca usar X direto como resposta. Perguntar `2^X` ou `2^X − 2`? Escrever a conta antes do número final. O `-2` mora **só** na fórmula de hosts (descontando endereço de rede + broadcast); sub-redes não levam `-2`.

## Exemplo — `/24` dividido em 4 sub-redes `/29`

**Cenário:** rede `192.168.1.0/24`, dividir em 4 grupos com 2 PCs + 1 gateway cada (3 hosts mínimos por grupo).

**Por que `/29`?**

| Máscara | Hosts úteis | Cabe 3? |
|---|---|---|
| `/30` | 2 | ❌ |
| `/29` | 6 | ✅ (sobra 3) |
| `/28` | 14 | ✅ (sobra 11, desperdiça) |

Princípio do construtor de prédios: **menor máscara que comporta o requisito** sem desperdiçar bloco.

**Cálculo das 4 sub-redes** — cada bloco `/29` ocupa 8 IPs, andares começam em múltiplos de 8:

| Sub-rede | CIDR | Rede | Broadcast | Faixa útil | Gateway |
|---|---|---|---|---|---|
| 1 | `192.168.1.0/29` | `.0` | `.7` | `.1`–`.6` | `.1` |
| 2 | `192.168.1.8/29` | `.8` | `.15` | `.9`–`.14` | `.9` |
| 3 | `192.168.1.16/29` | `.16` | `.23` | `.17`–`.22` | `.17` |
| 4 | `192.168.1.24/29` | `.24` | `.31` | `.25`–`.30` | `.25` |

Sobram 28 sub-redes `/29` vagas dentro do `/24` (32 possíveis − 4 usadas). Espaço pra crescer.

## Máscara em decimal — derivação

`/29` em binário: `11111111.11111111.11111111.11111000`. Último octeto:

```
1·128 + 1·64 + 1·32 + 1·16 + 1·8 + 0·4 + 0·2 + 0·1 = 248
```

Logo `/29` em decimal = `255.255.255.248`.

## Por que importa pra DevOps

- **AWS VPC:** subnets dentro de uma VPC são subnetting clássico. CIDR `/16` da VPC dividida em `/24` pra app, `/28` pra RDS isolado, `/30` pra VPC peering. Errar o tamanho = ou desperdiça IPs ou estrangula crescimento.
- **Kubernetes:** `PodCIDR` e `ServiceCIDR` são sub-redes do cluster network. Cada nó recebe um bloco; pod scheduling depende de IP livre na sub-rede do nó.
- **Terraform:** `cidrsubnet("10.0.0.0/16", 4, 2)` — `4` é bits roubados, `2` é índice da sub-rede. Entender a fórmula evita criar VPC com sub-redes sobrepostas ou subdimensionadas.
- **Security groups + subnet isolation:** prod e staging em sub-redes distintas (`/26` cada) é prática SRE padrão — segregação por camada de rede, não só por SG.

## Conceito relacionado

- `Mascara-de-Rede.md` — a régua que define onde rede termina e host começa
- `RFC-1918.md` — faixas privadas onde o subnetting é geralmente aplicado

---

## Flashcards

Qual a diferenca estrutural entre rede e sub-rede?::Nenhuma — sao a mesma coisa. "Sub" e so posicao na hierarquia (sub-rede e uma rede recortada de outra).
A mascara da sub-rede pode ser igual a da rede mae?::Nao. Tem que ser maior (mais bits de rede). Igual seria a propria rede mae.
O que e "estender a mascara"?::Roubar bits da parte de host pra virarem bits de rede, criando mais sub-redes menores.
Cada bit roubado do host faz o que com sub-redes e hosts?::Dobra o numero de sub-redes; divide pela metade os IPs por sub-rede.
Como calcular quantas sub-redes foram criadas?::2^(bits roubados). Sem -2.
Como calcular quantos hosts uteis por sub-rede?::2^(bits de host) - 2. O -2 desconta endereco de rede e broadcast.
Por que o -2 mora so na formula de hosts?::Cada sub-rede precisa reservar 1 IP pra endereco de rede e 1 pra broadcast. Sub-redes em si nao tem reserva.
Em /24 dividido em /29, quantas sub-redes existem e com quantos IPs cada?::32 sub-redes (2^5), 8 IPs por sub-rede (2^3), 6 hosts uteis cada.
Qual o principio para escolher tamanho de sub-rede?::Menor mascara que comporta o requisito sem desperdicar IPs do bloco.
/29 em decimal e quanto?::255.255.255.248 (ultimo octeto: 11111000 = 128+64+32+16+8 = 248).
Os andares /29 dentro de /24 comecam em quais multiplos?::Multiplos de 8 — 0, 8, 16, 24, 32, ate 248.
Por que /30 nao serve para 2 PCs + 1 gateway?::/30 da apenas 2 hosts uteis (2^2 - 2). Faltaria 1 endereco para o terceiro host.
