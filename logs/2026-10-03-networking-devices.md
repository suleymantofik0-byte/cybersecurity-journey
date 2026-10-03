# Networking Devices

**Date:** 2026-10-03

## Overview

Different devices work at different OSI layers and do different jobs. Knowing what each one does (and what it can and cannot see) is essential for reading network diagrams and for understanding where security controls sit.

## Quick reference

| Device | Main job | OSI layer | Security relevance |
|--------|----------|-----------|--------------------|
| Router | Forwards packets between different networks using IP addresses | 3 (Network) | Connects the LAN to the internet; ACLs and NAT are configured here |
| Switch | Forwards frames inside a LAN using MAC addresses | 2 (Data Link) | Port security, VLANs, and segmentation; targeted by MAC flooding |
| Firewall | Allows or blocks traffic based on rules | 3 to 4 (stateful), up to 7 (next-gen) | Enforces the network boundary and segmentation |
| IDS / IPS | Detects (IDS) or detects and blocks (IPS) suspicious traffic | 3 to 7 | Primary source of alerts for a SOC |
| Load balancer | Distributes traffic across multiple servers | 4 or 7 | Availability; helps absorb DDoS and removes single points of failure |
| Proxy | Sits between clients and servers and makes requests on their behalf | 7 (Application) | Web filtering, caching, anonymity, and logging of user traffic |
| NAS | File-level storage shared over the network | Application level | Holds shared files; needs access control and backups |
| SAN | Block-level storage network for servers | Storage fabric | Holds critical data such as databases and VMs |
| Access point (AP) | Connects wireless devices to the wired network | 2 (Data Link) | Wi-Fi security (WPA2/WPA3); rogue APs are a risk |

## Details

### Router

Connects different networks together and chooses the best path for each packet using routing tables. A home router also does NAT, DHCP, and often includes a basic firewall and Wi-Fi.

### Switch

Learns which MAC address lives on which port and sends frames only to the correct port, unlike a hub, which repeats traffic to everyone. Managed switches support VLANs, port security, and monitoring (SPAN/mirror ports).

### Firewall

Filters traffic using rules. Types include packet-filtering, **stateful** (tracks connections), and **next-generation (NGFW)**, which understands applications, users, and can inspect content. It can be hardware, software, or cloud-based.

### IDS / IPS

- **IDS (Intrusion Detection System):** monitors a copy of the traffic and **alerts**. It is passive, so it does not block anything.
- **IPS (Intrusion Prevention System):** sits **inline** and can **block** malicious traffic automatically.
- Detection methods: signature-based (known patterns), anomaly-based (deviation from normal), and behavior-based.
- Watch out for **false positives** (harmless traffic flagged) and **false negatives** (real attacks missed).

### Load balancer

Spreads incoming requests across a pool of servers using algorithms such as round robin or least connections. It checks server health and stops sending traffic to servers that are down.

### Proxy

- **Forward proxy:** clients go through it to reach the internet (content filtering, logging).
- **Reverse proxy:** sits in front of servers and receives requests for them (protection, caching, TLS termination).

### NAS vs SAN

- **NAS (Network Attached Storage):** a storage device on the LAN that shares **files** (SMB/NFS). Easy to set up, good for file sharing and backups.
- **SAN (Storage Area Network):** a dedicated high-speed network that gives servers **block-level** storage that looks like a local disk. Used for databases, virtualization, and enterprise workloads.

### Access point

Bridges wireless clients to the wired network. Unlike a wireless router, an AP usually does not route; it just extends the LAN over Wi-Fi.

## Why it matters for a SOC analyst

- Firewall, IDS/IPS, proxy, and switch logs are the raw material for investigations.
- Knowing where each device sits in the network tells me what traffic it can see, and what it is blind to.
- Common mix-ups to remember: IDS only alerts, IPS blocks; firewall filters by rules, IDS/IPS inspects for malicious behavior; NAS is file-level, SAN is block-level.

## Still to practice

- Draw a simple network diagram placing each device in the correct position.
- Look at real firewall and proxy log samples.
