# Roteiro de configurção do NFS

## instalação do NFS

````
sudo apt update 
sudo apt insatall -y nfs-kernel-server 
`````

## Criar diretórios

````
sudo mkdir -p srv/nfs/publico
````

## Alterar permissão

````
sudo chown nobody:nogroup  srv/nfs/publico
````

## Alterando permissão para usuário, groups e outros

````
sudo chmod 777 srv/nfs/publico
````

## Acessando arquivo de configuração

````
sudo nano /etc/exports
`````

## Editando arquivo /etc/exports

````
# Adicionar linha abaixo
Exemplo 
/srv/nfs/publico 192.168.100.0/24(rw,sync,no\_subtree\_check)
````
ctrl + O > Enter > ctrl + X


Em seguida
````
sudo exportfs -a 
````

## Reiniciar

````
sudo systemctl restart nfs-kernel-server 
````

## Instalação do Cockpit

````
sudo apt install -y cockpit 
````

## Habilitando o serviço

````
sudo systemctl enable --now cockpit.socket 
````

## Testar no navegador

Acesse o **Navegador** digite na URL **localhost:9090**
Login com seu **usuário** e **senha**
Procure por montagem NFS
Digite o seguinte:

````
Endereço do servidor \[192.168.100.93] # IP da maquina 
Caminho no servidor  \[/srv/nfs/publico ]
ponto de montagem
local    \[/mmt/nfs\_publico]

# Clique em adiciona 
````

## Na vm Windows

* Acesse o painel de controle\*\*
* **Programas e Recursos**
* Ativar e desativar recursos Windows
* Procure por **Serviços de NFS** Habilite \[x]
* Habilite Cliente for NFS \[x]
* Clique em **OK**

## No PowerShell

Digite:

````
cmd /c "mount \\\\192.168.100.93\\srv\\nfs\\publico Z: -o anon"
````

## Verifique o disco compartilhado

* Windows + E
* Este computador

#### Finalizado

