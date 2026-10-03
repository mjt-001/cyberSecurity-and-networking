# Project 1: Secure Coffee Shop SOHO Network Architecture

## Executive Summary

This project delivers a complete SOHO (Small Office/Home Office) network architecture for a commercial coffee shop using Cisco Packet Tracer. The design implements dynamic IP addressing via Cisco IOS DHCP, Router-on-a-Stick (ROAS) inter-VLAN routing, and 802.1Q trunking. Network security is enforced through custom extended Access Control Lists (ACLs) that isolate point-of-sale (POS) systems and management infrastructure from public guest Wi-Fi traffic while permitting unrestricted internet access.

## Network Architecture & Key Features

- **Multi-VLAN Segmentation:** Segregates administrative management, operational POS terminals, and customer wireless devices into distinct layer 2 broadcast domains.
- **Router-on-a-Stick Inter-VLAN Routing:** Utilizes 802.1Q encapsulation subinterfaces on R1-Gateway for centralized traffic routing across VLANs.
- **Automated Address Assignment:** Features dedicated Cisco IOS DHCP address pools per subnet for seamless client onboardings.
- **Guest Traffic Isolation:** Applies inbound extended ACLs at the gateway boundary to enforce strict PCI-DSS-aligned traffic separation.

## IP Addressing & Subnetting Plan (VLSM)

| Network / Function | VLAN ID | Subnet / CIDR  | Subnet Mask | Usable Host Range | Default Gateway | Purpose |
| -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| Management / Native | 10     | 192.168.1.0/27     | 255.255.255.224     | 192.168.1.2 - 192.168.1.30     | 192.168.1.1     | Switch SVI, AP IP, Router Subinterface     |
| Staff & POS Network    | 20     | 192.168.1.32/27     | 255.255.255.224     | 192.168.1.34 - 192.168.1.62     | 192.168.1.33     | Registers, Manager PC, Staff Workstations     |
| Guest Wi-Fi Network    | 30     | 192.168.1.64/26     | 255.255.255.192     | 192.168.1.66 - 192.168.1.126     | 192.168.1.65     | Public Laptops, Tablets, Smartphones     |


## Device Configuration Scripts
### 1. Switch Configuration (SW1-Core)
```cisco
enable
configure terminal
hostname SW1-Core
no ip domain-lookup

! Create VLANs
vlan 10
 name Management_Native
vlan 20
 name Staff_POS
vlan 30
 name Guest_WiFi
exit

! Access Ports for Staff and POS
interface range FastEthernet 0/1 - 3
 switchport mode access
 switchport access vlan 20
 description Connected to Staff-PC, Manager-PC, POS-Register
 no shutdown
exit

! Access Port for Access Point
interface GigabitEthernet 0/2
 switchport mode access
 switchport access vlan 30
 description Connected to AP-Staff-Guest
 no shutdown
exit

! Trunk Port to Router
interface GigabitEthernet 0/1
 switchport mode trunk
 switchport trunk native vlan 10
 switchport trunk allowed vlan 10,20,30
 description 802.1Q Trunk Link to R1-Gateway
 no shutdown
exit

! Switch Management SVI
interface vlan 10
 ip address 192.168.1.2 255.255.255.224
 description Switch Management Interface
 no shutdown
exit

ip default-gateway 192.168.1.1
end
write memory
```

### 2. Router & DHCP Configuration (R1-Gateway)
```
enable
configure terminal
hostname R1-Gateway
no ip domain-lookup

! Physical Trunk Interface
interface GigabitEthernet0/0/1
 description Trunk Link to SW1-Core
 no shutdown
exit

! Subinterfaces (ROAS)
interface GigabitEthernet0/0/1.10
 description Management and Native VLAN
 encapsulation dot1Q 10 native
 ip address 192.168.1.1 255.255.255.224
exit

interface GigabitEthernet0/0/1.20
 description Staff and POS Terminals
 encapsulation dot1Q 20
 ip address 192.168.1.33 255.255.255.224
exit

interface GigabitEthernet0/0/1.30
 description Public Guest Wi-Fi Network
 encapsulation dot1Q 30
 ip address 192.168.1.65 255.255.255.192
exit

! DHCP Exclusions
ip dhcp excluded-address 192.168.1.1 192.168.1.3
ip dhcp excluded-address 192.168.1.33
ip dhcp excluded-address 192.168.1.65

! DHCP Pools
ip dhcp pool STAFF_POOL
 network 192.168.1.32 255.255.255.224
 default-router 192.168.1.33
 dns-server 8.8.8.8
exit

ip dhcp pool GUEST_POOL
 network 192.168.1.64 255.255.255.192
 default-router 192.168.1.65
 dns-server 8.8.8.8
exit
```
### 3. Security Extended ACL Implementation (R1-Gateway)
```
! Extended ACL Definition
ip access-list extended BLOCK_GUEST_TO_INTERNAL
 remark Deny Guest access to Staff POS network
 deny ip 192.168.1.64 0.0.0.63 192.168.1.32 0.0.0.31
 remark Deny Guest access to Infrastructure Management network
 deny ip 192.168.1.64 0.0.0.63 192.168.1.0 0.0.0.31
 remark Permit outbound Internet traffic for Guests
 permit ip 192.168.1.64 0.0.0.63 any
exit

! Apply Inbound on Guest Subinterface
interface GigabitEthernet0/0/1.30
 ip access-group BLOCK_GUEST_TO_INTERNAL in
exit
end
write memory
```

## Verification & Testing Evidence
### Test Case 1: VLAN 30 Dynamic Addressing & Default Gateway Connectivity
- **Goal:** Verify guest devices automatically acquire valid IP configuration and reach their local gateway.
- **Command:** ping 192.168.1.65 from Guest-Laptop-1
- **Result:** SUCCESS (4/4 packets received, 0% loss).

### Test Case 2: ACL Enforcement & POS Traffic Isolation
- **Goal:** Confirm guest wireless clients are explicitly blocked from accessing internal POS infrastructure.
- **Command:** ping 192.168.1.34 from Guest-Laptop-1
- **Result:** BLOCKED (Destination Host Unreachable).

### Test Case 3: Access Control List Match Counters
```
R1-Gateway# show access-lists BLOCK_GUEST_TO_INTERNAL
Extended IP access list BLOCK_GUEST_TO_INTERNAL
    10 deny ip 192.168.1.64 0.0.0.63 192.168.1.32 0.0.0.31 (4 matches)
    20 deny ip 192.168.1.64 0.0.0.63 192.168.1.0 0.0.0.31
    30 permit ip 192.168.1.64 0.0.0.63 any (8 matches)
```

## Lessons Learned & Troubleshooting
- **Trunk Link Operational Status:** Resolved an inactive trunk status on SW1-Core by executing no shutdown on R1-Gateway interface Gig0/0/1. Catalyst 2960 trunk links require physical layer up/up status on both line endpoints to transition to active 802.1Q trunking mode.
- **Subnet Boundary Precision:** Enforced accurate wildcard masks (0.0.0.31 for /27, 0.0.0.63 for /26) within ACL statements to prevent unintended blockages across adjacent subnets.

## How to Run This Project
1. Download and install Cisco Packet Tracer (v8.0 or later).
2. Clone this repository:
```
git clone https://github.com/your-username/coffee-shop-soho-network.git
```
3. Open the file topology/coffee_shop_SOHO_network.pkt in Packet Tracer.
4. Open device command prompts to verify DHCP leases, ping paths, and ACL blocks.