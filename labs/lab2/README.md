# Лабораторная работа. Развертывание коммутируемой сети с резервными канал  
    

 **Таблица адресации**   
  
| Устройство |Интерфейс    | IP-адрес     | Маска подсети  | 
|------------|-------------|--------------|----------------|
|    S1      | VLAN1       | 192.168.1.1  |255.255.255.0   | 
|    S2      | VLAN1       | 192.168.1.2  |255.255.255.0   |   
|    S3      | VLAN1       | 192.168.1.3  |255.255.255.0   |   


## Задачи   

1. Создание сети и настройка основных параметров устройства                 
2. Выбор корневого моста            
3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов          
4. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов                 

## Ход выполнения работы    
### 1. Настройка основных параметров устройств    
Создали сеть согласно заданию:  
![](pic/topology.png)       

Произвели базовую конфигурацию коммутаторов [S1](config/base_setting_S1), [S2](config/base_setting_S2), [S3](config/base_setting_S3).       

После этого проверили связь между коммутаторами.        
![](pic/test.png)        
           

### 2. Определение корневого моста.    
Отключим порты на коммутаторах      
``` 
S1(config)#interface range e0/0-3
S1(config-if-range)#shutdown        
```     

Настроим подключенные порты в качестве транковых        
``` 
S1(config-if-range)#switchport trunk encapsulation dot1q
S1(config-if-range)#switchport mode trunk 
S1(config-if-range)#switchport trunk allowed vlan 1     
```     

Включим порты e0/0 и e0/2 на всех коммутаторах      
``` 
S1(config)#interface range e0/0, e0/2
S1(config-if-range)#shutdown        
``` 
С помощью команды *show spanning-tree* посмотрим данные протокола STP   
![](pic/show.png)         
Видим, что корневым мостом является S1. В данном случае он является таковым из-за самого меньшего значения MAC среди всех коммутаторов.         
Порты e0/0, e0/2 коммутатора S1 являются назначенными. Порт e0/0 коммутатора S2 является корневым, а e0/2 назначенным . Порт e0/2 коммутатора S3 является альтернативным (был выбран таковым, потому что от него до корневого коммутатора самый длинный путь), а e0/0 - корневым.         

### 3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов         
С помощью команды *spanning-tree cost* изменим стоимость порта e0/0 на S3. Мы видим, что e0/2 стал назначенным, а e0/2 на S2 заблокировался.     
![](pic/show1.png)      

### 4. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов         
Для выполнения этого задания необходимо включить порты e0/1, e0/3 на каждом коммутаторе.      
После этого выполним команду *show spanning-tree*       
![](pic/show2.png)  

Мы видим, что на каждом из коммутаторов некорневого моста в качестве порта корневого моста выбран порт e0/1, т.к. по протоколу STP при равной стоимости портов и равным BID выбирается порт с наименьшим номером.      