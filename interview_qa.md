
## **3. interview_qa.md**
```markdown
# 💼 Interview Questions & Answers
## Operating System Security Fundamentals

---

## 🔐 Basic Concepts

### Q1: What is OS hardening?
**Answer:**  
OS hardening is the process of securing an operating system by reducing its attack surface. This involves:
- Disabling unnecessary services and features
- Removing default accounts and passwords
- Configuring security settings
- Applying patches and updates
- Implementing security policies
- Enabling logging and monitoring

**Example:** On a Linux server, hardening might include disabling SSH root login, enabling firewall, and configuring AppArmor.

---

### Q2: What is the principle of least privilege?
**Answer:**  
The principle of least privilege states that users and programs should only have the minimum access necessary to perform their tasks.

**Why it matters:**
- Reduces attack surface
- Limits damage from compromised accounts
- Makes privilege escalation harder
- Simplifies auditing and monitoring

**Real-world example:** A web server account should only have access to web files, not system configuration files.

---

### Q3: What is defense in depth?
**Answer:**  
Defense in depth is a security strategy that uses multiple layers of security controls. If one layer fails, others provide protection.

**Layers include:**
1. Physical security
2. Network security (firewalls)
3. Host security (OS hardening)
4. Application security
5. Data security (encryption)

---

## 🐧 Linux Security Questions

### Q4: Explain Linux file permissions (777, 755, 644)
**Answer:**  
Linux permissions use three-digit octal notation:
- **First digit**: Owner permissions
- **Second digit**: Group permissions  
- **Third digit**: Others permissions

**Permission values:**
- **4** = Read (r)
- **2** = Write (w)  
- **1** = Execute (x)

**Common permissions:**
- **777**: rwxrwxrwx (Read, Write, Execute for everyone) - **INSECURE!**
- **755**: rwxr-xr-x (Owner: rwx, Group/Others: r-x)
- **644**: rw-r--r-- (Owner: rw-, Group/Others: r--)
- **600**: rw------- (Only owner can read/write)

**Example commands:**
```bash
chmod 755 script.sh    # Makes script executable by all
chmod 600 secret.txt   # Only owner can read/write
chmod 644 web.html     # Web files typically
