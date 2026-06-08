# Networking Task 01 — Understanding Your Network Environment

**Author:** Lakshman
**OS used:** Windows 11 (Version 10.0.26200)
**Date:** 08 June 2026

This task explores the basic components of a computer network and documents the live network configuration of my own device using built-in Windows command-line tools.

---

## Part A — Network Information

Collected using `ipconfig /all`. The active connection is the **WiFi adapter** (Realtek RTL8188EU 802.11n USB); the Ethernet adapter was disconnected.

| # | Detail | Value |
|---|--------------------------|-----------------------------------|
| 1 | Hostname (Device Name)   | `LakshmanPC`                      |
| 2 | IPv4 Address             | `192.168.1.28`                    |
| 3 | MAC Address (Physical)   | `7C-C2-C6-20-CB-FB`               |
| 4 | Default Gateway          | `192.168.1.1`                     |
| 5 | DNS Server               | `103.57.86.8` (blr-tdc-bngs-13)   |

Additional details: Subnet Mask `255.255.255.0`, DHCP Enabled (lease obtained 08 June 2026, expires 09 June 2026), Link-local IPv6 `fe80::6b45:959b:1d6f:5e05`.

> Note: The DNS server is the ISP's resolver (`103.57.86.8`), not the local router. The same node also appears as hop 2 in the traceroute below (blr-tdc-bngs-13), confirming it is the ISP's broadband network gateway.

*Screenshot:* `ipconfig_all.png`

---

## Part B — Basic Networking Concepts (in my own words)

**IP Address**
A numeric label assigned to every device on a network so data can be sent to and from the correct place — like a postal address for a computer. My device's IPv4 is `192.168.1.28`. IPv4 uses four numbers (0–255) separated by dots.

**MAC Address**
A permanent hardware identifier burned into a network adapter by the manufacturer (e.g. `7C-C2-C6-20-CB-FB`). While an IP address can change, the MAC stays fixed to the physical hardware and is used to identify devices on the *local* network (Layer 2).

**Default Gateway**
The device (usually the home router, here `192.168.1.1`) that forwards traffic from my local network to other networks, especially the internet. If a packet's destination isn't on my own network, it's handed to the gateway to route onward.

**DNS (Domain Name System)**
The "phonebook of the internet." It translates human-readable names like `google.com` into machine IP addresses (e.g. `142.250.146.138`). Without DNS I'd have to memorise raw IP numbers for every website. My resolver is `103.57.86.8`.

**Public IP vs Private IP**
- **Private IP** — used *inside* a local network (ranges like `192.168.x.x`, `10.x.x.x`, `172.16–31.x.x`). Not reachable directly from the internet. My `192.168.1.28` is private.
- **Public IP** — assigned by the ISP and visible to the whole internet; it's how my home network is reached from outside. Many private devices share one public IP through the router using NAT (Network Address Translation).

---

## Part C — Basic Network Diagram

How my device connects to the internet, with real IPs labelled:

```
                 INTERNET
                    |
                    |  (ISP gateway: blr-tdc-bngs-13, 103.57.86.8)
                    |
        +-----------------------+
        |   Router / WiFi       |
        |   192.168.1.1         |   <-- Default Gateway
        +-----------------------+
                    |
                    |  WiFi (Realtek 802.11n USB)
                    |
        +-----------------------+
        |   My Device           |
        |   LakshmanPC          |
        |   IPv4: 192.168.1.28  |
        |   MAC: 7C-C2-C6-20-CB-FB |
        +-----------------------+
```

*Diagram file:* `network_diagram.png`

---

## Part D — Network Connectivity Test

Commands run: `ipconfig /all`, `ping google.com`, `tracert google.com`.

### Results

**ping google.com** → resolved to `142.250.146.138`
- Packets: Sent = 4, Received = 4, **Lost = 0 (0% loss)**
- Round-trip times: Min = 17 ms, Max = 26 ms, Avg = 20 ms

**tracert google.com** → 16 hops to `142.250.146.138`
- Hop 1: `192.168.1.1` (my router)
- Hop 2: `103.57.86.8` (ISP gateway, blr-tdc-bngs-13)
- Hops 3–9: ISP and Google backbone routers
- Hops 10–15: `Request timed out` (routers that don't reply to ICMP but still forward traffic)
- Hop 16: `pu-in-f138.1e100.net [142.250.146.138]` — destination reached, "Trace complete"

### Answers

**1. Was the ping successful?**
Yes. All 4 packets were sent and received with 0% loss and a low average latency of 20 ms, confirming a stable, working connection to google.com.

**2. How many hops were shown?**
16 hops to reach google.com. Hops 10–15 timed out (those routers silently forward traffic without responding to probes), but the route still completed successfully at hop 16.

**3. What is the purpose of traceroute?**
Traceroute maps the path packets take from my device to a destination, listing every router (hop) along the way and the time taken to reach each one. It's used to diagnose connectivity problems — for example, identifying *where* along the path traffic slows down or fails, distinguishing a local issue from an ISP or remote-server issue.

*Screenshots:* `ping.png`, `tracert.png`

---

## Files in This Folder

- `README.md` — this summary
- Screenshots: `ipconfig_all.png`, `ping.png`, `tracert.png`
- `network_diagram.png` — network diagram (Part C)
