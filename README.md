# Northern War Network Design

Six-site enterprise network designed and implemented in **Cisco Packet Tracer** for the Computer Networks (CSE421) final project.

The network connects **Aedrin, Cintra, Kaedwen, Kovir, Redenia, and Temeria** using VLSM subnetting, static and dynamic routing, DHCP, and distributed network services.

## Network Overview

- **Address space:** `10.13.0.0/16`
- **Subnetting:** VLSM based on the required device population
- **Host addressing:** Odd IP addresses only, as required by the project
- **Static addressing:** Cintra and Aedrin
- **DHCP:** Kaedwen, Kovir, Redenia, and Temeria
- **Dynamic routing:** RIPv2 on Aedrin, Cintra, and Kaedwen
- **Static routing:** Kovir, Redenia, and Temeria
- **Redundancy:** Floating static route
- **WAN:** Point-to-point `/30` links

![Network Topology](diagrams/topology.png)

## Network Services

| Site | Services |
|---|---|
| Cintra | Web Server, DNS Server |
| Kovir | Printer |
| Redenia | Printer |
| Temeria | Email Server |

The Cintra DNS server resolves:

```text
www.cintra.com
```

The website displays:

```text
Cintra is in Danger!
```

Email communication is configured between **Cintra and Temeria**.

## Addressing

### VLSM Tree

![VLSM Tree](diagrams/vlsm-tree.png)

### Subnet Allocation

![VLSM Subnetting](diagrams/vlsm-subnetting-table.png)

### IP Addressing

![IP Addressing Table](diagrams/interface-addressing-table.png)

## Routing

The network uses a combination of **RIPv2 and static routing**.

- Aedrin, Cintra, and Kaedwen use RIPv2.
- Kovir, Redenia, and Temeria use static routes.
- A floating static route provides a backup path.
- Default routes are not used for communication between the six kingdom networks.

## Verification

The completed network is tested for:

- Branch-to-branch connectivity using `ping`
- DHCP address assignment
- RIPv2 and static route propagation
- DNS resolution
- Web server access
- Email communication
- Floating-route failover

## Repository Structure

```text
Northern-War-Project/
├── diagrams/
│   ├── topology.png
│   ├── vlsm-tree.png
│   ├── vlsm-subnetting-table.png
│   └── interface-addressing-table.png
├── config/
│   ├── Aedrin.txt
│   ├── Cintra.txt
│   ├── Kaedwen.txt
│   ├── Kovir.txt
│   ├── Redenia.txt
│   └── Temeria.txt
└── packet-tracer/
    └── Northern-War.pkt
```

## Skills Demonstrated

**Cisco Packet Tracer · VLSM · IPv4 Addressing · DHCP · DHCP Relay · RIPv2 · Static Routing · Floating Static Routes · DNS · Web Services · Email Services · Network Troubleshooting**

## Tools

- Cisco Packet Tracer
