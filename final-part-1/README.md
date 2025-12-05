# final part 1

## network table

### Medical Center Network - Subnet/VLAN Table

#### Main Campus (East, Central, West Buildings)

| VLAN ID | VLAN Name | Network Address | Subnet Mask | Default Gateway | Notes |
|---------|-----------|-----------------|-------------|-----------------|-------|
| 10 | Backbone | 172.16.0.0/25 | 255.255.255.128 | 172.16.0.1 | Distribution routers (128 IPs available) |
| 20 | Clinic | 172.16.1.0/22 | 255.255.252.0 | 172.16.1.1 | Trunked between buildings (1024 IPs available) |
| 30 | Guest | 172.16.5.0/22 | 255.255.252.0 | 172.16.5.1 | Trunked between buildings (1024 IPs available) |
| 40 | Building Controls | 172.16.9.0/23 | 255.255.254.0 | 172.16.9.1 | Trunked between buildings (512 IPs available) |
| 50 | Psych (East) | 172.16.11.0/25 | 255.255.255.128 | 172.16.11.1 | East only - East Distribution Router gateway |
| 60 | Counseling (West) | 172.16.11.128/25 | 255.255.255.128 | 172.16.11.129 | West only - West Distribution Router gateway |
| 70 | Production Servers | 172.16.12.0/25 | 255.255.255.128 | 172.16.12.1 | Data Center - Central |
| 80 | Development Servers | 172.16.12.128/25 | 255.255.255.128 | 172.16.12.129 | Data Center - Central |
| 90 | Health Record Servers | 172.16.13.0/25 | 255.255.255.128 | 172.16.13.1 | Data Center - Central |

#### Community Hospital South

| VLAN ID | VLAN Name | Network Address | Subnet Mask | Default Gateway | Notes |
|---------|-----------|-----------------|-------------|-----------------|-------|
| 100 | Clinic (South) | 172.16.20.0/25 | 255.255.255.128 | 172.16.20.1 | South multi-layer switch gateway |
| 110 | Guest (South) | 172.16.20.128/25 | 255.255.255.128 | 172.16.20.129 | South multi-layer switch gateway |
| 120 | Building Controls (South) | 172.16.21.0/25 | 255.255.255.128 | 172.16.21.1 | South multi-layer switch gateway |

#### Community Hospital North

| VLAN ID | VLAN Name | Network Address | Subnet Mask | Default Gateway | Notes |
|---------|-----------|-----------------|-------------|-----------------|-------|
| 200 | Clinic (North) | 172.16.30.0/25 | 255.255.255.128 | 172.16.30.1 | North multi-layer switch gateway |
| 210 | Guest (North) | 172.16.30.128/25 | 255.255.255.128 | 172.16.30.129 | North multi-layer switch gateway |
| 220 | Building Controls (North) | 172.16.31.0/25 | 255.255.255.128 | 172.16.31.1 | North multi-layer switch gateway |

---

# configs

## Main Switch

```
enable
configure terminal
hostname Main Switch

! Create all VLANs
vlan 10
 name Backbone
exit

vlan 20
 name Clinic
exit

vlan 30
 name Guest
exit

vlan 40
 name Building-Controls
exit

vlan 50
 name Psych
exit

vlan 60
 name Counseling
exit

vlan 70
 name Production-Servers
exit

vlan 80
 name Development-Servers
exit

vlan 90
 name Health-Records
exit

! Configure trunk ports to distribution switches
interface FastEthernet0/1
 description Trunk to Main West
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,60
 no shutdown
exit

interface FastEthernet0/2
 description Trunk to Main Central
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,70,80,90
 no shutdown
exit

interface FastEthernet0/3
 description Trunk to Main East
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
 no shutdown
exit

end
write memory
```

## Main Central

