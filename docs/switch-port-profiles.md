# Switch Port Profiles

## Purpose
This document defines how switch ports are configured within the UniFi home lab network, including access ports, native VLAN assignment, and tagged VLAN handling.

Correct switch port configuration is critical to enforcing VLAN boundaries and preventing unintended network access.

---

## Port Profile Strategy
All end-device ports are configured as **access ports** with a single native VLAN assigned.

Tagged VLANs are **blocked** on end-device ports to ensure:
- Devices cannot inject tagged traffic
- VLAN hopping attacks are mitigated
- VLAN boundaries remain enforced

Trunk-style behavior is reserved only for infrastructure devices.

---

## Port Types

### 1. End-Device Access Ports
Used for:
- PCs and laptops
- Smart TVs
- IoT devices
- Printers and consumer electronics

**Configuration characteristics:**
- One native VLAN per port
- Tagged VLANs: blocked
- No dynamic VLAN assignment
- No trunking enabled

---

### 2. Infrastructure / Uplink Ports
Used for:
- Switch-to-switch uplinks
- Switch-to-UDM-SE connections
- Access point uplinks

**Configuration characteristics:**
- Native VLAN defined (management)
- Required VLANs allowed as tagged
- Used only between trusted infrastructure devices

---

## VLAN Assignment by Device Type

| Device Type | Port Type | Native VLAN | Tagged VLANs |
|-----------|----------|-------------|--------------|
| PC / Laptop | Access | Trusted (VLAN 10) | None |
| Smart TV | Access | IoT (VLAN 20) | None |
| IoT Devices | Access | IoT (VLAN 20) | None |
| Guest Wired Device | Access | Guest (VLAN 30) | None |
| UniFi AP | Uplink | Management VLAN | Trusted, IoT, Guest |
| Switch Uplink | Trunk | Management VLAN | All required VLANs |

---

## Native VLAN Handling
- Native VLAN is explicitly defined on all ports
- No ports are left on default VLAN unintentionally
- Native VLAN selection matches the connected device’s trust level

This avoids:
- Accidental access to unintended networks
- Misplaced devices joining the wrong VLAN
- Troubleshooting ambiguity

---

## Tagged VLAN Management
- **End-device ports:** Tagged VLANs blocked
- **Infrastructure ports:** Tagged VLANs explicitly allowed

This ensures only VLAN-aware devices (switches, APs) handle tagged traffic.

---

## Security Considerations
- Endpoints cannot see or interact with VLANs outside their assigned network
- VLAN hopping risks are minimized
- Infrastructure devices are isolated from end-user misconfiguration
- Port behavior is predictable and auditable

---

## Operational Notes
- Port profiles are documented and reused consistently
- Any deviation from standard profiles is documented before deployment
- Changes to port profiles are reviewed alongside firewall rules

---

## Related Documentation
- Network overview: `network-overview.md`
- VLAN design: `vlan-design.md`
- Firewall rules: `firewall-rules.md`
