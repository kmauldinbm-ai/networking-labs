# OSPF Multi-Router Network Lab

## Overview

This lab was created in Cisco Packet Tracer to practice dynamic routing using OSPF in a multi-router environment.

The topology consists of three routers connected through point-to-point transit networks with OSPF configured to dynamically advertise and learn routes.



# Objectives

- Configure router-to-router links
- Configure point-to-point /30 subnets
- Configure OSPF routing
- Form OSPF neighbor relationships
- Verify dynamically learned routes
- Test end-to-end connectivity



# Technologies Used

- Cisco Packet Tracer
- OSPF
- Dynamic Routing
- Point-to-Point Networking
- Cisco IOS CLI
- Layer 3 Routing
- Route Advertisement
- Network Troubleshooting



# Topology

The network consists of:

- 3 Routers
- Transit point-to-point links
- VLAN networks connected behind R1



# IP Addressing

## R1 ↔ R2

| Device | IP Address |
|---|---|
| R1 | 10.0.0.1/30 |
| R2 | 10.0.0.2/30 |

## R2 ↔ R3

| Device | IP Address |
|---|---|
| R2 | 10.0.0.5/30 |
| R3 | 10.0.0.6/30 |



# OSPF Configuration Example


router ospf 1

network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0




# Verification Commands

## Verify OSPF Neighbors


show ip ospf neighbor


## Verify Routing Table


show ip route


## Verify Interface Status


show ip interface brief




# Troubleshooting Performed

## Issues Encountered

- Incorrect interface assignments
- Unassigned router interfaces
- Connectivity failures between routers
- OSPF neighbor relationships not forming

## Troubleshooting Steps

- Verified interface status using `show ip interface brief`
- Corrected router interface IP addressing
- Verified physical connectivity between routers
- Verified OSPF network statements
- Tested connectivity with ICMP ping



# Skills Practiced

- Dynamic routing
- OSPF configuration
- Point-to-point subnetting
- Route advertisement
- Multi-router networking
- Routing table analysis
- Layer 3 troubleshooting
- Cisco IOS CLI navigation





# Packet Tracer File

The Packet Tracer lab file is included in this repository.
