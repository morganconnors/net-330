# walkthrough

test ping 

<img width="411" height="251" alt="image" src="https://github.com/user-attachments/assets/02b76ba5-bd76-4274-8447-0ecb87585846" />

note: apparently there is a password you will need - `cisco`

configure router 3
```
en
conf t

ip access-list standard STND-1
deny 192.168.11.0 0.0.0.255
permit any
exit

int serial 0/0/0
ip access-group STND-1 in

exit
copy run start
```

pc3 can no longer reach pc5
<img width="697" height="623" alt="image" src="https://github.com/user-attachments/assets/4ca62e00-ff06-44bb-8db8-5c5b2ebfcafc" />

configure router 2
```
en
conf t
ip access-list extended EXTEND-1
deny ip 192.168.10.0 0.0.0.255 host 200.200.200.1
permit ip any any
exit

int Serial0/0/0
ip access-group EXTEND-1 out

exit
exit
copy run start
```

test config

<img width="423" height="523" alt="image" src="https://github.com/user-attachments/assets/ce737943-f32c-4660-b5fa-8c223d3ae19d" />

# bonus stuff

block isp to file server r1
```
en 
conf t

ip access-list extended Bonus1
deny ip 200.200.200.0 0.0.0.255 host 192.168.20.210
exit

interface Serial 0/2/0
ip access-group Bonus1 in

exit
exit
copy run start
```

test w/ name

<img width="494" height="291" alt="image" src="https://github.com/user-attachments/assets/7173b960-e9ea-46cd-b3fc-4f038d760853" />

next bonus
```
en
conf t

ip access-list extended Bonus2
permit tcp any host 192.168.20.200 eq 25
permit tcp any host 192.168.20.200 eq 110
permit tcp any host 192.168.20.200 eq 143
deny ip any host 192.168.20.200
exit
int fa0/0
ip access-group Bonus2 in

exit
exit
copy run start
```

sleepy time
