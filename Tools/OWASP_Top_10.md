
---

# 🔐 OWASP Top 10 (2021 Edition) - Full Explanation

The **OWASP Top 10** is a **standard awareness document** for developers and security professionals that highlights the **ten most critical security risks to web applications**.

---

## ✅ OWASP Top 10 List

| Code     | Name                                       |
| -------- | ------------------------------------------ |
| A01:2021 | Broken Access Control                      |
| A02:2021 | Cryptographic Failures                     |
| A03:2021 | Injection                                  |
| A04:2021 | Insecure Design                            |
| A05:2021 | Security Misconfiguration                  |
| A06:2021 | Vulnerable and Outdated Components         |
| A07:2021 | Identification and Authentication Failures |
| A08:2021 | Software and Data Integrity Failures       |
| A09:2021 | Security Logging and Monitoring Failures   |
| A10:2021 | Server-Side Request Forgery (SSRF)         |

---

## 🔹 A01: Broken Access Control

**Access control** enforces policies like user roles and permissions. If broken, attackers can gain unauthorized access to admin functions, sensitive files, or other users' data.

### ❗ Example

```http
GET /api/users/12345/profile  ← Normal user
GET /api/users/12346/profile  ← Accessing another user's data (IDOR)
```

### 🔐 Prevention

* Enforce access control on the **server-side**
* Deny by default
* Use secure frameworks
* Log access control failures

---

## 🔹 A02: Cryptographic Failures

Formerly “Sensitive Data Exposure”, it focuses on **data protection failures** such as using weak or no encryption.

### ❗ Example

* Storing passwords in plaintext
* Transmitting data over HTTP instead of HTTPS
* Using broken cryptographic algorithms (e.g., MD5, SHA1)

### 🔐 Prevention

* Use strong algorithms (AES, bcrypt, SHA-256)
* Use HTTPS everywhere
* Do not store sensitive data unless necessary

---

## 🔹 A03: Injection

Occurs when **untrusted data is sent to an interpreter** (SQL, OS, LDAP, etc.) and executed as a command.

### ❗ Example (SQL Injection)

```sql
SELECT * FROM users WHERE username = '$user' AND password = '$pass'
```

Input:

```sql
' OR 1=1 --
```

### 🔐 Prevention

* Use **parameterized queries (prepared statements)**
* Validate and sanitize all inputs
* Use ORM frameworks (e.g., Hibernate)

---

## 🔹 A04: Insecure Design

Focuses on **flaws in application architecture and design**, not just implementation bugs.

### ❗ Example

* No rate limiting on login
* Allowing direct access to internal resources
* No threat modeling performed

### 🔐 Prevention

* Threat modeling early in SDLC
* Use secure design patterns
* Enforce business logic rules securely

---

## 🔹 A05: Security Misconfiguration

This is one of the **most common vulnerabilities**. It includes default settings, verbose error messages, open ports, unpatched software, etc.

### ❗ Example

* Exposed admin panel (`/admin`)
* Directory listing enabled
* Stack trace shown in error response

### 🔐 Prevention

* Harden servers and services
* Disable unnecessary features
* Regularly scan for misconfigurations (e.g., with Nessus)

---

## 🔹 A06: Vulnerable and Outdated Components

Using libraries or components with known vulnerabilities exposes the application.

### ❗ Example

* Using jQuery v1.8 with known XSS issues
* Outdated Apache server with RCE vulnerability

### 🔐 Prevention

* Use tools like `OWASP Dependency-Check`
* Monitor CVEs of dependencies
* Apply patches and updates regularly

---

## 🔹 A07: Identification and Authentication Failures

Weak or broken authentication allows attackers to compromise user or admin accounts.

### ❗ Example

* No account lockout after failed attempts
* Weak password policies
* Using session IDs in URLs

### 🔐 Prevention

* Implement MFA (Multi-Factor Authentication)
* Use secure password hashing (bcrypt, Argon2)
* Regenerate session ID after login

---

## 🔹 A08: Software and Data Integrity Failures

Trusting software updates, plugins, or data without verifying integrity can be dangerous.

### ❗ Example

* Auto-updating from untrusted source
* CI/CD pipeline not secured
* Malicious plugins or dependencies (e.g., event-stream backdoor)

### 🔐 Prevention

* Use signed updates (code signing)
* Secure CI/CD environments
* Verify the integrity of packages (checksums, hashes)

---

## 🔹 A09: Security Logging and Monitoring Failures

If applications do not **log and monitor** events, attacks can go unnoticed.

### ❗ Example

* No alerting on failed logins
* No logs for privilege escalation
* Attackers remain undetected after breach

### 🔐 Prevention

* Enable logging for authentication, access control, errors
* Monitor logs in real-time
* Use SIEM tools (Splunk, ELK, Graylog)

---

## 🔹 A10: Server-Side Request Forgery (SSRF)

Occurs when a server-side app fetches a URL specified by the user without validation. This can lead to **internal network scanning**, **metadata stealing**, or **remote code execution**.

### ❗ Example

```http
GET /fetch?url=http://169.254.169.254/latest/meta-data/
```

✔️ AWS metadata service can return sensitive info like IAM keys.

### 🔐 Prevention

* Whitelist allowed URLs
* Disable unnecessary URL fetch features
* Use SSRF protection libraries (e.g., OpenRewrite)

---

## 🧪 Tools to Test OWASP Top 10

| Tool                 | Purpose                                    |
| -------------------- | ------------------------------------------ |
| **Burp Suite**       | Manual/automated web vulnerability testing |
| **OWASP ZAP**        | Open-source web scanner                    |
| **Nikto**            | Web server scanner                         |
| **SQLMap**           | SQL injection                              |
| **Nmap**             | Network scanning                           |
| **Dependency-Check** | Finds vulnerable libraries                 |
| **Metasploit**       | Exploitation framework                     |
| **SonarQube**        | Code analysis and bug detection            |

---

## 🧭 Summary Table

| OWASP ID | Risk                   | Impact                     |
| -------- | ---------------------- | -------------------------- |
| A01      | Broken Access Control  | Unauthorized actions       |
| A02      | Cryptographic Failures | Data theft                 |
| A03      | Injection              | Data loss, full compromise |
| A04      | Insecure Design        | Systemic vulnerabilities   |
| A05      | Misconfiguration       | Exposure of services       |
| A06      | Outdated Components    | Known vulnerabilities      |
| A07      | Auth Failures          | Account compromise         |
| A08      | Integrity Failures     | Supply chain attacks       |
| A09      | Logging Failures       | Undetected attacks         |
| A10      | SSRF                   | Internal resource access   |

---

## 🧠 Pro Tips

* Combine OWASP Top 10 awareness with **threat modeling**, **secure coding**, and **regular pentesting**
* Use **DAST + SAST + IAST** for comprehensive testing
* Stay updated with latest CVEs and OWASP updates

---

## 📘 Additional Resources

* [OWASP Top 10 official site](https://owasp.org/www-project-top-ten/)
* [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
* [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
* [PortSwigger Web Security Academy](https://portswigger.net/web-security)

---

 