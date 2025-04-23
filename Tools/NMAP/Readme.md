Great question — let’s break down **Nmap** clearly and thoroughly.  
I’ll explain the theory, practical uses, and then list useful commands for you.

---

# 📖 Nmap — Full Theory & Commands

---

## 📌 What is Nmap?

**Nmap (Network Mapper)** is a free, open-source network scanning tool used to:
- **Discover hosts and services** on a computer network.
- **Audit security** and identify vulnerabilities.
- **Map a network's structure** and devices.
- **Check open ports**, services, and running versions.

It is heavily used in **hacking**, **penetration testing**, **cybersecurity audits**, and **network administration**.

---

## 📌 What Can Nmap Do?

✔️ Host discovery (finding live devices)  
✔️ Port scanning (find open/closed/filtered ports)  
✔️ Service detection (detect service versions and software info)  
✔️ OS detection (identify operating systems)  
✔️ Script scanning (run predefined scripts for vulnerabilities)  
✔️ Network mapping

---

## 📌 How Does Nmap Work?

Nmap sends specially crafted packets to target systems and **analyzes the responses** to:
- Check if hosts are **up or down**.
- Find out **which ports are open/closed/filtered**.
- Detect **services running on those ports**.
- Identify **OS type and version** (if possible).
- Run **vulnerability detection scripts** (via Nmap Scripting Engine).

---

## 📌 Nmap Port States

- **open** → Application actively accepting connections.  
- **closed** → Port reachable but no application is listening.  
- **filtered** → Nmap can't determine (firewall might be blocking).  
- **unfiltered** → Nmap can access, but can't determine if open/closed.  
- **open|filtered** → Possibly open, but Nmap isn't sure.  
- **closed|filtered** → Possibly closed, but Nmap isn't sure.

---

## 📌 Nmap Scan Types

| Scan Type            | Command Option | Description                                  |
|:--------------------|:---------------|:----------------------------------------------|
| TCP SYN Scan         | `-sS`           | Stealth scan — sends SYN, waits for response. |
| TCP Connect Scan     | `-sT`           | Full TCP connection (less stealthy).          |
| UDP Scan             | `-sU`           | Scans UDP ports.                              |
| TCP ACK Scan         | `-sA`           | Checks firewall rules.                        |
| Xmas Scan            | `-sX`           | Sends FIN, URG, PSH flags.                    |
| Null Scan            | `-sN`           | Sends no flags (blank packet).                |
| FIN Scan             | `-sF`           | Sends only FIN flag.                          |
| Ping Scan (Host discovery) | `-sn`       | Check which hosts are alive without ports.     |

---

## 📌 Nmap Useful Commands  

### 📌 Basic Host Discovery
```bash
nmap 192.168.1.1
```
- Scan a single IP.

```bash
nmap 192.168.1.0/24
```
- Scan a subnet.

---

### 📌 Stealth (SYN) Scan  
```bash
nmap -sS 192.168.1.1
```
- Most common scan — avoids full TCP handshake.

---

### 📌 Scan Multiple IPs  
```bash
nmap 192.168.1.1 192.168.1.5 192.168.1.10
```

---

### 📌 Service and Version Detection  
```bash
nmap -sV 192.168.1.1
```
- Detect service versions on open ports.

---

### 📌 OS Detection  
```bash
nmap -O 192.168.1.1
```
- Tries to detect the operating system.

---

### 📌 Aggressive Scan  
```bash
nmap -A 192.168.1.1
```
- Combines `-O`, `-sV`, script scanning, and traceroute.

---

### 📌 Scan Specific Port  
```bash
nmap -p 80 192.168.1.1
```
- Scan only port 80.

```bash
nmap -p 1-1000 192.168.1.1
```
- Scan ports 1 to 1000.

---

### 📌 Scan a Range of IPs  
```bash
nmap 192.168.1.1-50
```

---

### 📌 UDP Scan  
```bash
nmap -sU 192.168.1.1
```

---

### 📌 Disable DNS Resolution  
```bash
nmap -n 192.168.1.1
```

---

### 📌 Save Scan Output to a File  
```bash
nmap -oN scan_result.txt 192.168.1.1
```

---

### 📌 Scan Using a List of IPs  
```bash
nmap -iL ips.txt
```
(*ips.txt contains one IP per line*)

---

## 📌 Nmap Example Output

```bash
nmap -sS 137.97.153.219
```
**Output:**
```
Host is up (0.036s latency).
Not shown: 996 filtered ports
PORT     STATE SERVICE
21/tcp   open  ftp
80/tcp   open  http
443/tcp  open  https
7070/tcp open  realserver
```

---

## 📌 Nmap Advanced Scripting Engine (NSE)

**Example:**
```bash
nmap --script vuln 192.168.1.1
```
- Runs default vulnerability detection scripts.

Or check open HTTP services:
```bash
nmap --script http-enum 192.168.1.1
```

---

## 📌 Summary  
| Nmap Function       | Command Example                   |
|:--------------------|:-----------------------------------|
| Basic Scan           | `nmap 192.168.1.1`                 |
| Stealth SYN Scan      | `nmap -sS 192.168.1.1`             |
| Aggressive Scan      | `nmap -A 192.168.1.1`              |
| OS Detection         | `nmap -O 192.168.1.1`              |
| Service Detection    | `nmap -sV 192.168.1.1`             |
| UDP Scan             | `nmap -sU 192.168.1.1`             |
| Save Results         | `nmap -oN scan.txt 192.168.1.1`    |

---

## 📌 Installation (if not already)
```bash
sudo apt update
sudo apt install nmap
```

---

If you’d like — I can turn this into a clean **PDF**, **Markdown**, or cheat sheet for you too.  
Want that? 📄✨