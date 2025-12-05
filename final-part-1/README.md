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

## vlans

west edge
```
en
conf t
vlan 20
name Clinic
vlan 30
name Guest
vlan 40
name Building Control
vlan 60
name Counseling
exit
```

main central edge
```
en
conf t
vlan 20
name Clinic
vlan 30
name Guest
vlan 40
name Building-Control
exit
```

main data edge
```
en
conf t
vlan 70
name production
vlan 80
name development
vlan 90
name health-records
```

main east edge
```
en
conf t
vlan 20
name Clinic
vlan 30
name Guest
vlan 40
name Building-Control
vlan 50
name psych
```











































