# Network Overview

## Purpose
This document provides a high-level overview of the UniFi home lab network architecture, including core components, traffic flow, and design intent.

The network is designed to emulate production environments by enforcing segmentation, least-privilege access, and clear trust boundaries between device categories.

## Core Components
- **Gateway / Controller:** UniFi Dream Machine SE (UDM-SE)
- **Wireless:** UniFi U7 Pro Access Point
- **Switching:** UniFi managed switches
- **Clients:** Wired and wireless endpoints across multiple trust zones

## High-Level Architecture
All traffic is routed through the UDM-SE, which performs:
- Inter-VLAN routing
- Firewall policy enforcement
- Network address translation (NAT)
- Traffic inspection and logging

Wireless and wired networks are logically segmented using VLANs and mapped consistently across switch ports and Wi-Fi SSIDs.

Refer to /diagrams/logical-network-architecture.png for a visual representation of VLAN segmentation, firewall enforcement, and traffic flow.

## Network Zones
| Zone     | Purpose                                   | Access Level |
|----------|-------------------------------------------|--------------|
| Trusted  | Primary user devices (PCs, laptops)       | Full LAN + WAN |
| IoT      | Smart TV and smart home devices            | Restricted |
| Guest    | Visitor devices                            | Internet-only |

## Traffic Flow Summary
- Trusted → WAN: Allowed
- Trusted → IoT: Allowed (limited use cases)
- IoT → Trusted: Denied
- Guest → LAN: Denied
- Guest → WAN: Allowed

## Design Principles
- **Least Privilege:** Devices receive only the access they require
- **Isolation:** Compromised IoT devices cannot reach trusted endpoints
- **Consistency:** VLANs are applied uniformly across wired and wireless networks
- **Observability:** Firewall rules are logged and auditable

## Assumptions
- All UniFi devices are centrally managed
- VLAN-aware switching is enabled
- No legacy flat network segments exist

## Related Documentation
- VLAN design: `vlan-design.md`
- Firewall policies: `firewall-rules.md`
- Wi-Fi design: `wifi-design.md`
