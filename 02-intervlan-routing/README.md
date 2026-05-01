Inter‑VLAN Routing (Router‑on‑a‑Stick) Lab
🎯 Objective
Configure a router to enable communication between VLANs using subinterfaces (Router‑on‑a‑Stick). Devices in VLAN 10 and VLAN 20 should be able to ping each other.

🧰 Tools Used
Cisco Packet Tracer

1 Cisco 2960 Switch

1 Router (ISR or similar)

2 PCs

🗺️ Topology
See topology.png in this folder.

Code
PC0 ---- Fa0/1     Switch     Fa0/24 ---- Router G0/0/0
PC1 ---- Fa0/2
📝 VLANs & IP Scheme
VLAN Table
VLAN	Name	Subnet	Gateway
10	Sales	192.168.10.0/24	192.168.10.1
20	HR	192.168.20.0/24	192.168.20.1


PC IP Assignments
PC0 (VLAN 10)

IP: 192.168.10.10

Mask: 255.255.255.0

Gateway: 192.168.10.1

PC1 (VLAN 20)

IP: 192.168.20.10

Mask: 255.255.255.0

Gateway: 192.168.20.1

🔧 Configuration Steps
1. Switch Configuration
Create VLANs
Code
vlan 10
name Sales
vlan 20
name HR
Assign Access Ports
Code
interface fa0/1
switchport mode access
switchport access vlan 10

interface fa0/2
switchport mode access
switchport access vlan 20
Configure Trunk to Router
Code
interface fa0/24
switchport mode trunk
switchport trunk allowed vlan 10,20
2. Router Configuration (Router‑on‑a‑Stick)
Note: This router uses interface g0/0/0.

Create Subinterfaces
Code
interface g0/0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface g0/0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
Enable the Physical Interface
Code
interface g0/0/0
no shutdown
✔️ Verification
On the switch:
Code
show vlan brief
show interfaces trunk
On the router:
Code
show ip interface brief
Testing from PCs
PC0 →

Ping 192.168.10.1

Ping 192.168.20.1

Ping 192.168.20.10

PC1 →

Ping 192.168.20.1

Ping 192.168.10.1

Ping 192.168.10.10

All pings should succeed.

📘 What I Learned
How inter‑VLAN routing works

How router subinterfaces operate

How trunking carries multiple VLANs

Why VLANs require a Layer 3 device to communicate

📂 Files Included
02-intervlan-routing.pkt

topology.png

configs.txt
