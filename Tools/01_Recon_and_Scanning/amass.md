
---

# 🧠 What is Amass?

**Amass** is an **advanced open-source reconnaissance tool** used to perform **DNS enumeration**, **subdomain discovery**, **network mapping**, and **attack surface mapping** for organizations.

It is built and maintained by the **OWASP Foundation**, and is one of the **most powerful tools** for **active and passive reconnaissance**.

---

## 📦 Core Capabilities of Amass

| Feature                    | Description                                           |
| -------------------------- | ----------------------------------------------------- |
| 🔎 Subdomain Enumeration   | Passive, active, brute force, recursive               |
| 🌐 DNS Enumeration         | Forward, reverse, zone transfers                      |
| 🧩 Data Sources            | Uses 60+ APIs (CRT.sh, Shodan, VirusTotal, etc.)      |
| 🛠️ Active Recon           | Uses DNS probing, zone walking                        |
| 🕵️ Infrastructure Mapping | ASN, CIDR, IP resolution, netblocks                   |
| 📈 Graph Database          | Tracks discovered assets over time                    |
| 🧪 Supports Brute Forcing  | Dictionary-based subdomain brute force                |
| 🔌 Extensible              | Custom configuration and data sources                 |
| 🛡️ Red Teaming            | Useful for stealth recon and attack surface discovery |

---

## 🛠️ Installation

### ✅ On Kali Linux

```bash
sudo apt install amass
```

### ✅ Using Go (Latest Version)

```bash
go install -v github.com/owasp-amass/amass/v4/...@master
```

Make sure Go is installed and `$GOPATH/bin` is in your `$PATH`.

---

## 🗂️ Configuration (API Keys)

To unlock **more data** from APIs like Shodan, Censys, VirusTotal, etc.:

```bash
amass intel -config ~/.config/amass/config.ini
```

### Sample `config.ini` file:

```ini
[virustotal]
apikey = YOUR_API_KEY

[shodan]
apikey = YOUR_API_KEY

[censys]
id = YOUR_ID
secret = YOUR_SECRET
```

---

## 🔧 Core Components of Amass

| Subcommand     | Description                                  |
| -------------- | -------------------------------------------- |
| `amass enum`   | Subdomain enumeration (main mode)            |
| `amass intel`  | Collects target infrastructure (CIDRs, ASNs) |
| `amass viz`    | Visualize graph data                         |
| `amass db`     | Interact with local Amass database           |
| `amass track`  | Track asset changes over time                |
| `amass dns`    | Perform DNS lookups manually                 |
| `amass net`    | Discover related netblocks, domains          |
| `amass script` | Custom scripts (Lua)                         |

---

## 🧾 Basic Syntax

```bash
amass enum -d <domain> [options]
```

---

## ✅ Examples and Use Cases

---

### 🔍 1. Passive Subdomain Enumeration

```bash
amass enum -passive -d example.com
```

✔️ Gathers subdomains using **passive sources** (no DNS resolution or probing).

---

### 🧱 2. Active Subdomain Enumeration

```bash
amass enum -active -d example.com
```

✔️ Performs **active DNS probing** to validate subdomains.

---

### 📂 3. Save Output to File

```bash
amass enum -d example.com -o example_subs.txt
```

✔️ Stores all found subdomains in a text file.

---

### 🧪 4. Combine Active + Passive + Brute Force

```bash
amass enum -d example.com -brute -min-for-recursive 2 -active
```

✔️ Performs **brute force**, **recursive**, **active DNS**, and **passive** together.

---

### 📄 5. Subdomain List from a Wordlist

```bash
amass enum -d example.com -brute -src -w wordlist.txt
```

✔️ Performs a **dictionary attack** using your custom `wordlist.txt`.

---

### 🔎 6. Discover ASN and CIDR Info

```bash
amass intel -asn 13335
```

✔️ Finds all domains and subdomains belonging to ASN 13335 (Cloudflare).

---

### 🌐 7. Get ASN/Netblock for a domain

```bash
amass intel -whois -d google.com
```

✔️ Outputs ASNs, CIDRs, and other info from whois records.

---

### 🧩 8. Track Changes to Assets Over Time

```bash
amass track -d example.com
```

✔️ Compares current results with previous ones to find **new or removed subdomains**.

---

### 📈 9. Visualize Results as a Graph

```bash
amass viz -d3 -dir ./amass_output/ -o amass_graph.html
```

✔️ Creates a **graphical HTML view** of subdomain relationships.

---

## 🧠 Real-World Bug Bounty Workflow

1. **Initial Subdomain Recon**:

   ```bash
   amass enum -passive -d target.com -o passive.txt
   ```

2. **Active Enumeration**:

   ```bash
   amass enum -active -brute -d target.com -o active.txt
   ```

3. **Merge + Filter**:

   ```bash
   sort passive.txt active.txt | uniq > all_subs.txt
   ```

4. **Check Which Subdomains Are Alive**:

   ```bash
   cat all_subs.txt | httpx -silent > live_subs.txt
   ```

5. **Scan for Vulnerabilities**:

   ```bash
   nuclei -l live_subs.txt -o results.txt
   ```

---

## 🛡️ Use Cases

| Use Case               | Example                                 |
| ---------------------- | --------------------------------------- |
| 🕸️ Map Attack Surface | Find every online asset of a target org |
| 🧱 DNS Bruteforce      | Discover hidden services                |
| 🧪 Red Teaming         | Use stealthy passive sources            |
| 🗂️ Asset Management   | Track subdomains and IPs over time      |
| 🧩 Bug Bounty          | Find dev/test environments to exploit   |

---

## 📘 Output Formats

Amass supports various output formats:

```bash
amass enum -d example.com -o example.txt      # Text
amass enum -d example.com -json example.json  # JSON
amass enum -d example.com -oA output_prefix   # All formats
```

✔️ Useful for integration with other tools and dashboards.

---

## 🛠️ Combine With Tools

| Tool      | Purpose                        |
| --------- | ------------------------------ |
| `httpx`   | Check for live domains         |
| `nuclei`  | Scan for known vulnerabilities |
| `dnsx`    | DNS record validation          |
| `subjack` | Detect subdomain takeover      |
| `massdns` | High-speed DNS resolution      |
| `jq`      | Parse JSON outputs from Amass  |

---

## 🔐 Legal Usage & Ethics

* ✅ Use Amass **only** on domains you **own** or have **explicit permission** to test.
* ❌ Never use on random websites without consent.
* 🛑 Improper use may result in **legal issues or account bans** (especially when using APIs).

---

## 🧭 Summary

| Feature      | Description                           |
| ------------ | ------------------------------------- |
| Tool         | OWASP Amass                           |
| Language     | Go                                    |
| Type         | Subdomain Enumeration, Recon          |
| Modes        | Passive, Active, Brute, Recursive     |
| Output       | TXT, JSON, Graph                      |
| Integrations | `httpx`, `nuclei`, `dnsx`, `jq`       |
| Usage        | Recon, Bug Bounty, OSINT, Red Teaming |

---

## 📚 References

* GitHub: [https://github.com/owasp-amass/amass](https://github.com/owasp-amass/amass)
* Docs: [https://owasp.org/www-project-amass/](https://owasp.org/www-project-amass/)
* Bug Bounty Guide: [https://bugcrowd.com/resources](https://bugcrowd.com/resources)

---

