Here is the complete content of the **"Cybersecurity Top 50 Interview Q\&A"** document, including all theoretical and scenario-based questions.

---

## ✅ **Top 50 Cybersecurity Interview Questions and Answers**

---

### 🔹 **Part A – 40 Theoretical Questions**

---

#### 1. **What is Cryptography?**

Cryptography is the science of securing data by converting it into unreadable formats using mathematical algorithms, ensuring confidentiality, integrity, and authentication.

---

#### 2. **Difference Between Symmetric and Asymmetric Encryption**

| Feature  | Symmetric Encryption | Asymmetric Encryption       |
| -------- | -------------------- | --------------------------- |
| Keys     | Same key for both    | Public and private key pair |
| Speed    | Faster               | Slower                      |
| Example  | AES, DES             | RSA, ECC                    |
| Use Case | Bulk data transfer   | Secure key exchange         |

---

#### 3. **Difference Between IDS and IPS**

* **IDS (Intrusion Detection System)**: Monitors and alerts on suspicious activity.
* **IPS (Intrusion Prevention System)**: Monitors, detects, and blocks threats in real-time.

---

#### 4. **What is the CIA Triad?**

* **Confidentiality**: Protect data from unauthorized access.
* **Integrity**: Prevent unauthorized data modification.
* **Availability**: Ensure resources are accessible when needed.

---

#### 5. **Encryption vs Hashing**

| Feature     | Encryption      | Hashing         |
| ----------- | --------------- | --------------- |
| Reversible? | Yes (with key)  | No              |
| Purpose     | Confidentiality | Integrity check |
| Examples    | AES, RSA        | MD5, SHA-256    |

---

#### 6. **What is a Firewall?**

A firewall is a security system that monitors and controls incoming/outgoing network traffic using predetermined rules to block threats.

---

#### 7. **VA vs PT**

| Feature    | Vulnerability Assessment | Penetration Testing          |
| ---------- | ------------------------ | ---------------------------- |
| Focus      | Finding vulnerabilities  | Exploiting vulnerabilities   |
| Intrusive? | Non-intrusive            | Intrusive (simulated attack) |

---

#### 8. **Explain Three-Way Handshake (TCP)**

1. **SYN**: Client → Server
2. **SYN-ACK**: Server → Client
3. **ACK**: Client → Server

---

#### 9. **HTTP Response Status Codes**

* **1xx**: Informational
* **2xx**: Success
* **3xx**: Redirection
* **4xx**: Client error
* **5xx**: Server error

---

#### 10. **What is Traceroute?**

A tool that traces the path of a packet across a network, showing each hop and latency.

---

#### 11. **HIDS vs NIDS**

* **HIDS**: Installed on host (e.g., OS logs).
* **NIDS**: Monitors traffic across entire network.

---

#### 12. **Steps to Secure a Firewall**

1. Change default credentials
2. Disable remote admin
3. Enable logging
4. Allow only required ports
5. Update firmware regularly

---

#### 13. **What is SSL?**

Secure Sockets Layer is a protocol for encrypting information over the internet.

---

#### 14. **How to Secure a Server**

* Disable unnecessary ports/services
* Apply patches regularly
* Enforce strong passwords
* Enable firewalls and antivirus

---

#### 15. **What is Data Leakage?**

Unauthorized transmission of data from inside an organization to an external destination.

---

#### 16. **Types of Cyber Attacks**

* Phishing
* Malware
* DDoS
* SQL Injection
* Man-in-the-Middle (MITM)

---

#### 17. **What is a Brute Force Attack?**

Trying every possible password to gain unauthorized access.
**Prevention**: Account lockout, CAPTCHA, 2FA

---

#### 18. **What is Port Scanning?**

Technique used to identify open ports and services on a host using tools like Nmap.

---

#### 19. **7 Layers of OSI Model**

1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

---

#### 20. **What is a VPN?**

Virtual Private Network secures your internet connection by creating an encrypted tunnel over public networks.

---

#### 21. **Risk vs Threat vs Vulnerability**

| Concept       | Definition                        |
| ------------- | --------------------------------- |
| Risk          | Threat exploiting a vulnerability |
| Threat        | Potential danger or attacker      |
| Vulnerability | Weakness that can be exploited    |

