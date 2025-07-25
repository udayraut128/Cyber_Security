🔥 You’ve chosen **John the Ripper (JtR)** — one of the most famous, powerful, and versatile password-cracking tools in offensive security.

Here’s **the complete, detailed explanation of John the Ripper**, including **all core topics, modes, commands, formats, and real-world examples — nothing skipped.**

---

# 🐉 Kali GPT’s Full John the Ripper Guide

---

# 📖 **What is John the Ripper?**

* **John the Ripper (JtR)** is an open-source **password-cracking tool**.
* Designed to **detect weak passwords** by performing:

  * Brute-force attacks
  * Dictionary attacks
  * Hybrid attacks
  * Incremental (pure brute-force) attacks
* Supports **a wide variety of password hash formats**, including:

  * Linux (`/etc/shadow`)
  * Windows (`SAM`)
  * MD5, SHA, NTLM, LM, bcrypt, and more.
* Multi-threaded and GPU-accelerated (via John Jumbo version).

✅ Pre-installed in Kali Linux
✅ Can crack hashes, encrypted files, ZIP/RAR archives, SSH keys, and more.

---

# 🚀 **John the Ripper Basic Syntax**

```bash
john [options] <hashfile>
```

Example:

```bash
john --wordlist=rockyou.txt hashes.txt
```

---

# 🔧 **John the Ripper Core Modes**

| Mode              | Description                                     |
| ----------------- | ----------------------------------------------- |
| Wordlist mode     | Cracks passwords using a wordlist               |
| Incremental mode  | Brute-force all possible character combinations |
| Single crack mode | Cracks based on user information (fastest mode) |
| External mode     | Highly customizable cracking via external rules |
| Hybrid mode       | Combines dictionary and brute-force             |

---

# 🎯 **Hash Formats Supported (Partial List)**

* DES (Unix)
* MD5 (Unix and raw)
* SHA-256 / SHA-512 (Unix)
* bcrypt
* NTLM (Windows)
* LM (Windows legacy)
* MD4
* SHA-1
* MySQL
* SHA-1(\$salt)
* ZIP/RAR archives
* PDF/Office documents
* WiFi WPA/WPA2 handshakes (via hash extraction)

👉 Supported formats list:

```bash
john --list=formats
```

---

# 🛠️ **Essential Workflow: Step-by-Step**

---

## ✅ Step 1: Prepare Hashes

Example hash file:

```text
$6$eBZaQw...$2yAKn7f.kM5/MjcdyR8
```

Copy hashes into `hashes.txt`.

---

## ✅ Step 2: Run Wordlist Attack

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

* Uses rockyou.txt to guess passwords.

---

## ✅ Step 3: View Cracked Passwords

```bash
john --show hashes.txt
```

* Displays cracked passwords.

---

## ✅ Step 4: Resume Cracking (if interrupted)

```bash
john --restore
```

---

## ✅ Step 5: Brute-Force Mode

```bash
john --incremental hashes.txt
```

* Tries **all possible character combinations.**

---

## ✅ Step 6: Single Crack Mode

```bash
john --single hashes.txt
```

* Uses hints from usernames, filenames, etc.
* Fastest mode.

---

## ✅ Step 7: Save and Resume Sessions

Start named session:

```bash
john --session=mycrack --wordlist=rockyou.txt hashes.txt
```

Resume session:

```bash
john --restore=mycrack
```

---

# ⚙️ **John the Ripper Common Options**

| Option            | Purpose                                   |
| ----------------- | ----------------------------------------- |
| `--wordlist=FILE` | Specify wordlist file                     |
| `--rules`         | Apply mangling rules                      |
| `--format=TYPE`   | Specify hash type                         |
| `--show`          | Show cracked passwords                    |
| `--session=NAME`  | Save cracking session                     |
| `--incremental`   | Brute-force all combos                    |
| `--restore`       | Resume previous session                   |
| `--mask=PATTERN`  | Pattern-based cracking                    |
| `--fork=N`        | Multi-core cracking                       |
| `--pot=FILE`      | Use custom potfile                        |
| `--stdout`        | Output generated guesses without cracking |

---

# 🧩 **How to Identify Hashes**

