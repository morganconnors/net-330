# TJ4- Tech Journal Assignment 2 

Pools: 

```
enable
conf t

# Configure vlans 100-140
int vlan 100
ip helper-address 10.34.100.2
int vlan 110
ip helper-address 10.34.100.2
int vlan 120
ip helper-address 10.34.100.2
int vlan 130
ip helper-address 10.34.100.2
int vlan 140
ip helper-address 10.34.100.2
```

Console access: 

1. Plug cables into switch and pc/laptop
2. Use putty to connect
3. Serial connection
4. Find COM port
5. Speed is probably 9600

Clear configuration from Cisco Catalyst

```
Switch# write erase
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete

Switch# reload
System configuration has been modified. Save? [yes/no]: no
Proceed with reload? [confirm]
```

Packet tracer notes:

Desktop --> ip configuration is easiest way to config end device IP






































