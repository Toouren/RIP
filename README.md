# RIP Homework
##### Новиков Василий. КН-202. Вариант 18.
![N|Solid](https://i.imgur.com/taSiHle.png)

### Задание

Запустить протокол динамической маршрутизации RIP в сети из трех маршрутизаторов.

### Решение

1. Расположил и стал соединять устройства, как показано в условии.
![N|Solid](https://i.imgur.com/ha9uiWv.png)
2. Столкнулся с проблемой нехватки портов. Добавил на роутеры платы NM-1FE-TX, которые добавили по одному FastEthernet порту на каждый роутер. Соеденил все сервера с роутерами.
3. Настроил IP Configuration на PC-0, PC-1, Server 0, 1, 2.
![N|Solid](https://i.imgur.com/ZcFz482.png)
4. На каждом роутере (Router 0-2) настроил интерфейсы. В соответствии с условием, назначил им IP и маску.
    ```sh
        Router(config)#interface FastEthernet0/0
        Router(config-if)#ip address 10.18.1.1 255.255.255.0
    ```
5. Для всех роутеров настроил RIP.
    ```sh
        Router(config)#router rip 
        Router(config-router)#network 192.168.1.0
        Router(config-router)#network 192.168.10.0
        Router(config-router)#network 10.18.1.0
        Router(config-router)#exit
    ```
### Результат
Получилась сеть с настроенным протоколом RIP. Проверить это можно с помощью команд:```show ip interface brief``` и ``` show ip route```.
#### Router 0:
```sh
        Router#show ip interface brief 
        Interface              IP-Address      OK? Method Status            Protocol 
        FastEthernet0/0        10.18.1.1       YES manual up                    up 
        FastEthernet0/1        192.168.10.1    YES manual up                    up 
        FastEthernet1/0        192.168.1.1     YES manual up                    up 
        Vlan1                  unassigned      YES unset  administratively down down
        Router#show ip route 
        Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
               D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
               N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
               E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
               i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
               * - candidate default, U - per-user static route, o - ODR
               P - periodic downloaded static route
        
        Gateway of last resort is not set
        
             10.0.0.0/24 is subnetted, 1 subnets
        C       10.18.1.0 is directly connected, FastEthernet0/0
        C    192.168.1.0/24 is directly connected, FastEthernet1/0
        R    192.168.2.0/24 [120/1] via 192.168.10.2, 00:00:00, FastEthernet0/1
        R    192.168.3.0/24 [120/1] via 10.18.1.2, 00:00:08, FastEthernet0/0
             192.168.10.0/30 is subnetted, 2 subnets
        C       192.168.10.0 is directly connected, FastEthernet0/1
        R       192.168.10.4 [120/1] via 192.168.10.2, 00:00:00, FastEthernet0/1
```

#### Router 1:
```sh
        Router#show ip interface brief 
        Interface              IP-Address      OK? Method Status                Protocol 
        FastEthernet0/0        192.168.10.2    YES manual up                    up 
        FastEthernet0/1        192.168.10.6    YES manual up                    up 
        FastEthernet1/0        192.168.2.1     YES manual up                    up 
        Vlan1                  unassigned      YES unset  administratively down down
        Router#show ip route
        Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
               D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
               N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
               E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
               i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
               * - candidate default, U - per-user static route, o - ODR
               P - periodic downloaded static route
        
        Gateway of last resort is not set
        
        R    10.0.0.0/8 [120/1] via 192.168.10.5, 00:00:21, FastEthernet0/1
                        [120/1] via 192.168.10.1, 00:00:14, FastEthernet0/0
        R    192.168.1.0/24 [120/1] via 192.168.10.1, 00:00:14, FastEthernet0/0
        C    192.168.2.0/24 is directly connected, FastEthernet1/0
        R    192.168.3.0/24 [120/1] via 192.168.10.5, 00:00:21, FastEthernet0/1
             192.168.10.0/30 is subnetted, 2 subnets
        C       192.168.10.0 is directly connected, FastEthernet0/0
        C       192.168.10.4 is directly connected, FastEthernet0/1
```

#### Router 2:
```sh
        Router#show ip interface brief 
        Interface              IP-Address      OK? Method Status                Protocol 
        FastEthernet0/0        10.18.1.2       YES manual up                    up 
        FastEthernet0/1        192.168.10.5    YES manual up                    up 
        FastEthernet1/0        192.168.3.1     YES manual up                    up 
        Vlan1                  unassigned      YES unset  administratively down down
        Router#show ip route
        Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
               D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
               N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
               E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
               i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
               * - candidate default, U - per-user static route, o - ODR
               P - periodic downloaded static route
        
        Gateway of last resort is not set
        
             10.0.0.0/24 is subnetted, 1 subnets
        C       10.18.1.0 is directly connected, FastEthernet0/0
        R    192.168.1.0/24 [120/1] via 10.18.1.1, 00:00:14, FastEthernet0/0
        R    192.168.2.0/24 [120/1] via 192.168.10.6, 00:00:14, FastEthernet0/1
        C    192.168.3.0/24 is directly connected, FastEthernet1/0
             192.168.10.0/30 is subnetted, 2 subnets
        R       192.168.10.0 [120/1] via 192.168.10.6, 00:00:14, FastEthernet0/1
        C       192.168.10.4 is directly connected, FastEthernet0/1
```
