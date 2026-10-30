# Networking Labs

Hands-on Cisco Packet Tracer labs documenting networking fundamentals, enterprise design, and NOC-style troubleshooting.

## Incident troubleshooting

- [INC-013 — DHCP DNS option failure](dhcp-dns-incident-triage/) — Isolate hostname-resolution failure from IP reachability, compare DHCP scope settings, and verify recovery.
- [INC-012 — DHCP relay incident triage](dhcp-relay-incident-triage/) — Trace a branch DHCP failure through relay configuration, routing, and lease verification.

## Routing and services

- [DHCP and OSPF multi-router lab](dhcp-ospf-multi-router-lab/) — Practice DHCP relay across a routed OSPF network.
- [DHCP and OSPF route failover](dhcp-ospf-route-failover/) — Test path changes and service reachability after a route failure.
- [OSPF multi-router network lab](ospf-multi-router-network-lab/) — Configure and verify OSPF adjacencies and learned routes.
- [Static routing](static-routing/) — Configure static routes and verify end-to-end reachability.
- [Basic router configuration](basic-router-configuration/) — Practice initial Cisco IOS device setup and connectivity checks.

## Switching and segmentation

- [Basic VLAN lab](01-basic-vlan-lab/) — Create VLANs and assign switch access ports.
- [Inter-VLAN routing](02-intervlan-routing/) — Route traffic between VLANs and verify gateway connectivity.
- [Network segmentation and VLAN routing](network-segmentation-and-vlan-routing/) — Practice VLAN-based segmentation and inter-VLAN communication.

## Related projects

- [Multi-Site Enterprise Network](https://github.com/kmauldinbm-ai/multi-site-enterprise-network) — Enterprise design, redundancy, and failure recovery.
- [NOC Network Monitoring and Incident Response](https://github.com/kmauldinbm-ai/noc-network-monitoring-incident-response) — Monitoring, outage response, and service restoration.
- [OSPF Duplicate Router ID Troubleshooting](https://github.com/kmauldinbm-ai/ospf-duplicate-router-id-troubleshooting) — OSPF fault isolation and repair.

Labs include Packet Tracer files, screenshots, verification commands, and incident write-ups where available. Each project README lists its specific scope and included evidence.
