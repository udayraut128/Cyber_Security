Certainly! Here's a **complete, in-depth explanation of the `subfinder` tool**, a widely used **subdomain discovery tool** in cybersecurity and bug bounty hunting. This guide includes definitions, features, installation, usage with examples, real-world scenarios, and advanced options—**nothing is skipped**.

---

# 🔍 What is `subfinder`?

**`subfinder`** is a **subdomain enumeration tool** designed to discover valid subdomains for websites using **passive online sources**. It is developed and maintained by **ProjectDiscovery**, the same team behind `nuclei`, `httpx`, and other popular tools.

---

## 🚀 Why Use `subfinder`?

* Quickly discovers **subdomains** for a target domain.
* Uses **passive sources only** (no brute-forcing or DNS brute).
* Fast and reliable.
* Ideal for **recon**, **bug bounty**, **red teaming**, and **OSINT**.

---

## ⚙️ Features

| Feature                | Description                                                     |
| ---------------------- | --------------------------------------------------------------- |
| 🧩 Passive Enumeration | Uses APIs and online services (no brute force)                  |
| ⚡ Fast & Lightweight   | Written in Go (compiled binary)                                 |
| 🔑 Supports API Keys   | For private/full access to services like Censys, SecurityTrails |
| 🧪 Accurate            | Filters dead or false-positive domains                          |
| 🔄 Easy Integration    | Works well with `amass`, `nuclei`, `httpx`, etc.                |
| 🔌 Plugin-based        | Easily extendable                                               |

---

## 🔧 Supported Data Sources (Examples)

`subfinder` uses over **50 passive sources**, including:

* AlienVault
* Anubis
* CertSpotter
* CRT.sh
* Facebook CT
* HackerTarget
* Shodan (API)
* SecurityTrails (API)
* Censys (API)
* URLScan
* ThreatCrowd
* VirusTotal (API)
* WaybackMachine

> API keys unlock **more data** and higher rate limits.

---

## 💻 Installation

### ✅ On Kali Linux

```bash
sudo apt install subfinder
```

### ✅ From Source (Linux/macOS)

```bash
GO111MODULE=on go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

Make sure Go is installed.

### ✅ On Windows (via Scoop)

```bash
scoop install subfinder
```

---

## 📁 Configuration (API Keys)

To use full sources, add your API keys:

```bash
subfinder -setup
```

This generates a file at:

```
~/.config/subfinder/provider-config.yaml
```

Edit this file and add keys like:

```yaml
securitytrails:
  - your_api_key
virustotal:
  - your_api_key
shodan:
  - your_api_key
```

---

## 🧾 Basic Usage

```bash
subfinder -d example.com
```

✔️ This command discovers subdomains for **example.com** using default passive sources.

---

## 📌 Command-Line Options

| Option    | Description                      |
| --------- | -------------------------------- |
| `-d`      | Target domain                    |
| `-dL`     | List of domains from a file      |
| `-o`      | Output to file                   |
| `-oJ`     | Output in JSON                   |
| `-oD`     | Output in domain-specific files  |
| `-all`    | Use all sources (even slow ones) |
| `-silent` | Output only results (no banner)  |
| `-nW`     | Remove wildcard subdomains       |
| `-t`      | Threads (default: 10)            |

---

## ✅ Examples

---

### 🔎 1. Discover subdomains of a single domain

```bash
subfinder -d tesla.com
```

✔️ Lists all subdomains found for `tesla.com`.

---

### 📂 2. Scan multiple domains from a file

```bash
subfinder -dL domains.txt
```

Where `domains.txt` contains:

```
google.com
tesla.com
hackerone.com
```

✔️ Runs subdomain enumeration for each domain in the list.

---

### 📝 3. Output results to a text file

```bash
subfinder -d tesla.com -o tesla_subs.txt
```

✔️ Saves all found subdomains into `tesla_subs.txt`.

---

### 🧱 4. Use JSON output for automation

```bash
subfinder -d example.com -oJ -o output.json
```

✔️ Useful for parsing or integrating with other tools like Python scripts.

---

### 🎯 5. Remove Wildcard Subdomains

```bash
subfinder -d example.com -nW
```

✔️ Removes false-positive wildcard subdomains (e.g., `*.example.com` that always resolve).

---

### 🧪 6. Use All Available Sources

```bash
subfinder -d example.com -all
```

✔️ Uses every known passive source, including slow or unreliable ones (more results).

---

### ⚡ 7. Combine with `httpx` to check which subdomains are alive

```bash
subfinder -d tesla.com -silent | httpx -silent
```

✔️ First finds subdomains, then filters the **live HTTP/HTTPS services**.

---

## 🧠 Real-World Bug Bounty Workflow

1. **Find Subdomains**

   ```bash
   subfinder -d target.com -o target_subs.txt
   ```

2. **Filter Live Domains**

   ```bash
   cat target_subs.txt | httpx -silent -status-code -o live_subs.txt
   ```

3. **Run Vulnerability Scans**

   ```bash
   nuclei -l live_subs.txt -o vulns.txt
   ```

4. **Manual Pentesting**
   Investigate login pages, admin panels, outdated services.

---

## 🛠️ Use with Other Tools

| Tool         | Integration Purpose                     |
| ------------ | --------------------------------------- |
| **httpx**    | Check which subdomains are live         |
| **nuclei**   | Vulnerability scanning                  |
| **amass**    | Deeper subdomain enumeration            |
| **dnsx**     | Validate subdomain DNS records          |
| **Chaos DB** | Use known subdomains of public programs |
| **ffuf**     | Fuzzing found subdomains or directories |

---

## 🔐 Subdomain Types You Might Find

| Type                  | Description          |
| --------------------- | -------------------- |
| `dev.example.com`     | Development server   |
| `staging.example.com` | Staging/testing site |
| `admin.example.com`   | Admin panel          |
| `api.example.com`     | API endpoints        |
| `mail.example.com`    | Email server         |

These are useful for:

* Privilege escalation
* Gaining unauthorized access
* Finding outdated/vulnerable services

---

## 🔒 Legal Use & Ethics

* ✅ Use **only** on domains you own or have **explicit permission** to test.
* ❌ Never run `subfinder` against real companies without authorization (e.g., bug bounty program scope).
* ⚠️ Violations may result in legal consequences.

---

## 🧭 Summary

| Feature             | Description                        |
| ------------------- | ---------------------------------- |
| **Tool Name**       | `subfinder`                        |
| **Purpose**         | Passive subdomain enumeration      |
| **Developer**       | ProjectDiscovery                   |
| **Data Sources**    | 50+ APIs & services                |
| **Speed**           | Very fast                          |
| **Usage**           | Bug bounty, recon, OSINT           |
| **Works Well With** | `httpx`, `nuclei`, `amass`, `dnsx` |

---

## 📘 Further Learning

* [🔗 Subfinder GitHub Repo](https://github.com/projectdiscovery/subfinder)
* [🔗 ProjectDiscovery Tools](https://projectdiscovery.io/)
* [🔐 Bugcrowd University - Recon](https://github.com/bugcrowd/bugcrowd_university)
* [🎓 PortSwigger Academy](https://portswigger.net/web-security)

---

