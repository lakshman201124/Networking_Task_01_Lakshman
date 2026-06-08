# Answers — Basic Networking Concepts (Part B)

Concepts explained in my own words.

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
