# 🦈 Wireshark — Complete Detailed Guide  

---

## 📖 What is Wireshark?

**Wireshark** is a free, open-source, and powerful **network packet analyzer** that captures and displays data packets traveling through a network in real-time.

It helps:
- **Inspect network traffic**
- **Troubleshoot network issues**
- **Analyze security incidents**
- **Reverse-engineer protocols**
- **Learn about how networking works**

---

## 🛠️ Features of Wireshark  

✅ Real-time **packet capturing**  
✅ **Detailed protocol analysis**  
✅ Support for **hundreds of protocols (TCP, UDP, HTTP, DNS, etc.)**  
✅ Capture from **Ethernet, Wi-Fi, Bluetooth, VPN tunnels**  
✅ **Filtering, sorting, and highlighting** of captured packets  
✅ **Export and save capture data** in various formats  
✅ Supports **decryption for protocols like SSL/TLS, WPA/WPA2**  
✅ Works on **Linux, Windows, macOS**

---

## 📦 Installation

### 📌 On Kali Linux (Pre-installed)
Check version:
```bash
wireshark --version
```

If not:
```bash
sudo apt update
sudo apt install wireshark
```

Add user to Wireshark group to capture without root:
```bash
sudo usermod -aG wireshark $(whoami)
sudo reboot
```

---

## 🎛️ How Wireshark Works  

Wireshark captures **network frames (packets)** from network interfaces like Ethernet, Wi-Fi, or virtual interfaces.  
It decodes the protocols and allows you to:
- **View live packet streams**
- **Filter traffic by protocol, IP, or port**
- **Inspect packet contents in detail**

---

## 🕹️ Basic Usage  

**Start Wireshark GUI:**
```bash
wireshark
```

**Start capturing:**
- Select your **network interface (eth0, wlan0, etc.)**
- Click **Start Capturing Packets**

**Stop capturing:**
- Click **Stop**

---

## 🔍 Display Filters  

Use filters to narrow down the packets you want to analyze.

| Filter Example | Description |
|:----------------|:--------------------|
| `ip.addr == 192.168.1.1` | Show traffic to/from 192.168.1.1 |
| `tcp.port == 80` | Show HTTP traffic |
| `udp` | Show only UDP packets |
| `http` | Show only HTTP traffic |
| `dns` | Show DNS traffic |
| `tcp.flags.syn == 1` | Show TCP SYN packets |
| `ip.src == 10.0.0.2` | Show packets from a specific source IP |
| `tcp.analysis.retransmission` | Show retransmitted TCP packets |

👉 Enter these in the **Display Filter** bar.

---

## 📊 Example Packet Analysis  

When you click on a captured packet, you’ll see:
1. **Frame info:** Number, size, capture time.
2. **Ethernet Header:** Source & destination MAC addresses.
3. **IP Header:** Source & destination IP addresses.
4. **Protocol info:** TCP/UDP/ICMP flags, ports.
5. **Payload data:** Actual transmitted content (if available).

---

## ⚙️ Capture Filters (Before Capture)  

Capture only what you need from the start.

| Capture Filter | Description |
|:----------------|:--------------------|
| `host 192.168.1.5` | Capture traffic to/from specific IP |
| `port 80` | Capture HTTP traffic |
| `tcp` | Capture only TCP traffic |
| `udp` | Capture only UDP traffic |
| `net 192.168.1.0/24` | Capture traffic from subnet |
| `src 192.168.1.5` | Capture packets sent from an IP |
| `dst port 443` | Capture HTTPS traffic |

👉 Go to **Capture Options** → Enter this in **Capture Filter**.

---

## 🔐 Decrypt SSL/TLS (Optional)

If you have the SSL keys:
1. Go to **Edit → Preferences → Protocols → SSL**
2. Enter the SSL key log file path.
3. Wireshark will decrypt HTTPS traffic.

---

## 📁 Exporting and Saving

| Format | Use |
|:-------------|:----------------|
| **.pcap/.pcapng** | Raw packet capture (used by other tools) |
| **.csv/.json** | Export as readable data |
| **.txt** | Export selected packet details |

---

## 🎯 Common Use Cases  

| Situation | How Wireshark Helps |
|:--------------|:----------------|
| **Detect Network Attacks** | View abnormal traffic spikes, SYN floods, scans |
| **Capture Credentials** | If traffic is unencrypted, see usernames, passwords |
| **Monitor HTTP/HTTPS** | See requests, responses, status codes |
| **DNS Analysis** | Look up which domains a device queries |
| **Troubleshooting** | Identify dropped packets, retransmissions, delays |
| **Reverse Engineering** | Analyze unknown protocols, malware traffic |
| **Capture Hidden Devices** | Detect rogue devices on the network |

---

## 📌 Wireshark CLI Tool — tshark  

Wireshark has a terminal-based tool too:
```bash
tshark -i wlan0
```

Common commands:
```bash
tshark -i eth0 -c 50                # Capture 50 packets
tshark -i wlan0 -f "port 80"        # Capture HTTP traffic only
tshark -r capture.pcap              # Read a pcap file
tshark -i eth0 -Y "ip.addr==192.168.1.1"   # Filter specific IP
```

---

## ✅ Summary  

| What It Does | How |
|:------------------|:------------|
| **Capture network packets in real-time** | From any connected interface |
| **Analyze packets, headers, payloads** | Through detailed GUI layers |
| **Filter by protocols, IPs, ports** | Display and Capture filters |
| **Support multiple export formats** | PCAP, CSV, XML, JSON |
| **Decrypt encrypted traffic** | With appropriate keys |
| **Find attacks, weaknesses, and errors** | Through expert analysis |
| **Command-line support via tshark** | Lightweight CLI capture |

---

## 📝 Wireshark Cheat Sheet  

```bash
wireshark                             # Start GUI
wireshark -k -i wlan0                 # Start capturing on wlan0

# Common Capture Filters (before capture)
host 192.168.1.1
port 80
tcp
udp

# Common Display Filters (after capture)
ip.addr == 192.168.1.1
tcp.port == 443
http
dns
tcp.flags.syn == 1

# tshark Examples (CLI)
tshark -i eth0 -c 100
tshark -r capture.pcap
tshark -i eth0 -Y "ip.addr==10.0.0.5"
```

---

