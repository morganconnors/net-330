# screenshots

## ipv6 show route on 3 routers

cc roouter  
<img width="699" height="520" alt="image" src="https://github.com/user-attachments/assets/7f369da0-69aa-48ca-b8fd-357438d926e7" />

middle router  
<img width="699" height="520" alt="image" src="https://github.com/user-attachments/assets/21652966-e6d7-4777-9bf9-2a7e954fc5e9" />

vtel router  
<img width="699" height="520" alt="image" src="https://github.com/user-attachments/assets/180b8262-7ec7-443f-afc5-abb78913e3d3" />

## ping test

<img width="1036" height="646" alt="image" src="https://github.com/user-attachments/assets/d96de14b-cf87-458a-ad09-1456cb0aa487" />

# configs

cc router
```
en
conf t
ipv6 general-prefix cc-pre 2620:E4:C000::/64
int fa0/1
ipv6 address 2620:E4:C000::1/64
no shut 
exit
ipv6 unicast-routing
exit
copy run start
```

turn on auto config for ipv6   
<img width="699" height="520" alt="image" src="https://github.com/user-attachments/assets/ecf95ba5-3ef3-4c83-ae68-3d91d3d7f7ea" />

middlebury router
```
en 
conf t
ipv6 general-prefix middle-pre 2001:1890:139D::/64
int fa0/1
ipv6 address 2001:1890:139D::/64
no shut
exit
ipv6 unicast-routing
exit
copy run start
```

turn on auto config for ipv6    
<img width="699" height="520" alt="image" src="https://github.com/user-attachments/assets/2f4406e7-0dff-4664-b6e3-31a7b27d9be7" />

vtel router
```
en
conf t
ipv6 unicast-routing
int fa0/0
ipv6 address 1800:2200:185::/64 eui-64
no shut
exit
do show ipv6 interface brief
exit
copy run start
```

now set autoconfig for routers

cc router
```
en
conf t
int fa0/0
ipv6 address autoconfig
no shut
exit
do show ipv6 interface brief
exit
copy run start
```

middlebury router
```
en
conf t
int fa0/0
ipv6 address autoconfig
no shut
exit
do show ipv6 interface brief
exit
copy run start
```

ok now rip

cc router
```
en
conf t
int fa0/0
ipv6 rip process1 enable
int fa0/1
ipv6 rip process1 enable
exit
exit
copy run start
```

middlebury router
```
en 
conf t
int fa0/0
ipv6 rip process1 enable
int fa0/1
ipv6 rip process1 enable
exit
exit
copy run start
```

vtel router
```
en 
conf t
int fa0/0
ipv6 rip process1 enable
exit
exit
copy run start
```

