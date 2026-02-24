# UniFi Home Lab – Network Architecture & Segmentation

## Overview
This repository documents the design, implementation, and troubleshooting of a UniFi-based home lab network built using a UniFi Dream Machine SE (UDM-SE) and UniFi U7 Pro access point.

The project is designed to mirror production-style network engineering practices, with a strong emphasis on segmentation, security boundaries, and clear documentation.

## Objectives
- Design and implement VLAN-based network segmentation
- Enforce firewall isolation between network zones
- Apply correct switch port profiles (access vs native VLAN)
- Map Wi-Fi SSIDs to dedicated VLANs
- Document real-world troubleshooting scenarios

## Environment
### Hardware
- UniFi Dream Machine SE (UDM-SE)
- UniFi U7 Pro Access Point
- UniFi managed switches

### Network Zones
- Trusted (Primary user devices)
- IoT (Smart TV and smart devices)
- Guest (Isolated guest access)

## Key Concepts Demonstrated
- VLAN design and traffic isolation
- Firewall rule logic and traffic flow control
- Access ports vs trunk behavior
- IoT network containment
- Production-style documentation and change tracking

## Repository Structure
- `/docs` – Network design and configuration documentation
- `/diagrams` – Logical and physical topology diagrams
- `/configs` – Configuration references and design tables
- `/lessons-learned` – Mistakes, fixes, and future improvements

## Status
This project is actively documented and expanded as the lab evolves.
