Sure! Here's a **complete and detailed explanation of the `httpx` tool**, including its features, use cases, examples, installation, and real-world applications—**nothing skipped**.

---

# 🧠 What is `httpx`?

**`httpx`** is a **fast and multi-purpose HTTP toolkit** created by **ProjectDiscovery**. It's designed for **probing URLs and domains** to discover **live web servers** and extract **HTTP-related information** such as:

* Status codes
* Page titles
* Content length
* TLS information
* HTTP methods
* Technologies used
* Web server details
* Redirects
* Response headers

---

## ⚡ Why Use `httpx`?

It helps answer key questions like:

* Is this subdomain live?
* What technology does this website use?
* Is there a web server running?
* Is there SSL/TLS enabled?
* Does it redirect somewhere else?

This is extremely useful in:

* Bug bounty hunting
* Web asset discovery
* Reconnaissance
* Security testing
* Red teaming
* Vulnerability scanning (with `nuclei`)

---

## 🛠️ Installation

### 🟢 Via Go (Latest Version)

```bash
go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
```

Ensure `$GOPATH/bin` is in your `$PATH`.

### 🟢 On Kali Linux

```bash
sudo apt install httpx
```

---

## 📄 Basic Syntax

```bash
httpx -l domains.txt
```

> Probes the domains in `domains.txt` to check which are **live HTTP/HTTPS servers**.

---

## ✅ Key Features

| Feature                                      | Description                             |
| -------------------------------------------- | --------------------------------------- |
| ✅ HTTP/HTTPS Probing                         | Check for live web services             |
| ✅ TLS Info                                   | Grab TLS cert, version, subject, issuer |
| ✅ Title                                      | Extract page titles                     |
| ✅ Status Code                                | Get HTTP response codes                 |
| ✅ Technology Detection                       | What tech runs the website              |
| ✅ Response Time                              | Measure response delay                  |
| ✅ Content-Length                             | Size of response                        |
| ✅ Redirects                                  | Follow and show redirects               |
| ✅ JSON/CSV Output                            | For automation or parsing               |
| ✅ Pipelining, concurrency, retries, timeouts |                                         |
| ✅ Can work with stdin and large input files  |                                         |

---

## 🔧 Most Common Options

| Option                 | Description                                  |
| ---------------------- | -------------------------------------------- |
| `-l`                   | Input file (list of domains/URLs)            |
| `-silent`              | Clean output (just URLs)                     |
| `-status-code`         | Show HTTP response codes                     |
| `-title`               | Show page title                              |
| `-tech-detect`         | Show technologies                            |
| `-ip`                  | Show IP address                              |
| `-cname`               | Show CNAME                                   |
| `-location`            | Show redirect location                       |
| `-content-length`      | Show length of response                      |
| `-tls-grab`            | Show TLS certificate info                    |
| `-server`              | Show web server                              |
| `-cdn`                 | Check if behind CDN                          |
| `-p`                   | Custom port probing (e.g., `-p 80,443,8080`) |
| `-json`                | Output in JSON                               |
| `-o`                   | Output file                                  |
| `-retries`, `-timeout` | Retry/timeout control                        |

---

## 🔍 Examples (Real Usage)

---

### ✅ 1. Check Which Domains Are Live

```bash
httpx -l domains.txt -silent
```

✔️ Outputs only live domains (clean list)

---

### 🌐 2. Probe Specific Ports

```bash
httpx -l domains.txt -p 80,443,8080
```

✔️ Checks those ports for HTTP/S services

---

### 🧠 3. Show Status Code, Title, and Server Info

```bash
httpx -l domains.txt -title -status-code -server -ip
```

✔️ See status, server type, title, and IP

---

### 🔒 4. Grab TLS Certificate Info

```bash
httpx -l domains.txt -tls-grab
```

✔️ Shows issuer, subject, expiry, etc.

---

### 📁 5. Output to JSON

```bash
httpx -l domains.txt -json -o results.json
```

✔️ Easily parse with `jq` or Python scripts

---

### 📥 6. Combine With Subdomain Tools

#### With `subfinder`

```bash
subfinder -d example.com -silent | httpx -title -status-code -tech-detect -o live.txt
```

✔️ Passive discovery → Probing → Tech info

#### With `amass`

```bash
amass enum -passive -d example.com -o subs.txt
cat subs.txt | httpx -status-code -title -o alive.txt
```

---

### 🔄 7. Follow Redirects and Show Location

```bash
httpx -l domains.txt -follow-redirects -location
```

✔️ Shows where redirects lead (e.g., HTTP → HTTPS)

---

### 🛑 8. Filter for Only 200 OK Responses

```bash
httpx -l domains.txt -status-code | grep "200"
```

✔️ Only keep web services returning `200 OK`

---

### 🔍 9. Technology Detection

```bash
httpx -l domains.txt -tech-detect
```

✔️ Shows tech stack (e.g., WordPress, Nginx, jQuery)

---

### 📊 10. Full Recon Summary

```bash
httpx -l domains.txt -status-code -title -tech-detect -tls-grab -server -content-length -ip -cdn -o summary.txt
```

✔️ Comprehensive info in one run.

---

## ⚙️ Advanced Options

| Option           | Description                         |
| ---------------- | ----------------------------------- |
| `-retries 3`     | Retry 3 times on failure            |
| `-timeout 10`    | Timeout after 10s                   |
| `-threads 100`   | Set concurrency                     |
| `-probe-all-ips` | Resolve multiple A records          |
| `-random-agent`  | Use random User-Agent               |
| `-no-color`      | Disable colored output              |
| `-no-fallback`   | Don't fallback between http/https   |
| `-rate-limit`    | Throttle requests (e.g., 100 req/s) |

---

## 🧑‍💻 Real Bug Bounty Pipeline

```bash
subfinder -d example.com -silent | dnsx -silent -a -resp | httpx -status-code -title -tech-detect -o web_targets.txt
```

✔️ `subfinder` → `dnsx` (resolve) → `httpx` (probe web services)

---

## 🧪 Real-World Use Cases

* Web asset discovery in reconnaissance
* Verifying live subdomains from subdomain bruteforce
* TLS certificate analysis for expiry
* Detecting exposed development or admin panels
* Quickly finding misconfigured web apps
* Finding technologies for targeted exploitation

---

## ⚠️ Ethics & Legal Use

* Only use on targets you own or have permission to test
* Abide by scope boundaries in bug bounty programs
* Use concurrency responsibly to avoid denial of service

---

## 📦 Summary Table

| Attribute     | Description                                                                            |
| ------------- | -------------------------------------------------------------------------------------- |
| Tool Name     | `httpx`                                                                                |
| Developer     | ProjectDiscovery                                                                       |
| Language      | Golang                                                                                 |
| Main Function | HTTP/S probing and information gathering                                               |
| Speed         | Very high (multi-threaded)                                                             |
| Input Format  | stdin, `-l file.txt`                                                                   |
| Output Format | Plain text, JSON, CSV                                                                  |
| Use Cases     | Bug bounty, recon, automation                                                          |
| Useful With   | `subfinder`, `dnsx`, `nuclei`, `amass`                                                 |
| Website       | [https://github.com/projectdiscovery/httpx](https://github.com/projectdiscovery/httpx) |

---

## 📚 Resources

* GitHub: [https://github.com/projectdiscovery/httpx](https://github.com/projectdiscovery/httpx)
* Docs: [https://httpx.projectdiscovery.io](https://httpx.projectdiscovery.io)
* Discord: [https://discord.gg/projectdiscovery](https://discord.gg/projectdiscovery)

---


