---
tipo: conceito
area: Redes
camada-osi: 3
tags: [conceito, flashcards, redes]
---

# Roteador

Opera na **Camada 3** do [[Conceitos/Modelo-OSI]].

Conecta **redes diferentes**. Recebe pacotes e decide qual caminho seguir baseado no endereço IP de destino.

**Analogia:** agência dos Correios. Liga um prédio ao outro — sabe o caminho entre bairros.

**Diferença do [[Conceitos/Switch]]:** o switch opera dentro de uma rede. O roteador opera entre redes.

Cada interface do roteador pertence a uma rede diferente e atua como [[Conceitos/Gateway]] para os dispositivos daquela rede.

## Labs onde foi ensinado
- [[Mes-01-Redes-Fundamentos/1.2-Componentes-de-Rede]]
- Será essencial em: Docker networking, AWS VPC, Kubernetes

---

## Flashcards

O que o roteador faz?::Conecta redes diferentes. Opera na Camada 3.
<!--SR:!2026-05-03,3,268-->
Qual a diferenca entre switch e roteador?::Switch opera DENTRO de uma rede (Camada 2). Roteador conecta redes DIFERENTES (Camada 3).
<!--SR:!2026-05-02,1,208-->
Cada interface de um roteador pertence a que?::Uma rede diferente. E atua como Gateway dos dispositivos daquela rede.
<!--SR:!2026-05-02,1,170-->
Analogia do roteador?::Agencia dos Correios — liga um predio ao outro.
<!--SR:!2026-05-02,2,248-->
