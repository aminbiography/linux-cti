# Suricata (Windows & Linux)

1. **Objective** 
2. **Command** 
3. **Expected Output** 

---

## 1. Verify Suricata Installation

### Objective

Confirm Suricata is installed and operational.

### Windows

```cmd
suricata.exe -V
```

### Linux

```bash
suricata -V
```

### Expected Output

```text
This is Suricata version 8.0.1 RELEASE
```

### Interpretation

   **Suricata is installed correctly.**

---

# 2. View Build Information

### Objective

See which features were compiled into Suricata.

### Windows

```cmd
suricata.exe --build-info
```

### Linux

```bash
suricata --build-info
```

### Expected Output

```text
Suricata Configuration:
  Rust support: yes
  PCAP support: yes
  Hyperscan support: yes
```

### Interpretation

✅ Shows available capabilities.

---

# 3. List Supported Application Protocols

### Objective

See which protocols Suricata can inspect.

### Windows

```cmd
suricata.exe --list-app-layer-protos
```

### Linux

```bash
suricata --list-app-layer-protos
```

### Expected Output

```text
http
dns
tls
smtp
ftp
ssh
smb
mqtt
```

### Interpretation

✅ Suricata can decode these protocols.

---

# 4. Test Configuration

### Objective

Verify that `suricata.yaml` and rules load correctly.

### Windows

```cmd
suricata.exe -T -c suricata.yaml
```

### Linux

```bash
suricata -T -c /etc/suricata/suricata.yaml
```

### Expected Output

```text
Info: Configuration provided was successfully loaded
Info: 5000 rules processed
Success:
```

### Interpretation

✅ Configuration is valid.

---

# 5. Show Available Run Modes

### Objective

Display supported operating modes.

### Windows

```cmd
suricata.exe --list-runmodes
```

### Linux

```bash
suricata --list-runmodes
```

### Expected Output

```text
Runmodes:
  autofp
  workers
  single
```

### Interpretation

✅ Engine supports these processing modes.

---

# 6. Show Active Configuration

### Objective

Display current settings.

### Windows

```cmd
suricata.exe --dump-config
```

### Linux

```bash
suricata --dump-config
```

### Expected Output

```text
vars:
  address-groups:
    HOME_NET: "[192.168.1.0/24]"
```

```text
default-log-dir: log
```

### Interpretation

✅ Shows active runtime configuration.

---

# 7. Show Supported Features

### Objective

Display enabled engine features.

### Windows

```cmd
suricata.exe --dump-features
```

### Linux

```bash
suricata --dump-features
```

### Expected Output

```text
NFQ: no
PCAP: yes
Rust: yes
Lua: yes
```

### Interpretation

✅ Shows which components are available.

---

# 8. Analyze a PCAP File

### Objective

Analyze captured traffic offline.

### Windows

```cmd
suricata.exe -r sample.pcap -c suricata.yaml
```

### Linux

```bash
suricata -r sample.pcap -c /etc/suricata/suricata.yaml
```

### Expected Output

```text
Info: Processing sample.pcap
Info: Alerts: 5
Info: Packets: 12000
```

### Interpretation

✅ Traffic successfully analyzed.

---

# 9. Read Human-Friendly Alerts

### Objective

View IDS alerts.

### Windows

```cmd
type fast.log
```

### Linux

```bash
cat fast.log
```

### Expected Output

```text
[**] ET SCAN Nmap TCP Scan [**]
```

### Interpretation

✅ Suricata detected suspicious activity.

---

# 10. Read Structured Events

### Objective

View detailed event records.

### Windows

```cmd
type eve.json
```

### Linux

```bash
cat eve.json
```

### Expected Output

```json
{
  "event_type":"dns",
  "src_ip":"192.168.1.10",
  "dest_ip":"8.8.8.8"
}
```

### Interpretation

✅ DNS traffic recorded.

---

# 11. Monitor Live Traffic

### Objective

Capture and inspect live network traffic.

### Windows

```cmd
suricata.exe -i 1 -c suricata.yaml
```

### Linux

```bash
suricata -i eth0 -c /etc/suricata/suricata.yaml
```

### Expected Output

```text
Info: Starting capture on interface
Info: Packets captured: 0
```

As traffic appears:

```text
Info: Packets captured: 1500
```

### Interpretation

✅ Live monitoring is active.

---

# 12. Test a Custom Rule

### Objective

Validate your own detection rule.

### Example Rule

```text
alert icmp any any -> any any (msg:"Ping Detected"; sid:1000001; rev:1;)
```

### Windows

```cmd
suricata.exe -T -S local.rules
```

### Linux

```bash
suricata -T -S local.rules
```

### Expected Output

```text
Info: 1 rule successfully loaded
Success:
```

### Interpretation

✅ Rule syntax is valid.

---

# 13. Increase Verbosity

### Objective

Get more troubleshooting details.

### Windows

```cmd
suricata.exe -vv
```

### Linux

```bash
suricata -vv
```

### Expected Output

```text
Info: Loading signatures
Info: Initializing detection engine
Info: Capture started
```

### Interpretation

✅ Useful for debugging startup issues.

---

# Beginner Workflow (Daily Practice)

### Step 1 – Verify Installation

```cmd
suricata.exe -V
```

Expected:

```text
This is Suricata version 8.0.1 RELEASE
```

---

### Step 2 – Validate Configuration

```cmd
suricata.exe -T -c suricata.yaml
```

Expected:

```text
Success:
```

---

### Step 3 – Analyze Traffic

```cmd
suricata.exe -r sample.pcap -c suricata.yaml
```

Expected:

```text
Processing complete
```

---

### Step 4 – Check Alerts

```cmd
type fast.log
```

Expected:

```text
ET SCAN
ET POLICY
ET TROJAN
```

---

### Step 5 – Check Detailed Events

```cmd
type eve.json
```

Expected:

```json
{
 "event_type":"dns"
}
{
 "event_type":"http"
}
{
 "event_type":"tls"
}
{
 "event_type":"alert"
}
```

If you can understand the outputs of these **five commands**, you have already covered roughly **70% of beginner-level Suricata operations** on both Windows and Linux.

