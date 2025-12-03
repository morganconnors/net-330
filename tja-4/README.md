# TJ9-Tech Journal Assignment 3

**Steps and explanation of configuring OSPF**

Basically, define a router to use OSPF and then define IPs to be in areas that use OSPF. 

```
en
conf t
router ospf 1
network 10.1.1.0 0.0.0.7 area 0
network 10.1.1.20 0.0.0.3 area 0
network 10.1.1.32 0.0.0.3 area 0
exit
exit
copy run start
```

**Steps and explanation of configuring BGP**

Basically, define bgp and then configure networks to share to specific neighbors

```
router bgp 3033
network 172.16.0.0 mask 255.255.255.0
network 172.16.10.0 mask 255.255.255.0
network 172.16.0.0 mask 255.255.255.252
neighbor 192.168.2.1 remote-as 1010
redistribute ospf 1
```









