# configure


btv router
```
en
conf t
hostname BTV-Router

int fa0/0


int se0/1/0
ip address 172.16.0.1 255.255.255.252

```

mtl router 
```
en
conf t
hostname MTL-Rotuer

int fa0/0
ip address 172.16.20.1 255.255.0.0
no shut

int Serial0/1/0
ip address 172.16.0.2 255.255.255.252
no shut

router ospf 1
network 172.16.20.0 0.0.0.255 area 0
network 172.16.0.0 0.0.0.255 area 0

exit
exit
copy run start
```

multilayer switch
```
en
conf t 
hostname BTV-Dist-MultiLayerSwitch

ip routing

vlan 5
name BTVUser
exit 

vlan 6 
name BTVDataCenter
exit

vlan 10
name GW

int vlan 5
ip address 172.16.5.1 255.255.255.0

int vlan 6
ip address 172.16.6.1 255.255.255.0

int vlan 10
ip address 172.16.10.2 255.255.255.0

int GigabitEthernet0/1
switchport mode access
switchport access vlan 5
no shutdown

int GigabitEthernet0/2
switchport mode access
switchport access vlan 6
no shutdown

int GigabitEthernet0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 5
switchport trunk allowed vlan add 6
switchport trunk allowed vlan add 10
no shutdown
exit

router ospf 1
network 172.16.10.0 0.0.0.255 area 0
network 172.16.6.0 0.0.0.255 area 0
network 172.16.5.0 0.0.0.255 area 0
```
