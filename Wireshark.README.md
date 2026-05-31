# Wireshark - Windows & Linux

---

# 1. Verify Wireshark Installation

### Objective

Confirm Wireshark is installed.

### Windows

```cmd
wireshark -v
```

### Linux

```bash
wireshark -v
```

### Expected Output

```text
Wireshark 4.x.x
```

### Interpretation

* Wireshark is installed correctly.

---

# 2. List Available Interfaces

### Objective

View available capture interfaces.

### Windows

```cmd
tshark -D
```

### Linux

```bash
tshark -D
```

### Expected Output

```text
1. Ethernet
2. Wi-Fi
3. Loopback
```

### Interpretation

* Shows interfaces available for packet capture.

---

# 3. Start Live Packet Capture

### Objective

Capture live network traffic.

### Windows

```cmd
tshark -i 1
```

### Linux

```bash
sudo tshark -i eth0
```

### Expected Output

```text
Capturing on Ethernet
1 0.000000 192.168.1.10 → 8.8.8.8 DNS
```

### Interpretation

* Live traffic is being captured.

---

# 4. Read a PCAP File

### Objective

Analyze previously captured traffic.

### Windows

```cmd
tshark -r sample.pcap
```

### Linux

```bash
tshark -r sample.pcap
```

### Expected Output

```text
1 0.000 DNS Query google.com
2 0.050 HTTP GET /
```

### Interpretation

* Packets are being read from the capture file.

---

# 5. Count Packets

### Objective

Determine packet volume.

### Windows/Linux

```bash
tshark -r sample.pcap | wc -l
```

### Expected Output

```text
1250
```

### Interpretation

* Capture contains 1,250 packets.

---

# 6. Display Only DNS Traffic

### Objective

Analyze domain lookups.

### Windows/Linux

```bash
tshark -r sample.pcap -Y dns
```

### Expected Output

```text
DNS Standard query A google.com
```

### Interpretation

* Shows DNS requests.

---

# 7. Display Only HTTP Traffic

### Objective

Analyze web browsing.

### Windows/Linux

```bash
tshark -r sample.pcap -Y http
```

### Expected Output

```text
GET /index.html HTTP/1.1
```

### Interpretation

* Shows HTTP requests.

---

# 8. Display Only TLS Traffic

### Objective

Analyze encrypted connections.

### Windows/Linux

```bash
tshark -r sample.pcap -Y tls
```

### Expected Output

```text
TLSv1.3 Client Hello
```

### Interpretation

* Shows encrypted HTTPS sessions.

---

# 9. Display Only ICMP Traffic

### Objective

Analyze ping traffic.

### Windows/Linux

```bash
tshark -r sample.pcap -Y icmp
```

### Expected Output

```text
Echo (ping) request
Echo (ping) reply
```

### Interpretation

* Shows ping activity.

---

# 10. Display Only TCP Traffic

### Objective

Analyze TCP sessions.

### Windows/Linux

```bash
tshark -r sample.pcap -Y tcp
```

### Expected Output

```text
TCP SYN
TCP SYN ACK
TCP ACK
```

### Interpretation

* Shows TCP connection establishment.

---

# 11. Display Only UDP Traffic

### Objective

Analyze UDP communication.

### Windows/Linux

```bash
tshark -r sample.pcap -Y udp
```

### Expected Output

```text
UDP 53 DNS Query
```

### Interpretation

* Shows UDP packets.

---

# 12. Find Traffic From a Specific IP

### Objective

Investigate a host.

### Windows/Linux

```bash
tshark -r sample.pcap -Y "ip.addr==192.168.1.10"
```

### Expected Output

```text
192.168.1.10 → 8.8.8.8
```

### Interpretation

* Displays all packets involving that IP.

---

# 13. Find Traffic to a Specific Port

### Objective

Investigate service usage.

### Windows/Linux

```bash
tshark -r sample.pcap -Y "tcp.port==80"
```

### Expected Output

```text
HTTP GET
HTTP Response
```

### Interpretation

* Shows traffic using port 80.

---

# 14. Show DNS Query Names

### Objective

Extract requested domains.

### Windows/Linux

```bash
tshark -r sample.pcap -Y dns -T fields -e dns.qry.name
```

### Expected Output

```text
google.com
github.com
microsoft.com
```

### Interpretation

* Lists queried domains.

---

# 15. Show Source and Destination IPs

### Objective

Identify communications.

### Windows/Linux

```bash
tshark -r sample.pcap -T fields -e ip.src -e ip.dst
```

### Expected Output

```text
192.168.1.10 8.8.8.8
192.168.1.10 142.250.190.78
```

### Interpretation

* Shows packet endpoints.

---

# 16. Follow a TCP Conversation (GUI)

### Objective

View a complete session.

### Wireshark GUI

```text
Right Click Packet
→ Follow
→ TCP Stream
```

### Expected Output

```text
GET /index.html HTTP/1.1
Host: example.com
```

### Interpretation

* Shows application-layer conversation.

---

# Most Important Wireshark Filters

| Objective         | Display Filter            |
| ----------------- | ------------------------- |
| DNS Traffic       | `dns`                     |
| HTTP Traffic      | `http`                    |
| HTTPS/TLS Traffic | `tls`                     |
| TCP Traffic       | `tcp`                     |
| UDP Traffic       | `udp`                     |
| Ping Traffic      | `icmp`                    |
| Specific IP       | `ip.addr == 192.168.1.10` |
| Port 80           | `tcp.port == 80`          |
| Port 443          | `tcp.port == 443`         |
| DNS Query Name    | `dns.qry.name`            |

---

# Workflow

### Step 1

Open a PCAP:

```bash
tshark -r sample.pcap
```

### Step 2

Check DNS:

```bash
tshark -r sample.pcap -Y dns
```

### Step 3

Check HTTP:

```bash
tshark -r sample.pcap -Y http
```

### Step 4

Check TLS:

```bash
tshark -r sample.pcap -Y tls
```

### Step 5

Identify IP addresses:

```bash
tshark -r sample.pcap -T fields -e ip.src -e ip.dst
```

### Step 6

Follow a TCP stream in the GUI.

1. Who communicated?
2. Which protocol was used?
3. Which domain was requested?
4. Which IP was contacted?
5. Which port was used?
6. What data was exchanged?

---

