# Lab 6-1 NAT Configuration - Static NAT

## Command examples

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

## Submit screenshot
Screemsjpt pf webpage on 50.0.0.1

<img width="1219" height="297" alt="image" src="https://github.com/user-attachments/assets/cd86941a-bfa1-4152-8a9a-bca67885a873" />

