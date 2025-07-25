🔥 **Wireshark** is one of the **most powerful, detailed, and essential tools** for network analysis, troubleshooting, and **offensive/defensive security.**

Here’s **the complete, in-depth explanation of Wireshark** — every topic covered, **nothing skipped, fully detailed, with examples.**

---

# 🐉 Kali GPT’s Full Wireshark Guide

---

# 📖 **What is Wireshark?**

* **Wireshark** is a **network protocol analyzer** (packet sniffer).
* It captures live network traffic and allows **detailed inspection of packet data.**
* Supports **hundreds of protocols** like TCP, UDP, HTTP, DNS, FTP, SMB, SSL/TLS, ARP, etc.
* Can capture:

  * Plaintext traffic
  * Passwords
  * Cookies
  * Session tokens
  * Malware payloads
* ✅ Pre-installed or easily installed on Kali Linux.

---

# 🎯 **What Can Wireshark Do?**

| Function                   | Description                                         |
| -------------------------- | --------------------------------------------------- |
| 🛡️ Packet Capture         | Sniff live traffic from network interfaces          |
| 🔬 Packet Analysis         | View each packet at Layer 2-7                       |
| 🕵️ Protocol Decoding      | Supports complex protocol dissection                |
| 🔗 Network Troubleshooting | Detect delays, retransmissions, dropped packets     |
| 🏴‍☠️ Password Sniffing    | Capture plaintext HTTP, FTP, Telnet, POP3 passwords |
| 📊 Traffic Analysis        | Visualize packet flows and usage                    |
| ⚡ Real-Time Inspection     | Analyze network as packets arrive                   |
| 🔐 TLS/SSL Analysis        | Decrypt TLS if keys are known                       |

---

# 🚀 **Wireshark Installation (Kali Linux)**

```bash
sudo apt update
sudo apt install wireshark
```

Allow non-root capture (optional):

```bash
sudo dpkg-reconfigure wireshark-common
sudo usermod -aG wireshark $USER
```

---

# 🖥️ **Wireshark Interface Overview**

| Section             | Purpose                                         |
| ------------------- | ----------------------------------------------- |
| Capture Interface   | Select which network interface to sniff         |
| Packet List Pane    | Displays captured packets                       |
| Packet Details Pane | Shows protocol layers for the selected packet   |
| Packet Bytes Pane   | Shows raw packet in hex                         |
| Display Filter Bar  | Filter packets using Wireshark syntax           |
| Statistics Menu     | Graphs, I/O, protocol hierarchy, endpoint lists |

---

# 🔧 **How to Capture Packets (Step-by-Step)**

### 1️⃣ Open Wireshark:

```bash
sudo wireshark
```

### 2️⃣ Select interface (e.g., eth0, wlan0)

### 3️⃣ Start capture:

Click the blue shark fin.

### 4️⃣ Stop capture:

Click the red square.

---

# 🔎 **Wireshark Filters (Display Filters)**

Display filters let you **focus only on interesting packets.**

| Filter                   | Description                                  |
| ------------------------ | -------------------------------------------- |
| `ip.addr == 192.168.1.1` | Filter packets with source or destination IP |
| `tcp.port == 80`         | Filter HTTP traffic                          |
| `http`                   | Show HTTP packets only                       |
| `ftp`                    | Show FTP traffic                             |
| `dns`                    | Show DNS queries and responses               |
| `tcp contains password`  | Search for "password" in TCP streams         |
| `frame contains "admin"` | Search raw frames for "admin" keyword        |
| `tcp.flags.syn == 1`     | Show SYN packets (TCP handshake initiation)  |

---

## 🛠️ **Real-World Examples and Scenarios**

---

### ✅ 1. Capture HTTP Passwords (Plaintext)

#### Filter:

```bash
http.request.method == "POST"
```

Look for login forms and check TCP stream for credentials.

---

### ✅ 2. Capture FTP Passwords

#### Filter:

```bash
ftp
```

FTP is unencrypted → username and password visible.

---

