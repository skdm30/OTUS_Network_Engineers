R28#show run
Building configuration...

Current configuration : 2421 bytes
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R28
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
clock timezone EET 2 0
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
!
!
!
!
no ip domain lookup
ip cef
no ipv6 cef
!
multilink bundle-name authenticated
!
!
!
!
!
!
!
!
!
redundancy
!
!
!
track 1 ip sla 1 reachability
 delay down 10 up 5
!
track 2 ip sla 2 reachability
 delay down 10 up 5
!
!
!
!
!
!
!
!
!
!
!
!
interface Ethernet0/0
 ip address 150.50.50.6 255.255.255.252
 shutdown
!
interface Ethernet0/1
 ip address 150.50.50.2 255.255.255.252
!
interface Ethernet0/2
 no ip address
 ip policy route-map PBR_TO_R25_R26
!
interface Ethernet0/2.10
 encapsulation dot1Q 10
 ip address 172.16.8.1 255.255.255.192
!
interface Ethernet0/2.20
 encapsulation dot1Q 20
 ip address 172.16.8.65 255.255.255.192
 ip policy route-map PBR_TO_R25_R26
!
interface Ethernet0/2.30
 encapsulation dot1Q 30
 ip address 172.16.8.129 255.255.255.192
 ip policy route-map PBR_TO_R25_R26
!
interface Ethernet0/3
 no ip address
 shutdown
!
interface Ethernet1/0
 no ip address
 shutdown
!
interface Ethernet1/1
 no ip address
 shutdown
!
interface Ethernet1/2
 no ip address
 shutdown
!
interface Ethernet1/3
 no ip address
 shutdown
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
!
ip access-list extended ACL_IT_to_R26
 permit ip 172.16.8.64 0.0.0.63 any
 deny   ip any any
ip access-list extended ACL_SALES_to_R25
 permit ip 172.16.8.128 0.0.0.63 any
 deny   ip any any
!
ip sla auto discovery
ip sla 1
 icmp-echo 150.50.50.5 source-interface Ethernet0/0
 threshold 10
 frequency 10
ip sla schedule 1 life forever start-time now
ip sla 2
 icmp-echo 150.50.50.1 source-interface Ethernet0/1
 threshold 10
 frequency 10
ip sla schedule 2 life forever start-time now
!
route-map PBR_TO_R25_R26 permit 10
 match ip address ACL_IT_to_R26
 set ip next-hop verify-availability 150.50.50.5 10 track 1
 set ip next-hop verify-availability 150.50.50.1 20 track 2
!
route-map PBR_TO_R25_R26 permit 20
 match ip address ACL_SALES_to_R25
 set ip next-hop verify-availability 150.50.50.1 10 track 2
 set ip next-hop verify-availability 150.50.50.5 20 track 1
!
!
!
control-plane
!
!
!
!
!
!
!
line con 0
 logging synchronous
line aux 0
line vty 0 4
 login
 transport input all
!
!
end
