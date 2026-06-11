# 03 — Configuração de FQDN e Testes de Ping por Nome

## 1. O que é FQDN

**FQDN** (Fully Qualified Domain Name) é o nome completo e único de um host dentro de uma hierarquia de domínios. No contexto deste projeto, o FQDN identifica cada VM de forma inequívoca na rede local do laboratório.

Formato adotado pela turma:

```
<hostname>.<grupo>-<turma>.maceio.lab
```

Exemplo:

```
g2-pc1-vm1.grupo2-bsi-26-1.maceio.lab
```

---

## 2. Domínio do Grupo 2

| Campo                 | Valor                        |
| :-------------------- | :--------------------------- |
| Grupo                 | `grupo2`                     |
| Turma                 | `bsi-26-1`                   |
| TLD local             | `maceio.lab`                 |
| Domínio (zona)        | `grupo2.bsi-26-1.maceio.lab` |
| Domínio usado no FQDN | `grupo2-bsi-26-1.maceio.lab` |

### Tabela de FQDNs

| Hostname     | FQDN Completo                           | IP              |
| :----------- | :-------------------------------------- | :-------------- |
| `g2-pc1-vm1` | `g2-pc1-vm1.grupo2-bsi-26-1.maceio.lab` | `192.168.26.17` |
| `g2-pc1-vm2` | `g2-pc1-vm2.grupo2-bsi-26-1.maceio.lab` | `192.168.26.18` |
| `g2-pc2-vm1` | `g2-pc2-vm1.grupo2-bsi-26-1.maceio.lab` | `192.168.26.19` |
| `g2-pc2-vm2` | `g2-pc2-vm2.grupo2-bsi-26-1.maceio.lab` | `192.168.26.20` |
| `g2-pc3-vm1` | `g2-pc3-vm1.grupo2-bsi-26-1.maceio.lab` | `192.168.26.21` |
| `g2-pc3-vm2` | `g2-pc3-vm2.grupo2-bsi-26-1.maceio.lab` | `192.168.26.22` |
| `g2-pc4-vm1` | `g2-pc4-vm1.grupo2-bsi-26-1.maceio.lab` | `192.168.26.23` |
| `g2-pc4-vm2` | `g2-pc4-vm2.grupo2-bsi-26-1.maceio.lab` | `192.168.26.24` |

---

## 3. Configurando o Hostname de Cada VM

O hostname de cada VM deve ser definido com o FQDN completo usando o `hostnamectl`:

```bash
# Exemplo para g2-pc1-vm1 — substitua pelo hostname de cada VM
sudo hostnamectl set-hostname g2-pc1-vm1.grupo2-bsi-26-1.maceio.lab
```

Verificar após a configuração:

```bash
hostnamectl
```

Saída esperada:

```
 Static hostname: g2-pc1-vm1.grupo2-bsi-26-1.maceio.lab
       Icon name: computer-vm
         Chassis: vm
  Virtualization: oracle
Operating System: Ubuntu 22.04.4 LTS
          Kernel: Linux 5.15.0-...
    Architecture: x86-64
```

> **Atenção:** após usar `hostnamectl`, verifique se o arquivo `/etc/hosts` não recebeu uma linha `127.0.1.1 <fqdn>` automática. Se sim, substitua o FQDN nessa linha pelo hostname curto (ex: `127.0.1.1 g2-pc1-vm1`), mantendo o FQDN apenas na entrada com o IP real.

---

## 4. Mapeamento IP/Nomes — Arquivo `/etc/hosts`

O arquivo `/etc/hosts` funciona como um DNS local. O mapeamento deve ser adicionado em **todas as 8 VMs**:

```bash
sudo nano /etc/hosts
```

Conteúdo a adicionar em cada máquina (abaixo das entradas padrão de `localhost`):

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

---

## 5. Testes de Ping por FQDN e Alias

Após configurar o `/etc/hosts`, teste a resolução de nomes:

```bash
# Por FQDN completo
ping -c 4 g2-pc1-vm2.grupo2-bsi-26-1.maceio.lab
ping -c 4 g2-pc2-vm1.grupo2-bsi-26-1.maceio.lab
ping -c 4 g2-pc2-vm2.grupo2-bsi-26-1.maceio.lab

# Por alias curto (hostname)
ping -c 4 g2-pc3-vm1
ping -c 4 g2-pc3-vm2
ping -c 4 g2-pc4-vm1
ping -c 4 g2-pc4-vm2
```

Saída esperada (resolução de nome funcionando):

```
PING g2-pc1-vm2.grupo2-bsi-26-1.maceio.lab (192.168.26.18) 56(84) bytes of data.
64 bytes from g2-pc1-vm2.grupo2-bsi-26-1.maceio.lab (192.168.26.18): icmp_seq=1 ttl=64
...
4 packets transmitted, 4 received, 0% packet loss
```

> Se o ping por nome falhar mas por IP funcionar, verifique se o `/etc/hosts` foi salvo corretamente em todas as VMs e se não há entradas duplicadas para o mesmo FQDN.

> Evidências em [05-testes-validacao.md](05-testes-validacao.md).

Proxima etapa: [04-ssh-e-testes.md](04-ssh-e-testes.md)
