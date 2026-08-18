# Northern War Network Design

Six-site enterprise network built in Cisco Packet Tracer — VLSM subnetting, mixed static/dynamic routing, DHCP relay, and distributed services (Web, DNS, Email, Print).

Final project for Computer Networks (CSE421). Nominally a 3-person group project; the network design, addressing plan, and full router configuration were completed independently.

## Overview

Six sites needed to be connected under a single address space, each playing a different role: two with static IP addressing, the rest DHCP-served; three routing dynamically via RIPv2, three via static routes; and a small set of services (web, DNS, email, print) placed at specific sites. The task was to design the full addressing scheme from one `/16` block, build the topology, and configure every router for end-to-end reachability.

## Topology

![Network Topology](diagrams/topology.png)

Six kingdom routers connected via nine `/30` WAN links (`Wan1`–`Wan9`), all carved from the same `10.13.0.0/16` block used for the site networks.

## Addressing & Site Roles

| Site    | Network         | Hosts | Addressing | Routing | Role |
|---------|-----------------|:-----:|:----------:|:-------:|------|
| Cintra  | 10.13.0.0/22    | 1000  | Static     | RIPv2   | Web + DNS Server |
| Aedrin  | 10.13.4.0/22    | 800   | Static     | RIPv2   | — |
| Kaedwen | 10.13.8.0/22    | 784   | DHCP       | RIPv2   | — |
| Kovir   | 10.13.12.0/22   | 519   | DHCP       | Static  | Printer |
| Redenia | 10.13.16.0/23   | 401   | DHCP       | Static  | Printer |
| Temeria | 10.13.18.0/23   | 302   | DHCP       | Static  | Email Server |

Subnets are sized by VLSM to fit each site's actual host count rather than a flat allocation, keeping address waste to a minimum.

**VLSM Subnetting Tree**
![VLSM Tree](diagrams/vlsm-tree.png)

**Per-Site Subnet Allocation**
![Subnetting Table](diagrams/vlsm-subnetting-table.png)

**Per-Interface Addressing**
![Interface Addressing Table](diagrams/interface-addressing-table.png)

## Repo Structure

```
├── diagrams/       # Topology, VLSM tree, addressing tables
├── config/         # show running-config, one file per router
└── packet-tracer/  # Full .pkt topology file
```

## Skills Demonstrated

- VLSM subnetting and IP address planning under real allocation constraints
- Static and dynamic (RIPv2) routing configuration across a multi-site topology
- DHCP relay (`ip helper-address`) configuration across subnets
- Multi-service network design (Web, DNS, Email, print) mapped to specific sites
- Reading and auditing real router configuration output

## Status

Core design and configuration are complete and working. Closing out a few compliance items against the original spec:

- Add a floating static route (backup path with an explicit administrative distance) — not yet present.
- Replace a few default-route workarounds on the static-routing sites with explicit static routes to the remaining kingdom networks.
- Clean up leftover test IP addresses on a couple of unused interfaces.
