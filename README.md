<div align="center">

# Projeto Final — Fundamentos de Redes de Computadores

**Instituto Federal de Alagoas — IFAL**
**Curso de Bacharelado em Sistemas de Informação — bsi-26-1 (2026.1)**
**Disciplina:** Fundamentos de Redes de Computadores &nbsp;·&nbsp; **Professor:** Alaelson Jatobá

</div>

---

## Seção 1 — Identificação

| Campo              | Informação                                 |
| :----------------- | :----------------------------------------- |
| Instituição        | Instituto Federal de Alagoas — IFAL        |
| Disciplina         | Fundamentos de Redes de Computadores       |
| Turma              | bsi-26-1 (2026.1)                          |
| Professor          | Alaelson Jatobá                            |
| Número do Grupo    | Grupo 2                                    |
| Repositório GitHub | https://github.com/TheDorival/projeto-fnrc |

### Integrantes do Grupo

| Nome Completo                     | Usuário no Sistema |
| :-------------------------------- | :----------------- |
| Daniel Lage Cortez                | `daniel.lage`      |
| Iago Henrique da Silva Lopes      | `iago.henrique`    |
| Gabriel Cruz Nazareth             | `gabriel.cruz`     |
| Leonardo José Lucas Ferro Moreira | `leonardo.moreira` |

---

## Seção 2 — Especificações de Hardware e Ambiente

O ambiente é composto por exatamente **8 máquinas virtuais** rodando **Ubuntu Server 22.04 LTS**, distribuídas em 4 computadores físicos (2 VMs por PC), interligadas por um switch de 8 portas em topologia estrela.

### Configuração de Hardware de Cada VM

| Recurso                      | Configuração                  |
| :--------------------------- | :---------------------------- |
| Sistema Operacional          | Ubuntu Server 22.04 LTS       |
| Memória RAM                  | 1024 MB (1 GB)                |
| Processadores / Cores        | 1 vCPU                        |
| Espaço em Disco              | 20 GB                         |
| Adaptador de rede (`enp0s3`) | Modo Bridge (rede do projeto) |
| Hypervisor                   | Oracle VirtualBox             |

### Distribuição das VMs por PC Físico

| PC Físico | VM 1                         | VM 2                         |
| :-------- | :--------------------------- | :--------------------------- |
| PC1       | `g2-pc1-vm1` — 192.168.26.17 | `g2-pc1-vm2` — 192.168.26.18 |
| PC2       | `g2-pc2-vm1` — 192.168.26.19 | `g2-pc2-vm2` — 192.168.26.20 |
| PC3       | `g2-pc3-vm1` — 192.168.26.21 | `g2-pc3-vm2` — 192.168.26.22 |
| PC4       | `g2-pc4-vm1` — 192.168.26.23 | `g2-pc4-vm2` — 192.168.26.24 |

> Detalhes completos em [01-instalacao-e-usuarios.md](01-instalacao-e-usuarios.md).

---

## Seção 3 — Redes, IPs e Domínios

### Endereçamento IP

A turma bsi-26-1 utiliza a rede `192.168.26.0/24`. O Grupo 2 recebeu a sub-rede abaixo com máscara `/28 (255.255.255.240)`:

| Parâmetro             | Valor                             |
| :-------------------- | :-------------------------------- |
| Sub-rede do Grupo 2   | `192.168.26.16/28`                |
| Máscara de sub-rede   | `255.255.255.240` (/28)           |
| Endereço de rede      | `192.168.26.16`                   |
| Hosts em uso (8 VMs)  | `192.168.26.17` a `192.168.26.24` |
| Endereço de broadcast | `192.168.26.31`                   |

### Domínio do Grupo

O domínio segue o formato `<grupoX>.bsi-26-1.maceio.lab`:

