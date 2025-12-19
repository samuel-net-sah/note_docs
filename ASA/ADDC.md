# Guia de introdução e configuração ao ADDC

## Etapa 1: Configurar Interface de Rede 
 
### Na Maquina Virtual: CLIENTE WINDOWS E CLIENTE UBUNTU 

- Vá em  **Configurações** > **Rede**
**Adaptador: 1**  > **Rede Interna**  

## Etapa 2: Adiciona IPS nas VM (CLIENTE WINDOWS E CLIENTE UBUNTU)

- CLIENTE WINDONS 
> IP 192.168.10.3/24
- CLIENTE UBUNTU 
> IP 192.168.10.4/24

## Etapa 3: Configurar VM UBUNTU-SERVER
### Configurações de interface de rede 
- Adaptador 1: Rede NAT 
- Adaptador 2: Rede Interna 

## Configuração Netplan 
````
cd /etc/netplan 
sudo nano arquivo.yml
````
## Editando arquivo.yml 
````
network: 
 version: 2 
   ethernet: 
    enp0s3
    dhcp4: true 
   ethernet:
    enp0s8
    adresses: [192.168.10.2/24]
    nameservers: 
     adresses: [8.8.8.8]
````
### Aplicar Configuração 
````
sudo netplan applay
````
## Etapa Final: 
Testar ping
- CLIENTE UBUNTU 
> ping 192.168.10.2
- CLINTE WINDOWS 
> ping 102.168.10.2

#### Finalizado








 





