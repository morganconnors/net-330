# Lab 3-3: Techjournal
## Config DHCP Server

I enabled DHCP and set up the DHCP pools for DHCP-01.

<img width="800" height="713" alt="image" src="https://github.com/user-attachments/assets/ec0605f3-d6ae-4298-a000-a862b9c05c59" />

## Testing DHCP

DHCP has been turned on for the new computer and it is able to succesfully get an IP address.

<img width="1004" height="367" alt="image" src="https://github.com/user-attachments/assets/4867e9ad-3445-401d-8c9e-7759abd6c1d1" />

## Configure DHCP Relay

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

## Configure clients to use DHCP

Workstations/laptops/etc have been configured to use DHCP and are able to get addresses.

Ping test:

<img width="1604" height="706" alt="image" src="https://github.com/user-attachments/assets/9eec1faa-1510-4de4-acae-555bdeb6672a" />
