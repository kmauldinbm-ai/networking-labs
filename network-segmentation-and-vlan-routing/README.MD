# Multi-Switch Network Segmentation and VLAN Routing Lab

## Overview

This project was built in Cisco Packet Tracer to practice VLAN segmentation, trunking, and inter-VLAN routing in a multi-switch environment.

The lab simulates a small business network containing multiple departments separated into VLANs while still allowing communication between networks through router-on-a-stick inter-VLAN routing.



# Network Topology

## Devices Used

- 1 Cisco Router
- 2 Cisco 2960 Switches
- 5 PCs



# VLANs and Subnets

| VLAN | Department | Network |
|------|-------------|----------|
| 10 | SALES | 192.168.10.0/24 |
| 20 | IT | 192.168.20.0/24 |
| 30 | HR | 192.168.30.0/24 |



# Objectives

- Configure multiple VLANs
- Assign switch access ports to VLANs
- Configure 802.1Q trunking between switches
- Configure router-on-a-stick inter-VLAN routing
- Verify communication between VLANs
- Troubleshoot VLAN and trunking issues



# Technologies Used

- Cisco Packet Tracer
- VLAN Configuration
- 802.1Q Trunking
- Inter-VLAN Routing
- Router-on-a-Stick
- Layer 2 Switching
- Layer 3 Routing
- Cisco IOS CLI



# Router Configuration Example


interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0

interface g0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0




# Switch Configuration Example

## Access Port Configuration


interface fa0/1
 switchport mode access
 switchport access vlan 10


## Trunk Port Configuration

interface fa0/24
 switchport mode trunk




# Verification Commands

## Verify VLAN Assignments


show vlan brief


## Verify Trunk Links


show interfaces trunk


## Verify Router Interfaces


show ip interface brief




# Troubleshooting Performed

During the lab several issues were encountered and resolved.

## Issues Encountered

- Incorrect switchport VLAN assignments
- Native VLAN mismatch errors
- PCs unable to reach default gateways
- Trunk/access port misconfigurations

## Troubleshooting Steps

- Verified VLAN membership using `show vlan brief`
- Verified trunk links using `show interfaces trunk`
- Corrected switchport VLAN assignments
- Verified router subinterfaces and encapsulation settings
- Confirmed PC IP addressing and default gateways



# Skills Practiced

- VLAN implementation
- Network segmentation
- Inter-VLAN routing
- Router-on-a-stick configuration
- Layer 2 troubleshooting
- Layer 3 troubleshooting
- Cisco IOS CLI navigation
- Network verification and testing



# Screenshots

## Network Topology

(Add topology screenshot here)

## VLAN Verification

(Add VLAN screenshot here)

## Trunk Verification

(Add trunk screenshot here)

## Successful Connectivity Tests

(Add ping test screenshot here)



# Packet Tracer File

The Packet Tracer lab file is included in this repository.



# Future Improvements

Potential future additions to this lab include:

- Access Control Lists (ACLs)
- DHCP Services
- EtherChannel
- Spanning Tree Protocol (STP) optimization
