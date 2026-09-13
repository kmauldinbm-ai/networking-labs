# INC-011 — OSPF Duplicate Router ID Troubleshooting

## Overview

This Cisco Packet Tracer troubleshooting lab involved a connectivity failure between client VLANs and a remote router. I used a structured troubleshooting process to isolate the problem from basic Layer 3 connectivity to an OSPF adjacency issue.

**Lab Source:** Fix The Network  
**Ticket:** Trouble Ticket #2.1  
**Status:** Resolved

## Technologies and Skills

- Cisco Packet Tracer
- OSPF
- VLANs
- Layer 3 switching
- Dynamic routing
- Cisco IOS troubleshooting
- OSPF neighbor-state analysis

## Reported Problem

PCs in VLAN 10 and VLAN 20 were unable to communicate with R2's G0/0/0 interface at 10.1.2.1.

## Troubleshooting Summary

Connectivity testing showed that the PCs could successfully reach DSW2's interface toward R2, but could not reach R2 itself. R2's interfaces were operational, but its routing table contained no dynamically learned routes.

Comparison with another router showed that the network was using OSPF. Checking R2's OSPF neighbor relationship revealed that the adjacency with DSW2 was stuck in the `EXSTART` state.

Further inspection revealed that R2 and DSW2 were both using OSPF router ID `3.3.3.3`.

## Root Cause

R2 and DSW2 were configured with duplicate OSPF router IDs. Because OSPF router IDs must uniquely identify each OSPF router, the duplicate IDs prevented the neighbor relationship from reaching the FULL state and prevented R2 from learning the remote VLAN routes.

## Resolution

R2's OSPF router ID was changed from `3.3.3.3` to the unique router ID `4.4.4.4`. After the OSPF adjacency reestablished, the neighbor relationship reached the FULL state and routes were exchanged normally.

## Verification

After the repair:

- The OSPF adjacency reached `FULL/BDR`.
- R2 learned remote routes through OSPF.
- PCs in the affected VLANs were able to successfully reach R2's G0/0/0 interface.

## Commands Used

```text
show ip interface brief
show ip route
show ip ospf neighbor
show running-config | section router ospf
```

## Documentation

See `INC-011-Incident-Report.md` for the complete troubleshooting process.

## Evidence Files

The supporting Packet Tracer file and screenshots document the topology, the OSPF `EXSTART` condition, duplicate router IDs, the corrected FULL adjacency, and successful end-to-end connectivity.
