Configuração e instalação do serviço WEB (Apache2)



instalação do serviço

&nbsp;  1. sudo apt update 

&nbsp;  2. sudo apt install -y apache2



Configuração no diretório (/var/www)

&nbsp;  1. cd /var/www

&nbsp;  2. mkdir -p zeus/public\_html 

&nbsp;  3. cd zeus/public\_html 

&nbsp;  4. sudo nano index.html 



Configuração no diretório(/etc/apache2/sites-avaiable)

&nbsp; 1. cd /etc/apache2/sites-avaiable 

&nbsp; 2. sudo cp 000-defalt.conf zeus.conf 

&nbsp; 3.sudo nano zeus.conf 

&nbsp;ServerAdmin admin@zeus.com 

&nbsp;ServerName zeus.com

&nbsp;ServerAlias www.zeus.con

&nbsp;DocumentsRoot /var/www/zeus/public\_html

&nbsp;4. sudo a2ensite zeus.conf

&nbsp;5. sudo a2dissite 000-defalt.conf 

&nbsp;sudo systemctl restart apache2 



