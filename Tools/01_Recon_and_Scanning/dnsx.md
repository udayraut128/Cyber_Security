Absolutely! Here's a **complete, detailed guide to the `dnsx` tool**, which is widely used in **bug bounty**, **subdomain validation**, and **DNS reconnaissance** workflows.

---

# 🧠 What is `dnsx`?

**`dnsx`** is a **fast and multi-purpose DNS toolkit** designed for **reliable DNS probing and validation of subdomains**. It's developed by **ProjectDiscovery**, the same team behind tools like `nuclei`, `httpx`, and `subfinder`.

It is especially useful when you've already gathered a list of potential subdomains using tools like `subfinder`, `amass`, or `assetfinder`, and you want to **verify which subdomains actually resolve (i.e., are live)**.

---

## 🔧 Key Features of `dnsx`

| Feature                                                 | Description                                |
| ------------------------------------------------------- | ------------------------------------------ |
| ✅ Fast DNS resolution                                   | Resolves thousands of domains very quickly |
| ✅ Supports A, AAAA, CNAME, TXT, MX, NS records          |                                            |
| ✅ Supports wildcard filter, retries, timeouts           |                                            |
| ✅ Validates subdomains discovered using other tools     |                                            |
| ✅ Output in plain, JSON, and CSV formats                |                                            |
| ✅ Easy to integrate into pipelines (stdin/stdout based) |                                            |
| ✅ Custom resolvers supported                            |                                            |
| ✅ DNSSEC, PTR and SOA support                           |                                            |

---

## 🛠️ Installation

### 🔹 Using `go` (latest version)

```bash
go install -v github.com/projectdiscovery/dnsx/cmd/dnsx@latest
```

Make sure `$GOPATH/bin` is in your `$PATH`.

### 🔹 On Kali Linux

If not already available:

```bash
sudo apt install dnsx
```

---

## 🧾 Basic Syntax

```bash
dnsx -l domains.txt
```

This will resolve all domains from `domains.txt` and print the **valid** (resolving) domains.

---

## ✅ Examples and Use Cases

---

### 📄 1. Validate Subdomains (A Record)

```bash
cat subdomains.txt | dnsx
```

✔️ Resolves A records of all subdomains from input and outputs the valid ones.

---

### 📂 2. Output to File

```bash
dnsx -l subdomains.txt -o live_subs.txt
```

✔️ Writes results to `live_subs.txt`.

---

### 📊 3. Show Status and IP Address

```bash
dnsx -l subdomains.txt -a -resp
```

✔️ `-a`: Show A record IP addresses
✔️ `-resp`: Show full DNS response info

---

### 🔧 4. Query Specific DNS Record Types

#### A Record (IPv4)

```bash
dnsx -l subs.txt -a
```

#### AAAA Record (IPv6)

```bash
dnsx -l subs.txt -aaaa
```

#### CNAME Record

```bash
dnsx -l subs.txt -cname
```

#### TXT Record

```bash
dnsx -l subs.txt -txt
```

#### NS (Name Server) Record

```bash
dnsx -l subs.txt -ns
```

#### MX (Mail Exchange) Record

```bash
dnsx -l subs.txt -mx
```

#### SOA (Start of Authority) Record

```bash
dnsx -l subs.txt -soa
```

#### DNSSEC Support

```bash
dnsx -l subs.txt -dnssec
```

#### PTR (Reverse DNS Lookup)

```bash
dnsx -ptr -l ips.txt
```

---

### 📡 5. Use Custom DNS Resolvers

```bash
dnsx -l subs.txt -r 1.1.1.1,8.8.8.8
```

✔️ Uses Cloudflare and Google DNS.

---

### 🧠 6. Handle Wildcard DNS and Filter

```bash
dnsx -l subs.txt -filter
```

✔️ Filters out **wildcard DNS** responses that may return the same IP for non-existent subdomains.

---

### 🧪 7. Retry on Failure and Set Timeout

```bash
dnsx -l subs.txt -retry 3 -timeout 5
```

✔️ Retry failed lookups 3 times
✔️ Timeout after 5 seconds

---

### 📤 8. Output in JSON or CSV

```bash
dnsx -l subs.txt -json -o output.json
dnsx -l subs.txt -csv -o output.csv
```

---

### 🧩 9. Combine With Other Tools

#### Use `subfinder` and `dnsx` Together

```bash
subfinder -d example.com -silent | dnsx -a -resp -o live.txt
```

✔️ Fast passive subdomain discovery + DNS resolution.

#### Use with `amass`

```bash
amass enum -passive -d example.com -o subs.txt
dnsx -l subs.txt -a -o resolved.txt
```

---

## ⚙️ Common Options

| Option                  | Description                  |
| ----------------------- | ---------------------------- |
| `-l`                    | File input                   |
| `-silent`               | Clean output without banners |
| `-o`                    | Output file                  |
| `-json`, `-csv`         | Output format                |
| `-a`, `-aaaa`, `-cname` | Record types                 |
| `-r`                    | Custom resolvers             |
| `-retry`, `-timeout`    | Request control              |
| `-filter`               | Filter wildcard DNS          |
| `-ptr`                  | Reverse DNS lookup           |

---

## 🧑‍💻 Real Bug Bounty Workflow Example

```bash
subfinder -d example.com -silent | tee subs.txt
dnsx -l subs.txt -a -resp -o live.txt
httpx -l live.txt -title -tech -o active_webs.txt
nuclei -l active_webs.txt -o scan_results.txt
```

---

## 🛡️ Legal & Ethical Use

* ✅ Use `dnsx` only on **domains you own or have permission** to test.
* ❌ Never use on unauthorized domains.
* 🛑 Be mindful of rate limits if using company/public resolvers.

---

## 📦 Summary

| Tool           | `dnsx`                                  |
| -------------- | --------------------------------------- |
| Developer      | ProjectDiscovery                        |
| Purpose        | DNS resolution and validation           |
| Best For       | Validating subdomains, mass DNS lookups |
| Speed          | High (multi-threaded)                   |
| Integrations   | `subfinder`, `amass`, `httpx`, `nuclei` |
| Output Formats | Text, JSON, CSV                         |
| Install        | `go install`, APT, binaries             |

---

## 📚 Resources

* GitHub: [https://github.com/projectdiscovery/dnsx](https://github.com/projectdiscovery/dnsx)
* Docs: [https://dnsx.projectdiscovery.io](https://dnsx.projectdiscovery.io)
* Community: [https://discord.gg/projectdiscovery](https://discord.gg/projectdiscovery)

---


