# Firewall Rules

## Purpose
This document defines the firewall policy applied at the UniFi Dream Machine SE (UDM-SE) to control traffic flow between VLANs and the internet.

The firewall configuration follows a **default-deny** approach and enforces strict trust boundaries between network zones.

---

## Firewall Design Philosophy
- **Deny by default** between all VLANs
- **Explicit allow rules** for required traffic only
- **Stateful inspection** for established and related connections
- **Untrusted zones** (IoT, Guest) are never allowed to initiate connections to trusted networks
- **Logging enabled** for critical deny rules to aid troubleshooting and auditing

---

## Zone Trust Model

| Zone | Trust Level | Description |
|-----|------------|------------|
| Trusted | High | Managed user devices |
| IoT | Medium-Low | Unmanaged or semi-trusted devices |
| Guest | Low | Fully untrusted devices |

---

## Inter-VLAN Firewall Policy

### Allowed Traffic

| Rule | Source | Destination | Action | Reason |
|----|-------|------------|--------|--------|
| F-01 | Trusted | WAN | Allow | Normal internet access |
| F-02 | Trusted | IoT | Allow (restricted) | Media streaming and device control |
| F-03 | IoT | WAN | Allow (restricted) | Cloud-based IoT services |
| F-04 | Guest | WAN | Allow | Internet access only |

---

### Denied Traffic

| Rule | Source | Destination | Action | Reason |
|----|-------|------------|--------|--------|
| F-05 | IoT | Trusted | Deny (log) | Prevent lateral movement |
| F-06 | Guest | Trusted | Deny (log) | Security isolation |
| F-07 | Guest | IoT | Deny (log) | Prevent cross-zone access |
| F-08 | Any | Management interfaces | Deny | Protect infrastructure |

---

## Rule Ordering Strategy
Firewall rules are evaluated **top-down**, with:
1. Explicit allow rules for required traffic
2. Explicit deny rules for restricted flows
3. Implicit default deny for all other traffic

Critical deny rules are placed above general allow rules to avoid accidental bypass.

---

## Stateful Traffic Handling
- Return traffic for established sessions is automatically allowed
- No inbound rules are created for untrusted VLANs
- Port forwarding is disabled for IoT and Guest networks

---

## Logging and Monitoring
- Deny rules between VLANs are logged
- Logs are reviewed during troubleshooting and network changes
- Excessive logging is avoided to reduce noise

---

## Security Considerations
- IoT devices are treated as potentially compromised by default
- Guest devices are never trusted
- Management plane access is restricted to the Trusted VLAN only
- Firewall rules are reviewed after network changes

---

## Related Documentation
- Network overview: `network-overview.md`
- VLAN design: `vlan-design.md`
- Switch port profiles: `switch-port-profiles.md`
