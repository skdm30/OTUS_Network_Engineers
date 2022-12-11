# Лабораторная работа №10
![](pic/map_lab5.png)     
       
Адресный план указан тут https://github.com/skdm30/OTUS_Network_Engineers/tree/main/labs/lab4     
В данной работе необходимо:
1. Настроить iBGP в офисе Москва
2. Настроить iBGP в сети провайдера Триада
3. Организовать полную IP связанность всех сетей  

**1. Настроим на R14 и R15 iBGP:** 
``` 
R14#show run | s bgp
router bgp 1001
 bgp log-neighbor-changes
 neighbor 10.10.10.15 remote-as 1001
 neighbor 10.10.10.15 update-source Loopback0
 neighbor 90.90.90.2 remote-as 101
 !
 address-family ipv4
  network 10.10.10.14 mask 255.255.255.255
  neighbor 10.10.10.15 activate
  neighbor 90.90.90.2 activate
 exit-address-family
``` 

``` 
R15#show run | s bgp
router bgp 1001
 bgp log-neighbor-changes
 neighbor 10.10.10.14 remote-as 1001
 neighbor 10.10.10.14 update-source Loopback0
 neighbor 90.90.90.6 remote-as 301
 !
 address-family ipv4
  network 10.10.10.15 mask 255.255.255.255
  neighbor 10.10.10.14 activate
  neighbor 90.90.90.6 activate
 exit-address-family
``` 
**2. Настроим iBGP в провайдере Триада, с использованием RR:  
В качестве RR выберем R23.  
``` 
R23#show run | s bgp
router bgp 520
 bgp log-neighbor-changes
 neighbor 10.10.10.24 remote-as 520
 neighbor 10.10.10.24 update-source Loopback0
 neighbor 10.10.10.24 route-reflector-client
 neighbor 10.10.10.24 next-hop-self
 neighbor 10.10.10.25 remote-as 520
 neighbor 10.10.10.25 update-source Loopback0
 neighbor 10.10.10.25 route-reflector-client
 neighbor 10.10.10.25 next-hop-self
 neighbor 10.10.10.26 remote-as 520
 neighbor 10.10.10.26 update-source Loopback0
 neighbor 10.10.10.26 route-reflector-client
 neighbor 10.10.10.26 next-hop-self
``` 

``` 
R24#show run | s bgp
router bgp 520
 bgp log-neighbor-changes
 neighbor 10.10.10.23 remote-as 520
 neighbor 10.10.10.23 update-source Loopback0
 neighbor 50.50.50.38 remote-as 2042
 neighbor 50.50.50.42 remote-as 301
 !
 address-family ipv4
  neighbor 10.10.10.23 activate
  neighbor 10.10.10.23 next-hop-self
  neighbor 50.50.50.38 activate
  neighbor 50.50.50.42 activate
 exit-address-family
``` 
``` 
R25#show run | s bgp
router bgp 520
 bgp log-neighbor-changes
 redistribute static
 neighbor 10.10.10.23 remote-as 520
 neighbor 10.10.10.23 update-source Loopback0
 neighbor 10.10.10.23 next-hop-self
``` 

``` 
R26#show run | s bgp
router bgp 520
 bgp log-neighbor-changes
 redistribute static
 neighbor 10.10.10.23 remote-as 520
 neighbor 10.10.10.23 update-source Loopback0
 neighbor 10.10.10.23 next-hop-self
 neighbor 50.50.50.34 remote-as 2042
``` 


