Sure! Here's a **complete and detailed explanation of the `nuclei` tool** — covering **everything** without skipping anything, including real-world **examples**, **features**, use cases, **installation**, and **automation tips**.

---

# 🧬 What is `nuclei`?

**Nuclei** is a **fast, flexible, and powerful vulnerability scanner** based on **community-contributed templates**. It helps in **automated scanning of known CVEs, misconfigurations, exposures, and more** using customizable YAML templates.

It’s developed by **ProjectDiscovery** and is widely used in **bug bounty**, **pentesting**, and **recon workflows**.

---

## 🧠 What Does It Do?

* Scans web targets using **vulnerability templates**
* Detects **CVE vulnerabilities**, **misconfigurations**, **exposed panels**, **default logins**, **files**, **takeovers**, **open APIs**, etc.
* Fast, thanks to **multi-threaded engine**
* Templates are regularly updated by the **community**
* Works seamlessly with tools like `subfinder`, `httpx`, `naabu`, etc.

---

## 🧰 Key Features

| Feature                   | Description                                             |
| ------------------------- | ------------------------------------------------------- |
| 🔍 Template-driven        | Scans based on YAML templates (CVE, misconfig, etc.)    |
| ⚡ Super fast              | Built in Go, concurrent engine                          |
| 🧠 Intelligent Matching   | Regex, word matchers, status code filters               |
| 🎯 Specific Targeting     | Headers, body, status, DNS, files                       |
| 💬 Customizable Templates | Write your own detection logic                          |
| 🔗 Automation Friendly    | Easily integrated in bash scripts                       |
| 🧩 Modular                | Supports DNS, TCP, HTTP, SSL, File, WebSocket protocols |
| 📦 GitHub Integration     | Pull templates with one command                         |
| 🔒 Silent Mode            | For clean automation outputs                            |

---

# 🔧 Installation

### ✅ On Kali Linux

```bash
sudo apt install nuclei
```

### ✅ Using Go (recommended)

```bash
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

Make sure `GOPATH/bin` is in your `$PATH`.

---

# 📚 Template Installation

Before scanning, download nuclei templates:

```bash
nuclei -update
nuclei -update-templates
```

Templates are stored in:

```bash
~/.local/nuclei-templates/
```

Or clone manually:

```bash
git clone https://github.com/projectdiscovery/nuclei-templates.git
```

---

# 🧪 Basic Usage

```bash
nuclei -u https://example.com
```

Scans the target using **default templates**.

---

# 💥 Real-World Examples

---

### ✅ 1. Scan a Website Using Default Templates

```bash
nuclei -u https://example.com
```

---

### ✅ 2. Scan a List of Domains

```bash
nuclei -l targets.txt
```

`targets.txt`:

```
https://site1.com
https://site2.com
```

---

### ✅ 3. Use Specific Template Categories

```bash
nuclei -u https://example.com -t cves/
```

Other categories:

* `misconfiguration/`
* `exposures/`
* `takeovers/`
* `vulnerabilities/`
* `default-logins/`

---

### ✅ 4. CVE-Specific Scanning

```bash
nuclei -u https://example.com -t cves/2021/CVE-2021-41773.yaml
```

---

### ✅ 5. Scan with Rate Limit & Threads

```bash
nuclei -u https://example.com -t cves/ -rl 150 -c 50
```

* `-rl`: Requests per second (rate limit)
* `-c`: Number of concurrent threads

---

### ✅ 6. Save Output to File

```bash
nuclei -u https://example.com -o output.txt
```

Or in JSON:

```bash
nuclei -u https://example.com -json -o result.json
```

---

### ✅ 7. Silent Output (for scripts)

```bash
nuclei -u https://example.com -silent
```

Returns only detected URLs — ideal for chaining tools.

---

### ✅ 8. Use Custom Wordlist with Templates (Fuzzing)

```bash
nuclei -u https://example.com -t fuzzing/path-traversal.yaml
```

---

### ✅ 9. Use Tags Instead of Template Paths

```bash
nuclei -u https://example.com -tags cve,xss,rce
```

---

### ✅ 10. Scan All Ports (non-HTTP)

```bash
nuclei -target http://IP:PORT -t vulnerabilities/

# With naabu
naabu -host example.com -silent | httpx -silent | nuclei -l -
```

---

# 🧩 Template Types

Templates are organized in directories:

| Directory           | Description                       |
| ------------------- | --------------------------------- |
| `cves/`             | Known vulnerabilities (CVE-based) |
| `misconfiguration/` | Unsafe settings or weak auth      |
| `takeovers/`        | Subdomain takeover detection      |
| `exposures/`        | Sensitive files, Git repo, logs   |
| `default-logins/`   | Default credential checks         |
| `fuzzing/`          | LFI, SQLi, Path Traversal         |
| `dns/`              | DNS-based checks                  |
| `network/`          | TCP/UDP level scans               |
| `technologies/`     | CMS and framework detection       |

---

# 📐 How Nuclei Templates Work

Templates are YAML files. A simple CVE template looks like:

```yaml
id: cve-2021-41773
info:
  name: Apache Path Traversal
  author: projectdiscovery
  severity: high
  tags: cve,cve2021,apache,path-traversal
requests:
  - method: GET
    path:
      - "{{BaseURL}}/cgi-bin/.%2e/%2e%2e/etc/passwd"
    matchers:
      - type: word
        words:
          - "root:x:0:0:"
```

You can create your own templates based on your use case.

---

# 🔄 Update Templates Regularly

Templates get updated frequently:

```bash
nuclei -update-templates
```

To check for nuclei updates:

```bash
nuclei -update
```

---

# 🔌 Integration with Other Tools

### Combine with Subfinder, Httpx, Naabu

```bash
subfinder -d example.com -silent | httpx -silent | nuclei -l -
```

---

# 🛡️ Use Cases

| Use Case                  | How Nuclei Helps                   |
| ------------------------- | ---------------------------------- |
| 🔍 Recon and Enumeration  | Finds exposed endpoints and files  |
| 🧪 CVE Testing            | Validates known CVEs               |
| 🔓 Misconfiguration Scans | Default creds, open panels         |
| 📦 CI/CD Scans            | Integrate into pipelines           |
| ⚔️ Bug Bounty Hunting     | Fast target enumeration            |
| 🔗 Takeover Testing       | Detects vulnerable CNAME takeovers |

---

# 🧠 Advanced Tips

* Use `-tags` for better control of template selection
* Use `-etags` to **exclude** unwanted tags
* Combine with `gf`, `waybackurls`, `gau` for endpoint discovery
* Use JSON output to feed into dashboards
* Use Docker for container-based automation

---

# 🧪 Example Bash Script

```bash
#!/bin/bash

domain=$1

subfinder -d $domain -silent | httpx -silent | nuclei -l - -o "${domain}_scan.txt"
```

---

# 📌 Summary Table

| Feature           | Value                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------- |
| Language          | Go                                                                                       |
| Speed             | ⚡ Fast (multi-threaded)                                                                  |
| Templates         | 5000+                                                                                    |
| Protocols         | HTTP, DNS, TCP, SSL, WebSocket                                                           |
| Output formats    | Text, JSON                                                                               |
| Silent mode       | ✅                                                                                        |
| Real-time updates | ✅                                                                                        |
| CI/CD Ready       | ✅                                                                                        |
| GitHub            | [https://github.com/projectdiscovery/nuclei](https://github.com/projectdiscovery/nuclei) |

---
