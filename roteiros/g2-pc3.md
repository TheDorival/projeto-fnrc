<div align="center">

# Roteiro PC1 - Projeto Final

**Instituto Federal de Alagoas — IFAL**
**Curso de Bacharelado em Sistemas de Informação — bsi-26-1 (2026.1)**
**Disciplina:** Fundamentos de Redes de Computadores &nbsp;·&nbsp; **Professor:** Alaelson Jatobá

</div>

## Seção 1 - Inicialização

Baixar appliance da VM base e importar, clonar no Oracle VirtualBox e executar ambas as VMs

Alterar arquivo de configuração de rede utilizando `sudo nano /etc/netplan/50-cloud-init.yaml` em ambas as VMS

[g2-pc3-vm1.yaml](/configs/netplan/g2-pc3-vm1.yaml)

[g2-pc3-vm2.yaml](/configs/netplan/g2-pc3-vm2.yaml)

Depois execute o comando

```bash
sudo netplan apply
```

Altere o nome de host com os seguintes comandos

```bash
sudo hostnamectl set-hostname g2-pc3-vm1.grupo2-bsi-26-1.maceio.lab
```

```bash
sudo hostnamectl set-hostname g2-pc3-vm2.grupo2-bsi-26-1.maceio.lab
```

## Seção 2 - Comandos

### Etapa 1

Execute na VM1

```bash
ping 192.168.26.24
# ping por ip para o PC4 VM2
```

### Etapa 2

Execute na VM2

```bash
ssh iago.henrique@192.168.26.17
# ssh por ip para o user3 no PC1 VM1
```

### Etapa 3

Execute na VM1

```bash
ping g2-pc2-vm2
# ping por fndq para o PC2 VM2
```

### Etapa 4

Execute na VM2

```bash
ping gabriel.cruz@g2-pc4-vm1
# ssh por fndq para o user4 no PC4 VM1
```
