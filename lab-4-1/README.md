# config

## West-MLS

```
en
conf t
hostname WEST-MLS

vlan 100
name West-Clinic

vlan 110
name West-Admin

interface vlan 100
ip address 192.168.10.1 255.255.255.0
no shut
exit

interface vlan 110
ip address 192.168.11.1 255.255.255.0
no shut
exit

interface range GigabitEthernet 0/1-2
switchport trunk encapsulation dot1q
switchport mode trunk
no shut
exit

end
copy running-config startup-config
```

## Central-MLS

```
en
conf t
hostname WEST-MLS

vlan 200
name West-Clinic

vlan 210
name West-Admin

interface vlan 200
ip address 192.168.20.1 255.255.255.0
no shut
exit

interface vlan 210
ip address 192.168.21.1 255.255.255.0
no shut
exit

interface range GigabitEthernet 0/1-2
switchport trunk encapsulation 
switchport mode trunk
no shut
exit

end
copy running-config startup-config
```

## East-MLS

```
en
conf t
hostname East-MLS

vlan 300
name West-Clinic

vlan 310
name West-Admin

interface vlan 300
ip address 192.168.30.1 255.255.255.0
no shut
exit

interface vlan 310
ip address 192.168.31.1 255.255.255.0
no shut
exit

interface range GigabitEthernet 0/1-2
switchport trunk encapsulation 
switchport mode trunk
no shut
exit

end
copy running-config startup-config
```

## NW-Wing Config

```
en
conf t

hostname North-West-Wing-SW

vlan 100
name West-Clinic
exit

vlan 110
name West-Admin
exit

interface GigabitEthernet 0/1
switchport mode trunk
no shut
exit

interface FastEthernet 0/1
switchport mode access
switchport access
vlan 100
no shut
exit

end
copy running-config startup-config
```

## SW-Wing Config

```
en
conf t

hostname South-West-Wing-SW

vlan 100
name West-Clinic
exit

vlan 110
name West-Admin
exit

interface GigabitEthernet 0/2
switchport mode trunk
no shut
exit

interface FastEthernet 0/1
switchport mode access
switchport access
vlan 110
no shut
exit

end
copy running-config startup-config
```
























