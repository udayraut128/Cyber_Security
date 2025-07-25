
---

# 🔎 What is `feroxbuster`?

**`feroxbuster`** is a **fast, simple, recursive content discovery tool** written in **Rust**. It helps identify **hidden web files, directories, and endpoints** on a website by brute-forcing URLs using **wordlists**.

It's like **DirBuster**, **gobuster**, or **dirsearch**, but with extra **speed**, **recursion**, and **flexibility**.

---

## 🧠 What is it used for?

* Finding hidden directories (e.g., `/admin/`, `/backup/`, `/login/`)
* Finding sensitive files (e.g., `.git`, `.env`, `config.php`)
* **Recursive brute-forcing** (go deeper into discovered directories)
* Automating part of the **web reconnaissance** and **attack surface discovery** process

---

# ⚙️ Features

| Feature               | Description                                                       |
| --------------------- | ----------------------------------------------------------------- |
| ⚡ Written in Rust     | Extremely fast and efficient                                      |
| 🔁 Recursive          | Automatically scans directories it finds                          |
| 📑 Custom Wordlists   | Supports any wordlist                                             |
| 📄 Extension guessing | Try `.php`, `.html`, `.bak`, etc.                                 |
| 🧾 Output formats     | JSON, HTML, CSV, and plaintext                                    |
| 📤 Proxy support      | Use tools like Burp or an intercepting proxy                      |
| 🔐 Auth support       | Supports Basic Auth, Bearer Token, and custom headers             |
| 📦 Easy integration   | Works well with automation tools and scripts                      |
| 🧠 Smart filtering    | Filters based on status codes, content length, words, lines, etc. |
| 🚀 Resumable scans    | Continue interrupted scans using `--resume-from`                  |

---

## 🖥️ Installation

### ✅ On Kali Linux

```bash
sudo apt install feroxbuster
```

### ✅ Using Cargo (Rust)

```bash
cargo install feroxbuster
```

### ✅ Precompiled Binary

Download from:
👉 [https://github.com/epi052/feroxbuster/releases](https://github.com/epi052/feroxbuster/releases)

Make it executable:

```bash
chmod +x feroxbuster
```

---

# 📌 Basic Syntax

```bash
feroxbuster -u <URL> -w <wordlist>
```

---

# 🔍 Usage Examples

---

### ✅ 1. Basic Directory Bruteforce

```bash
feroxbuster -u https://example.com -w /usr/share/wordlists/dirb/common.txt
```

Scans `example.com` using the given wordlist.

---

### 🔁 2. Recursive Scanning

```bash
feroxbuster -u https://example.com -w /usr/share/wordlists/dirb/common.txt -r
```

Adds recursion: if `/admin/` is found, it scans `https://example.com/admin/` too.

---

### 🔒 3. Use HTTP Authentication

```bash
feroxbuster -u https://example.com -w wordlist.txt -b user:password
```

---

### 🎭 4. Set Custom Headers (e.g., JWT token)

```bash
feroxbuster -u https://example.com -H "Authorization: Bearer <token>" -w wordlist.txt
```

---

### 📁 5. Use Multiple Extensions

```bash
feroxbuster -u https://example.com -w wordlist.txt -x php,html,bak,txt
```

Scans for `login.php`, `login.html`, `login.bak`, etc.

---

### 💥 6. Ignore Certain Status Codes

```bash
feroxbuster -u https://example.com -w wordlist.txt --filter-status 403,404
```

Removes forbidden/not found results from output.

---

### 📊 7. Save Output

```bash
feroxbuster -u https://example.com -w wordlist.txt -o output.txt
```

Save all findings to `output.txt`.

---

### 📂 8. Scan Multiple URLs

```bash
feroxbuster -U urls.txt -w wordlist.txt
```

Where `urls.txt` contains:

```
https://example.com
https://test.com
```

---

### ⚙️ 9. Limit Threads/Connections

```bash
feroxbuster -u https://example.com -w wordlist.txt -t 25
```

Limits threads to 25 (default is 50). Good for slow servers.

---

### 🧠 10. Smart Filtering by Size

```bash
feroxbuster -u https://example.com -w wordlist.txt --filter-size 1234
```

Filter all results with size 1234 bytes (usually useless responses like 403s or 404s).

---

# 🧠 Advanced Features

---

### 📡 Proxy Support

```bash
feroxbuster -u https://target.com -w wordlist.txt --proxy http://127.0.0.1:8080
```

Perfect for sending requests through **Burp Suite** or a **logging proxy**.

---

### 💾 Resume From Last Path

```bash
feroxbuster -u https://example.com -w wordlist.txt --resume-from /admin/
```

Restarts a scan from the given path.

---

### 🧪 Follow Redirects

```bash
feroxbuster -u https://example.com -w wordlist.txt --follow-redirects
```

Useful when the server auto-redirects certain paths.

---

### 🐍 Run from Python script

```python
import subprocess

subprocess.run([
    "feroxbuster", 
    "-u", "https://example.com", 
    "-w", "/usr/share/wordlists/dirb/common.txt", 
    "-o", "found.txt"
])
```

---

# 🚨 Real-World Bug Bounty Use Case

### 🔗 Combine with Subfinder and Httpx

```bash
subfinder -d example.com -silent | httpx -silent | while read url; do 
    feroxbuster -u $url -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html,bak,txt,json -r -o "$url.txt"; 
done
```

---

# 📌 Summary Table

| Feature            | Details                                                                        |
| ------------------ | ------------------------------------------------------------------------------ |
| Tool               | feroxbuster                                                                    |
| Written In         | Rust                                                                           |
| Main Use           | Content discovery (files & directories)                                        |
| Recursion          | ✅                                                                              |
| Auth Support       | ✅ Basic & Bearer                                                               |
| Proxy Support      | ✅ (e.g., Burp)                                                                 |
| Extensions Support | ✅                                                                              |
| Filter Options     | ✅ Status, size, words, lines                                                   |
| Output Formats     | Plain, JSON, CSV, HTML                                                         |
| Multi-threaded     | ✅                                                                              |
| CLI Friendly       | ✅ Easy to integrate with scripts                                               |
| GitHub             | [https://github.com/epi052/feroxbuster](https://github.com/epi052/feroxbuster) |

---

# 📚 Wordlist Recommendations

* `/usr/share/wordlists/dirb/common.txt`
* `/usr/share/seclists/Discovery/Web-Content/raft-large-words.txt`
* `/usr/share/seclists/Discovery/Web-Content/common.txt`

> Tip: Use large lists + recursion to uncover deep, hidden endpoints.

---

# 🧠 Tips

* Use `--depth` to limit recursion depth
* Pair with `waybackurls` and `gau` to find known URLs
* Scan for specific extensions to reduce noise
* Use proxies or rate limiting for stealth

---