```
enable
configure terminal
hostname Main Central

! Enable IP routing
ip routing

! Create VLANs
vlan 10
 name Backbone
exit

vlan 20
 name Clinic
exit

vlan 30
 name Guest
exit

vlan 40
 name Building-Controls
exit

vlan 70
 name Production-Servers
exit

vlan 80
 name Development-Servers
exit

vlan 90
 name Health-Records
exit

! Configure VLAN interfaces (SVIs)
interface Vlan10
 description Backbone VLAN
 ip address 172.16.0.1 255.255.255.128
 no shutdown
exit

interface Vlan20
 description Clinic VLAN
 ip address 172.16.1.1 255.255.252.0
 no shutdown
exit

interface Vlan30
 description Guest VLAN
 ip address 172.16.5.1 255.255.252.0
 no shutdown
exit

interface Vlan40
 description Building Controls VLAN
 ip address 172.16.9.1 255.255.254.0
 no shutdown
exit

interface Vlan70
 description Production Servers VLAN
 ip address 172.16.12.1 255.255.255.128
 no shutdown
exit

interface Vlan80
 description Development Servers VLAN
 ip address 172.16.12.129 255.255.255.128
 no shutdown
exit

interface Vlan90
 description Health Records VLAN
 ip address 172.16.13.1 255.255.255.128
 no shutdown
exit

! Configure trunk port to Core Switch
interface FastEthernet0/1
 description Trunk to Main Switch
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,70,80,90
 no shutdown
exit

! Configure trunk port to Central Edge Switch
interface FastEthernet0/2
 description Trunk to Main Central Edge
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 20,30,40
 no shutdown
exit

! Configure trunk port to Data Center Edge Switch
interface FastEthernet0/3
 description Trunk to Main Data Edge
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 70,80,90
 no shutdown
exit

! Configure OSPF
router ospf 1
 router-id 1.1.1.1
 log-adjacency-changes
 area 0 authentication message-digest
 network 172.16.0.0 0.0.0.127 area 0
 network 172.16.1.0 0.0.3.255 area 0
 network 172.16.5.0 0.0.3.255 area 0
 network 172.16.9.0 0.0.1.255 area 0
 network 172.16.12.0 0.0.0.127 area 0
 network 172.16.12.128 0.0.0.127 area 0
 network 172.16.13.0 0.0.0.127 area 0
exit

! Apply OSPF authentication to VLAN interfaces
interface Vlan10
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan20
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan30
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan40
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan70
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan80
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan90
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

end
write memory
```

## Main East

```
enable
configure terminal
hostname Main East

! Enable IP routing
ip routing

! Create VLANs
vlan 10
 name Backbone
exit

vlan 20
 name Clinic
exit

vlan 30
 name Guest
exit

vlan 40
 name Building-Controls
exit

vlan 50
 name Psych
exit

! Configure VLAN interfaces (SVIs)
interface Vlan10
 description Backbone VLAN
 ip address 172.16.0.2 255.255.255.128
 no shutdown
exit

interface Vlan20
 description Clinic VLAN
 ip address 172.16.1.2 255.255.252.0
 no shutdown
exit

interface Vlan30
 description Guest VLAN
 ip address 172.16.5.2 255.255.252.0
 no shutdown
exit

interface Vlan40
 description Building Controls VLAN
 ip address 172.16.9.2 255.255.254.0
 no shutdown
exit

interface Vlan50
 description Psych VLAN - East Gateway
 ip address 172.16.11.1 255.255.255.128
 no shutdown
exit

! Configure trunk port to Core Switch
interface FastEthernet0/1
 description Trunk to Main Switch
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
 no shutdown
exit

! Configure trunk port to East Edge Switch
interface FastEthernet0/2
 description Trunk to Main East Edge
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 20,30,40,50
 no shutdown
exit

! Configure OSPF
router ospf 1
 router-id 2.2.2.2
 log-adjacency-changes
 area 0 authentication message-digest
 network 172.16.0.0 0.0.0.127 area 0
 network 172.16.1.0 0.0.3.255 area 0
 network 172.16.5.0 0.0.3.255 area 0
 network 172.16.9.0 0.0.1.255 area 0
 network 172.16.11.0 0.0.0.127 area 0
exit

! Apply OSPF authentication to VLAN interfaces
interface Vlan10
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan20
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan30
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan40
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan50
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

end
write memory
```

## Main West

```
enable
configure terminal
hostname Main West

! Enable IP routing
ip routing

! Create VLANs
vlan 10
 name Backbone
exit

vlan 20
 name Clinic
exit

vlan 30
 name Guest
exit

vlan 40
 name Building-Controls
exit

vlan 60
 name Counseling
exit

! Configure VLAN interfaces (SVIs)
interface Vlan10
 description Backbone VLAN
 ip address 172.16.0.3 255.255.255.128
 no shutdown
exit

interface Vlan20
 description Clinic VLAN
 ip address 172.16.1.3 255.255.252.0
 no shutdown
exit

interface Vlan30
 description Guest VLAN
 ip address 172.16.5.3 255.255.252.0
 no shutdown
exit

interface Vlan40
 description Building Controls VLAN
 ip address 172.16.9.3 255.255.254.0
 no shutdown
exit

interface Vlan60
 description Counseling VLAN - West Gateway
 ip address 172.16.11.129 255.255.255.128
 no shutdown
exit

! Configure trunk port to Core Switch
interface FastEthernet0/1
 description Trunk to Main Switch
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,60
 no shutdown
exit

! Configure trunk port to West Edge Switch
interface FastEthernet0/2
 description Trunk to Main West Edge
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 20,30,40,60
 no shutdown
exit

! Configure OSPF
router ospf 1
 router-id 3.3.3.3
 log-adjacency-changes
 area 0 authentication message-digest
 network 172.16.0.0 0.0.0.127 area 0
 network 172.16.1.0 0.0.3.255 area 0
 network 172.16.5.0 0.0.3.255 area 0
 network 172.16.9.0 0.0.1.255 area 0
 network 172.16.11.128 0.0.0.127 area 0
exit

! Apply OSPF authentication to VLAN interfaces
interface Vlan10
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan20
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan30
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan40
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

interface Vlan60
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 cisco123
exit

end
write memory
```

