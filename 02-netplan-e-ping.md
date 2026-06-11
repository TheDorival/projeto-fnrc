# 02 — Configuração de Rede (Netplan) e Testes de Ping

## 1. Sub-rede do Grupo 2

A turma bsi-26-1 utiliza a rede `192.168.26.0/24`. O Grupo 2 recebeu a sub-rede abaixo com máscara `/28 (255.255.255.240)`:

| Parâmetro | Valor |
|:---|:---|
| Sub-rede do Grupo 2 | `192.168.26.16/28` |
| Máscara de sub-rede | `255.255.255.240` (/28) |
| Endereço de rede | `192.168.26.16` |
| Primeiro host utilizável | `192.168.26.17` |
| Último host utilizável | `192.168.26.30` |
| Endereço de broadcast | `192.168.26.31` |
| Hosts em uso (8 VMs) | `192.168.26.17` a `192.168.26.24` |

### Tabela de Endereços IP das VMs

| VM | Hostname | Interface | Endereço IP | Máscara |
|:---|:---|:---|:---|:---|
| PC1 — VM1 | `g2-pc1-vm1` | `enp0s3` | `192.168.26.17` | `255.255.255.240` |
| PC1 — VM2 | `g2-pc1-vm2` | `enp0s3` | `192.168.26.18` | `255.255.255.240` |
| PC2 — VM1 | `g2-pc2-vm1` | `enp0s3` | `192.168.26.19` | `255.255.255.240` |
| PC2 — VM2 | `g2-pc2-vm2` | `enp0s3` | `192.168.26.20` | `255.255.255.240` |
| PC3 — VM1 | `g2-pc3-vm1` | `enp0s3` | `192.168.26.21` | `255.255.255.240` |
| PC3 — VM2 | `g2-pc3-vm2` | `enp0s3` | `192.168.26.22` | `255.255.255.240` |
| PC4 — VM1 | `g2-pc4-vm1` | `enp0s3` | `192.168.26.23` | `255.255.255.240` |
| PC4 — VM2 | `g2-pc4-vm2` | `enp0s3` | `192.168.26.24` | `255.255.255.240` |

---

## 2. Configuração de IP Estático — Netplan

O IP estático foi configurado editando o arquivo `/etc/netplan/50-cloud-init.yaml` em cada VM. O campo `addresses` é o único que muda entre as máquinas:

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        - 192.168.26.17/28   # alterar para o IP de cada VM (.17 a .24)
```

Após editar, aplicar as configurações:

```bash
sudo netplan apply
```

Verificar se o IP foi aplicado corretamente:

```bash
ip addr show enp0s3
```

---

## 3. Testes de Ping por Endereço IP

Com o IP estático configurado, teste a conectividade entre as VMs:

```bash
# Sintaxe
ping -c 4 <ip-destino>

# Exemplos — a partir da VM g2-pc1-vm1 (192.168.26.17)
ping -c 4 192.168.26.18   # → g2-pc1-vm2
ping -c 4 192.168.26.19   # → g2-pc2-vm1
ping -c 4 192.168.26.20   # → g2-pc2-vm2
ping -c 4 192.168.26.21   # → g2-pc3-vm1
ping -c 4 192.168.26.22   # → g2-pc3-vm2
ping -c 4 192.168.26.23   # → g2-pc4-vm1
ping -c 4 192.168.26.24   # → g2-pc4-vm2
```

Saída esperada:

```
PING 192.168.26.18 (192.168.26.18) 56(84) bytes of data.
64 bytes from 192.168.26.18: icmp_seq=1 ttl=64 time=X.XXX ms
64 bytes from 192.168.26.18: icmp_seq=2 ttl=64 time=X.XXX ms
64 bytes from 192.168.26.18: icmp_seq=3 ttl=64 time=X.XXX ms
64 bytes from 192.168.26.18: icmp_seq=4 ttl=64 time=X.XXX ms

--- 192.168.26.18 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss
```

> Evidências e tabela de RTT em [05-testes-validacao.md](05-testes-validacao.md).
