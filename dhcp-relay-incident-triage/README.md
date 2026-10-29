# NOC Incident Challenge: DHCP Relay Failure

A Cisco Packet Tracer troubleshooting exercise built from the DHCP/OSPF multi-router topology. A branch's new clients cannot obtain DHCP leases while another branch remains operational. Work the issue as a NOC incident: establish scope, collect evidence, isolate the failing service path, restore service, verify recovery, and document the ticket.

## Incident

**Ticket:** INC-012  
**Priority:** P2 — partial branch service impact  
**Reported symptom:** New clients on Branch North (`192.168.10.0/24`) are not receiving usable IPv4 configuration. Branch South (`192.168.20.0/24`) is reported operational.  
**Change window:** None reported.

Do not assume DHCP is the only possible cause. Confirm the scope and collect evidence before making a change.

## Topology and files

The project uses the existing four-router DHCP/OSPF topology. The DHCP server is `10.0.0.1`; Branch North is connected to R3 and Branch South to R4. Refer to the Packet Tracer file for exact interface addressing.

- [`dhcp-ospf-route-failover-fixed.pkt`](dhcp-ospf-route-failover-fixed.pkt) — known-good topology after remediation. Use it as the baseline when preparing a faulted challenge copy.
- [`facilitator-notes.md`](facilitator-notes.md) — fault injection and answer; keep this from the learner during a live challenge.
- [`incident-report.md`](incident-report.md) — report from the completed troubleshooting run.

## Learner tasks

1. Test a new DHCP client on each branch and record address, mask, gateway, and DNS.
2. Compare affected and control clients to establish the impact boundary.
3. Check interface status, OSPF neighbors, and expected routes. Distinguish routing health from DHCP relay behavior.
4. Inspect the affected router's client-facing interface, DHCP server reachability, pool for the branch subnet, and lease/binding state.
5. Identify the root cause and cite evidence that supports it.
6. Apply the smallest corrective change, renew the affected client's lease, and verify local and cross-branch reachability.
7. Update the incident report with observed commands, output, timeline, cause, action, and recovery evidence.

## Useful commands

```text
show ip interface brief
show ip ospf neighbor
show ip route
show running-config | include helper-address
show running-config | section interface GigabitEthernet0/1
show ip dhcp pool
show ip dhcp binding
```

Packet Tracer's IOS filter support varies. If `section` or `include` is unavailable, use `show running-config` and inspect the relevant interface manually. A filter only displays configured matches; an empty result can be significant when checking for a missing command.

## Completion criteria

The issue is resolved when a new Branch North client receives a valid lease, reaches its default gateway and a destination on the other branch, the control branch remains operational, and the incident notes explain the scope, diagnosis, fix, and verification.

## Packet Tracer

Open the `.pkt` file with Cisco Packet Tracer. To practice the incident, first save a separate challenge copy and use the facilitator notes to seed the fault. Preserve the provided fixed topology as your known-good baseline.

This is a simulated learning exercise, not a production network.
