
# VLAN Design

## Purpose
This document defines the VLAN architecture used within the UniFi home lab network.  
The design focuses on segmentation, security isolation, and consistent application across wired and wireless networks.

The VLAN structure mirrors production environments by separating devices based on trust level and function.

---

## VLAN Summary

| VLAN Name | VLAN ID | Subnet | Purpose | Routing |
|----------|--------|--------|--------|--------|
| Trusted | 10 | 192.168.10.0/24 | Primary user devices (PCs, laptops) | Inter-VLAN + WAN |
| IoT | 20 | 192.168.20.0/24 | Smart TV and IoT devices | Restricted |
| Guest | 30 | 192.168.30.0/24 | Guest and visitor devices | WAN only |

---

## VLAN Design Rationale

### Trusted VLAN
- Assigned to personally managed devices
- Full access to internal services and internet
- Acts as the administrative and management network
- Allowed to initiate limited connections to IoT devices when required

### IoT VLAN
- Dedicated to unmanaged or semi-trusted devices
- Prevents lateral movement toward trusted endpoints
- Internet access restricted to required outbound services
- No inbound access to Trusted VLAN

### Guest VLAN
- Fully isolated from internal networks
- Internet access only
- No east-west or north-south LAN access
- Treated as an untrusted zone

---

## Inter-VLAN Communication Policy

| Source | Destination | Action | Reason |
|------|------------|--------|-------|
| Trusted | IoT | Allow (limited) | Device control and media access |
| IoT | Trusted | Deny | Prevent compromise spread |
| Guest | Trusted | Deny | Security isolation |
| Guest | IoT | Deny | Security isolation |
| Guest | WAN | Allow | Internet access |

---

## VLAN Assignment Strategy

### Wired Devices
- VLANs are applied using **access ports** on UniFi switches
- Native VLAN is explicitly defined per port
- Tagged VLANs are blocked on end-device ports

### Wireless Devices
- Each SSID is mapped to a single VLAN
- SSIDs are isolated at Layer 2 using VLAN tagging
- Guest SSID uses UniFi guest policies and firewall rules

---

## Subnet Sizing Considerations
- /24 networks chosen for simplicity and growth headroom
- Clear numerical separation improves readability and troubleshooting
- Subnet ranges align with VLAN IDs for intuitive mapping

---

## Design Principles
- **Least Privilege:** Devices receive only the access they require
- **Isolation First:** Default deny between VLANs
- **Consistency:** Same VLAN logic across wired and wireless
- **Scalability:** VLAN IDs and subnets allow future expansion

---

## Related Documentation
- Network overview: `network-overview.md`
- Firewall rules: `firewall-rules.md`
- Switch port profiles: `switch-port-profiles.md`
