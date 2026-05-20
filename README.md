🌐 Enterprise Network Design — Brothers & Sisters Retail
Designed by: Sechaba Khoboko  
Tool: Cisco Packet Tracer  
Status: ✅ Completed  
Institution: Botho University — BSc Computing (Networking & Software)
---
📋 Project Overview
This project involves the design and full implementation of an enterprise network for Brothers & Sisters Retail, connecting a Head Office and a Branch Office using Cisco Packet Tracer. The network applies real-world enterprise configurations including VLANs, routing protocols, wireless infrastructure, security policies, and network services.
---
🏗️ Network Topology
```
┌─────────────────────────────────┐       WAN Link        ┌─────────────────────────────────┐
│         HEAD OFFICE             │◄─────────────────────►│         BRANCH OFFICE           │
│                                 │                        │                                 │
│  [Core Switch] ── [Router-HO]  │                        │  [Router-BO] ── [Access Switch] │
│       │                         │                        │                      │          │
│  [Access Switches]              │                        │              [End Devices]      │
│       │                         │                        │                                 │
│  [End Devices per VLAN]         │                        │  [Wireless Users via WLC]       │
│  [WLC + APs]                    │                        │                                 │
└─────────────────────────────────┘                        └─────────────────────────────────┘
```
---
📁 Project Structure
```
cisco-enterprise-network/
│
├── README.md                        ← You are here
├── configs/
│   ├── HO-Router-config.txt         ← Head Office Router configuration
│   ├── BO-Router-config.txt         ← Branch Office Router configuration
│   ├── HO-CoreSwitch-config.txt     ← Core Switch configuration
│   ├── HO-AccessSwitch-config.txt   ← Access Switch configuration
│   └── BO-AccessSwitch-config.txt   ← Branch Office Switch configuration
├── docs/
│   ├── IP-Addressing-Table.md       ← Full IP scheme
│   ├── VLAN-Table.md                ← VLAN plan
│   └── Network-Design-Notes.md      ← Design decisions and notes
└── screenshots/
    └── (add your Packet Tracer screenshots here)
```
---
⚙️ Features Implemented
Feature	Description
VLANs	Separate VLANs for Management, Sales, IT, and Guest
Inter-VLAN Routing	Router-on-a-stick configuration
OSPF	Dynamic routing between Head Office and Branch Office
NAT/PAT	Internet access for internal users
DHCP	Automatic IP assignment per VLAN
WLC + RADIUS	Wireless LAN Controller with secure authentication
Port Security	Limits MAC addresses on access ports
DHCP Snooping	Protects against rogue DHCP servers
DAI	Dynamic ARP Inspection to prevent ARP spoofing
ACLs	Access Control Lists to restrict traffic between VLANs
---
🔢 VLAN Plan
VLAN ID	Name	Subnet	Purpose
VLAN 10	Management	192.168.10.0/24	Network devices management
VLAN 20	Sales	192.168.20.0/24	Sales department PCs
VLAN 30	IT	192.168.30.0/24	IT department PCs
VLAN 40	Guest	192.168.40.0/24	Guest wireless users
VLAN 99	Native	—	Trunk native VLAN
---
🌍 IP Addressing Table
Head Office
Device	Interface	IP Address	Subnet Mask	Gateway
HO-Router	Gi0/0.10	192.168.10.1	255.255.255.0	—
HO-Router	Gi0/0.20	192.168.20.1	255.255.255.0	—
HO-Router	Gi0/0.30	192.168.30.1	255.255.255.0	—
HO-Router	Gi0/0.40	192.168.40.1	255.255.255.0	—
HO-Router	Se0/0/0	10.0.0.1	255.255.255.252	—
Core Switch	VLAN 10	192.168.10.2	255.255.255.0	192.168.10.1
Branch Office
Device	Interface	IP Address	Subnet Mask	Gateway
BO-Router	Gi0/0	192.168.50.1	255.255.255.0	—
BO-Router	Se0/0/0	10.0.0.2	255.255.255.252	—
---
🔧 Key Configurations
OSPF Routing
```
router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
```
NAT/PAT
```
ip nat inside source list 1 interface Se0/0/0 overload
access-list 1 permit 192.168.0.0 0.0.255.255
interface Se0/0/0
 ip nat outside
interface Gi0/0
 ip nat inside
```
DHCP (Head Office)
```
ip dhcp pool VLAN20-Sales
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 dns-server 8.8.8.8

ip dhcp excluded-address 192.168.20.1 192.168.20.10
```
Port Security (Access Switch)
```
interface FastEthernet0/1
 switchport mode access
 switchport access vlan 20
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation restrict
 switchport port-security mac-address sticky
```
DHCP Snooping
```
ip dhcp snooping
ip dhcp snooping vlan 10,20,30,40
no ip dhcp snooping information option
interface Gi0/1
 ip dhcp snooping trust
```
ACL Example (Block Guest from IT VLAN)
```
ip access-list extended BLOCK-GUEST
 deny ip 192.168.40.0 0.0.0.255 192.168.30.0 0.0.0.255
 permit ip any any

interface Gi0/0.40
 ip access-group BLOCK-GUEST in
```
---
🛡️ Security Summary
Port Security — prevents unauthorized devices connecting to switches
DHCP Snooping — blocks rogue DHCP servers
DAI (Dynamic ARP Inspection) — prevents ARP poisoning attacks
ACLs — controls traffic flow between VLANs
RADIUS Authentication — secures wireless access via WLC
---
🚀 How to Open This Project
Install Cisco Packet Tracer (free from Cisco NetAcad)
Download the `.pkt` file from this repo (upload your file here)
Open it in Packet Tracer
Use the configs in the `/configs` folder as reference
---
📚 Skills Demonstrated
✅ Enterprise network design and topology planning
✅ VLAN segmentation and Inter-VLAN routing
✅ OSPF dynamic routing protocol
✅ NAT/PAT for internet connectivity
✅ Wireless infrastructure (WLC + RADIUS)
✅ Layer 2 security hardening
✅ Access Control Lists (ACLs)
✅ Network documentation
---
👤 Author
Sechaba Khoboko  
BSc Computing (Networking & Software) — Botho University, Lesotho  
📧 sechaba.khoboko@bothouniversity.com  
🔗 LinkedIn  
🐙 GitHub
