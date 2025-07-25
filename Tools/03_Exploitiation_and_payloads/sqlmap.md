
---

# 💉 SQL Injection Tools — In Detail  

---

## 📖 What is SQL Injection (SQLi)?

**SQL Injection** is a code injection technique that exploits vulnerabilities in an application’s database layer. Attackers insert or "inject" malicious SQL code into input fields (like forms, URLs, or cookies) to:
- Bypass authentication  
- Retrieve sensitive data  
- Modify or delete database content  
- Execute administrative operations  

**Example:**  
```sql
' OR '1'='1
```
If not handled properly, this can alter a database query's logic.

---

## 🛠️ Popular SQL Injection Tools  

Let’s detail the top tools used for detecting, testing, and exploiting SQL injection vulnerabilities:

---

### 1️⃣ **sqlmap** 🥇  

**Overview:**  
- The most popular open-source, fully automated SQL injection and database takeover tool.
- Written in Python.
- Can detect and exploit different types of SQLi vulnerabilities.

**Features:**  
✅ Supports multiple injection techniques:  
– Boolean-based  
– Error-based  
– Union query-based  
– Time-based blind  
– Stacked queries  

✅ Extracts databases, tables, columns, and data  
✅ Supports database fingerprinting  
✅ Supports password hash cracking  
✅ Bypasses Web Application Firewalls (WAFs)

**Installation:**
```bash
sudo apt update
sudo apt install sqlmap
```

**Basic Usage:**
```bash
sqlmap -u "http://target.com/page.php?id=1" --batch
```

**Extract Database Names:**
```bash
sqlmap -u "http://target.com/page.php?id=1" --dbs
```

**Extract Table Names:**
```bash
sqlmap -u "http://target.com/page.php?id=1" -D database_name --tables
```

**Extract Data:**
```bash
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T table_name --dump
```

---

### 2️⃣ **Havij**

**Overview:**  
- A famous, easy-to-use automated SQL Injection tool with a graphical user interface (GUI).
- Was widely used, though now mostly outdated and Windows-only.

**Features:**  
✅ Easy-to-use point-and-click interface  
✅ Can extract DB data, users, and passwords  
✅ Detects DBMS (MySQL, MSSQL, Oracle, etc.)  
✅ Password hash decoding

**Limitations:**  
- Mostly outdated, detectable by modern WAFs  
- Not included in Kali by default

---

### 3️⃣ **SQLNinja**

**Overview:**  
- An open-source tool specifically designed to exploit SQL Injection on Microsoft SQL Server.

**Features:**  
✅ Database fingerprinting  
✅ Extract database schema  
✅ Upload and execute shell payloads  
✅ Reverse TCP shell to attacker's machine

**Installation:**
```bash
sudo apt-get install sqlninja
```

**Usage Example:**
```bash
sqlninja -u "http://target.com/page.asp?id=1"
```

**Limitation:**  
- Limited to **Microsoft SQL Server**

---

### 4️⃣ **NoSQLMap**

**Overview:**  
- A Python tool for automating attacks on NoSQL databases (like MongoDB).
- Detects and exploits NoSQL Injection vulnerabilities.

**Features:**  
✅ Detects NoSQL Injection points  
✅ Exploits unauthorized access to databases  
✅ Can retrieve documents, collections, etc.

**Installation:**
```bash
git clone https://github.com/codingo/NoSQLMap.git
cd NoSQLMap
python3 nosqlmap.py
```

**Use case:**  
Modern web apps using NoSQL backends like **MongoDB**

---

### 5️⃣ **BBQSQL (Blind SQLi Exploitation Tool)**

**Overview:**  
- A Blind SQL Injection tool written in Python.
- Useful when no visible data is returned, only delays or page content changes.

**Features:**  
✅ Timing-based Blind SQLi exploitation  
✅ Interactive command-line interface  
✅ Supports custom payloads

**Installation:**
```bash
git clone https://github.com/Neohapsis/bbqsql.git
cd bbqsql
python3 bbqsql.py
```

**Use case:**  
For applications where only blind SQLi is possible.

---

### 6️⃣ **jSQL Injection**

**Overview:**  
- A Java-based GUI tool that automates SQL injection attacks.

**Features:**  
✅ Cross-platform (Java)  
✅ Supports error-based, blind, and time-based attacks  
✅ Data extraction, file reading, and command execution  
✅ Can run SQL shell on the server

**Installation:**
Download:
👉 [https://github.com/ron190/jsql-injection](https://github.com/ron190/jsql-injection)

Run:
```bash
java -jar jsql-injection-vX.X.X.jar
```

**Use case:**  
Beginners who prefer a GUI.

---

## 📊 Comparison Table  

| Tool           | Type         | DB Support         | Interface | Strength                              |
|:----------------|:--------------|:------------------|:--------------|:--------------------------------|
| **sqlmap**         | Automated CLI | MySQL, MSSQL, Oracle, PostgreSQL | CLI | Highly powerful, versatile |
| **Havij**           | Automated GUI | Multiple (outdated)             | GUI | User-friendly, outdated    |
| **SQLNinja**        | Automated CLI | **Microsoft SQL Server**        | CLI | Focused, powerful for MSSQL |
| **NoSQLMap**        | Automated CLI | **MongoDB, NoSQL**              | CLI | Targets NoSQL Databases |
| **BBQSQL**          | Blind SQLi CLI| MySQL, PostgreSQL               | CLI | Excellent for blind attacks |
| **jSQL Injection**  | Automated GUI | Multiple                       | GUI | Simple cross-platform GUI |

---

## ✅ How to Stay Safe  

As powerful as these tools are for testing, misuse is illegal and unethical. Only use them on:
- Systems you own
- Environments you have permission to test

👉 For professional penetration testing, always **get written authorization**.

---

## 📘 Final Thoughts  

- **sqlmap** is the king of SQL injection tools — feature-rich, powerful, actively maintained.
- **BBQSQL** and **SQLNinja** are great for blind and MSSQL-specific cases.
- **NoSQLMap** is vital for modern NoSQL systems.
- GUI options like **jSQL** and **Havij** are beginner-friendly but limited in professional scope.

---
