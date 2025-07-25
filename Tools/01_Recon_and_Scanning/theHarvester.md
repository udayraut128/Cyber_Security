
---

## 🔍 What is TheHarvester?

**TheHarvester** is an **OSINT tool** used to **gather information (especially emails, domain names, subdomains, IPs, and more)** from **public sources** like search engines, social media, and public PGP key servers.

It is **pre-installed in Kali Linux** and written in **Python**.

---

## 📌 Use Cases

1. **Collect email addresses of a domain for spear phishing**
2. **Discover subdomains and hosts for vulnerability scanning**
3. **Identify employee names for social engineering**
4. **Fingerprint target infrastructure before launching attacks**

---

## ⚙️ Data Sources Supported

| Source              | Data Type                       |
| ------------------- | ------------------------------- |
| Google, Bing, Yahoo | Emails, hosts                   |
| LinkedIn, Twitter   | Usernames                       |
| Shodan              | IPs, banners                    |
| DNS Dumpster        | Subdomains                      |
| PGP Servers         | Emails                          |
| Hunter.io           | Emails                          |
| Netcraft            | Subdomains                      |
| Baidu, DuckDuckGo   | Emails, subdomains              |
| Virustotal          | Domain info                     |
| crt.sh              | SSL/TLS certificate information |

---

## 🛠️ Installation

If not pre-installed, you can install it using:

```bash
git clone https://github.com/laramies/theHarvester.git
cd theHarvester
pip3 install -r requirements.txt
python3 theHarvester.py -h
```

---

## 📖 Basic Syntax

```bash
theHarvester -d <domain> -b <source>
```

### Options:

* `-d` → Target domain (e.g., **example.com**)
* `-b` → Data source (e.g., google, bing, shodan, etc.)
* `-l` → Limit the number of results (default: 500)
* `-f` → Output file name
* `-s` → Start from result number
* `-v` → Verbose
* `-h` → Help

---

## ✅ Examples

---

### 1. 🔎 Basic Email & Host Collection from Google

```bash
theHarvester -d tesla.com -b google
```

✔️ Gathers emails and hostnames related to **tesla.com** from **Google** search results.

---

### 2. 🖧 Collect Subdomains from Bing

```bash
theHarvester -d microsoft.com -b bing -l 100
```

✔️ Searches for **subdomains** of **microsoft.com** from Bing with a limit of 100 results.

---

### 3. 🕵️‍♀️ Discover Emails from PGP Key Servers

```bash
theHarvester -d apple.com -b pgp
```

✔️ Searches **public PGP servers** for email addresses associated with **apple.com**.

---

### 4. 🌐 Using Shodan for Host Discovery

```bash
theHarvester -d facebook.com -b shodan
```

✔️ Queries **Shodan** to get **IP addresses**, **open ports**, **banners**, etc.

🔑 **Note:** You need a **Shodan API key** for this to work.

---

### 5. 📄 Save Results to File (HTML)

```bash
theHarvester -d github.com -b google -f github_results
```

✔️ Saves output to `github_results.xml` and `github_results.html`.

---

### 6. 🧠 Combine Multiple Sources

```bash
theHarvester -d tesla.com -b google,bing,linkedin,pgp
```

✔️ Searches multiple sources for broader data collection.

---

## 🔐 API Key Setup (for some sources)

Some sources like Shodan, Hunter.io, or Bing require **API keys**. To configure:

Edit this file:

```bash
config.json
```

Example:

```json
{
  "shodan_api_key": "YOUR_SHODAN_KEY",
  "hunterio_api_key": "YOUR_HUNTERIO_KEY"
}
```

---

## 📊 Sample Output

Here’s what TheHarvester might return for `-d example.com`:

```
Emails found:
- john.doe@example.com
- admin@example.com

Hosts found:
- mail.example.com
- dev.example.com

IPs:
- 192.168.1.2
- 10.0.0.1
```

---

## 📌 Advantages

* Easy to use and lightweight
* No need for login or credentials (for most sources)
* Covers multiple engines and sources
* Useful in **reconnaissance** and **information gathering phase** of pentesting

---

## 🚫 Limitations

* Dependent on public sources (may miss private/internal data)
* Some data sources block automated queries (like Google after too many requests)
* May require proxies to avoid rate limiting
* Some sources need paid API keys

---

## 🧠 Tips for Usage

1. 🔁 Rotate user-agents or use proxies if IP gets blocked.
2. 📁 Always store output in a file for further analysis.
3. 🧪 Combine TheHarvester with tools like `Maltego`, `Recon-ng`, `Amass`, or `Spiderfoot` for advanced recon.
4. 🕔 Use `cron` or scripts to automate recon on targets periodically.

---

## 🧩 Real-World Example

### Scenario:

You’re hired to perform a security audit on `acmecorp.com`.

### Step 1: Recon with TheHarvester

```bash
theHarvester -d acmecorp.com -b google,linkedin,pgp,shodan -l 500 -f acmecorp_report
```

### Step 2: Analyze output

* Found `john@acmecorp.com` → may try password spraying
* Found subdomain `vpn.acmecorp.com` → try connecting
* Shodan says `vpn.acmecorp.com` has outdated SSL → vulnerability

---

## 🧰 Alternative Tools for Recon

| Tool              | Purpose                 |
| ----------------- | ----------------------- |
| `Amass`           | Subdomain enumeration   |
| `Recon-ng`        | Modular recon framework |
| `Maltego`         | Graphical link analysis |
| `Spiderfoot`      | Automated recon         |
| `OSINT Framework` | Manual source list      |

---

## 🏁 Conclusion

**TheHarvester** is a **must-have** in any pentester's or red teamer's toolkit for **initial reconnaissance**. It gives a **quick overview** of a target's public-facing footprint including **emails**, **subdomains**, and **hostnames** that can lead to deeper vulnerabilities.

---

 