---

#### 22. **How to Prevent Identity Theft**

* Use strong, unique passwords
* Monitor financial statements
* Avoid public Wi-Fi for sensitive transactions

---

#### 23. **Types of Hackers**

* **White Hat**: Ethical
* **Black Hat**: Malicious
* **Gray Hat**: Between the two

---

#### 24. **Patch Management Frequency**

Critical patches should be applied immediately. Others can follow a regular schedule (weekly/monthly).

---

#### 25. **How to Reset BIOS Password?**

Remove CMOS battery for a few minutes and reinsert to reset BIOS.

---

#### 26. **MITM Attack and Prevention**

Intercepts communication between two parties.
**Prevention**: HTTPS, VPN, DNSSEC

---

#### 27. **DDoS Attack and Prevention**

* **DDoS**: Flooding server with traffic.
* **Prevention**: Rate limiting, CDN, WAF, load balancers.

---

#### 28. **XSS Attack and Prevention**

Injects scripts into web applications.
**Prevention**: Input sanitization, content security policy

---

#### 29. **What is ARP?**

Address Resolution Protocol maps IP to MAC address in LAN.

---

#### 30. **What is Port Blocking in LAN?**

Disabling unused ports to reduce attack surface.

---

#### 31. **Protocols Under TCP/IP**

| Layer       | Protocols            |
| ----------- | -------------------- |
| Application | HTTP, FTP, DNS, SMTP |
| Transport   | TCP, UDP             |
| Internet    | IP, ICMP, ARP        |
| Link        | Ethernet, PPP        |

---

#### 32. **What is a Botnet?**

A network of infected devices used to launch DDoS or spam attacks.

---

#### 33. **What is Salt in Hashing?**

Random data added to input before hashing to make attacks like rainbow tables ineffective.

---

#### 34. **SSL vs TLS**

| Feature  | SSL (Old)   | TLS (Current)   |
| -------- | ----------- | --------------- |
| Security | Less secure | More secure     |
| Version  | Deprecated  | Active standard |

---

#### 35. **Data in Transit vs At Rest**

* **In Transit**: Moving over network. Encrypt with TLS.
* **At Rest**: Stored. Encrypt with AES or BitLocker.

---

#### 36. **What is 2FA?**

Two-Factor Authentication requires two credentials: something you know and something you have.

---

#### 37. **What is Cognitive Cybersecurity?**

Using AI to detect and respond to threats in real-time by learning attack patterns.

---

#### 38. **VPN vs VLAN**

| Feature    | VPN           | VLAN                   |
| ---------- | ------------- | ---------------------- |
| Encryption | Yes           | No                     |
| Scope      | Internet-wide | LAN-level segmentation |

---

#### 39. **Phishing and Prevention**

* Fake emails/websites to steal info
* **Prevention**: Spam filters, training, DMARC

---

#### 40. **SQL Injection and Prevention**

Injects SQL queries via input fields.
**Prevention**: Prepared statements, input validation

---

### 🔸 **Part B – 10 Scenario-Based Questions**

---

#### 1. **Credential Request via Email**

**Answer**: Phishing attempt. Report it and don’t respond.

---

#### 2. **Received an E-Card from a Friend**

**Answer**: Verify with the sender before opening — could be malware.

---

#### 3. **Getting Multiple Newsletters with Personal Questions**

**Answer**: You are being targeted for identity theft.

---

#### 4. **Bill Prints Show Another User's Data**

**Answer**: Logout properly, clear cache/history before leaving.

---

#### 5. **Yahoo Account Active Even After Logout**

**Answer**: Logout failure. Use private mode and clear cookies.

---

#### 6. **Bank Asks for Details via Email**

**Answer**: Never share banking details via email. It’s phishing.

---

#### 7. **Mouse Moving on Its Own**

**Answer**: Possible remote access. Unplug network, report incident.

---

#### 8. **Evaluate Strongest Password**

`UcSc4Evr!` – contains uppercase, lowercase, digit, and special character.

---

#### 9. **Email with Bank Login Link**

**Answer**: Never click links. Go to the official site directly.

---

#### 10. **University Computer Sending Spam**

**Answer**: System compromised. Change password, update software, scan for malware.

---
