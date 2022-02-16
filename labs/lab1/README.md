# Лабораторная работа. Внедрение маршрутизации между виртуальными локальными сетями
## Задачи
**1. Создание сети и настройка основных параметров устройства** 

**2. Создание сетей VLAN и назначение портов коммутатора**  

**3. Настройка транка 802.1Q между коммутаторами.** 

**4. Настройка маршрутизации между сетями VLAN**  

**5. Проверка, что маршрутизация между VLAN работает**  
  
    
     
      
  ***Таблица адресации*** 
  
  
| Устройство |Интерфейс     | IP-адрес      | Маска подсети  | Шлюз по умолчанию|
|------------|--------------|---------------|----------------|------------------|
|    R1      | G 0/0/1.10   | 192.168.10.1  |255.255.255.0   |        -         |
|            | G 0/0/1.20   | 192.168.10.1  |255.255.255.0   |        -         |
|            | G 0/0/1.30   | 192.168.10.1  |255.255.255.0   |        -         |
|            | G 0/0/1.1000 | -             |  -             |        -         |
|    S1      | VLAN 10      | 192.168.10.11 |255.255.255.0   |    192.168.10.1  |
|    S2      | VLAN 10      | 192.168.10.12 |255.255.255.0   |    192.168.10.1  |
|    PC0     | NIC          | 192.168.20.3  |255.255.255.0   |    192.168.20.1  |
|    PC1     | NIC          | 192.168.30.3  |255.255.255.0   |    192.168.30.1  | 
  
  

***Таблица VLAN***      
  

|      VLAN     |    Имя          |   Назначенный интерфейс     | 
|---------------|-----------------|-----------------------------|
|   10          |Управление       |  S1: VLAN 10                |
|               |                 |  S2: VLAN 10                |
|   20          |Sales            |  S1: F0/6                   |
|   30          |Operations       |  S2: F0/18                  |
|   999         |Parking_Lot      |  С1: F0/2-4, F0/7-24,G0/1-2 |
|               |                 |  С2: F0/2-17,F0/19-24,G0/1-2|
            
               


## Ход выполнения работы    
### 1. Создание сети и настройка основных параметров устройств    
Для выполнения работы создадим сеть согласно топологии    
![](pic/topology.png)    

Настройку выполним на примере SW1.
Войдем в режим глобальной конфигурации:  
``` 
Switch>enable
Switch#conf t
``` 
Назначим имя устройства:  
``` 
Switch(config)#hostname SW1
``` 
Отключим поиск DNS: 
```   
SW1(config)#no ip domain-lookup
```   
Назначим пароли на привелигированный режим, пароль консоли и пароль виртуального терминала, после чего зашифруем открытые пароли: 
```
SW1(config)#enable secret class
SW1(config)#line con 0
SW1(config-line)#password cisco
SW1(config-line)#login
SW1(config-line)#logging synchronous
SW1(config-line)#exit
SW1(config)#line
SW1(config)#line vty 0 4
SW1(config-line)#password cisco
SW1(config-line)#login
SW1(config-line)#exit   
SW1(config)#service password-encryption
``` 
Создадим баннер и сохраним конфигурацию:  
```
SW1(config)#banner motd #Attention! This is a private space!Unauthorized access is prohibited!#   
SW1(config)#exit  
SW1#wr
``` 
Настроим время на устройстве: 
``` 
SW1# clock set 21:10:55 16 February 2022  
``` 

Результат настройки базовых конфигураций можно посмотреть тут - [R1](config/base_setting_R1), [S1](config/base_setting_S1), [S2](config/base_setting_S1). 

Настройка PC-A:     
```
VPCS> ip 192.168.3.3/24 192.168.3.1
Checking for duplicate address...
PC1 : 192.168.3.3 255.255.255.0 gateway 192.168.3.1
``` 
и PC-B: 
``` 
VPCS> ip 192.168.4.3/24 192.168.4.1
Checking for duplicate address...
PC1 : 192.168.4.3 255.255.255.0 gateway 192.168.4.1

VPCS> save
``` 
  
### 2. Создание сети и настройка основных параметров устройств    
#### 2.1 Создание сети VLAN на коммутаторах   
Создадим и назовем необходимые VLAN на каждом коммутаторе в соответствие с таблицей.
Настроим интерфейс управления и шлюз по умолчанию на каждом коммутаторе. 
Назначим все неиспользуемые порты коммутатора VLAN Parking_Lot, настроим их для статического режима доступа и административно деактивируем их:       
``` 
SW1(config)#vlan 3
SW1(config-vlan)#name MANAGEMENT
SW1(config-vlan)#exit
SW1(config)#vlan 7
SW1(config-vlan)#name PARKING_LOT
SW1(config-vlan)#exi
SW1(config)#vlan 8
SW1(config-vlan)#name NATIVE
SW1(config-vlan)#exit
SW1(config)#int vlan 3
SW1(config-if)#ip address 192.168.3.11 255.255.255.0
SW1(config-if)#exit
SW1(config)#ip default-gateway 192.168.3.1
SW1(config)#int ethernet 0/1
SW1(config)#int e 0/3
SW1(config-if)#swi mod ac
SW1(config-if)#swi acc vlan 7
SW1(config-if)#shutdown
SW1(config-if)#exit
SW1(config)#
```   
#### 2.2 Назначьте сети VLAN соответствующим интерфейсам коммутатора    
Назначим используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настроим их для режима статического доступа: 
``` 
SW1(config)#int ethernet 0/1
SW1(config-if)#switchport mode access
SW1(config-if)#sw acc vlan 3
SW1(config-if)#exit 
```   

Убедимся, что все VLAN назначены правильно: 
![](pic/show_vlan_SW1.png) 





