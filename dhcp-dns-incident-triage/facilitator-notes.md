# Facilitator Notes — INC-013 DHCP DNS Option Failure

Use these notes to prepare the challenge version. The public repository includes the answer, so the lab is intended for self-study and portfolio review.

## Prepare the challenge instance

1. Open INC-013-DNS-TRIAGE.Fixed.pkt in Cisco Packet Tracer.
2. Save a separate copy as INC-013-DNS-TRIAGE-Challenge.pkt.
3. Confirm Server0 at 192.168.10.2 has DNS service enabled and the record pc2.lab mapped to 192.168.20.11.
4. On the DHCP router, inject the fault in LAN_R3 only:

~~~text
configure terminal
ip dhcp pool LAN_R3
 dns-server 192.168.10.99
end
~~~

5. Renew PC1's DHCP lease and verify with ipconfig /all that the client now uses 192.168.10.99. Leave LAN_R4 set to 192.168.10.2 so PC2 remains a control.
6. Save the challenge copy.

## Expected troubleshooting evidence

- PC1's nslookup pc2.lab request times out because 192.168.10.99 is not the DNS server.
- PC1 can still ping PC2 at 192.168.20.11 by IP. This tests reachability without requiring DNS.
- PC2 still uses 192.168.10.2 and resolves pc2.lab to 192.168.20.11.
- The DHCP router's LAN_R3 pool contains the incorrect dns-server option; LAN_R4 is correct.

A first lookup may time out once in Packet Tracer before a retry returns an answer. Repeat the lookup to distinguish a transient initial delay from a persistent failure.

## Root cause and corrective action

The DHCP router handed out the wrong resolver address to clients in LAN_R3. The DNS service on Server0 was available; the affected clients were directed to 192.168.10.99 instead of 192.168.10.2.

Restore the LAN_R3 option:

~~~text
configure terminal
ip dhcp pool LAN_R3
 dns-server 192.168.10.2
end
~~~

On PC1, renew the lease, confirm the DNS server with ipconfig /all, then verify with nslookup pc2.lab. The expected answer is 192.168.20.11. Confirm PC2 continues to resolve the name as well.

## NOC reasoning points

- DHCP supplies DNS server information to clients; the DNS server itself is configured separately.
- A DNS failure can prevent hostname-based access while direct IP traffic still works.
- Comparing an affected client with an unaffected client helps locate a scope-specific DHCP option issue.
- A DHCP pool change reaches a client when that client obtains or renews its lease.

## Scoring guide (10 points)

- Establishes the affected subnet and verifies a control client (2)
- Separates DNS resolution from IP reachability using nslookup and ping by IP (2)
- Finds the incorrect DNS option in LAN_R3 (2)
- Restores the correct resolver and renews PC1's lease (2)
- Verifies name resolution and documents evidence, cause, and recovery (2)