Use:

```bash
john --list=formats
```

Or:

```bash
hashid hash.txt
```

Or:

```bash
hashcat -m --example-hashes
```

👉 Alternatively, inspect the hash structure (example: `$6$` prefix = SHA-512 crypt).

---

# 🔒 **Real-World Examples for Different Hashes**

---

### ✅ Crack Linux Password Hashes (from `/etc/shadow`)

```bash
unshadow /etc/passwd /etc/shadow > hashes.txt
john --wordlist=rockyou.txt hashes.txt
```

---

### ✅ Crack Windows NTLM Hashes

```bash
john --format=NT --wordlist=rockyou.txt ntlm_hashes.txt
```

---

### ✅ Crack ZIP File Password

Extract hash:

```bash
zip2john secret.zip > ziphash.txt
```

Crack:

```bash
john --wordlist=rockyou.txt ziphash.txt
```

---

### ✅ Crack WPA2 Handshake (via hashcat preferred, but possible)

Extract handshake:

```bash
hccapx2john handshake.hccapx > wpa_hash.txt
```

Crack:

```bash
john --wordlist=rockyou.txt wpa_hash.txt
```

---

### ✅ Hybrid Mode (Wordlist + Bruteforce)

```bash
john --wordlist=rockyou.txt --rules hashes.txt
```

* Applies mangling rules (adds numbers, symbols, etc.)

---

### ✅ Incremental Mode (Full Brute-Force)

```bash
john --incremental=All hashes.txt
```

* Bruteforce using all characters.

---

### ✅ Mask Mode (Pattern-Based)

```bash
john --mask='?u?l?l?l?d?d' hashes.txt
```

* Example: uppercase + lowercase + lowercase + lowercase + digit + digit
* Useful when password format is known.

---

### ✅ Session Management

Start a session:

```bash
john --session=ftpcrack --wordlist=ftp.txt hashes.txt
```

Resume:

```bash
john --restore=ftpcrack
```

---

### ✅ Show Cracked Passwords

```bash
john --show hashes.txt
```

---

### ✅ Parallel Processing (Fork)

```bash
john --fork=4 --wordlist=rockyou.txt hashes.txt
```

* Utilizes 4 CPU cores.

---

### ✅ Output Password Guesses Only

```bash
john --wordlist=rockyou.txt --stdout
```

* Does not attempt cracking → useful for generating password lists.

---

# 🛡️ **John the Ripper Pro Tips**

* Use **wordlist + rules** first → fastest success rate.
* Use **incremental mode** as a last resort → very slow for complex passwords.
* Always save sessions to avoid losing progress.
* Use **zip2john, rar2john, pdf2john, ssh2john** to extract hashes from encrypted files.
* Use **john-jumbo** version for maximum format support.

---

# 🔥 Additional John the Ripper Tools

| Tool       | Purpose                                       |
| ---------- | --------------------------------------------- |
| `unshadow` | Combine `/etc/passwd` and `/etc/shadow` files |
| `zip2john` | Extract hash from ZIP archives                |
| `rar2john` | Extract hash from RAR archives                |
| `pdf2john` | Extract hash from encrypted PDFs              |
| `ssh2john` | Extract passphrase hashes from SSH keys       |

---

# ✅ John the Ripper Cheat Sheet

| Action                  | Command                                 |
| ----------------------- | --------------------------------------- |
| Wordlist attack         | `john --wordlist=file hashes.txt`       |
| Incremental brute-force | `john --incremental hashes.txt`         |
| Resume session          | `john --restore`                        |
| Show cracked passwords  | `john --show hashes.txt`                |
| Crack ZIP password      | `zip2john file.zip > hash && john hash` |
| Mask-based attack       | `john --mask='?l?l?l?d?d?d' hashes.txt` |

---

# 🔐 John the Ripper Strengths and Weaknesses

| Strength                         | Weakness                           |
| -------------------------------- | ---------------------------------- |
| Supports many hash types         | Can be slow for complex hashes     |
| Highly customizable              | Less GPU support than Hashcat      |
| Supports encrypted file cracking | Requires hash extraction           |
| Supports session management      | Some formats require Jumbo version |

---


