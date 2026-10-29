# Facilitator Notes — DHCP Relay Failure

**Do not provide this file to a learner before the challenge.**

## Prepare the challenge instance

1. Open `dhcp-ospf-route-failover-fixed.pkt` in Cisco Packet Tracer.
2. Save a separate copy as `dhcp-relay-challenge.pkt`.
3. On R3, remove the relay address from the Branch North client-facing interface, GigabitEthernet0/1:

```text
R3# configure terminal
R3(config)# interface gigabitEthernet0/1
R3(config-if)# no ip helper-address 10.0.0.1
R3(config-if)# end
```

4. Save the challenge copy. Keep the fixed file unchanged as the recovery baseline.
5. Use a fresh DHCP request from a Branch North client. Existing clients may retain a previously leased address; a new client or explicit renewal gives a clearer test.

## Expected diagnosis and recovery

The R3 G0/1 DHCP relay helper address is missing. DHCP client broadcasts do not cross the router without a relay, so new clients on `192.168.10.0/24` cannot obtain leases from the central server. The Branch South LAN remains the control segment.

Restore the relay configuration:

```text
R3# configure terminal
R3(config)# interface gigabitEthernet0/1
R3(config-if)# ip helper-address 10.0.0.1
R3(config-if)# end
```

Renew the affected client lease. Verify its addressing, default gateway reachability, cross-branch reachability, and the DHCP server binding. Also capture OSPF neighbor and route output as evidence that the routed underlay is healthy.

## Scoring guide (10 points)

- Establishes affected and unaffected scope (2)
- Captures client and control test results before changing configuration (1)
- Checks OSPF/interface/routing state without misattributing DHCP failure (2)
- Finds missing helper on the correct interface and supports diagnosis with evidence (2)
- Restores only the required relay configuration (1)
- Verifies a fresh lease and end-to-end connectivity (1)
- Writes a clear ticket update with a useful handoff (1)
