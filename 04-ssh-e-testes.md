# 04 — Configuração SSH e Testes de Acesso

## 1. Verificação do Serviço SSH

O serviço SSH (`openssh-server`) já vem instalado e ativo no Ubuntu Server 22.04 LTS por padrão. Para confirmar:

```bash
sudo systemctl status ssh
```

Saída esperada:

```
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled)
     Active: active (running)
```

Caso não esteja instalado:

```bash
sudo apt update && sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
```

---

## 2. Parâmetros de Conexão

| Parâmetro | Valor |
|:---|:---|
| Porta SSH | `22` (padrão) |
| Autenticação | Senha |
| Usuários disponíveis | `adminifal`, `daniel.lage`, `iago.henrique`, `gabriel.cruz`, `leonardo.moreira` |

---

## 3. Conexão por Endereço IP

```bash
# Sintaxe geral
ssh <usuario>@<ip-da-vm>

# Exemplos com usuários dos integrantes
ssh daniel.lage@192.168.26.18
ssh iago.henrique@192.168.26.19
ssh gabriel.cruz@192.168.26.20
ssh leonardo.moreira@192.168.26.21
```

Saída esperada após login bem-sucedido:

```
daniel.lage@192.168.26.18's password:
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0 x86_64)

daniel.lage@g2-pc1-vm2:~$
```

---

## 4. Conexão por Hostname e FQDN

Após configurar o `/etc/hosts` (ver [03-fqdn-e-ping.md](03-fqdn-e-ping.md)), é possível usar o nome da máquina no lugar do IP:

```bash
# Por alias curto (hostname)
ssh iago.henrique@g2-pc2-vm1

# Por FQDN completo
ssh gabriel.cruz@g2-pc2-vm2.grupo2-bsi-26-1.maceio.lab
ssh leonardo.moreira@g2-pc3-vm1.grupo2-bsi-26-1.maceio.lab
```

> Evidências e tabela de resultados em [05-testes-validacao.md](05-testes-validacao.md).
