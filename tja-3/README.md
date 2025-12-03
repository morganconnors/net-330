# TJ6- Tech Journal Assignment 3 

Setting NAT interfaces

```
ip route 30.0.0.0 255.0.0.0 20.0.0.1
```

and

```
int fa0/0
ip nat inside
exit
int serial 0/0/0
ip nat outside
exit
```

and

```
ip nat inside source static 10.0.0.2 50.0.0.1
```

Commands to configure PAT

```
interface fastEthernet 0/0
ip nat inside
exit

interface serial 0/0/0
ip nat outside
exit

ip nat inside source static 10.0.0.2 50.0.0.1

ip nat pool test 30.0.0.120 30.0.0.120 netmask 255.0.0.0

access-list 1 permit 192.168.0.0 0.0.0.255

ip nat inside source list 1 pool test overload
```













