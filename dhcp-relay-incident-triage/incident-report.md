# Incident Report — INC-012 DHCP Relay Failure

**Status:** Resolved in Packet Tracer  
**Priority:** P2 — partial branch service impact  
**Affected service:** DHCP for Branch North clients (`192.168.10.0/24`)

## Impact and scope

The exercise used PC1 on Branch North and PC2 on Branch South as affected and control clients. Before fault injection, PC1 had `192.168.10.12` and PC2 had `192.168.20.11`. After the repair, PC1 completed a fresh DHCP request. A ping from PC1 to its default gateway and a ping to PC2 (`192.168.20.11`) succeeded.

The exact failed-client address and pre-change ping output were not recorded during this run.

## Diagnosis

The DHCP relay helper address was absent from R3's Branch North client-facing interface, GigabitEthernet0/1. The central DHCP server is `10.0.0.1`. Without the relay, the branch's client broadcast could not be forwarded to the server.

## Corrective action

Restored the DHCP relay target on R3 G0/1:

```text
ip helper-address 10.0.0.1
```

## Recovery verification

- PC1 obtained a DHCP lease after the relay configuration was restored.
- PC1 successfully pinged its configured default gateway.
- PC1 successfully pinged PC2 at `192.168.20.11`.

## Evidence gap / next run

The next run should capture the failed client's lease state before remediation, the output of `show ip ospf neighbor` and `show ip route`, the relevant R3 interface configuration before and after the fix, and the DHCP binding after recovery. Do not add output that was not actually captured.
