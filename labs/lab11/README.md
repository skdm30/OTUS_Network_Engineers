# Лабораторная работа №11
![](pic/map_lab5.png)     
       
**Сети Point-To-Point**


| host | Port  | IPv4 address |   Network       |    IPv6 address             | IPv6 LL address | Description  |
|------|-------|--------------|-----------------|-----------------------------|-----------------|--------------|
| R12  | e0/0  |              |                 |20FF:AAAA:BBBB:A1::0012:0/64 |  FE80::12       |              |   
| R12  | e0/1  | 172.16.10.37 | 172.16.10.36/30 |20FF:AAAA:BBBB:A1::0012:1/64 |  FE80::12       | to R13 e0/1  |   
| R12  | e0/2  | 172.16.10.1  | 172.16.10.0/30  |20FF:AAAA:BBBB:A1::0012:2/64 |  FE80::12       | to R14 e0/0  |  
| R12  | e0/3  | 172.16.10.5  | 172.216.10.4/30 |20FF:AAAA:BBBB:A1::0012:3/64 |  FE80::12       | to R15 e0/1  |  
| R13  | e0/0  |              |                 |20FF:AAAA:BBBB:A1::0013:0/64 |  FE80::13       |              |    
| R13  | e0/1  | 172.16.10.38 | 172.16.10.36/30 |20FF:AAAA:BBBB:A1::0013:1/64 |  FE80::13       | to R12 e0/1  |    
| R13  | e0/2  | 172.16.10.9  | 172.16.10.8/30  |20FF:AAAA:BBBB:A1::0013:2/64 |  FE80::13       | to R15 e0/0  |  
| R13  | e0/3  | 172.16.10.13 | 172.16.10.12/30 |20FF:AAAA:BBBB:A2::0013:3/64 |  FE80::13       | to R14 e0/1  |  
| R14  | e0/0  | 172.16.10.2  | 172.16.10.0/30  |20FF:AAAA:BBBB:A1::0014:0/64 |  FE80::14       | to R12 e0/2  |  
| R14  | e0/1  | 172.16.10.14 | 172.16.10.12/30 |20FF:AAAA:BBBB:A2::0014:1/64 |  FE80::14       | to R13 e0/3  |    
| R14  | e0/2  | 90.90.90.1   | 90.90.90.0 /30  |20FF:1111:1111:A1::0014:2/64 |  FE80::14       | to R22 e0/0  | -> Kitorn
| R14  | e0/3  | 172.16.10.17 | 172.16.10.16/30 |20FF:AAAA:BBBB:A3::0014:3/64 |  FE80::14       | to R19 e0/0  |
| R14  | e1/0  | 172.16.10.41 | 172.16.10.40/30 |20FF:AAAA:BBBB:A4::0014:4/64 |  FE80::14       | to R15 e1/0  |
| R15  | e0/0  | 172.16.10.10 | 172.16.10.8/30  |20FF:AAAA:BBBB:A1::0015:0/64 |  FE80::15       | to R13 e0/2  |  
| R15  | e0/1  | 172.16.10.6  | 172.16.10.4/30  |20FF:AAAA:BBBB:A2::0015:1/64 |  FE80::15       | to R12 e0/3  |  
| R15  | e0/2  | 90.90.90.5   | 90.90.90.4/30   |20FF:1111:1111:A1::0015:2/64 |  FE80::15       | to R21 e0/0  | -> Lamas
| R15  | e0/3  | 172.16.10.21 | 172.16.10.20/30 |20FF:AAAA:BBBB:A3::0015:3/64 |  FE80::15       | to R20 e0/0  |  
| R15  | e1/0  | 172.16.10.42 | 172.16.10.40/30 |20FF:AAAA:BBBB:A4::0015:4/64 |  FE80::14       | to R19 e0/0  |
| R16  | e0/0  |              |                 |20FF:BBBB:BBBB:A1::0016:0/64 |  FE80::16       |              |   
| R16  | e0/1  | 172.16.10.25 | 172.16.10.24/30 |20FF:BBBB:BBBB:A1::0016:1/64 |  FE80::16       | to R18 e0/0  | 
| R16  | e0/2  |              |                 |20FF:BBBB:BBBB:A1::0016:2/64 |  FE80::16       |              |  
| R16  | e0/3  | 172.16.10.29 | 172.16.10.28/30 |20FF:BBBB:BBBB:A1::0016:3/64 |  FE80::16       | to R32 e0/0  |
| R16  | e1/0  | 172.16.10.34 | 172.16.10.32/30 |20FF:BBBB:BBBB:A1::0016:4/64 |  FE80::16       | to R17 e0/3  |
| R17  | e0/0  |              |                 |20FF:BBBB:BBBB:A1::0017:0/64 |  FE80::17       |              |    
| R17  | e0/1  | 172.16.10.29 | 172.16.10.28/30 |20FF:BBBB:BBBB:A1::0017:1/64 |  FE80::17       | to R18 e0/1  |    
| R17  | e0/2  |              |                 |20FF:BBBB:BBBB:A1::0017:2/64 |  FE80::17       |              |
| R17  | e0/3  | 172.16.10.33 | 172.16.10.32/30 |20FF:BBBB:BBBB:A1::0017:3/64 |  FE80::17       | to R16 e1/0  |
| R18  | e0/0  | 172.16.10.26 | 172.16.10.24/30 |20FF:BBBB:BBBB:A1::0018:0/64 |  FE80::18       | to R16 e0/1  |    
| R18  | e0/1  | 172.16.10.30 | 172.26.10.28/30 |20FF:BBBB:BBBB:A1::0018:1/64 |  FE80::18       | to R17 e0/1  |  
| R18  | e0/2  | 50.50.50.38  | 50.50.50.36/30  |20FF:BBBB:BBBB:A1::0018:2/64 |  FE80::18       | to R24 e0/3  |   
| R18  | e0/3  | 50.50.50.34  | 50.50.50.32/30  |20FF:BBBB:BBBB:A2::0018:3/64 |  FE80::18       | to R26 e0/3  |  
| R19  | e0/0  | 172.16.10.18 | 172.26.10.16/30 |20FF:AAAA:BBBB:A3::0019:/64  |  FE80::19       | to R14 e0/3  |  
| R20  | e0/0  | 172.16.10.22 | 172.26.10.20/30 |20FF:AAAA:BBBB:A3::0020:1/64 |  FE80::20       | to R15 e0/3  |  
| R21  | e0/0  | 90.90.90.6   | 90.90.90.4/30   |20FF:1111:1111:A1::0021:0/64 |  FE80::21       | to R15 e0/2  |  
| R21  | e0/1  | 90.90.90.9   | 90.90.90.8/30   |20FF:1111:1111:A2::0021:1/64 |  FE80::21       | to R22 e0/1  | 
| R21  | e0/2  | 90.90.90.13  | 90.90.90.12/30  |20FF:1111:1111:A3::0021:2/64 |  FE80::21       | to R24 e0/0  |  
| R22  | e0/0  | 90.90.90.2   | 90.90.90.0/30   |20FF:1111:1111:A1::0022:0/64 |  FE80::22       | to R14 e0/2  |  
| R22  | e0/1  | 90.90.90.10  | 90.90.90.8/30   |20FF:1111:1111:A2::0022:1/64 |  FE80::22       | to R21 e0/1  |  
| R22  | e0/2  | 50.50.50.42  | 50.50.50.40/30  |20FF:1111:1111:A4::0022:2/64 |  FE80::22       | to R23 e0/0  |  
| R23  | e0/0  | 50.50.50.18  | 50.50.50.16/30  |20FF:1111:1111:A4::0023:0/64 |  FE80::23       | to R22 e0/2  |  
| R23  | e0/1  | 50.50.50.1   | 50.50.50.0/30   |20FF:1111:1111:A1::0023:1/64 |  FE80::23       | to R25 e0/0  |  
| R23  | e0/2  | 50.50.50.5   | 50.50.50.4/30   |20FF:1111:1111:A2::0023:2/64 |  FE80::23       | to R24 e0/2  |  
| R24  | e0/0  | 50.50.50.41  | 50.50.50.40/30  |20FF:1111:1111:A1::0024:0/64 |  FE80::24       | to R21 e0/2  |  
| R24  | e0/1  | 50.50.50.9   | 50.50.50.8/30   |20FF:1111:1111:A3::0024:1/64 |  FE80::24       | to R26 e0/0  |  
| R24  | e0/2  | 50.50.50.6   | 50.50.50.4/30   |20FF:1111:1111:A2::0024:2/64 |  FE80::24       | to R23 e0/2  |  
| R24  | e0/3  | 50.50.50.37  | 50.50.50.36/30  |20FF:BBBB:BBBB:A1::0024:3/64 |  FE80::24       | to R18 e0/2  |  
| R25  | e0/0  | 50.50.50.2   | 50.50.50.0/30   |20FF:1111:1111:A1::0025:0/64 |  FE80::25       | to R23 e0/1  |  
| R25  | e0/1  | 50.50.50.21  | 50.50.50.20/30  |20FF:1111:1111:A27::0025:1/64 |  FE80::25       | to R27 e0/0  |  
| R25  | e0/2  | 50.50.50.13  | 50.50.50.12/30  |20FF:1111:1111:A26::0025:2/64 |  FE80::25       | to R26 e0/2  |  
| R25  | e0/3  | 50.50.50.25  | 50.50.50.24/30  |20FF:1111:1111:A25::0025:3/64 |  FE80::25       | to R28 e0/1  |  
| R26  | e0/0  | 50.50.50.10  | 50.50.50.8/30   |20FF:1111:1111:A3::0026:0/64 |  FE80::26       | to R24 e0/1  |  
| R26  | e0/1  | 50.50.50.29  | 50.50.50.28/30  |20FF:1111:1111:A10::0026:1/64 |  FE80::26       | to R28 e0/0  |  
| R26  | e0/2  | 50.50.50.14  | 50.50.50.12/30  |20FF:1111:1111:A26::0026:2/64 |  FE80::26       | to R25 e0/2  |  
| R26  | e0/3  | 50.50.50.33  | 50.50.50.32/30  |20FF:BBBB:BBBB:A2::0026:3/64 |  FE80::26       | to R18 e0/3  |  
| R27  | e0/0  |  50.50.50.22 | 50.50.50.20/30 |20FF:1111:1111:A27::0027:0/64 |  FE80::27       | to R25 e0/1  |  
| R28  | e0/0  | 50.50.50.30  | 50.50.50.28/30  |20FF:1111:1111:A10::0028:0/64 |  FE80::28       | to R26 e0/1  |  
| R28  | e0/1  | 50.50.50.26  | 50.50.50.24/30  |20FF:1111:1111:A25::0028:1/64 |  FE80::28       | to R25 e0/3  | 
| R32  | e0/0  | 172.16.10.22 | 172.26.10.20/30 |20FF:BBBB:BBBB:A1::0032:0/64 |  FE80::32       | to R15 e0/3  |  

