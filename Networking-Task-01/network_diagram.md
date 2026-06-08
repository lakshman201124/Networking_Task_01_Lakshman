# Network Diagram (Part C)

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
