# Northern Kingdoms Network Design

A full network design and implementation in Cisco Packet Tracer, connecting six sites under a shared address space with VLSM, mixed static/dynamic routing, DHCP, and distributed network services.

## [The Problem](The_Northern_War.pdf) (Click to see more details)

Design and implement a network connecting six sites (Cintra, Aedrin, Kaedwen, Kovir, Redenia, Temeria), each with a different number of hosts, under the following constraints:

- Subnet a single `/16` address block across all six sites using VLSM, sized to each site's actual host count to minimize address waste.
- Only odd host IP addresses may be assigned to end devices.
- Cintra and Aedrin use static IP addressing; the remaining four sites use DHCP.
- Cintra hosts a Web Server and DNS Server, with the website accessible through `www.cintra.com`.
- Cintra hosts an Email Server used for communication between Cintra and Temeria.
- Kovir and Redenia each get a network printer in place of a database.
- Aedrin, Cintra, and Kaedwen use dynamic routing (RIPv2); Kovir, Redenia, and Temeria use static routing.
- At least one floating static route is required as a backup path.
- Default routes are reserved for ISP-bound traffic only — every inter-site path must use a real static or dynamic route.
- Every site must be able to reach every other site.

## What Was Built

The network was implemented in Cisco Packet Tracer with VLSM-based addressing, static and dynamic routing, DHCP, DNS, Web, Email, and printer services, along with full inter-site connectivity.

![Network Topology](diagrams/topology.png)

Six sites interconnected over six point-to-point WAN links, carved from the same `10.13.0.0/16` block used for the site networks. Aedrin and Kaedwen form the core of the WAN, each connecting to three other sites; Kovir and Temeria sit as single-link leaf sites.

## Network Services

| Site | LAN Network | Hosts Needed | Addressing | Routing | Services |
|---------|-----------------|:------------:|:----------:|:-------:|----------|
| Cintra | 10.13.0.0/21 | 1000 | Static | RIPv2 | Web, DNS, Email Server |
| Aedrin | 10.13.8.0/21 | 800 | Static | RIPv2 | — |
| Kaedwen | 10.13.16.0/21 | 784 | DHCP | RIPv2 | — |
| Kovir | 10.13.24.0/21 | 519 | DHCP | Static | Printer, DHCP Server |
| Redenia | 10.13.32.0/22 | 401 | DHCP | Static | Printer |
| Temeria | 10.13.36.0/22 | 302 | DHCP | Static | Email client access |

The Cintra DNS server resolves:

```
www.cintra.com
````

The website displays:

![Cintra Website](diagrams/cintraDanger.png)

Email communication is configured between Cintra and Temeria using the Email Server hosted on the Cintra LAN.

## Addressing

### VLSM Tree

![VLSM Tree](diagrams/vlsm-tree.png)

Each LAN subnet is sized by VLSM to fit its host count with minimal waste; WAN links use `/29` subnets carved from a shared `10.13.40.0/22` block.

### Subnet Allocation

![VLSM Subnetting](diagrams/vlsm-subnetting-table.png)

### IP Addressing

![IP Addressing Table](diagrams/interface-addressing-table.png)

## Routing

The network uses a combination of RIPv2 and static routing.

* Aedrin, Cintra, and Kaedwen use RIPv2 as their primary dynamic routing protocol.
* Kovir, Redenia, and Temeria use static routing.
* Static and floating routes are also used where required for backup and reachability.
* A floating static route provides a backup path.
* Default routes are not used for communication between the six kingdom networks.

## Testing

* Verified inter-site connectivity using ICMP ping tests.
* Verified DHCP address assignment on the DHCP-based LANs.
* Verified `www.cintra.com` resolves through the Cintra DNS server and displays the required message.
* Verified email delivery between Cintra and Temeria.
* Verified printer connectivity in Kovir and Redenia.

## Repository Structure

```
Northern-War-Project/
├── diagrams/
│   ├── cintraDanger.png
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

* VLSM subnetting and IP address planning under real allocation constraints
* Static and dynamic (RIPv2) routing design across a multi-site WAN topology
* Floating static routes for automatic path failover
* DHCP server and relay configuration across subnets
* Network service deployment (Web, DNS, Email, and printing) mapped to specific sites
* Cisco Packet Tracer
* Network Troubleshooting

