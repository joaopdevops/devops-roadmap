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

## Flashcards

O que e DNS?::Sistema que traduz nome de dominio (google.com) em IP (142.250.78.78).
Por que DNS existe?::Para humanos pensarem em nomes e maquinas usarem numeros — sem DNS a internet seria lista de IPs decorados.
Em qual camada OSI o DNS atua?::Camada 7 (Aplicacao) — roda principalmente sobre UDP na porta 53.
O que e um servidor DNS recursivo?::Servidor que faz a viagem inteira pela hierarquia (raiz, TLD, autoritativo) e devolve o IP final pro cliente.
O que e cache DNS?::Memoria temporaria de respostas recentes, para nao refazer a hierarquia toda vez. Tem TTL — depois do prazo, re-pergunta.
Qual a diferenca entre TTL do pacote IP e TTL do DNS?::TTL do IP conta saltos por roteador (mata pacote em loop). TTL do DNS conta segundos em cache (define quando re-perguntar pelo registro).
Quem define o TTL de um registro DNS?::O dono do dominio, ao configurar o registro no servidor autoritativo.
O que e um registro tipo A?::Mapeamento direto de nome para endereco IPv4. Ex: google.com -> 142.250.78.78.
O que e um registro CNAME?::Apelido — aponta um nome para outro nome. Ex: www.exemplo.com -> exemplo.com.
O que e o servidor 8.8.8.8?::DNS publico do Google — um dos mais usados como recursivo.
Onde fica configurado o servidor DNS no Linux?::No arquivo /etc/resolv.conf — geralmente entregue automaticamente pelo DHCP.
Por que o ditado "It's always DNS" existe no DevOps?::Porque grande parte dos incidentes de "site fora do ar" sao causados por problema de DNS, nao pela aplicacao em si.
Na sua casa, quem e o servidor DNS de verdade?::O DNS do provedor (ou um publico como 8.8.8.8). O roteador domestico nao e a agenda — so repassa a pergunta (forwarder/relay).
Onde existe um servidor DNS dedicado na pratica?::Redes corporativas (Windows Server/AD com nomes internos .local), cloud (AWS Route 53) e Kubernetes (CoreDNS). Casa nao tem — usa o do provedor.
Que comando testa a resolucao de um nome no terminal?::nslookup seguido do nome (ex: nslookup www.lab.local) — pergunta direto ao servidor DNS e mostra o IP retornado.
Ao configurar um servidor DNS, o que e adicionar um registro A?::Cadastrar um contato na agenda: ligar um nome (www.lab.local) a um IPv4 (192.168.10.10).