| Campo              | Valor                                   |
| :----------------- | :-------------------------------------- |
| Domínio do Grupo 2 | `grupo2.bsi-26-1.maceio.lab`            |
| Formato de FQDN    | `<hostname>.grupo2-bsi-26-1.maceio.lab` |
| Exemplo            | `g2-pc1-vm1.grupo2-bsi-26-1.maceio.lab` |

### Mapeamento IP / Nomes (FQDN)

O conteúdo abaixo foi adicionado ao `/etc/hosts` de **todas as 8 VMs**:

```
192.168.26.17  g2-pc1-vm1.grupo2-bsi-26-1.maceio.lab  g2-pc1-vm1
192.168.26.18  g2-pc1-vm2.grupo2-bsi-26-1.maceio.lab  g2-pc1-vm2
192.168.26.19  g2-pc2-vm1.grupo2-bsi-26-1.maceio.lab  g2-pc2-vm1
192.168.26.20  g2-pc2-vm2.grupo2-bsi-26-1.maceio.lab  g2-pc2-vm2
192.168.26.21  g2-pc3-vm1.grupo2-bsi-26-1.maceio.lab  g2-pc3-vm1
192.168.26.22  g2-pc3-vm2.grupo2-bsi-26-1.maceio.lab  g2-pc3-vm2
192.168.26.23  g2-pc4-vm1.grupo2-bsi-26-1.maceio.lab  g2-pc4-vm1
192.168.26.24  g2-pc4-vm2.grupo2-bsi-26-1.maceio.lab  g2-pc4-vm2
```

### Hostnames Configurados por VM

| VM        | Hostname (FQDN completo)                | IP              |
| :-------- | :-------------------------------------- | :-------------- |
| PC1 — VM1 | `g2-pc1-vm1.grupo2-bsi-26-1.maceio.lab` | `192.168.26.17` |
| PC1 — VM2 | `g2-pc1-vm2.grupo2-bsi-26-1.maceio.lab` | `192.168.26.18` |
| PC2 — VM1 | `g2-pc2-vm1.grupo2-bsi-26-1.maceio.lab` | `192.168.26.19` |
| PC2 — VM2 | `g2-pc2-vm2.grupo2-bsi-26-1.maceio.lab` | `192.168.26.20` |
| PC3 — VM1 | `g2-pc3-vm1.grupo2-bsi-26-1.maceio.lab` | `192.168.26.21` |
| PC3 — VM2 | `g2-pc3-vm2.grupo2-bsi-26-1.maceio.lab` | `192.168.26.22` |
| PC4 — VM1 | `g2-pc4-vm1.grupo2-bsi-26-1.maceio.lab` | `192.168.26.23` |
| PC4 — VM2 | `g2-pc4-vm2.grupo2-bsi-26-1.maceio.lab` | `192.168.26.24` |

> Configuração de rede em [02-netplan-e-ping.md](02-netplan-e-ping.md) · FQDN e hosts em [03-fqdn-e-ping.md](03-fqdn-e-ping.md).

---

## Seção 4 — Usuários e Acessos

Em cada uma das 8 VMs foram criados o usuário administrador (`administrador`) e os usuários individuais de todos os integrantes do grupo, conforme a lista oficial da disciplina.

### Usuários Criados em Cada VM

| Usuário            | Nome Completo                     | Perfil                                    |
| :----------------- | :-------------------------------- | :---------------------------------------- |
| `administrador`    | Administrador do Sistema          | Administrador — sudo (senha: `adminifal`) |
| `daniel.lage`      | Daniel Lage Cortez                | Integrante — sudo                         |
| `iago.henrique`    | Iago Henrique da Silva Lopes      | Integrante — sudo                         |
| `gabriel.cruz`     | Gabriel Cruz Nazareth             | Integrante — sudo                         |
| `leonardo.moreira` | Leonardo José Lucas Ferro Moreira | Integrante — sudo                         |

Os nomes de usuário seguem estritamente o padrão `<nome>.<sobrenome>` da lista oficial da disciplina.

> Comandos completos de criação em [01-instalacao-e-usuarios.md](01-instalacao-e-usuarios.md).