## Main West Edge

```
enable
configure terminal
hostname Main West Edge

! Create VLANs
vlan 20
 name Clinic
exit

vlan 30
 name Guest
exit

vlan 40
 name Building-Controls
exit

vlan 60
 name Counseling
exit

! Configure trunk port to Main West Distribution
interface FastEthernet0/1
 description Trunk to Main West
 switchport mode trunk
 switchport trunk allowed vlan 20,30,40,60
 no shutdown
exit

! Configure access port for Counseling VLAN
interface FastEthernet0/2
 description Access port - Counseling VLAN
 switchport mode access
 switchport access vlan 60
 spanning-tree portfast
 no shutdown
exit

! Configure access port for Clinic VLAN
interface FastEthernet0/3
 description Access port - Clinic VLAN
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 no shutdown
exit

end
write memory
```

## Main central edge

```
enable
configure terminal
hostname Main Central Edge

! Create VLANs
vlan 20
 name Clinic
exit

vlan 30
 name Guest
exit

vlan 40
 name Building-Controls
exit

! Configure trunk port to Main Central Distribution
interface FastEthernet0/1
 description Trunk to Main Central
 switchport mode trunk
 switchport trunk allowed vlan 20,30,40
 no shutdown
exit

! Configure access port for Clinic VLAN
interface FastEthernet0/2
 description Access port - Clinic VLAN
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 no shutdown
exit

end
write memory
```

## Main data edge

```
enable
configure terminal
hostname Main Data Edge

! Create VLANs
vlan 70
 name Production-Servers
exit

vlan 80
 name Development-Servers
exit

vlan 90
 name Health-Records
exit

! Configure trunk port to Main Central Distribution
interface FastEthernet0/1
 description Trunk to Main Central
 switchport mode trunk
 switchport trunk allowed vlan 70,80,90
 no shutdown
exit

! Configure access port for Production Servers VLAN
interface FastEthernet0/2
 description Access port - Production Servers VLAN
 switchport mode access
 switchport access vlan 70
 spanning-tree portfast
 no shutdown
exit

end
write memory
```

## main east edge

```
enable
configure terminal
hostname Main East Edge

! Create VLANs
vlan 20
 name Clinic
exit

vlan 30
 name Guest
exit

vlan 40
 name Building-Controls
exit

vlan 50
 name Psych
exit

! Configure trunk port to Main East Distribution
interface FastEthernet0/1
 description Trunk to Main East
 switchport mode trunk
 switchport trunk allowed vlan 20,30,40,50
 no shutdown
exit

! Configure access port for Psych VLAN
interface FastEthernet0/2
 description Access port - Psych VLAN
 switchport mode access
 switchport access vlan 50
 spanning-tree portfast
 no shutdown
exit

end
write memory
```

## workstations

WORKSTATION: Counseling West (connected to Main West Edge Fa0/2)
---------------------------------------------------------------
IP Address: 172.16.11.130
Subnet Mask: 255.255.255.128
Default Gateway: 172.16.11.129

WORKSTATION: Clinic West (connected to Main West Edge Fa0/3)
---------------------------------------------------------------
IP Address: 172.16.1.10
Subnet Mask: 255.255.252.0
Default Gateway: 172.16.1.1

WORKSTATION: Clinic Central (connected to Main Central Edge Fa0/2)
---------------------------------------------------------------
IP Address: 172.16.1.11
Subnet Mask: 255.255.252.0
Default Gateway: 172.16.1.1

WORKSTATION: Production Data Center (connected to Main Data Edge Fa0/2)
---------------------------------------------------------------
IP Address: 172.16.12.10
Subnet Mask: 255.255.255.128
Default Gateway: 172.16.12.1

WORKSTATION: Psych West (connected to Main East Edge Fa0/2)
---------------------------------------------------------------
IP Address: 172.16.11.10
Subnet Mask: 255.255.255.128
Default Gateway: 172.16.11.1


















































