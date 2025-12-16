# Roteiro De configuração do samba

## instalação 
#### No ubuntu Linux 
````
sudo apt update 
sudo apt install -y samba
````
## Criação de usuário 
```
cd /home 
sudo adduser --disabled-login -no-create-home joao
sudo adduser --disabled-login -no-create-home maria
```
## Criação de grupos
````
sudo addgrup alunos
sudo addgrup professores
````
### Adicionar usuários aos grupos 
````
sudo usermod -aG professores joao 
sudo usermod -aG alunos maria 
````
## Criar diretório principal samba
````
sudo mkdir samba

ls
````
### Atribuir permissão 
````
sudo chmod 775 samba 

ls -l 
````
### Criar 2 diretório 
````
cd samba
sudo mkdir professores 
sudo mkdir alunos 
````
### Altera permissões 
````
sudo chmod 770 alunos 
sudo chmod 770 professores
ls -l 
````
### Altera permissão dono/grupos
````
sudo chown -R root:alunos alunos/
sudo chown R root:professores professores/
````
### Alterando senha dos usuários
````
sudo smbpasswd -a maria 
sudo smbpasswd -a joao 
````
## Configurando arquivo de configuração samba
````
sudo mv smb.conf  bkp.smb.conf 
sudo nano smb.conf
````
### Editando o arquivo smb.conf
```
[global]
        netbios name = servidorSamba 
	workgrup = WORKGROUP

[arquivos]
        path = /homo/samba
	writeable = yes 
	avallable = yes 
	force group = alunos
	force group = professores 
	create mask = 0770
	directory mask = 0770 
	valid user = @alunos, @professores
	
ctrl + o > Enter > ctrl + x    # para sair e salvar 
````
## Reiniciar samba serviços 
````
sudo systemctl restart smbd.service 
````
## Testando na vm Windows 
Na vm *Windows*  use o atalho **Windows + E** na barra de busca caminho no canto superior.
Digite \\IP 
#### Exemplo: 
````
\\192.168.100.93
```` 
> Acesse com os usuários 
-  maria [°°°°°°°]
-  joao [°°°°°°°]
> Acesse a pasta arquivos/alunos 
-  crie uma pasta  [Nome pasta]
> Acesse a pasta arquivos/professores 
-  crie uma pasta  [Nome pasta]


#### Finalizou !!!



 