В данной работе в офисе Чокурдах необходимо настроить маршрутизацию на основи политик *PBR*  

**Описание/Пошаговая инструкция выполнения домашнего задания:** 
 1. Настроить фильтрацию в офисе Москва так, чтобы не появилось транзитного трафика(As-path).
 2. Настроить фильтрацию в офисе С.-Петербург так, чтобы не появилось транзитного трафика(Prefix-list).
 3. Настроить провайдера Киторн так, чтобы в офис Москва отдавался только маршрут по умолчанию.
 4. Настроить провайдера Ламас так, чтобы в офис Москва отдавался только маршрут по умолчанию и префикс офиса С.-Петербург.
 5. Все сети в лабораторной работе должны иметь IP связность.  
 
**Ход выполнения работы**   

**1.** Для фильтрации транзитного трафика в AS1001 решено отфильровать все внутренние маршруты AS провайдеров на граничных маршрутизаторах R14 и R15:     

**R14**
```   
router bgp 1001
 bgp log-neighbor-changes
 neighbor 10.10.10.15 remote-as 1001
 neighbor 10.10.10.15 update-source Loopback0
 neighbor 90.90.90.2 remote-as 101
 !
 address-family ipv4
  network 10.10.10.14 mask 255.255.255.255
  neighbor 10.10.10.15 activate
  neighbor 10.10.10.15 next-hop-self
  neighbor 10.10.10.15 soft-reconfiguration inbound
  neighbor 90.90.90.2 activate
  neighbor 90.90.90.2 filter-list 100 out
 exit-address-family

ip as-path access-list 100 permit ^$      
ip as-path access-list 100 deny .*
```   
**R15** 
``` 
router bgp 1001
 bgp log-neighbor-changes
 neighbor 10.10.10.14 remote-as 1001
 neighbor 10.10.10.14 update-source Loopback0
 neighbor 90.90.90.6 remote-as 301
 !
 address-family ipv4
  network 10.10.10.15 mask 255.255.255.255
  neighbor 10.10.10.14 activate
  neighbor 10.10.10.14 next-hop-self
  neighbor 10.10.10.14 soft-reconfiguration inbound
  neighbor 90.90.90.6 activate
  neighbor 90.90.90.6 route-map LP-150 in
  neighbor 90.90.90.6 filter-list 100 out
 exit-address-family

ip as-path access-list 100 permit .*ip as-path access-list 100 permit ^$      
ip as-path access-list 100 deny .*
```     
Выполнив команду *show ip bgp* на R22, увидим, что через AS1001 не проходит транзитный трафик. (На скриншоте также присутствует результат этой команды до применения фильтрации)
![](pic/11.png)      

