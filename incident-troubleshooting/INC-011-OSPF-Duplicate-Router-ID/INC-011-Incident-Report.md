# Incident Report INC-011

## Incident Summary

**Status:** Resolved  
**Environment:** Cisco Packet Tracer  
**Lab Source:** Fix The Network  
**Ticket:** Trouble Ticket #2.1  

---

## Reported Problem

PCs in VLAN 10 and VLAN 20 were unable to communicate with R2's G0/0/0 interface.

---

## Initial Assessment

I tested connectivity from each PC by pinging each Layer 3 hop along the path until I identified where communication failed.

All PCs were able to successfully reach DSW2's interface connecting toward R2. However, the PCs were unable to ping R2's G0/0/0 interface.

Based on these results, I suspected a routing or configuration issue involving R2.

---

## Troubleshooting

### Step 1

**Action:**  
I checked R2's interfaces to determine whether the interface was operational or administratively shut down.

**Command/Test:**

```text
show ip interface brief
```

**Result:**  
R2's relevant interfaces were in the `up/up` state.

**What this tells me:**  
The physical and data-link states of the interface were operational, so I moved on to investigate a possible routing issue.

---

### Step 2

**Action:**  
I checked R2's routing table to determine whether it had routes to the affected networks.

**Command/Test:**

```text
show ip route
```

**Result:**  
The routing table contained only connected and local routes. No dynamically learned routes were present.

**What this tells me:**  
R2 was not learning routes to the remote networks. I needed to determine what routing protocol was being used by the neighboring Layer 3 devices.

---

### Step 3

**Action:**  
I checked R1's routing table to compare its routing information with R2.

**Command/Test:**

```text
show ip route
```

**Result:**  
R1's routing table contained routes learned through OSPF.

**What this tells me:**  
The network was using OSPF for dynamic routing. I returned to R2 to determine whether OSPF was missing or whether R2 was experiencing an OSPF adjacency problem.

---

### Step 4

**Action:**  
I checked R2's OSPF neighbor relationships.

**Command/Test:**

```text
show ip ospf neighbor
```

**Result:**  
The OSPF neighbor relationship between R2 and DSW2 was stuck in the `EXSTART` state.

**What this tells me:**  
R2 and DSW2 were communicating through OSPF, but something was preventing them from forming a full adjacency and exchanging routing information.

---

### Step 5

**Action:**  
I inspected R2's OSPF configuration to investigate why the adjacency could not fully form.

**Command/Test:**

```text
show running-config | section router ospf
```

**Result:**  
R2 was configured with OSPF router ID `3.3.3.3`. DSW2 was also using OSPF router ID `3.3.3.3`.

**What this tells me:**  
R2 and DSW2 were configured with duplicate OSPF router IDs. OSPF router IDs must uniquely identify each OSPF router. The duplicate IDs prevented the devices from establishing a full OSPF adjacency and exchanging routes.

---

## Root Cause

R2 and DSW2 were using the same OSPF router ID of `3.3.3.3`.

The duplicate router IDs prevented the OSPF neighbor relationship from reaching the FULL state. As a result, R2 was unable to learn the remote VLAN networks through OSPF, causing the reported connectivity failure.

---

## Resolution

I changed R2's OSPF router ID from `3.3.3.3` to the correct unique router ID of `4.4.4.4`.

After changing the router ID, the OSPF process was allowed to reestablish its neighbor relationship with DSW2.

---

## Verification

After the configuration change:

- R2 successfully established its OSPF adjacency.
- R2 was able to learn the remote routes through OSPF.
- PCs in VLAN 10 and VLAN 20 were able to successfully communicate with R2's G0/0/0 interface.

The incident was resolved.

---

## Lessons Learned

An OSPF process being configured does not necessarily mean that routes are being successfully exchanged. Checking the OSPF neighbor state helped identify that the problem was related to adjacency formation rather than basic interface connectivity.

OSPF router IDs must be unique. When an OSPF neighbor relationship becomes stuck before reaching the FULL state, checking router IDs and other adjacency parameters can help identify the cause.
