<div align="center">

# Roteiro da Apresentação - Projeto Final

**Instituto Federal de Alagoas — IFAL**
**Curso de Bacharelado em Sistemas de Informação — bsi-26-1 (2026.1)**
**Disciplina:** Fundamentos de Redes de Computadores &nbsp;·&nbsp; **Professor:** Alaelson Jatobá

</div>

## Seção 1 - Inicialização

### Roteiro especifico para cada membro da equipe

Daniel Lage: [g2-pc1.md](roteiros/g2-pc1.md)

Iago Henrique: [g2-pc2.md](roteiros/g2-pc2.md)

Gabriel Cruz: [g2-pc3.md](roteiros/g2-pc3.md)

Leonardo Moreira: [g2-pc4.md](roteiros/g2-pc4.md)

Baixar appliance da VM base e importar, clonar no Oracle VirtualBox e executar ambas as VMs

Alterar arquivo de configuração de rede utilizando `sudo nano /etc/netplan/50-cloud-init.yaml` de acordo com a tabela a seguir

|     | VM1                                                | VM2                                                |
| :-- | :------------------------------------------------- | :------------------------------------------------- |
| PC1 | [g2-pc1-vm1.yaml](configs/netplan/g2-pc1-vm1.yaml) | [g2-pc1-vm2.yaml](configs/netplan/g2-pc1-vm2.yaml) |
| PC2 | [g2-pc2-vm1.yaml](configs/netplan/g2-pc2-vm1.yaml) | [g2-pc2-vm2.yaml](configs/netplan/g2-pc2-vm2.yaml) |
| PC3 | [g2-pc3-vm1.yaml](configs/netplan/g2-pc3-vm1.yaml) | [g2-pc3-vm2.yaml](configs/netplan/g2-pc3-vm2.yaml) |
| PC4 | [g2-pc4-vm1.yaml](configs/netplan/g2-pc4-vm1.yaml) | [g2-pc4-vm2.yaml](configs/netplan/g2-pc4-vm2.yaml) |

Depois execute o comando

```bash
sudo netplan apply
```

Altere o nome de host com o seguinte comando

```bash
sudo hostnamectl set-hostname g2-pc<numero_do_pc>-vm<numero_da_vm>.grupo2-bsi-26-1.maceio.lab
```

Substituir @ pelos valores apropriados de acordo com o PC e VM

## Seção 2 - Comandos

```bash
ping 192.168.26.<restante_do_ip>
```

```bash
ssh <usuario>@192.168.26.<restante_do_ip>
```

```bash
ping g2-pc<numero_do_pc>-vm<numero_da_vm>
```

```bash
ssh <usuario>@g2-pc<numero_do_pc>-vm<numero_da_vm>
```

## Seção 3 - Planejamento

Alvos para atingir

Comandos

- ping por ip
- ssh por ip
- ping por fndq
- ssh por fndq

Usuarios

- daniel.lage
- iago.henrique
- gabriel.cruz
- leonardo.moreira

Hospedeiros

- PC1 -> VM1, VM2
- PC2 -> VM1, VM2
- PC3 -> VM1, VM2
- PC4 -> VM1, VM2

### Execução

PC1 (Daniel Lage)

1. VM1: ping por ip para o PC2 VM2
2. VM2: ssh por ip para o user1 no PC3 VM1
3. VM1: ping por fndq para o PC4 VM2
4. VM2: ssh por fndq para o user2 no PC2 VM1

PC2 (Iago Henrique)

1. VM1: ping por ip para o PC3 VM2
2. VM2: ssh por ip para o user2 no PC4 VM1
3. VM1: ping por fndq para o PC1 VM2
4. VM2: ssh por fndq para o user3 no PC3 VM1

PC3 (Gabriel Cruz)

1. VM1: ping por ip para o PC4 VM2
2. VM2: ssh por ip para o user3 no PC1 VM1
3. VM1: ping por fndq para o PC2 VM2
4. VM2: ssh por fndq para o user4 no PC4 VM1

PC4 (Leonardo Moreira)

1. VM1: ping por ip para o PC1 VM2
2. VM2: ssh por ip para o user4 no PC2 VM1
3. VM1: ping por fndq para o PC3 VM2
4. VM2: ssh por fndq para o user1 no PC1 VM1
