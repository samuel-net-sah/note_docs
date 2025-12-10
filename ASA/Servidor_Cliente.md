# Configuração de serviços WEB, DNS, FTP, SSH 

## Configuração  Netplan  
1. cd /etc/netplan 
2. sudo nano  arquivo.yml 
````
network:
 version: 2
   ethernets:
    enp0s3:
    dhcp4: false
    addresses:
     - 192.168.150.254/24
    gateway4: 192.168.150.1
    nameservers:
     addresses: [8.8.8.8, 1.1.1.1]
````
3. Sudo netplan apply 
4. ip -c  a

## Serviço web 
1. sudo apt update 
2. sudo apt install -y apache2 
3. sudo systemctl status apache2 
4. cd /var/www 
5. sudo mkdir -p zeus/public_html 
6. cd zeus/public_html 
7. sudo nano index.html 
8. cd /etc/apache2/sites-available
9. sudo cp 000-default.conf zeus.conf 
10. sudo nano zeus.conf
````    
 ServerAdmin adimin@zeus.com
 ServerName zeus.com 
 ServerAlias www.zeus.com 
````
11. sudo a2ensite zeus.conf  
12. sudo a2dissite 000-default.conf 
13. sudo systemctl restart apache2 
## Serviço DNS 
1. sudo apt install -y bind9
2. cd /etc/ bind
3. sudo cp named.conf.local  named.conf.localOLD 
4. sudo nano named.conf.local 


```
//Zona direta 
zone “zeus.com”{
      type master; 
       file “/etc/bind/db.zeus”;
};

//Zona reversa254
zone “192.168.158.-in.addr.arpa{
         type master;
          file “/etc/bind/db.reverso254”
};
````   

5. sudo cp named.local  db.zeus 
6. sudo cp db.127 reverso254 
7. sudo cp db.local db.zeus
8. sudo nano /etc/resolv.conf

````
Apaga nameserver 127.0.0.1
Substituir por nameserver 192.168.150.254
````




9. sudo  systemctl restart named 

## Serviço SSH

1. sudo apt install -y openssh-server
2. ssh-keygen -t rsa -b 4096 
3. cd ~/ssh 
4. ssh-copy-id  zeus@192.168.150.254
5. cd /etc/ssh 
6. sudo nano sshd.config 

````
#Port 22

PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
PermitEmptyPasswords no 

#MaxAuthTries 6
#LoginGraceTime 10

#ClientAliveInterval 120
#ClientAliveCountMax 5

Authorizedkeysfile
kbdInterActiveAuthentification 
````

7. sudo systemctl restart ssh 
	
## Serviço FTP 
1. sudo apt install -y vsftpd 
2. sudo nano /etc/vsftpd 
````
Descomentar 
# write_enable=YES  
write_enable=YES
````
3. sudo systemctl restart vsftpd
4. cd /home
5. Sudo adduser ftpuser
````
 Usuário: ftpuser
 Senha: Senh@123
````
5. Gerenciador de arquivos → Outros locais ftp://IP da máquina 

# Erros comuns :
## Serviço web
## Serviço DNS 
## Serviço sssh 
## Serviço FTP

