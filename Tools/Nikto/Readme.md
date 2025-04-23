Great choice — **Nikto** is another powerful tool every cybersecurity learner and ethical hacker should be familiar with. Let’s dive deep into it just like we did with John the Ripper:

---

# 🔍 Nikto — Full Detailed Guide  

---

## 📖 What is Nikto?  
**Nikto** is an open-source, command-line-based **web server scanner** used for:
- **Vulnerability scanning**
- **Detecting server misconfigurations**
- **Finding potentially dangerous files and programs**
- **Checking outdated server software**

Nikto isn’t stealthy — it’s fast and loud, meant for **thorough and visible web scanning**.

---

## 🛠️ Features of Nikto  

✅ Detects **over 6700 potentially dangerous files/CGIs**  
✅ Checks for **outdated versions of over 1250 servers**  
✅ Identifies **server configuration issues**  
✅ Supports **SSL** scanning  
✅ Outputs in **HTML, CSV, XML, NBE, or text formats**  
✅ Checks for **HTTP server headers**, security options  
✅ Supports **mutation and plugin-based testing**

---

## 📦 Installation  

### 📌 On Kali Linux (Pre-installed)
```bash
nikto -Version
```

If not installed:
```bash
sudo apt update
sudo apt install nikto
```

Or clone manually:
```bash
git clone https://github.com/sullo/nikto.git
cd nikto
perl nikto.pl
```

---

## 🕹️ Basic Usage

```bash
nikto -h http://example.com
```
- `-h` → Target host (domain or IP)

✅ It scans and lists vulnerabilities found on the target web server.

---

## 🎯 Common Commands  

| Command | Description |
|:-----------|:-------------|
| `nikto -h http://192.168.1.1` | Scan target IP |
| `nikto -h https://example.com` | Scan target HTTPS domain |
| `nikto -h 192.168.1.1 -p 8080` | Scan on a specific port |
| `nikto -h example.com -o output.txt` | Save scan report to a file |
| `nikto -h example.com -Format html -o report.html` | Save as HTML format |
| `nikto -h example.com -Tuning 123` | Run selective tests (see tuning options) |
| `nikto -h example.com -ssl` | Force SSL mode |
| `nikto -C all -h example.com` | Check all known config files |
| `nikto -Display V` | Verbose output |

---

## 📊 Example Scan Output  

```bash
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          192.168.1.10
+ Target Hostname:    testsite.local
+ Port:               80
+ Server:             Apache/2.4.29
+ The anti-clickjacking X-Frame-Options header is not present.
+ Server leaks inodes via ETags, header found with file/inode information.
+ Found directory: /admin/
+ OSVDB-3092: /test/: Directory indexing found.
+ Uncommon header 'x-powered-by' found, with value 'PHP/7.2.24'
---------------------------------------------------------------------------  
```

---

## ⚙️ Important Options

| Option | Meaning |
|:-----------|:--------------------------|
| `-h` | Target host |
| `-p` | Custom port |
| `-ssl` | Force SSL |
| `-o` | Output file |
| `-Format` | Output format (csv, html, nbe, txt, xml) |
| `-Tuning` | Specify test categories |
| `-Cgidirs` | Scan custom CGI directories |
| `-Display V` | Verbose output |
| `-evasion` | Use evasion techniques |

---

## 🎛️ Tuning Options  

`-Tuning` lets you run specific categories of tests.

| Value | Test Type |
|:----------|:--------------|
| `0` | File Upload |
| `1` | Interesting files |
| `2` | Misconfigurations |
| `3` | Default files |
| `4` | Authorization bypass |
| `5` | SQL Injection |
| `6` | Remote File Include |
| `7` | Command Execution |
| `8` | Known vulnerabilities |
| `9` | Administrative access |
| `a` | All tests |

👉 **Example:**  
```bash
nikto -h http://example.com -Tuning 123
```
✅ Runs test categories 1, 2, and 3 only.

---

## 🔐 SSL/TLS and HTTPS Scanning  
To scan a **HTTPS server**:
```bash
nikto -h https://example.com
```
Or force SSL mode:
```bash
nikto -h example.com -ssl
```

---

## 📁 Output Formats  

| Format | Command Example |
|:----------|:----------------------------|
| Text | `-o result.txt` |
| HTML | `-Format html -o report.html` |
| CSV  | `-Format csv -o result.csv` |
| XML  | `-Format xml -o result.xml` |

---

## 🕵️‍♂️ Evading Detection  

Use `-evasion` options to evade WAF/IDS detection:
```bash
nikto -h example.com -evasion 1
```

| Evasion Technique | Code |
|:------------------|:---------|
| Random URI encoding | `1` |
| Random user agent   | `2` |
| Append characters   | `3` |
| Multiple combinations | `123` |

---

## 🔥 Why Use Nikto?  

✅ Open-source and easy to use  
✅ Supports wide range of web vulnerabilities  
✅ Regularly updated vulnerability database  
✅ Works with SSL/TLS and custom ports  
✅ Supports output logging and reporting  
✅ Very useful for **Recon, Vulnerability Assessment, Web Pentesting**

---

## 📚 Common Use Cases  

| Situation                        | Example |
|:-----------------------------------|:------------|
| Scan a website for vulnerabilities | `nikto -h http://site.com` |
| Save a scan report | `nikto -h site.com -o report.txt` |
| Scan a custom port | `nikto -h 192.168.1.1 -p 8080` |
| Run selected test categories | `nikto -h site.com -Tuning 135` |
| Scan over HTTPS | `nikto -h https://site.com` |
| Evade detection | `nikto -h site.com -evasion 1` |

---

## ✅ Summary  

| What It Does               | How |
|:----------------------------|:--------|
| Scan web servers for vulnerabilities | Using Nikto’s extensive test library |
| Detect misconfigurations, outdated software, dangerous files | Automated scanning |
| Support for SSL, custom ports, evasion, reporting | Flexible options |
| Good for **Recon, Vulnerability Scanning, Web Security Audit** | CLI-based tool |

---

## 📦 Quick Command Cheat Sheet  

```bash
nikto -h http://target.com               # Basic scan
nikto -h target.com -p 8080              # Scan on port 8080
nikto -h https://target.com              # Scan HTTPS site
nikto -h target.com -o report.txt        # Save results to a file
nikto -h target.com -Format html -o report.html   # Save as HTML
nikto -h target.com -Tuning 135          # Run selected tests
nikto -h target.com -evasion 1           # Evade detection
nikto -Display V                         # Verbose output
```

---

## 🎨 Want it in Markdown, PDF, or Cheat Sheet Format?  
I can generate a clean **Markdown file**, **PDF version**, or a **ready-to-print cheat sheet** for Nikto too — just let me know 📑🔥  

Would you like that? 🚀