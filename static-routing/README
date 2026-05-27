
# Cisco Static Routing Lab

## Overview

This lab demonstrates static routing configuration using multiple Cisco routers in Packet Tracer.  
The objective was to establish end-to-end connectivity between multiple LANs by configuring router interfaces, assigning IPv4 addresses, and implementing static routes.

---

# Objectives

- Configure router interfaces
- Configure IPv4 addressing
- Implement static routing
- Configure default gateways on PCs
- Verify connectivity between remote networks
- Troubleshoot routing and interface issues
- Practice Cisco IOS CLI commands

---

# Network Topology

![Topology](screenshots/topology.png)

---

# IP Addressing Table

| Device | Interface | IP Address | Subnet Mask |
|---|---|---|---|
| R1 | G0/0 | 192.168.1.1 | 255.255.255.0 |
| R1 | G0/1 | 192.168.12.1 | 255.255.255.0 |
| R2 | G0/0 | 192.168.12.2 | 255.255.255.0 |
| R2 | G0/1 | 192.168.23.1 | 255.255.255.0 |
| R3 | G0/0 | 192.168.23.2 | 255.255.255.0 |
| R3 | G0/1 | 192.168.3.1 | 255.255.255.0 |

---

# Static Routes

## R1

```bash
ip route 192.168.3.0 255.255.255.0 192.168.12.2
```

## R2

```bash
ip route 192.168.1.0 255.255.255.0 192.168.12.1
ip route 192.168.3.0 255.255.255.0 192.168.23.2
```

## R3

```bash
ip route 192.168.1.0 255.255.255.0 192.168.23.1
```

---

# Verification Commands

## Verify Interface Status


show ip interface brief
```

## Verify Routing Table


show ip route
```

## Verify Connectivity

ping
```

traceroute
```

---

# Connectivity Testing

Successful end-to-end connectivity was verified between all PCs across different networks.

## Successful Ping Test

![Successful Ping](screenshots/successful-ping.png)

---

# Router Verification

## R1 Routing Table

![R1 Route Table](screenshots/R1-show-ip-route.png)

## R2 Routing Table

![R2 Route Table](screenshots/R2-show-ip-route.png)

## R3 Routing Table

![R3 Route Table](screenshots/R3-show-ip-route.png)

---

# Troubleshooting

During this lab, the following troubleshooting steps were performed:

- Verified interface status using:

  show ip interface brief
  ```

- Verified routing tables using:

  show ip route
  ```

- Checked for:
  - Incorrect static routes
  - Incorrect next-hop addresses
  - Incorrect default gateways
  - Interfaces in administratively down state
  - Layer 1 and Layer 2 connectivity issues

---

# Skills Demonstrated

- Cisco IOS CLI configuration
- Static routing
- IPv4 addressing and subnetting
- Router interface configuration
- Network troubleshooting
- End-to-end connectivity testing
- Routing table verification
- Packet Tracer lab development

---

# Files Included

- Packet Tracer lab file (`.pkt`)
- Router configuration files
- Network topology screenshots
- Verification screenshots

---

# Technologies Used

- Cisco Packet Tracer
- Cisco IOS CLI
- IPv4 Networking
- Static Routing
