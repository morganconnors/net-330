# Techjournal Assignment 1

Interfaces: 

```
Switch> enable
Switch# configure terminal
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# exit
Switch(config)# exit
Switch# disable
Switch>
```

VLANs:

```
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name test
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# name test2
Switch(config-vlan)# exit
```

Access ports: 

```
Switch(config)# interface gigabitethernet 0/5
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

Trunk ports:

```
Switch(config)# interface gigabitethernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# exit
```

Inteface ranges:  

```
Switch(config)# interface range gigabitethernet 0/1-12
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit
```

















