alternative btw

# screenshot

central admin is on south-central switch and central pc is on north-central switch

<img width="978" height="881" alt="{4DA5F986-E7FC-4160-A973-0CDD75DB77DE}" src="https://github.com/user-attachments/assets/a2000400-c9b9-4328-8c06-35bb05d330ff" />

# table

<img width="500" height="212" alt="image" src="https://github.com/user-attachments/assets/c37dea26-2dd6-479e-af5e-19c0bbaaa418" />

# config

## West-MLS

```
en
conf t

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

interface range fa0/1-2
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

interface range fa0/1-2
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

interface range fa0/1-2
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

vlan 100
name West-Clinic
exit

vlan 110
name West-Admin
exit

interface fa0/2
switchport mode trunk
no shut
exit

interface fa0/1
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

vlan 100
name West-Clinic
exit

vlan 110
name West-Admin
exit

interface fa0/2
switchport mode trunk
no shut
exit

interface fa0/1
switchport mode access
switchport access
vlan 110
no shut
exit

end
copy running-config startup-config
```
























