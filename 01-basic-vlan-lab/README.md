Basic VLAN Lab
🎯 Objective
Create two VLANs on a single switch, assign access ports, and verify that devices in different VLANs cannot communicate without routing.

🧰 Tools Used
Cisco Packet Tracer

1 Cisco 2960 Switch

2 PCs

🗺️ Topology
See topology.png in this folder.

Code
PC0 ---- Fa0/1   Switch   Fa0/2 ---- PC1
📝 VLANs
VLAN 10 – Sales

VLAN 20 – HR

🔧 Configuration Steps
1. Create VLANs
Code
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config)# vlan 20
Switch(config-vlan)# name HR
2. Assign Ports to VLANs
PC0 → VLAN 10

Code
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
PC1 → VLAN 20

Code
Switch(config)# interface fa0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
3. Verification
Code
Switch# show vlan brief
Switch# show interfaces status
4. Testing
PC0 can ping itself

PC1 can ping itself

PC0 cannot ping PC1

PC1 cannot ping PC0

This is expected because there is no router.

📘 What I Learned
How to create VLANs

How to assign switchports to VLANs

How VLANs isolate broadcast domains

Why devices in different VLANs cannot communicate without routing

📂 Files Included
01-basic-vlan-lab.pkt

topology.png

configs.txt
