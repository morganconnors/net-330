# screenshots

totally did not goof my config and have to fix it before getting screenshots

ping from champ server to middle server   
<img width="949" height="505" alt="image" src="https://github.com/user-attachments/assets/ea33f5de-a431-4957-a1f8-f92d779d75b0" />

champ show ipsec  
<img width="684" height="635" alt="image" src="https://github.com/user-attachments/assets/76ff6780-3054-4364-9d71-2cf645a8cde3" />

middle show ipsec  
<img width="684" height="554" alt="image" src="https://github.com/user-attachments/assets/887d4f2d-ef4f-43e0-bd54-643d1ea783ec" />


# configs

need to configure routers

champlain router
```
en 
conf t

int fa0/0
ip address 216.93.144.2 255.255.255.0
no shut 

int fa0/1
ip address 172.16.84.1 255.255.255.0
no shut 
exit 

ip route 0.0.0.0 0.0.0.0 216.93.144.1
exit
copy run start
```


middlebury router
```
en
conf t

int fa0/0
ip address 140.230.18.2 255.255.255.0
no shut 

int fa0/1
ip address 192.168.25.1 255.255.255.0
no shut 
exit

ip route 0.0.0.0 0.0.0.0 140.230.18.1
exit
copy run start
```

vtel
```
en
conf t

int fa0/0
ip address 216.93.144.1 255.255.255.0
no shut 

int fa0/1
ip address 140.230.18.1 255.255.255.0
no shut

exit
exit
copy run start
```

ok now config end devices

champ server   
<img width="704" height="306" alt="image" src="https://github.com/user-attachments/assets/2ef3418c-a65e-4ba9-8176-dec716f471a3" />


middlebury server   
<img width="704" height="306" alt="image" src="https://github.com/user-attachments/assets/a4ed22ae-76e2-44a6-9118-ea80c8a25c2b" />



ok now IKE configs

champlain roouter 
```
en
conf t

access-list 110 permit ip 172.16.84.0 0.0.0.255 192.168.25.0 0.0.0.255

encryption, pre-shared authentication, and DH group 5
crypto isakmp policy 10
encryption aes 256
authentication pre-share
group 5
exit
crypto isakmp key NET330 address 140.230.18.2

crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac

crypto map VPN-MAP 10 ipsec-isakmp
description VPN connection to Middlebury
set peer 140.230.18.2
set transform-set VPN-SET
match address 110
exit

int fa0/0
crypto map VPN-MAP
exit
exit
copy run start
```

middlebury router
```
en
conf t

access-list 110 permit ip 192.168.25.0 0.0.0.255 172.16.84.0 0.0.0.255
 
crypto isakmp policy 10
encryption aes 256
authentication pre-share
group 5
exit

crypto isakmp key NET330 address 216.93.144.2
crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac
crypto map VPN-MAP 10 ipsec-isakmp
description VPN connection to Champlain
set peer 216.93.144.2
set transform-set VPN-SET
match address 110
exit

int fa0/0
crypto map VPN-MAP
exit
exit
copy run start
```












