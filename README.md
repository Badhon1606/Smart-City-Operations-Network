# Smart City Operations Network

A Cisco Packet Tracer simulation of the network infrastructure for **Metropolis Smart City Operations** — a centralized, fault-tolerant platform connecting all critical city services.

---

## Overview

The network integrates real-time data from traffic management, public utilities, emergency dispatch, civic portals, and environmental monitoring stations across the city.

### Operational Units

| Unit | Abbreviation | Devices | Role |
|------|-------------|---------|------|
| City Operations Hub | COH | 500 | Central backbone unit |
| Traffic Management Center | TMC | 300 | Manages all traffic signals and sensors |
| Public Utilities Node | PUN | 220 | Water, power, and waste monitoring |
| Emergency Dispatch Unit | EDU | 180 | Fire, police, ambulance coordination |
| Environmental Monitoring Post | EMP | 90 | Air quality, weather, flood sensors |
| Remote Field Station | RFS | 50 | Outpost with limited connectivity |

---

## Network Topology

- **COH** is the central backbone, connecting directly to TMC, EDU, and EMP
- **TMC** connects to PUN and EMP via a shared backbone switch
- **PUN** connects to EDU
- **RFS** connects only to EMP with no alternate path

Each unit is represented by a router with at least two PCs and one printer connected via a switch.

---

## Key Configurations

### Addressing
- Base network derived from group member student IDs using VLSM subnetting
- Subnetting order: COH → TMC → PUN → EDU → EMP → RFS → point-to-point links

### DHCP
- **COH** — dedicated DHCP server with IP helper address (relay)
- **TMC, PUN, EDU, EMP** — routers act as DHCP servers
- **RFS** — static IP addressing only (no DHCP)
- All routers, servers, and printers use static IPs

### Routing
- **RIPv2** — used among TMC, PUN, EDU, and COH (toward TMC and EMP)
- **Static routing** — COH uses next-hop static routes to EDU; RFS uses exit-interface static routes via EMP
- **Recursive static route** — EMP reaches COH via TMC as intermediate hop
- **Floating static route** — TMC has a backup route to COH via PUN (AD = 150), activates if primary RIPv2 link fails
- No default routes anywhere in the network

### Servers (hosted at COH)
- **DNS** — central DNS server
- **Web** — `www.metropolis.city` → "Smart City Operations - Online."
- **Email** — `mail.coh.city` and `mail.tmc.city` with SMTP and POP3

---

## Files

| File | Description |
|------|-------------|
| `Smart City Operations Network.pkt` | Cisco Packet Tracer simulation file |
| `Smart City Operations Network.pdf` | Project requirements and specifications |
| `Smart City Operations Network Configaration.pdf` | Full network configuration documentation |

---

## Tools Used

- [Cisco Packet Tracer](https://www.netacad.com/cisco-packet-tracer)
