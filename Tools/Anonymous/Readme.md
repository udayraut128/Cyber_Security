Awesome — you’ve written a super clean, step-by-step guide!  
And yes — let’s turn it into a neat **Markdown document** for GitHub or your documentation collection.  
Here’s a cleanly formatted **Markdown version** for you:

---

# 🛡️ Anonymous Browsing with Tor, Tornet, and Firefox Proxy  

Securely route your browser traffic through the Tor network with automatic IP rotation using **Tornet**.

---

## 📦 Install Tornet

Install **Tornet** via `pip` or `pipx`:
```bash
pip install tornet
# or
pipx install tornet
```

---

## ⚙️ Enable and Start Tor Service

### Enable Tor service to start at boot:
```bash
sudo systemctl enable tor
```

### Start Tor service:
```bash
sudo systemctl start tor
```

---

## ✅ Verify Tor Service Status

Check if the Tor service is running:
```bash
service tor status
```
You should see:
```
Active: active (running)
```

---

## 🌐 Configure Firefox for Tor Proxy

1. Open **Firefox**.
2. Go to **Settings**.
3. Search for **"Proxy"**.
4. Select **Manual proxy configuration**.
5. Under **SOCKS Host**, enter:
   - **Host:** `127.0.0.1`
   - **Port:** `9050`
6. Save the settings.

---

## 🔄 Start IP Rotation with Tornet

Use Tornet to rotate Tor exit nodes:
```bash
sudo tornet --interval 2 --count 0
```
- `--interval 2` → Rotate every 2 seconds.
- `--count 0` → Infinite rotations.

---

## 🌍 Verify Your New IP Location

Visit:
> [https://am.i.mullvad.net/country](https://am.i.mullvad.net/country)

If it shows a country different from your real location, you’re successfully anonymized via Tor!

---

## 📖 References  
- 🔗 [Tornet Official](https://tornet.co/)  
- 📦 [Tornet PyPi](https://pydigger.com/pypi/tornet)  
- 📝 [Kali Linux Docs on Python Packages](https://www.kali.org/docs/general-use/python3-external-packages/)

---