**2.**  Настройка фильтрации в офисе С.-Петербург так, чтобы не появилось транзитного трафика с помощью Prefix-list.       
```    
R18#show run | s bgp
router bgp 2042
 bgp log-neighbor-changes
 bgp bestpath as-path multipath-relax
 neighbor 50.50.50.33 remote-as 520
 neighbor 50.50.50.37 remote-as 520
 !
 address-family ipv4
  network 10.10.10.18 mask 255.255.255.255
  network 172.16.10.24 mask 255.255.255.252
  network 172.16.10.28 mask 255.255.255.252
  neighbor 50.50.50.33 activate
  neighbor 50.50.50.33 prefix-list AS520_in in
  neighbor 50.50.50.33 prefix-list SPB-IN out
  neighbor 50.50.50.37 activate
  neighbor 50.50.50.37 prefix-list AS520_in in
  neighbor 50.50.50.37 prefix-list SPB-IN out
  maximum-paths 2
 exit-address-family
 
 
 !
ip prefix-list SPB-IN seq 10 permit 172.16.10.0/24 le 32
ip prefix-list SPB-IN seq 20 permit 50.50.50.0/24 le 32

```    

**3.**   Настройка провайдера Киторн так, чтобы в офис Москва отдавался только маршрут по умолчанию. 
На R22 необходимо произвести настройку, которая будет отдавать соседу R14 маршрут о умолчанию (команда ***neighbor 90.90.90.1 default-originate***)
```    
router bgp 101
 bgp log-neighbor-changes
 neighbor 50.50.50.18 remote-as 520
 neighbor 90.90.90.1 remote-as 1001
 neighbor 90.90.90.9 remote-as 301
 !
 address-family ipv4
  neighbor 50.50.50.18 activate
  neighbor 90.90.90.1 activate
  neighbor 90.90.90.1 default-originate
  neighbor 90.90.90.9 activate
 exit-address-family    
```
Вызвав команду ***show ip bgp*** получим: 
```    
R14#show ip bgp
BGP table version is 8, local router ID is 10.10.10.14
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *   0.0.0.0          90.90.90.2                             0 101 i
 *>i                  10.10.10.15              0    150      0 301 i
 *>  10.10.10.14/32   0.0.0.0                  0         32768 i
 r>i 10.10.10.15/32   10.10.10.15              0    100      0 i
 *>  10.10.10.27/32   90.90.90.2                             0 101 520 ?
 *>  172.16.8.0/24    90.90.90.2                             0 101 520 ?
 *   172.16.10.24/30  90.90.90.2                             0 101 520 2042 i
 *>i                  10.10.10.15              0    150      0 301 520 2042 i
 *   172.16.10.28/30  90.90.90.2                             0 101 520 2042 i
 *>i                  10.10.10.15              0    150      0 301 520 2042 i
```    
Видим, что появился маршрут по умолчанию к R22 (он не выбран ***best**, т.к. проверка проводилась после выполнения задания 4).       

