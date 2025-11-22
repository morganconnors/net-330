# table

<img width="672" height="158" alt="image" src="https://github.com/user-attachments/assets/3ff904e6-6365-4869-b125-20e5778f2e7d" />

# configs

datacenter router
```
en
conf t
hostname Morgan-DataCenter-Router3
interface GigabitEthernet0/0
ip address 10.1.1.22 255.255.255.252
no shutdown
interface GigabitEthernet0/1
ip address 10.1.1.33 255.255.255.252
no shutdown
interface GigabitEthernet0/2
ip address 10.1.1.2 255.255.255.248
no shutdown
exit
exit 
copy run start
```

border router
```
en 
conf t
hostname Morgan-Border-Router1
interface GigabitEthernet0/0
ip address 10.1.1.1 255.255.255.248
no shutdown
exit
exit
copy run start 
```

east router
```
en
conf t
hostname Morgan-East-Router2
interface GigabitEthernet0/0
ip address 10.1.1.21 255.255.255.252
no shutdown
interface GigabitEthernet0/1
ip address 10.1.20.1 255.255.255.0
no shutdown
exit
exit
copy run start
```

west router
```
en 
conf t
hostname Morgan-West-Router4
interface GigabitEthernet0/0
ip address 10.1.1.34 255.255.255.252
no shutdown
interface GigabitEthernet0/1
ip address 10.1.40.1 255.255.255.0
no shutdown
exit
exit
copy run start
```

working:  
<img width="602" height="486" alt="image" src="https://github.com/user-attachments/assets/da811901-5374-4f67-b657-45f2733f96b2" />


# ospf

datacenter router
```
en
conf t
router ospf 1
network 10.1.1.0 0.0.0.7 area 0
network 10.1.1.20 0.0.0.3 area 0
network 10.1.1.32 0.0.0.3 area 0
exit
exit
copy run start
```

border router
```
en 
conf t
router ospf 1
network 10.1.1.0 0.0.0.7 area 0
exit
exit
copy run start
```

east router
```
en
conf t
router ospf 1
network 10.1.1.20 0.0.0.3 area 0
network 10.1.20.0 0.0.0.255 area 0
exit
exit
copy run start
```

west router
```
en
conf t
router ospf 1
network 10.1.1.32 0.0.0.3 area 0
network 10.1.40.0 0.0.0.255 area 0
exit
exit
copy run start
```


# deliverables

## deliverable 1
ping from west to east

<img width="933" height="606" alt="image" src="https://github.com/user-attachments/assets/9cdf88ea-4e93-43ad-9e24-8ff2f2c61125" />

## deliverable 2
datacenter router

<img width="702" height="679" alt="image" src="https://github.com/user-attachments/assets/5591b688-4182-428b-bf3f-331a884ae5fc" />

## deliverable 2
east router

<img width="702" height="679" alt="image" src="https://github.com/user-attachments/assets/07a1a21d-1a33-435b-95f5-02d2d55c4614" />

## deliverable 2
west router

<img width="699" height="683" alt="image" src="https://github.com/user-attachments/assets/8cca32d7-c462-4739-992d-e4500e20f59d" />

