# Command Outputs — Network Connectivity Test (Part D)

Commands run: `ipconfig /all`, `ping google.com`, `tracert google.com`.

## Results

**ping google.com** → resolved to `142.250.146.138`
- Packets: Sent = 4, Received = 4, **Lost = 0 (0% loss)**
- Round-trip times: Min = 17 ms, Max = 26 ms, Avg = 20 ms

**tracert google.com** → 16 hops to `142.250.146.138`
- Hop 1: `192.168.1.1` (my router)
- Hop 2: `103.57.86.8` (ISP gateway, blr-tdc-bngs-13)
- Hops 3–9: ISP and Google backbone routers
- Hops 10–15: `Request timed out` (routers that don't reply to ICMP but still forward traffic)
- Hop 16: `pu-in-f138.1e100.net [142.250.146.138]` — destination reached, "Trace complete"

## Answers

**1. Was the ping successful?**
Yes. All 4 packets were sent and received with 0% loss and a low average latency of 20 ms, confirming a stable, working connection to google.com.

**2. How many hops were shown?**
16 hops to reach google.com. Hops 10–15 timed out (those routers silently forward traffic without responding to probes), but the route still completed successfully at hop 16.

**3. What is the purpose of traceroute?**
Traceroute maps the path packets take from my device to a destination, listing every router (hop) along the way and the time taken to reach each one. It's used to diagnose connectivity problems — for example, identifying *where* along the path traffic slows down or fails, distinguishing a local issue from an ISP or remote-server issue.

*Screenshots:* `ping.png`, `tracert.png`
