# screenshot

did multiple runs as i loaded it on multiple boxes

```
show ip nat translations
```
<img width="696" height="354" alt="{E4370D23-7906-47E1-9DC5-7C4059D524E4}" src="https://github.com/user-attachments/assets/132cd7a0-6572-4261-aa8c-5fe4b754f995" />

# config stuff

## router 1

```
en
conf t
hostname Router1

interface fastethernet 0/0
ip address 192.168.0.1 255.0.0.0
no shutdown
exit

interface serial 0/0/0
ip address 30.0.0.1 255.0.0.0
no shutdown
exit
```

## router 2

```
en
conf t
hostname Router2

interface fastethernet 0/0
ip address 20.0.0.1 255.0.0.0
no shutdown
exit

interface serial 0/0/0
ip address 30.0.0.2 255.0.0.0
no shutdown
exit
```

## routing on router 1

```
ip route 0.0.0.0 0.0.0.0 30.0.0.2
```

## port access translation for router 1

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

