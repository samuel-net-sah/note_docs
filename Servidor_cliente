Configuração  Netplan  Adicionando endereço IP
cd /etc/netplan 
sudo nano  arquivo.yml 


network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: false
      addresses:
        - 192.168.150.10/24
      gateway4: 192.168.150.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]




Sudo netplan apply 
ip -c  a


Serviço web 
sudo apt update 
sudo apt install -y apache2 
sudo systemctl status apache2 
cd /var/www 
sudo mkdir -p zeus/public_html 
cd zeus/public_html 
sudo touch index.html 
cd /etc/apache2/sites-available
sudo cp 000-default.conf zeus.conf 
sudo nano zeus.conf 


ServerAdmin adimin@zeus.com
ServerName zeus.com 
ServerAlias www.zeus.com 



sudo a2ensite zeus.conf  
sudo a2dissite 000-default.conf 
 sudo systemctl restart apache2 
Serviço DNS 
sudo apt install -y bind9
cd /etc/ bind
sudo cp named.conf.local  named.conf.localOLD 
sudo nano named.conf.local 


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

sudo cp named.local  db.zeus 
sudo cp db.127 reverso254 
sudo cp db.local db.zeus
sudo nano /etc/resolv.conf


Apagar 127.0.0.1
Substituir por nameserver 192.168.150.254





sudo  systemctl restart named 

Serviço SSH

sudo apt install -y openssh-server
ssh-keygen -t rsa -b 4096 
cd ~/ssh 
sudo scp id_rsa.pub  Servidor@192.168.150.254
cd /etc/ssh 
sudo nano sshd.config 


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






sudo systemctl restart ssh 
	
Serviço FTP 
sudo apt install -y vsftpd 
sudo nano /etc/vsftpd 


Descomentar 
# write_enable=YES  
write_enable=YES



sudo systemctl restart vsftpd
cd /home
Sudo adduser ftpuser
Usuário:  ftpuser Senha: Senh@123
Gerenciador de arquivos → ftp://IP da máquina 

Erros comuns :
Serviço web
Serviço DNS 
Serviço sssh 
Serviço FTP