**4.** Настройка провайдера Ламас так, чтобы в офис Москва отдавался только маршрут по умолчанию и префикс офиса С.-Петербург.       
Произведем настройку на R21 
```    
R21#show run | s bgp
router bgp 301
 bgp log-neighbor-changes
 neighbor 50.50.50.41 remote-as 520
 neighbor 90.90.90.5 remote-as 1001
 neighbor 90.90.90.10 remote-as 101
 !
 address-family ipv4
  neighbor 50.50.50.41 activate
  neighbor 90.90.90.5 activate
  neighbor 90.90.90.5 default-originate
  neighbor 90.90.90.5 prefix-list SPB out
  neighbor 90.90.90.10 activate
 exit-address-family



ip prefix-list SPB seq 10 permit 172.16.10.0/24 le 32
ip prefix-list SPB seq 20 permit 50.50.50.0/24 le 32
```    

Проверим результам с помощью команды ***show ip bgp neighbors 90.90.90.5 advertised-routes***, которая показывает, какие анонсы роутер передает конкретному соседу:

```    
R21#show ip bgp neighbors 90.90.90.5 advertised-routes
BGP table version is 11, local router ID is 10.10.10.21
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

Originating default network 0.0.0.0

     Network          Next Hop            Metric LocPrf Weight Path
 *>  172.16.10.24/30  50.50.50.41                            0 520 2042 i
 *>  172.16.10.28/30  50.50.50.41                            0 520 2042 i

Total number of prefixes 2
```    
Полные конфиги устройств можно посмотреть здесь: 
[R14](config/R14)    

[R15](config/R15)    

[R21](config/R21)    

[R22](config/R22)    

[R18](config/R18)   


