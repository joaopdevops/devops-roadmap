<div align="right">
  <a href="README.md">🇺🇸 Read in English</a>
</div>

# Roadmap Redes & Segurança → DevSecOps — João Pedro Ribeiro

**Sargento do Exército Brasileiro → Infraestrutura de Redes & Segurança | DevSecOps (em construção) | Brasil**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jo%C3%A3o-pedro-ribeiro-37156a361)
[![GitHub](https://img.shields.io/badge/GitHub-joaopdevops-181717?style=flat-square&logo=github)](https://github.com/joaopdevops)

---

## Sobre

Passei 8 anos no Exército Brasileiro. Ingressei em 2018, participei da Intervenção Federal no Rio de Janeiro e me formei na Escola de Sargentos das Armas (ESA) em 2022. Hoje sou 3º Sargento de carreira e apoio a seção de informática da minha OM com a rede do batalhão e servidores Linux — switches, cabeamento, servidores e chamados de suporte.

Em paralelo, curso Redes de Computadores na Estácio (EAD). Fiz estágios técnicos em Linux e Redes no Centro de Telemática de Área (5º CTA, Exército Brasileiro) e estou atualmente matriculado nos cursos de Fundamentos de Redes, Cabeamento de Dados e Logística de TI no Centro de Telemática de Área (1º CTA). Em 2025 tirei minha primeira certificação (Oracle OCI Foundations).

Meu foco é **infraestrutura de redes**: como a rede é endereçada, comutada, roteada, protegida e mantida de pé. Switches, roteadores, cabeamento, plano de endereçamento, troubleshooting de conectividade — as camadas física e lógica em que todo o resto se apoia. Automação vem depois, e só em cima dessa base: não dá pra automatizar nem proteger uma infraestrutura que você não entende. Estou na Fase 01, percorrendo a trilha completa de redes da Cisco (CCNA 1–3 via EsCom).

Toda fase aqui termina do mesmo jeito: algo construído, documentado e explicado — porque em infraestrutura, conserto sem documentação é conserto que ninguém consegue repetir.

---

## Progresso do Roadmap

A rota vai **em profundidade por infraestrutura de redes e segurança** primeiro, depois operação de infraestrutura, e só então automação em cima.

| Fase | Tema | Foco | Status |
|:----:|------|------|:------:|
| 01 | Redes Fundamentos | CCNA 1 (ITN) — OSI/TCP-IP, endereçamento IPv4 e IPv6, sub-redes, switching, rota estática, ICMP | 🔄 Em andamento |
| 02 | Switching, Roteamento e Wireless | CCNA 2 (SRWE) — VLANs, trunk, roteamento inter-VLAN, STP, EtherChannel, WLANs, roteamento dinâmico | ⏳ Próxima |
| 03 | Redes Empresariais e Segurança | CCNA 3 (ENSA) — ACLs, NAT, WAN, VPN, segurança de redes, QoS, monitoramento, introdução a automação | ⏳ Planejado |
| 04 | Linux + Segurança de Redes | Administração de servidores, hardening, firewall, SSH, logs | ⏳ Planejado |
| 05 | Infraestrutura e Operações | Virtualização, monitoramento e alertas, backup e restore, investigação de incidentes | ⏳ Planejado |
| 06 | Cloud, Containers e IaC | AWS, Docker, Kubernetes, Terraform | ⏳ Planejado |
| 07 | CI/CD + DevSecOps | Pipelines, checagens de segurança automatizadas, deploy | ⏳ Planejado |

---

## Estrutura do Repositório

```
devops-roadmap/
├── check-ins/                            # Logs diários de estudo (bilíngue EN/PT)
├── fase-01-redes-fundamentos/            # CCNA 1 — ITN
│   ├── labs/               # Labs numerados: mecanismo + ponte com o mundo real
│   ├── conceitos/          # Notas atômicas (1 conceito por arquivo) com flashcards
│   ├── resumos/            # Resumos semanais da fase
│   └── projeto-integrador/ # Projeto prático ao final da fase
├── fase-02-redes-avancado/               # CCNA 2 — SRWE
├── fase-03-redes-empresariais-seguranca/ # CCNA 3 — ENSA
├── fase-04-linux-seguranca/              # Linux + segurança de redes
├── fase-05-infra-operacoes/              # Virtualização, monitoramento, backup
├── fase-06-cloud-containers-iac/         # AWS, Docker, Kubernetes, Terraform
└── fase-07-cicd-devsecops/               # Pipelines + DevSecOps
```

Cada fase segue a mesma organização:
- `labs/` — labs numerados (objetivo, mecanismo, exemplos, ponte com o mundo real)
- `conceitos/` — notas atômicas com flashcards (`Pergunta?::Resposta`)
- `resumos/` — anotações semanais exportadas do Obsidian
- `projeto-integrador/` — projeto prático ao final de cada fase

---

## Stack

### Uso Atualmente

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Bash-121011?style=flat-square&logo=gnu-bash&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

### Aprendendo (rota adiante)

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazon-aws&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white)

---

## Certificações

| Certificação | Status |
|---|:---:|
| Oracle Cloud Infrastructure Foundations Associate | ✅ Mai/2025 |
| Introdução à Cibersegurança — Cisco Networking Academy (via EsCom, Exército Brasileiro) | ✅ Mar/2026 |
| Redes de Computadores — Centro de Telemática de Área, 5º CTA (Exército Brasileiro) | ✅ Abr/2026 |
| Linux — Centro de Telemática de Área, 5º CTA (Exército Brasileiro) | ✅ Abr/2026 |
| Fundamentos de Redes (parceria Teltec) — Centro de Telemática de Área, 1º CTA (Exército Brasileiro) | 🎯 Em andamento 2026 |
| Cabeamento de Redes e Dados — Centro de Telemática de Área, 1º CTA (Exército Brasileiro) | 🎯 Em andamento 2026 |
| Logística de TI — Centro de Telemática de Área, 1º CTA (Exército Brasileiro) | 🎯 Em andamento 2026 |
| CCNA 1: Introduction to Networks — Cisco Networking Academy (via EsCom, Exército Brasileiro) | 🎯 Em andamento 2026 |
| CCNA 2: Switching, Routing & Wireless Essentials — Cisco Networking Academy (via EsCom) | ⏳ Próxima |
| CCNA 3: Enterprise Networking, Security & Automation — Cisco Networking Academy (via EsCom) | ⏳ Planejado |
| CCNA 200-301 — Cisco Certified Network Associate | ⏳ Depois da trilha da academia |
| CKA — Certified Kubernetes Administrator | ⏳ Mais adiante |
| AWS Solutions Architect Associate | ⏳ Mais adiante |

---

## Metas Atuais

- Construir profundidade real em **infraestrutura de redes** — endereçamento, switching, roteamento, conectividade, segurança
- Concluir a trilha completa da academia Cisco (**CCNA 1 → 2 → 3**) via Escola de Comunicações do Exército (EsCom)
- Transformar cada fase em algo prático: topologias, diagramas e configurações documentadas
- Ficar mais afiado em **troubleshooting de rede** — ler o sintoma antes de mexer na configuração
- Treinar **explicar trabalho técnico em inglês**, porque documentação e comunicação são metade do serviço
- Crescer rumo ao **DevSecOps** — automação e segurança construídas em cima dessa base, não no lugar dela

---

## Projetos Exploratórios Anteriores

Antes de iniciar este roadmap estruturado, explorei vários tópicos de DevOps por conta própria. Esses repositórios contêm experimentos iniciais — imperfeitos, mas reais.

| Repositório | Descrição |
|---|---|
| [learning-terraform](https://github.com/joaopdevops/learning-terraform) | Primeiros experimentos com Terraform e provisionamento de S3 na AWS |
| [CI-CD](https://github.com/joaopdevops/CI-CD) | Experimento inicial de pipeline CI/CD com Terraform, Docker e GitHub Actions |
| [github-actions-simples](https://github.com/joaopdevops/github-actions-simples) | Primeiro pipeline CI com GitHub Actions, Python e pytest |
| [first-image-docker](https://github.com/joaopdevops/first-image-docker) | Minha primeira imagem Docker — Nginx servindo uma página HTML estática |
| [github-access-audit](https://github.com/joaopdevops/github-access-audit) | Script Shell de auditoria de acessos no GitHub, criado durante os estudos de Bash |

---

## Contato

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jo%C3%A3o-pedro-ribeiro-37156a361)
[![GitHub](https://img.shields.io/badge/GitHub-joaopdevops-181717?style=flat-square&logo=github)](https://github.com/joaopdevops)