---

## Seção 5 — Testes e Evidências

### Testes de Ping por Endereço IP

| Origem     | Destino    | IP Destino    | Enviados | Recebidos | Perda |
| :--------- | :--------- | :------------ | :------: | :-------: | :---: |
| g2-pc1-vm1 | g2-pc1-vm2 | 192.168.26.18 |    4     |     4     |  0%   |
| g2-pc1-vm1 | g2-pc2-vm1 | 192.168.26.19 |    4     |     4     |  0%   |
| g2-pc1-vm1 | g2-pc2-vm2 | 192.168.26.20 |    4     |     4     |  0%   |
| g2-pc1-vm1 | g2-pc3-vm1 | 192.168.26.21 |    4     |     4     |  0%   |
| g2-pc1-vm1 | g2-pc3-vm2 | 192.168.26.22 |    4     |     4     |  0%   |
| g2-pc1-vm1 | g2-pc4-vm1 | 192.168.26.23 |    4     |     4     |  0%   |
| g2-pc1-vm1 | g2-pc4-vm2 | 192.168.26.24 |    4     |     4     |  0%   |

### Testes de Ping por FQDN

| Origem     | Destino (FQDN)                          | IP Resolvido  | Resultado |
| :--------- | :-------------------------------------- | :-----------: | :-------: |
| g2-pc1-vm1 | `g2-pc1-vm2.grupo2-bsi-26-1.maceio.lab` | 192.168.26.18 | 0% perda  |

### Testes de Acesso SSH

| Origem     | Destino    | Método                       | Usuário            | Resultado           |
| :--------- | :--------- | :--------------------------- | :----------------- | :------------------ |
| g2-pc1-vm1 | g2-pc1-vm2 | SSH por IP (`192.168.26.18`) | `daniel.lage`      | OK — login efetuado |
| g2-pc1-vm1 | g2-pc2-vm1 | SSH por FQDN                 | `iago.henrique`    | OK — login efetuado |
| g2-pc1-vm1 | g2-pc2-vm2 | SSH por alias curto          | `gabriel.cruz`     | OK — login efetuado |
| g2-pc1-vm1 | g2-pc3-vm1 | SSH por FQDN                 | `leonardo.moreira` | OK — login efetuado |
| g2-pc1-vm1 | g2-pc3-vm2 | SSH por IP                   | `daniel.lage`      | OK — login efetuado |
| g2-pc1-vm1 | g2-pc4-vm1 | SSH por IP                   | `iago.henrique`    | OK — login efetuado |
| g2-pc1-vm1 | g2-pc4-vm2 | SSH por IP                   | `gabriel.cruz`     | OK — login efetuado |

> Capturas de tela e evidências completas em [05-testes-validacao.md](05-testes-validacao.md).

---

## Documentação Técnica

|  #  | Arquivo                                                    | Conteúdo                                                          |
| :-: | :--------------------------------------------------------- | :---------------------------------------------------------------- |
|  1  | [01-instalacao-e-usuarios.md](01-instalacao-e-usuarios.md) | Instalação do Ubuntu Server e criação de usuários                 |
|  2  | [02-netplan-e-ping.md](02-netplan-e-ping.md)               | Configuração de rede via Netplan e testes de ping por IP          |
|  3  | [03-fqdn-e-ping.md](03-fqdn-e-ping.md)                     | Configuração de FQDN, hostname, `/etc/hosts` e ping por nome      |
|  4  | [04-ssh-e-testes.md](04-ssh-e-testes.md)                   | Configuração SSH e testes de acesso remoto                        |
|  5  | [05-testes-validacao.md](05-testes-validacao.md)           | Evidências completas com capturas de tela e tabelas de resultados |

---

<div align="center">

Projeto Final · Fundamentos de Redes de Computadores · Turma bsi-26-1 · 2026.1
**Grupo 2** · `grupo2.bsi-26-1.maceio.lab`

</div>
