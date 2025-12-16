# Home Server
Este repositório documenta a implementação de um servidor caseiro feito com um computado reciclado. O qual é usado para rodar uma nuvem pessoal com NextCloud, um servidor de banco de dados MySql e PostgresSql para utilizar no desenvolvimento de minhas aplicações web

## Hardware
- i5 2a geração
- 12gb RAM DDR3
- HD wd green 500gb
  
## Stacks utilizadas 
- Ubuntu Server (LTS)
- Docker e Docker Compose

## Preparando ambiente

### Particionamento
Realizei um particionamento manual do HD na seguinte forma:
```
1GB para boot -> ponto de montagem /boot
50GB para o sistema -> ponto de montagem /
4GB para swap (opcional) -> ponto de montagem /swap
xGB para o usuário/armazenamento principal -> /home
````
### Configuração de rede
Descobrir o arquivo de configuração:

``
sudo ls etc/netplan/
``

Editando o arquivo:

``
sudo nano etc/netplan/<nome-arquivo>.yml
``

Arquivo de configuração de rede ethernet:

``
network:
  renderer: networkd
    ethernets:
      enp3s0: # nome da placa de rede
        dhcp4: false
        addresses:
        - 192.168.0.200/24 # exemplo de ip estático
        routes:
        - to: default
          via: 192.168.0.1 # exemplo de gatway
        nameservers:
          addresses: [8.8.8.8, 1.1.1.1] # servidores DNS
``

### Configurando acesso remoto
Instalando servidor ssh:

``
sudo apt update && sudo apt install openssh-server
``

Garantindo inicialização automática:

``
sudo systemctl enable ssh
``

Acessando SSH:

``
ssh usuário@endereço_ip
``
