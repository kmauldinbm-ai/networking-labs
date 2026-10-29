# NOC Incident Challenge: DHCP DNS Option Failure

Cisco Packet Tracer exercise for troubleshooting hostname-resolution failures that affect one client subnet while IP connectivity remains available.

## Incident

**Ticket:** INC-013  
**Priority:** P2 — partial service impact  
**Reported symptom:** Users on the R3 LAN cannot resolve hostnames. Users on the R4 LAN can resolve names, and PC1 can still reach PC2 by IP address.

The exercise practices scope identification, DNS versus routing fault isolation, DHCP option review, controlled remediation, lease renewal, and clear incident notes.

## Topology and address plan

| Device / role | Address | Notes |
| --- | --- | --- |
| R3 LAN gateway | 192.168.10.1/24 | Serves PC1's subnet |
| PC1 | 192.168.10.12/24 | DHCP client in LAN_R3 |
| Server0 DNS server | 192.168.10.2/24 | DNS service; pc2.lab record points to 192.168.20.11 |
| R4 LAN gateway | 192.168.20.1/24 | Serves PC2's subnet |
| PC2 | 192.168.20.11/24 | DHCP client in LAN_R4 |
| DHCP router | LAN_R3 and LAN_R4 pools | Supplies addressing and DNS options to both client subnets |

The DHCP pools are named LAN_R3 and LAN_R4. Both should hand out 192.168.10.2 as the DNS server. The DNS server is on the .10 subnet and can answer records for hosts on the .20 subnet because routing connects the subnets.

## Files

- INC-013-DNS-TRIAGE.Fixed.pkt — restored Packet Tracer baseline.
- facilitator-notes.md — fault injection steps, expected evidence, fix, and scoring rubric.
- incident-report.md — concise write-up of the observed troubleshooting run.

## Learner tasks

1. Confirm each client received the expected IP address, default gateway, and DNS server.
2. Compare PC1 and PC2 to define the impact boundary.
3. Use nslookup to test name resolution and ping by IP to test reachability independently.
4. Inspect the DHCP pool configuration and identify which DNS option was sent to the affected subnet.
5. Restore the correct DNS option, renew the affected client's DHCP lease, and verify name resolution.
6. Record the symptom, evidence, cause, change, and recovery check in an incident update.

## Useful commands

On the DHCP router:

~~~text
show ip dhcp pool
show running-config | section ip dhcp pool
~~~

On a Packet Tracer PC:

~~~text
ipconfig /all
ipconfig /renew
nslookup pc2.lab
ping 192.168.20.11
~~~

The DHCP pool's dns-server option tells clients which resolver IP to use. It does not turn the DHCP router into a DNS server. Server0 runs the DNS service; DHCP distributes Server0's address to clients.

## Completion criteria

The learner can explain why hostname lookup failed while ping by IP succeeded, identify the incorrect DNS address in LAN_R3, restore 192.168.10.2, renew PC1's lease, and confirm that pc2.lab resolves to 192.168.20.11. PC2 should remain a working control client throughout the fault.

## Packet Tracer

Open the .pkt file with Cisco Packet Tracer. To practice the incident, save a separate challenge copy and follow facilitator-notes.md to inject the fault. The solution notes are public in this portfolio repository, so this is a documented self-study lab rather than a blinded assessment.

This is a simulated learning exercise, not a production network.
