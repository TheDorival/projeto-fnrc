# 01 — Instalação do Ubuntu Server e Criação de Usuários

## 1. Especificações do Ambiente

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

---

## 2. Criação do Usuário Administrador

Em cada VM, crie o usuário administrador `administrador` com senha `adminifal` e conceda privilégios de superusuário:

```bash
sudo adduser administrador
# Quando solicitado, defina a senha: adminifal

sudo usermod -aG sudo administrador
```

Verifique se o usuário foi criado corretamente:

```bash
groups administrador
# Saída esperada: administrador : administrador sudo
```

---

## 3. Criação dos Usuários dos Integrantes

Em cada uma das 8 VMs, crie os usuários de todos os integrantes do grupo conforme a lista oficial da disciplina:

```bash
sudo adduser daniel.lage --allow-bad-names
sudo adduser iago.henrique --allow-bad-names
sudo adduser gabriel.cruz --allow-bad-names
sudo adduser leonardo.moreira --allow-bad-names

sudo usermod -aG sudo daniel.lage
sudo usermod -aG sudo iago.henrique
sudo usermod -aG sudo gabriel.cruz
sudo usermod -aG sudo leonardo.moreira
```

### Tabela de Usuários

| Usuário            | Nome Completo                     | Perfil                                    |
| :----------------- | :-------------------------------- | :---------------------------------------- |
| `administrador`    | Administrador do Sistema          | Administrador — sudo (senha: `adminifal`) |
| `daniel.lage`      | Daniel Lage Cortez                | Integrante — sudo                         |
| `iago.henrique`    | Iago Henrique da Silva Lopes      | Integrante — sudo                         |
| `gabriel.cruz`     | Gabriel Cruz Nazareth             | Integrante — sudo                         |
| `leonardo.moreira` | Leonardo José Lucas Ferro Moreira | Integrante — sudo                         |

### Verificação

```bash
# Listar todos os usuários criados
cat /etc/passwd | grep -E 'administrador|daniel|iago|gabriel|leonardo'

# Verificar grupos de um usuário
groups administrador
```

Proxima etapa: [02-netplan-e-ping.md](02-netplan-e-ping.md)
