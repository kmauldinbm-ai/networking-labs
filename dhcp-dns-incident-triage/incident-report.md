# Incident Report — INC-013 DHCP DNS Option Failure

**Status:** Remediated in Packet Tracer  
**Priority:** P2 — partial service impact  
**Affected scope:** R3 LAN clients on 192.168.10.0/24  
**Control scope:** R4 LAN clients on 192.168.20.0/24

## Impact and symptoms

PC1 on the R3 LAN could not resolve pc2.lab. A lookup through 192.168.10.99 timed out. PC1 could still ping PC2 at 192.168.20.11, showing that IP reachability between the subnets remained available. PC2 continued to resolve pc2.lab to 192.168.20.11 through 192.168.10.2.

## Diagnosis

The DHCP router's LAN_R3 pool supplied 192.168.10.99 as the DNS server. That address was not running the DNS service. The LAN_R4 pool continued to supply Server0 at 192.168.10.2, so PC2 remained able to resolve names.

## Corrective action

Restored the DNS option in LAN_R3 to the Server0 address, 192.168.10.2. The affected client must renew its DHCP lease to receive the corrected option.

## Verification

During the fault, PC1's name lookup timed out while its ping to PC2 by IP succeeded. PC2's DNS lookup succeeded and returned 192.168.20.11. After restoring the LAN_R3 setting, renew PC1's lease and run ipconfig /all and nslookup pc2.lab to confirm recovery in the saved Packet Tracer file.

This report records the observed fault evidence and the corrective configuration. It does not claim a post-remediation PC1 lookup that was not captured in the troubleshooting notes.
