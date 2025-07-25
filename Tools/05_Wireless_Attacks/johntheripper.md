Awesome — let’s dive deep into **John the Ripper (JtR)**, one of the classic and most powerful password-cracking tools used in ethical hacking and cybersecurity. I’ll break it down cleanly like we did for Metasploit:

---

# 🔐 John the Ripper — Complete Guide  

---

## 📖 What is John the Ripper?  
**John the Ripper (JtR)** is an open-source, fast, and flexible password-cracking tool used to test password strength and recover lost passwords by performing brute-force, dictionary, and hybrid attacks against password hashes.

It’s widely used by:
- **Ethical hackers**
- **Pentesters**
- **Sysadmins**
- **CTF players**

---

## 🛠️ How Does It Work?  
John takes a file containing hashed passwords and tries to crack them by comparing them against:
- Wordlist files (dictionary)
- Generated combinations (brute-force)
- Rule-based mutations (hybrid)

It supports various hash types:
- Unix `/etc/shadow`
- Windows LM/NTLM
- MD5, SHA, bcrypt, DES, Blowfish, etc.
- Zip, RAR, and many others

---

## 🎛️ Installation  
### 📦 On Kali Linux (pre-installed, but if needed)
```bash
sudo apt update
sudo apt install john
```

---

## 📂 Common Files  
| File                      | Purpose                       |
|:---------------------------|:--------------------------------|
| `john`                     | Main executable |
| `/usr/share/john/password.lst` | Default wordlist |
| `john.pot`                  | Stores cracked passwords |

---

## 🎯 Cracking Password Hashes  

### 1️⃣ **Basic Password Cracking**
```bash
john /path/to/hashfile
```
→ Cracks using the default wordlist.

---

### 2️⃣ **Crack with a Custom Wordlist**
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt /path/to/hashfile
```
✅ `rockyou.txt` is a famous password list pre-installed on Kali.

---

### 3️⃣ **Show Cracked Passwords**
```bash
john --show /path/to/hashfile
```
✅ Displays cracked passwords from `john.pot`.

---

### 4️⃣ **Identify Hash Type**
If you're unsure of the hash type:
```bash
john --list=formats
```
✅ Lists supported hash formats (like `raw-md5`, `nt`, `sha512crypt`).

---

## 📑 Example Hash File (`hash.txt`)
```
root:$6$Gf6Gh84J$VYjPdpPxWJnER5J2/3UAwfjEX0rO6BN:18326:0:99999:7:::
user:$1$TUXvJLzE$pp8pnpv8pq8Bnsd:18326:0:99999:7:::
```

---

## 🔥 Attack Modes in John the Ripper  

| Mode           | Description                            | Command Example |
|:----------------|:----------------------------------------|:----------------|
| **Wordlist Attack** | Uses a password list file | `john --wordlist=rockyou.txt hashes.txt` |
| **Incremental (Brute-force)** | Tries every possible combination | `john --incremental hashes.txt` |
| **Single Crack Mode** | Uses login names and user info | `john --single hashes.txt` |
| **External Mode** | Runs custom cracking logic (scripts) | `john --external=NAME hashes.txt` |

---

## 🔧 Customizing Rules

Rules are defined in:
```bash
/etc/john/john.conf
```
Or:
```bash
~/.john/john.conf
```

**Example rule:**
```
[List.Rules:Custom]
Az"[a-z0-9]" A0"[A-Z0-9]"
```
You can define your own mutations for smarter dictionary attacks.

---

## 📊 Session Management  

**Save a session**
```bash
john --session=mycrack --wordlist=rockyou.txt hashes.txt
```

**Resume a session**
```bash
john --restore=mycrack
```

---

## 📦 Supported Hash Types  

| Type         | Format |
|:---------------|:-----------|
| Linux SHA-512 | `sha512crypt` |
| Windows NTLM   | `nt` |
| MD5            | `raw-md5` |
| ZIP/ RAR       | `zip`, `rar` |
| bcrypt         | `bcrypt` |
| LM             | `lm` |

Check them all with:
```bash
john --list=formats
```

---

## 📚 Common Commands Cheat Sheet  

| Task                         | Command |
|:------------------------------|:---------|
| Start crack (default wordlist) | `john hashfile` |
| Use custom wordlist            | `john --wordlist=wordlist.txt hashfile` |
| Show cracked passwords         | `john --show hashfile` |
| Resume from a session          | `john --restore=session_name` |
| Brute-force (incremental)      | `john --incremental hashfile` |
| List supported hash formats    | `john --list=formats` |

---

## 🎮 Real-World Example (Shadow File)

1. **Extract hashes from `/etc/shadow`**
```bash
unshadow /etc/passwd /etc/shadow > hashfile
```

2. **Crack them**
```bash
john --wordlist=rockyou.txt hashfile
```

3. **View results**
```bash
john --show hashfile
```

---

## ✅ Why Use John the Ripper?

✅ Fast and multi-threaded  
✅ Supports tons of hash types  
✅ Flexible attack modes  
✅ Supports distributed cracking  
✅ Great for password audit and recovery  
✅ Works offline, ideal for pentesting

---

## 📌 Summary  

| What It Does             | How |
|:--------------------------|:-----|
| Crack password hashes       | Using wordlists, brute-force, or hybrid attacks |
| Test password strength      | Against real attack scenarios |
| Support wide hash formats   | Linux, Windows, Archive, Web hashes |
| Manage and resume sessions  | Using `--session` and `--restore` |
| Display cracked passwords   | Using `--show` |

---

If you want, I can also generate:
- 📄 A **Markdown version**
- 📚 A **PDF cheatsheet**
- 📦 A **practice lab guide** for John the Ripper  

Would you like me to create one for you too? 🚀