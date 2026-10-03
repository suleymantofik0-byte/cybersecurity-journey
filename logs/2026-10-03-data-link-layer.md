# Data Link Layer (Layer 2): MAC vs IP Addresses

**Date:** 2026-10-03

## What the Data Link layer does

The Data Link layer moves **frames** between devices on the **same local network** (the same LAN or broadcast domain). It adds a header and trailer to the packet from Layer 3, handles physical (MAC) addressing, detects errors with a Frame Check Sequence (FCS), and controls access to the shared medium. It is split into two sublayers:

- **LLC (Logical Link Control):** identifies the upper-layer protocol and handles flow control.
- **MAC (Media Access Control):** handles hardware addressing and decides when a device may transmit.

Switches and network interface cards (NICs) operate at this layer. Common protocols include Ethernet (802.3) and Wi-Fi (802.11).

## MAC address vs IP address

| | MAC address | IP address |
|---|-------------|------------|
| OSI layer | 2 (Data Link) | 3 (Network) |
| Type | Physical / hardware address | Logical address |
| Length | 48 bits (6 bytes), written as `AA:BB:CC:DD:EE:FF` | 32 bits (IPv4) or 128 bits (IPv6) |
| Assigned by | Manufacturer, burned into the NIC (the first half is the vendor ID, called the OUI) | Network admin or DHCP, based on the network the device joins |
| Changes? | Usually fixed (though it can be spoofed or randomized) | Changes when the device moves to another network |
| Scope | Only used inside the local network | Used end to end, across networks and the internet |
| Used by | Switches | Routers |

## Why each one matters

**MAC addresses** tell a switch exactly which port a frame should go out of on the local network. Without them, devices on the same LAN could not deliver frames to each other.

**IP addresses** tell routers where a packet should go across many networks. They are hierarchical (network part + host part), so routers can forward traffic without knowing every device in the world.

## How they work together

When my laptop sends data to a server on the internet:

1. The **source and destination IP addresses** stay the same for the whole trip (apart from NAT).
2. The **MAC addresses change at every hop**. My laptop addresses the frame to my **router's MAC** (the next hop), the router then rewrites the frame with a new source and destination MAC for the next link, and so on.
3. **ARP (Address Resolution Protocol)** is how a device finds the MAC address that belongs to a known IP address on the local network.

## Why it matters for a SOC analyst

- **ARP spoofing / poisoning** abuses the link between IP and MAC to perform man-in-the-middle attacks on a LAN.
- **MAC flooding** overwhelms a switch's MAC address table so it starts acting like a hub.
- **MAC spoofing** can bypass weak MAC-based filtering or impersonate another device.
- Mapping an IP to a MAC in logs (DHCP leases, switch tables) helps trace an alert back to a physical device.

## Still to practice

- Run `arp -a` and `ipconfig /all` (or `ip neigh` and `ip a`) and match IPs to MACs on my own network.
- Capture an ARP request and reply in Wireshark.
