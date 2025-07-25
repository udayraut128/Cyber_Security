Sure! Here's a **complete and detailed explanation of the `naabu` tool**, covering **everything** — its purpose, features, use cases, examples, installation, and automation — with **nothing skipped**.

---

# 🧠 What is `naabu`?

**`naabu`** is a **fast port scanner** written in **Go** by [ProjectDiscovery](https://projectdiscovery.io). It is designed to **scan IPs/domains for open ports** **quickly and reliably**, focusing on **speed, flexibility, and ease of automation** in reconnaissance workflows.

It’s often used in **bug bounty**, **CTF**, and **network scanning** scenarios as part of **web asset discovery**.

---

## 🔍 What Does `naabu` Do?

* Scans for **open TCP ports**
* Supports **multiple input sources** (domain, IP, CIDR)
* Performs **reliable host discovery**
* Outputs ports in various formats (text, JSON)
* Built for **speed** and **integration** with other tools (like `nmap`, `httpx`, `nuclei`)

> Think of `naabu` as the **masscan** or **fast mode of nmap**, specialized for port scanning in recon pipelines.

---

## 🛠️ Installation

### 📦 From Source (Go Required)

```bash
go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
```

> Ensure `$GOPATH/bin` is in your system `$PATH`.

### 📦 On Kali Linux

```bash
sudo apt install naabu
```

---

## 📄 Basic Syntax

```bash
naabu -host [IP or domain]
```

---

## ✅ Key Features

| Feature                                     | Description                                          |
| ------------------------------------------- | ---------------------------------------------------- |
| 🔍 Fast TCP scanning                        | Probes for open TCP ports                            |
| 📄 Multiple input methods                   | IP, domain, CIDR, stdin, file                        |
| 📈 Highly concurrent                        | Very fast, supports thousands of targets             |
| ⚡ Port filtering                            | Scan common ports, full port ranges, or custom sets  |
| 🔁 Retry logic                              | Retrying failed probes                               |
| 🧪 Nmap integration                         | Automatically runs nmap on open ports                |
| 🧾 JSON and plain output                    | Easy to parse for scripts                            |
| 🔐 Supports SYN scan (raw) and Connect scan |                                                      |
| 🧰 Integration-ready                        | Works well with `subfinder`, `httpx`, `nuclei`, etc. |

---

## 📚 Common Options

| Option           | Description                                 |
| ---------------- | ------------------------------------------- |
| `-host`          | Specify a single IP/domain                  |
| `-list`          | Input list of IPs/domains                   |
| `-p`             | Specific ports to scan (`-p 80,443,8080`)   |
| `-top-ports`     | Scan top `n` ports (e.g., `-top-ports 100`) |
| `-ports-file`    | Load custom ports list from file            |
| `-exclude-ports` | Skip specific ports                         |
| `-rate`          | Set scan speed (default: 1000)              |
| `-o`             | Save output to a file                       |
| `-json`          | JSON output format                          |
| `-silent`        | Clean output with just open IP\:port        |
| `-nmap`          | Automatically run `nmap` on found ports     |
| `-exclude-cdn`   | Ignore IPs behind known CDNs                |
| `-c`             | Show scanned ports and IPs                  |
| `-retries`       | Retry failed probes                         |
| `-timeout`       | Set timeout per probe                       |
| `-ping`          | Probe only live hosts                       |

---

## 🔍 Examples

---

### ✅ 1. Scan Single Domain/IP

```bash
naabu -host hackerone.com
```

✔️ Returns open ports on hackerone.com

---

### 📂 2. Scan List of Targets

```bash
naabu -list targets.txt
```

✔️ `targets.txt` contains domains or IPs (one per line)

---

### 🚀 3. Fast Scan of Top 100 Ports

```bash
naabu -host target.com -top-ports 100
```

---

### 🎯 4. Scan All 65535 Ports

```bash
naabu -host target.com -p -
```

✔️ `-p -` instructs to scan **all ports**

---

### 📦 5. Save Output to File (Plaintext)

```bash
naabu -list targets.txt -o results.txt
```

---

### 🧾 6. JSON Output

```bash
naabu -list targets.txt -json -o output.json
```

✔️ Useful for scripting/automation

---

### 📄 7. Scan Custom Port List from File

```bash
naabu -list targets.txt -ports-file ports.txt
```

✔️ `ports.txt` should contain ports, e.g.:

```
21
22
80
443
```

---

### 🔁 8. Retry Failed Hosts

```bash
naabu -list targets.txt -retries 3
```

---

### ⚠️ 9. Avoid CDN IPs (Helpful in Bug Bounty)

```bash
naabu -list targets.txt -exclude-cdn
```

✔️ Avoid scanning large CDNs like Cloudflare/Akamai

---

### 🧪 10. Automatically Run `nmap`

```bash
naabu -list targets.txt -nmap
```

✔️ Automatically runs `nmap -sV` on discovered open ports

---

## 🔗 Example Pipeline

### 🧨 Subdomain Recon + Port Scan + Web Probing

```bash
subfinder -d example.com -silent | naabu -silent -p 80,443,8080 | httpx -title -tech-detect -status-code -o alive.txt
```

✔️ `subfinder` → `naabu` (open ports) → `httpx` (tech info)

---

## 🚧 Real-World Use Case: Bug Bounty Recon

1. **Subdomain Enumeration**

   ```bash
   subfinder -d uber.com -silent > subs.txt
   ```

2. **Resolve and Scan Ports**

   ```bash
   dnsx -l subs.txt -a -silent | naabu -p 80,443 -silent -o ports.txt
   ```

3. **Web Probing**

   ```bash
   cat ports.txt | httpx -title -tech-detect -status-code -o webservices.txt
   ```

---

## 📦 Summary Table

| Attribute      | Details                                                                                |
| -------------- | -------------------------------------------------------------------------------------- |
| Tool           | `naabu`                                                                                |
| Purpose        | Fast TCP port scanning                                                                 |
| Created by     | ProjectDiscovery                                                                       |
| Written in     | Golang                                                                                 |
| Speed          | Very fast                                                                              |
| Output Formats | Text, JSON                                                                             |
| Input Formats  | Host, file, stdin                                                                      |
| Ports Scanned  | All or custom/top-N                                                                    |
| Integrations   | `httpx`, `nmap`, `subfinder`, `dnsx`, `nuclei`                                         |
| Great For      | Recon, bug bounty, attack surface mapping                                              |
| Website        | [https://github.com/projectdiscovery/naabu](https://github.com/projectdiscovery/naabu) |

---

## 📚 Official Resources

* GitHub: [https://github.com/projectdiscovery/naabu](https://github.com/projectdiscovery/naabu)
* Docs: [https://naabu.projectdiscovery.io](https://naabu.projectdiscovery.io)
* Community: [https://discord.gg/projectdiscovery](https://discord.gg/projectdiscovery)

---
 