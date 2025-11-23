# deliverables

Screenshot of "sh ip route" on Pacific ISP

<img width="674" height="570" alt="image" src="https://github.com/user-attachments/assets/e4682882-e596-4ff9-97a2-07a7237f8487" />

Screenshot of "sh ip route" on Vermont ISP

<img width="674" height="570" alt="image" src="https://github.com/user-attachments/assets/a98a096e-ba25-426f-9e92-67059dccf823" />

Screenshot of "sh ip route" on BTV-Router

<img width="674" height="570" alt="image" src="https://github.com/user-attachments/assets/9f6209b4-39a4-4cb9-b66b-091c645b2315" />

Screenshot of Customer PC pinging Data-Center Station


# configs

update btv router
```
en
conf t

interface fa0/1
ip address 192.168.2.2 255.255.255.252
no shut 
exit

ip route 0.0.0.0 0.0.0.0 192.168.2.1

router ospf 1
network 192.168.2.0 0.0.0.3 area 1
default-information originate
redistribute ospf 1
exit

router bgp 1010
redistribute ospf 1

exit
exit
copy run start
```

vermont isp router
```
en
conf t
hostname Vermont-ISP

interface fa0/0
ip address 192.168.1.1 255.255.255.252
no shut 

interface fa0/1
ip address 192.168.2.1 255.255.255.252
no shut

exit
router bgp 1010
neighbor 192.168.1.1 remote-as 2054
network 10.10.52.0 mask 255.255.255.0

exit
exit
copy run start
```

pacific rotuer
```
en 
conf t
hostname Pacific-ISP

router bgp 2054
neighbor 192.168.1.1 remote-as 1010
neighbor 192.168.3.2 remote-as 34908
neighbor 192.168.4.2 remote-as 5132
network 192.168.1.0 mask 255.255.255.252
network 192.168.4.0 mask 255.255.255.252
network 192.168.3.0 mask 255.255.255.252
exit

int fa0/0
ip address 192.168.1.2 255.255.255.252
no shut 

int fa0/1
ip address 192.168.3.1 255.255.255.252
no shut 

interface Serial0/1/0
ip address 192.168.4.1 255.255.255.252
no shut

exit
exit
copy run start
```

partner router
```
en 
conf t
hostname Partner-Co

router bgp 34908
neighbor 192.168.3.1 remote-as 2054
network 192.168.3.0 mask 255.255.255.252
network 10.16.6.0 mask 255.255.255.0

int fa0/0
ip address 192.168.3.2 255.255.255.252
no shut

int fa0/1
ip address 10.15.6.1 255.255.255.0
no shut

exit
exit
copy run start
```

customer router
```
en
conf t
hostname Customer-Co

interface Serial0/1/0
ip address 192.168.4.2 255.255.255.252
no shut 

int fa0/0
ip address 10.200.24.1 255.255.255.0
no shut 

router bgp 5132 
neighbor 192.168.4.1 remote-as 2054
network 192.168.4.0 mask 255.255.255.252
network 10.200.24.0 mask 255.255.255.0

exit
exit
copy run start
```
