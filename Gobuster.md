🔥 Excellent — Gobuster is a **powerful and fast brute-forcing tool** that every pentester must master.
Here’s the **complete, detailed explanation of Gobuster** — **no steps skipped, no topics lost.**

---

# 🐉 Kali GPT’s Full Gobuster Guide

---

# 📖 **What is Gobuster?**

* **Gobuster** is a **fast, CLI-based directory and file brute-forcing tool** written in Go.
* It’s widely used for:

  * **Web directory discovery**
  * **Virtual host discovery**
  * **DNS subdomain enumeration**
* Works **much faster than Dirb or Dirbuster** because it’s multi-threaded and highly efficient.

✅ Pre-installed on Kali Linux
✅ Fast and lightweight
✅ Supports **HTTP, HTTPS, DNS, S3, VHOSTS, Fuzzing**

---

# 🚀 **Gobuster Core Command Syntax**

```bash
gobuster [mode] -u [URL] -w [wordlist] [options]
```

Example:

```bash
gobuster dir -u http://target.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

---

# 🔧 **Gobuster Modes**

| Mode  | Purpose                                               |
| ----- | ----------------------------------------------------- |
| dir   | Directory/File brute-forcing                          |
| dns   | Subdomain brute-forcing                               |
| vhost | Virtual host brute-forcing                            |
| s3    | Amazon S3 bucket brute-forcing                        |
| fuzz  | Generic fuzzing (can brute-force any part of the URL) |

---

# 🎯 **Mode: Directory/File Brute-Forcing**

### Basic Example:

```bash
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt
```

* `dir` → Directory mode
* `-u` → Target URL
* `-w` → Wordlist

### Add extensions:

```bash
gobuster dir -u http://target.com -w common.txt -x php,html,txt
```

* `-x` → File extensions to append.

---

# 📂 Key Options for Directory Mode

| Option       | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| `-u`         | Target URL                                                   |
| `-w`         | Wordlist                                                     |
| `-x`         | File extensions                                              |
| `-t`         | Number of threads                                            |
| `-s`         | Expected status codes (default: 200,204,301,302,307,401,403) |
| `--wildcard` | Forces wildcard detection                                    |
| `-o`         | Output file                                                  |
| `-k`         | Ignore SSL certificate errors                                |
| `-r`         | Do not follow redirects                                      |
| `-b`         | Exclude specific status codes                                |
| `-q`         | Quiet mode (only successful results)                         |
| `-e`         | Show expanded URLs                                           |
| `-c`         | Add custom headers (like cookies)                            |

---

### Example: Multi-threaded scan

```bash
gobuster dir -u http://target.com -w common.txt -t 50
```

### Example: Exclude Status Codes

```bash
gobuster dir -u http://target.com -w common.txt -b 403,404
```

### Example: Save output to file

```bash
gobuster dir -u http://target.com -w common.txt -o gobuster_results.txt
```

---

# 🎯 **Mode: DNS Subdomain Brute-Forcing**

### Basic Example:

```bash
gobuster dns -d target.com -w /usr/share/wordlists/dns/namelist.txt
```

* `dns` → DNS mode
* `-d` → Domain name

### Add custom DNS server:

```bash
gobuster dns -d target.com -w namelist.txt -s 200 -r 8.8.8.8
```

* `-s` → Filter response status codes
* `-r` → Use Google DNS

---

# 🎯 **Mode: Virtual Host Brute-Forcing**

### Basic Example:

```bash
gobuster vhost -u http://target.com -w vhosts.txt
```

* Brute-forces virtual hosts on the same IP.

---

# 🎯 **Mode: Amazon S3 Bucket Brute-Forcing**

### Example:

```bash
gobuster s3 -w buckets.txt
```

* Brute-forces Amazon S3 bucket names using provided wordlist.

---

# 🎯 **Mode: Fuzzing (Advanced)**

### Example:

```bash
gobuster fuzz -u http://target.com/FUZZ -w wordlist.txt
```

* `FUZZ` → Placeholder where Gobuster will insert words from the list.

---

# 🔐 **Additional Options**

| Option                      | Purpose                         |
| --------------------------- | ------------------------------- |
| `-c "cookie"`               | Send cookies (session handling) |
| `-H "header"`               | Add custom HTTP headers         |
| `-a "agent"`                | Set User-Agent string           |
| `--delay`                   | Add delay between requests      |
| `--timeout`                 | Set HTTP timeout                |
| `--username` / `--password` | HTTP Basic Auth                 |

---

### Example: Use cookies and custom headers

```bash
gobuster dir -u http://target.com -w common.txt -c "PHPSESSID=abc123" -H "X-Forwarded-For: 127.0.0.1"
```

---

# ⚙️ **Real-World Pentesting Gobuster Workflow**

### 1️⃣ Directory Brute-Force

```bash
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt -x php,html,txt
```

### 2️⃣ Virtual Host Discovery

```bash
gobuster vhost -u http://target.com -w /usr/share/wordlists/vhost-wordlist.txt
```

### 3️⃣ Subdomain Enumeration

```bash
gobuster dns -d target.com -w /usr/share/wordlists/dns/namelist.txt -t 50
```

### 4️⃣ Fuzzing Parameters or Paths

```bash
gobuster fuzz -u http://target.com/login.php?user=FUZZ -w users.txt
```

---

# 🛡️ **Gobuster Tips and Best Practices**

* 🛑 Always verify wildcard responses using `--wildcard`.
* 🏹 Use targeted wordlists to speed up scans.
* ⚡ Start with small lists and increase if initial results look good.
* 🔒 Use the `-k` flag when dealing with self-signed SSL certs.
* 🎯 Combine with Nmap and Dirb for a more complete enumeration.

---

# ✅ Gobuster Cheat Sheet

| Purpose        | Command                                 |
| -------------- | --------------------------------------- |
| Directory scan | `gobuster dir -u URL -w wordlist`       |
| Add extensions | `-x php,html,txt`                       |
| Exclude status | `-b 404,403`                            |
| Save output    | `-o results.txt`                        |
| DNS scan       | `gobuster dns -d domain -w wordlist`    |
| Virtual host   | `gobuster vhost -u URL -w wordlist`     |
| Fuzzing        | `gobuster fuzz -u URL/FUZZ -w wordlist` |
| Proxy headers  | `-H "Header: Value"`                    |
| Use cookies    | `-c "cookie=value"`                     |

---

# 🔥 Pro-Tip: Combine Gobuster + Burp Suite

1. Run Gobuster to quickly identify hidden directories.
2. Use Burp Suite to manually inspect, fuzz, and exploit found paths.

---

 
