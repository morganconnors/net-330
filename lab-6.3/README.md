# useful setup commands

cc border router

```
en
conf t

access-list 1 permit 192.168.3.0 0.0.0.255
access-list 1 permit 192.168.1.0 0.0.0.255

interface FastEthernet0/0
ip nat inside

interface FastEthernet0/1
ip nat outside

ip nat inside source list 1 interface FastEthernet0/1 overload
```

ireland webserver

```
ip nat inside source static 192.168.7.2 219.93.144.2
show ip nat translations
```


<img width="708" height="341" alt="image" src="https://github.com/user-attachments/assets/9459966d-3dc5-453c-9af3-7978fbbd2b3d" />
