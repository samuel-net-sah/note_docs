# Guia de configuração ADDC no samba 

## Habilitar Adaptador 3 
- **Configurações** > **Rede** > **Placa de os hospedeiro exclusivo (host-only)** 

## Instalar o SSH (Na vm ubuntu server)
````
sudo apt update
sudo apt install -y openssh-server
````
# Configuração netplan 

````
network: 
 version: 2 
   ethernet: 
    enp0s3
    dhcp4: true 
   ethernet:
    enp0s8:
    adresses: [192.168.10.2/24]
     enp0s9:
      dhcp4: true 
    nameservers: 
     adresses: [8.8.8.8]
````
## Aplicando a configuração 
````
sudo netplan apply 
````
## Acessar via SSH vm ubuntu-server (PowerShell ou GitBash)
````
ssh usuario@192.168.0.1
````
Em caso de conflito de chaves execute:
````
ssh-keygen -R 192.168.0.1
````

## Altera nome da maquina 
````
sudo hostnamectl set-hostname dc 
````
## Alterando arquivo de hosts
````
sudo nano /etc/hosts 
````
## Editando arquivo /etc/hosts
````
127.0.0.1       localhost
127.0.0.1         samba
192.168.10.2   dc.samba.local dc
192.168.10.2     samba.local samba
````
## Verifica nome completo 
````
hostname -f
````
Verifica o endereço com o ping 
````
ping -c2 dc.samba.local
````
## Destivar  serviço system resolv
````
sudo systemctl disable --now systemd-resolved 
````
## Remover arquivo resolv.conf
````
sudo unlink /etc/resolv.conf
````
## Criando novo arquivo resolv.conf
````
sudo nano /etc/resolv.conf 
````
## Editando arquivo resolv.conf
````
nameserver 192.168.10.2
nameserver 8.8.8.8
search samba.local
````
## Torna o arquivo inalterado 
````
sudo chattr +i  /etc/resolv.conf 
````
# Instalação do samba 
````
sudo apt update && sudo apt install -y acl attr samba samba-dsdb-modules samba-vfs-modules smbclient winbind libpam-winbind libnss-winbind libpam-krb5 krb5-config krb5-user dnsutils chrony net-tools 
````
## Configuração de instalação 
- SAMBA.LOCAL > ok 
- dc.samba.local > ok
- dc.samba.local > ok

## Desabilitar 3 serviços do samba
````
sudo systemctl disable --now smbd nmbd winbind
````
## Remover o bloqueio do samba ADDC
````
sudo systemctl unmask samba-ad-dc
````
## Habilitar samba ADDC
````
sudo systemctl enable samba-ad-dc 
````
## Criar um copia de segurança do arquivo de configuração samba
````
sudo mv /etc/samba/smb.conf /etc/samba.bkp
````
## Roda o comando samba tools
````
sudo samba-tools domain provision
````
## Confirmação  
- ENTER 
- ENTER
- ENTER 
- 8.8.8.8
- PASSWORD
## Criar copia de segurança de rede 

```` 
sudo mv /etc/krb5.conf /etc/krb5.conf.bkp 
````
## Criar copia do arquivo krb5.conf 
````
sudo cp /var/lib/samba/private/krb5.conf /etc/krb5.conf
````
## Iniciar Serviços samba ADDC
````
sudo systemctl start samba-ad-dc
````
## Verifica status samba ADDC 
````
sudo systemctl status samba-ad-dc 
````
## Servidor samba funcionando 
 
#### Continua ...

 



 


