\# Documentação – Configuração do RIPng (IPv6) no Cisco Packet Tracer



\## Objetivo: 

* Ativar roteamento dinâmico IPv6 entre roteadores Cisco utilizando RIPng



## Cenário 



````

R1 --- R2 --- R3



````

## Endereçamento Ipv6 



**R1** 



````



Router> enable 
Router#> configure terminal 
Router(config)# ipv6 unicast-routing 
Router(config)# interface g0/2 
Router(config-fi)# ipv6 address 2001:db8:acad:1::1/64 
Router(config-fi)# no shutdown 



````

**R2**

````

Router> enable
Router#> configure terminal
Router(config)# ipv6 unicast-routing
Router(config)# interface g0/0
Router(config-fi)# ipv6 address 2001:db8:acad:2::1/64
Router(config-fi)# no shutdown

````

**R3**

````

Router> enable
Router#> configure terminal
Router(config)# ipv6 unicast-routing
Router(config)# interface g0/2
Router(config-fi)# ipv6 address 2001:db8:acad:3::1/64
Router(config-fi)# no shutdown

````

## Configurar ipv6 nas interfaces (Exemplo R1 ) 

````

Router(config)# interface g0/0
Router(config-fi)# ipv6 address 2001:db8:acad:13::1/64
Router(config-fi)# no shutdown


Router(config)# interface g0/1
Router(config-fi)# ipv6 address 2001:db8:acad:2::1/64
Router(config-fi)# no shutdown


````

**Exemplo R2**


````

Router(config)# interface g0/1
Router(config-fi)# ipv6 address 2001:db8:acad:12::1/64
Router(config-fi)# no shutdown


Router(config)# interface g0/2
Router(config-fi)# ipv6 address 2001:db8:acad:23::1/64
Router(config-fi)# no shutdown



````

**Exemplo R3**

````

Router(config)# interface g0/0
Router(config-fi)# ipv6 address 2001:db8:acad:23::1/64
Router(config-fi)# no shutdown


Router(config)# interface g0/1
Router(config-fi)# ipv6 address 2001:db8:acad:13::1/64
Router(config-fi)# no shutdown


````


## Ativar Ripng  nas interfaces 
````
Router(config)# ipv6 router rip "nome"
Router(config-rtr)# exit 
Router(config)# interface g0/1
Router(config-fi)# ipv6 rip "nome" enable

# Repita o processo em cada Roteador e  em cada Interface


````

## Testa ping 
Na rede do R1 
- ping 2001:db8:acad:2::1
- ping 2001:db8:acad:2::1










