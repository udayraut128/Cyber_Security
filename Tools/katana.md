Certainly! Here is a **complete and detailed explanation of the `katana` tool** — covering everything **without skipping anything**, including its purpose, features, installation, configuration, **real-world examples**, and usage in **bug bounty and penetration testing workflows**.

---

# 🗡️ What is Katana?

**Katana** is a **next-generation web crawler** developed by **ProjectDiscovery**, designed for **discovery of web assets**, endpoints, parameters, and directories. It’s **fast**, **extensible**, and ideal for **bug bounty hunting**, **recon**, and **security assessments**.

---

## 🧠 Why Use Katana?

Katana excels where traditional crawlers fall short:

✅ Crawls **JavaScript-based applications (JS parsing)**
✅ Extracts **URLs, endpoints, forms, files, parameters, hidden paths**
✅ Supports **headless browsing** (Chromium)
✅ Handles **modern SPAs**, dynamic pages, and **client-side routing**
✅ Can be integrated in **automation pipelines**

---

## 🔧 Installation

### ✅ 1. Using Go

```bash
go install github.com/projectdiscovery/katana/cmd/katana@latest
```

Make sure `GOBIN` is in your PATH:

```bash
export PATH=$PATH:$(go env GOPATH)/bin
```

### ✅ 2. On Kali Linux (manual)

```bash
git clone https://github.com/projectdiscovery/katana.git
cd katana/cmd/katana
go build .
sudo mv katana /usr/local/bin/
```

---

## ⚙️ Katana Architecture

Katana supports two main types of crawling:

| Type                  | Description                                                 |
| --------------------- | ----------------------------------------------------------- |
| **Static Crawling**   | Parses HTML content for links, forms, scripts, assets       |
| **JS Parsing**        | Parses inline and external JS for endpoints                 |
| **Headless Crawling** | Uses a browser engine (like Chromium) for full JS rendering |

It extracts:

* `href`, `src`, `action`, and JavaScript-based endpoints
* Parameters in links (e.g., `?id=`)
* Internal and external links
* Subdomains and endpoints

---

# 📚 Basic Usage

### ✅ Scan a Single URL

```bash
katana -u https://example.com
```

### ✅ Scan a List of URLs

```bash
katana -list urls.txt
```

---

## 🔥 Examples with Real Flags

---

### 📄 1. Save Output to File

```bash
katana -u https://example.com -o output.txt
```

---

### 🔎 2. Enable JavaScript Parsing

```bash
katana -u https://example.com -js-crawl
```

Finds hidden endpoints inside scripts like:

```js
var apiUrl = "/api/user";
```

---

### 🧠 3. Enable Headless Crawling (Dynamic JS Rendering)

```bash
katana -u https://example.com -headless
```

* Requires `Chromium` installed.
* Handles SPAs (React, Angular, Vue apps).

---

### ⚙️ 4. Use Depth and Concurrency

```bash
katana -u https://example.com -d 3 -c 30
```

* `-d`: Crawling depth (default is 1)
* `-c`: Number of concurrent threads

---

### 📦 5. Output as JSON

```bash
katana -u https://example.com -json -o result.json
```

---

### 🚫 6. Exclude Specific Parameters or File Types

```bash
katana -u https://example.com -exclude-paths ".jpg,.png,.svg,.css"
```

---

### 📂 7. Custom Headers or Cookies

```bash
katana -u https://example.com -H "Authorization: Bearer <token>"
```

Or using a cookie:

```bash
katana -u https://example.com -cookie "session=abcd1234"
```

---

### 🔄 8. Combine with Other Tools

```bash
subfinder -d example.com -silent | httpx -silent | katana -list -
```

Chain with nuclei:

```bash
katana -u https://example.com -silent | nuclei -l -
```

---

## 🔌 Advanced Options

| Option           | Description                                     |
| ---------------- | ----------------------------------------------- |
| `-js-crawl`      | Enable JS parsing                               |
| `-headless`      | Enable Chromium-based rendering                 |
| `-t`             | Number of threads                               |
| `-c`             | Concurrency per target                          |
| `-d`             | Maximum depth                                   |
| `-H`             | Custom headers                                  |
| `-exclude-paths` | Skip paths like `.png`, `.jpg`                  |
| `-o`             | Output file                                     |
| `-silent`        | Clean output for scripts                        |
| `-json`          | Output in JSON format                           |
| `-retries`       | Retry on request failure                        |
| `-timeout`       | Set request timeout                             |
| `-fuzzing`       | Detect parameterized URLs (`?id=`, `?q=`, etc.) |

---

## 🧑‍💻 Use Cases

| Use Case                 | Katana Capability                        |
| ------------------------ | ---------------------------------------- |
| 🔎 Endpoint discovery    | URLs, JS endpoints, parameters           |
| 💥 Hidden attack surface | JS parsing + headless crawling           |
| 🧪 Bug bounty recon      | Feed katana into nuclei, xray, etc.      |
| ⚙️ API enumeration       | Detect API paths (e.g., `/api/v1/login`) |
| 🎯 Parameter mining      | URLs like `/search?q=`                   |
| 🧵 Workflow automation   | Works in chains with other tools         |

---

## 🖼️ Output Format Example

### Text Output

```
https://example.com/login
https://example.com/api/user?id=12
```

### JSON Output

```json
{
  "source": "html",
  "tag": "a",
  "type": "link",
  "url": "https://example.com/admin"
}
```

---

## 💻 Chromium Installation (for `-headless`)

On Kali:

```bash
sudo apt install chromium
```

On Ubuntu:

```bash
sudo apt install chromium-browser
```

---

## 🧪 Example Bash Script

```bash
#!/bin/bash

domain=$1

subfinder -d $domain -silent | httpx -silent | katana -list - -js-crawl -d 3 -o "$domain-katana.txt"
```

---

## 🧩 Integration with Recon Pipeline

```bash
subfinder -d example.com -silent | \
httpx -silent | \
katana -list - -d 2 -js-crawl -silent | \
nuclei -l -
```

---

## 🔄 Updating Katana

If installed via Go:

```bash
go install github.com/projectdiscovery/katana/cmd/katana@latest
```

---

## 📌 Summary Table

| Feature             | Supported  |
| ------------------- | ---------- |
| Static crawling     | ✅          |
| JavaScript parsing  | ✅          |
| Headless crawling   | ✅          |
| Depth control       | ✅          |
| Output formats      | Text, JSON |
| Automation support  | ✅          |
| Modern SPA handling | ✅          |
| Parameter detection | ✅          |
| Integration-ready   | ✅          |

---

## 📎 GitHub Repo

🔗 [https://github.com/projectdiscovery/katana](https://github.com/projectdiscovery/katana)

---

