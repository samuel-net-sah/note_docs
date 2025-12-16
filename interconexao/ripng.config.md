# Configuração de roteamento dinâmico ipv6

## Entrando modo terminal no roteador 
````
enable 
configure terminal 
IPv6 unicast-runting 
````
## Atribuir ips nas interfaces R1 - R2 - R3
````
Interface g0/2 
IPv6  address 2001:db8:acad:1::1/64
no shutdown   #  para ativar interface 
exit 
````
### Repita o processo  em cada roteador
ficando assim: 


R1
````
Interface g0/0 
IPv6  2001:db8:acad:12::1/64
Interface g0/1
IPv6 2001:db8:acad:13::1/64
````
R2 
````
Interface g0/0 
IPv6 2001:db8:acad:2::1/64
interface g0/1
ipv6 2001:db8:acad:12::1/64
interface g0/2 
ipv6 2001:db8:acad:23::1/64
````
R3
````
Interface g0/0 
IPv6 2001:db8:acad:23::1/64
interface g0/1
ipv6 2001:db8:acad:13::1/64
interface g0/2 
ipv6 2001:db8:acad:::1/64
````
## Atribuindo protocolo rip 
````
ipv6 router ativar              # faça isso fora da interface 
exit                            # saia do modo "config-rtr)#  "
interface  g0/0                 # fazer em cada interface de cada roteador 
ipv6 rip nome enable            # ex: ipv6 rip processo1 enable
````
### processo finalizado 


