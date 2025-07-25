
---

# 🔐 What is Hashcat?

**Hashcat** is the **world's fastest password recovery tool** (password cracker). It is designed to **crack hashed passwords** using a variety of **attack modes** with **high performance** via **CPU**, **GPU**, or **FPGA** acceleration.

It supports a wide range of **hash types** (MD5, SHA1, bcrypt, NTLM, WPA2, etc.) and is widely used in **cybersecurity**, **CTFs**, **red teaming**, and **penetration testing**.

---

## 🧠 Key Features

✅ High performance: GPU/CPU parallel cracking
✅ Supports 300+ hash algorithms
✅ Multiple attack modes
✅ Supports rule-based attacks
✅ Supports hashlist and password dictionaries
✅ Supports mask/brute force with custom charset
✅ Open-source and cross-platform
✅ Can crack **WPA/WPA2**, NTLM, bcrypt, SHA-512, and more
✅ Supports recovery from interrupted sessions

---

## 🔧 Installation

### 🐧 On Linux (Kali/Ubuntu)

```bash
sudo apt update
sudo apt install hashcat -y
```

Verify:

```bash
hashcat --help
```

### 🍎 On macOS

```bash
brew install hashcat
```

### 🪟 On Windows

1. Download from official site: [https://hashcat.net/hashcat/](https://hashcat.net/hashcat/)
2. Extract ZIP and run `hashcat.exe` via command line.

---

## 🔢 Hash Types Supported

Here are a few common ones:

| Hash Type | Hashcat Mode | Example Hash                                                   |
| --------- | ------------ | -------------------------------------------------------------- |
| MD5       | `0`          | `5f4dcc3b5aa765d61d8327deb882cf99`                             |
| SHA1      | `100`        | `5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8`                     |
| SHA256    | `1400`       | `5e884898da28047151d0e56f8dc6292773603d0d6aabbdd`              |
| NTLM      | `1000`       | `8846f7eaee8fb117ad06bdd830b7586c`                             |
| bcrypt    | `3200`       | `$2a$12$KIXQ4zMJcXz6n2e/uNG82uv9sjBeTjD1I5iGaG5EyLPvfzg4sUL9u` |
| WPA/WPA2  | `2500/22000` | `.hccapx` or `.22000` files                                    |

Use `--example-hashes` to view built-in types:

```bash
hashcat --example-hashes
```

---

## ⚔️ Attack Modes in Hashcat

| Mode | Name                           | Description               |
| ---- | ------------------------------ | ------------------------- |
| 0    | Dictionary Attack              | Uses a wordlist           |
| 1    | Combinator Attack              | Combines two dictionaries |
| 3    | Brute-force / Mask             | Custom charset masks      |
| 6    | Hybrid Wordlist + Mask         | Wordlist + mask           |
| 7    | Hybrid Mask + Wordlist         | Mask + wordlist           |
| 9    | Association attack (optimized) | Specific for some formats |

---

# 🔥 Examples of Usage

---

### ✅ 1. Dictionary Attack (Mode 0)

**Crack an MD5 hash using rockyou.txt**

```bash
hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```

* `-m 0` = MD5 hash
* `-a 0` = Dictionary attack
* `hash.txt` = file containing the hash
* `rockyou.txt` = password wordlist

Example hash in `hash.txt`:

```
5f4dcc3b5aa765d61d8327deb882cf99
```

(Which is `"password"` in MD5)

---

### ✅ 2. Brute Force Attack (Mode 3)

**Try all lowercase 6-letter passwords for an NTLM hash**

```bash
hashcat -m 1000 -a 3 hash.txt ?l?l?l?l?l?l
```

* `?l` = lowercase (a-z)
* `?d` = digit
* `?u` = uppercase
* `?s` = special character

Example: `?u?l?l?l?l?d` = Uabcd7

---

### ✅ 3. Mask Attack + Dictionary (Mode 6)

**Use dictionary + 2 numbers at the end**

```bash
hashcat -m 0 -a 6 hash.txt rockyou.txt ?d?d
```

E.g., tries: `password01`, `admin99`, `12345678`

---

### ✅ 4. Combinator Attack (Mode 1)

**Combine two wordlists**

```bash
hashcat -m 0 -a 1 hash.txt list1.txt list2.txt
```

Will try combinations like: `hello123`, `adminroot`

---

### ✅ 5. Resume a Cracking Session

```bash
hashcat --restore
```

Or checkpoint resume:

```bash
hashcat --session=myjob --restore
```

---

### ✅ 6. Crack WPA/WPA2 Wi-Fi

```bash
hashcat -m 22000 -a 3 wifi.hc22000 ?d?d?d?d?d?d?d?d
```

* `hc22000` = converted WPA capture file
* Try 8-digit numeric PINs

To convert `.pcap` → `.22000`:

```bash
hcxpcapngtool wifi.pcapng -o wifi.hc22000
```

---

## 🔄 Custom Charset

```bash
?l = abcdefghijklmnopqrstuvwxyz
?u = ABCDEFGHIJKLMNOPQRSTUVWXYZ
?d = 0123456789
?s = Special (!, @, #, etc.)
?a = All above
```

---

## 📁 Output

Cracked passwords are saved in:

```
hashcat.potfile
```

To view cracked hashes:

```bash
cat hashcat.potfile
```

---

## ⚡ Performance Tips

* Use GPU for faster cracking (NVIDIA/AMD recommended)
* Use `--force` to override compatibility warnings (if needed)
* Limit session time using `--runtime` (e.g., `--runtime=60`)
* Use `--status` or `--status-timer=10` to show progress

---

## 🧠 Example: Full Workflow

```bash
echo -n "password123" | md5sum
# → 482c811da5d5b4bc6d497ffa98491e38

echo "482c811da5d5b4bc6d497ffa98491e38" > hash.txt

hashcat -m 0 -a 0 hash.txt rockyou.txt
```

If cracked:

```
hash.txt:password123
```

---

## 🧰 Helpful Options

| Option           | Description                     |
| ---------------- | ------------------------------- |
| `--session`      | Set session name                |
| `--restore`      | Resume session                  |
| `--show`         | Display cracked hashes          |
| `--username`     | Ignore usernames in hash file   |
| `--remove`       | Remove cracked hashes from file |
| `--status`       | Show status updates             |
| `--increment`    | Enable incremental masks        |
| `--potfile-path` | Set custom potfile path         |
| `--outfile`      | Save cracked results to a file  |

---

## 🧪 Example Hash File Format

For WPA:

```
example.hc22000
```

For general hashes (like NTLM, MD5):

```
<hash only>
```

Or with usernames:

```
username:hash
```

Use `--username` if needed.

---

## 🧬 Wordlists for Cracking

* `/usr/share/wordlists/rockyou.txt` (Kali default)
* `SecLists` repo: [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)
* Custom or generated using tools like `crunch`, `cewl`

---

## 📊 Benchmark Your System

```bash
hashcat -b
```

Gives hash speed per algorithm.

---

## 🔐 When to Use Hashcat?

| Scenario                    | Use Hashcat? |
| --------------------------- | ------------ |
| Penetration test (NTLM)     | ✅            |
| Cracking Wi-Fi (WPA/WPA2)   | ✅            |
| Cracking web app hash leaks | ✅            |
| CTF password recovery       | ✅            |
| Brute forcing random hashes | ✅            |
| Cracking hashed token APIs  | ✅            |

---

## ⚠️ Legal Warning

🔴 **Always have authorization** when cracking hashes. Use in CTFs, research, or environments where you have **explicit permission**. Unauthorized password cracking is illegal.

---

## 🔗 Official Resources

* 🔹 [Website](https://hashcat.net/hashcat/)
* 🔹 [Wiki](https://hashcat.net/wiki/)
* 🔹 [GitHub](https://github.com/hashcat/hashcat)
* 🔹 [Hash Mode List](https://hashcat.net/wiki/doku.php?id=hashcat)

---