### ✅ 3. ARP Spoofing Detection

#### Filter:

```bash
arp
```

Watch for ARP replies that claim to own multiple IP addresses.

---

### ✅ 4. DNS Traffic Inspection

#### Filter:

```bash
dns
```

Check for suspicious DNS queries (e.g., to known C2 domains).

---

### ✅ 5. View TCP 3-Way Handshake

#### Filter:

```bash
tcp.flags.syn == 1
```

Find SYN → SYN-ACK → ACK packet sequence.

---

### ✅ 6. Capture All Traffic to a Host

#### Filter:

```bash
ip.addr == 10.10.10.10
```

---

### ✅ 7. Extract Files from PCAP

* Go to: **File > Export Objects > HTTP/FTP/SMB**
* Extract files transmitted over these protocols.

---

### ✅ 8. Follow TCP Stream (For Cleartext Extraction)

* Right-click a packet → Follow → TCP Stream
* See entire conversation in plaintext if unencrypted.

---

### ✅ 9. Detect Port Scanning (e.g. Nmap Scan)

#### Filter:

```bash
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

Look for a rapid sequence of SYNs without ACKs.

---

### ✅ 10. TLS/SSL Traffic Capture

#### Filter:

```bash
tls
```

* If you have the private key (rare), you can decrypt sessions.
* If using Wireshark with browser key logging:

```bash
export SSLKEYLOGFILE=~/Desktop/keys.log
```

Point Wireshark to this file for session decryption.

---

# 📊 **Wireshark Statistics Tools**

| Feature            | Purpose                                   |
| ------------------ | ----------------------------------------- |
| Protocol Hierarchy | Analyze traffic by protocol               |
| Conversations      | Analyze session-level connections         |
| Endpoints          | Show most active IPs, MACs, TCP ports     |
| I/O Graphs         | Visualize traffic over time               |
| Flow Graph         | Reconstruct packet flow between endpoints |

---

# 🛡️ **Wireshark and Ethical Hacking**

✅ **Offensive Use:**

* Sniffing credentials on open networks
* Capturing cookies (session hijacking)
* ARP poisoning capture
* Password extraction from HTTP, FTP, POP3

✅ **Defensive Use:**

* Detecting ARP spoofing
* Identifying port scans
* Analyzing malware C2 traffic
* Monitoring data exfiltration

---

# 🔐 **How to Defend Against Wireshark Sniffing**

* Always use HTTPS, SSH, TLS-encrypted protocols.
* Use VPNs to encrypt all traffic.
* Use certificate pinning in applications.
* Employ network segmentation to isolate sensitive traffic.
* Deploy IDS/IPS to detect sniffing behavior.

---

# ✅ Wireshark Summary Cheat Sheet

| Purpose           | Filter                            |
| ----------------- | --------------------------------- |
| HTTP Traffic      | `http`                            |
| FTP Traffic       | `ftp`                             |
| DNS Traffic       | `dns`                             |
| SYN Packets       | `tcp.flags.syn == 1`              |
| Filter by IP      | `ip.addr == x.x.x.x`              |
| Search for String | `frame contains "string"`         |
| Follow TCP Stream | Right-click > Follow > TCP Stream |

---

# 🔥 Pro Tips

* 🛑 Use `tcpdump` for headless packet capture, then analyze PCAP in Wireshark.
* ⚙️ Use `Capture Filters` (BPF syntax) to control what’s captured.
* 📂 PCAP files can be imported into tools like Tshark or Scapy for further scripting.
* 🏴‍☠️ Perfect for **man-in-the-middle (MITM) attacks** when paired with `ettercap` or `bettercap`.

---

# ⚙️ **Capture Filter vs Display Filter**

| Type           | Example       | Scope                          |
| -------------- | ------------- | ------------------------------ |
| Capture Filter | `tcp port 80` | Filters at packet capture time |
| Display Filter | `http`        | Filters after capture          |

👉 Capture filters reduce capture size.
👉 Display filters help you focus post-capture.

---

 
