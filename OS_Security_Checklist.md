
## **2. OS_Security_Checklist.md**
```markdown
# 🔒 Operating System Security Checklist
## Comprehensive Hardening Checklist for Linux & Windows

---

## 📋 Linux Security Checklist

### 🔐 User Account Security
- [ ] **Password Policies**
  - [ ] Minimum password length: 12 characters
  - [ ] Password complexity requirements enabled
  - [ ] Password expiration: 90 days
  - [ ] Password history: 5 previous passwords
- [ ] **User Management**
  - [ ] Default users renamed (root → adminuser)
  - [ ] Guest account disabled
  - [ ] Unused accounts removed or disabled
  - [ ] Root login via SSH disabled
  - [ ] Sudo access restricted to specific users

### 🛡️ File System Security
- [ ] **Permissions**
  - [ ] /etc/passwd: 644 (rw-r--r--)
  - [ ] /etc/shadow: 600 (rw-------)
  - [ ] /etc/group: 644 (rw-r--r--)
  - [ ] Home directories: 750 (rwxr-x---)
  - [ ] World-writable files identified and secured
- [ ] **Mount Options**
  - [ ] /tmp mounted with noexec,nosuid
  - [ ] /home mounted with nosuid
  - [ ] /var/log mounted with noexec,nosuid

### 🔥 Firewall Configuration (UFW)
- [ ] **Basic Setup**
  - [ ] UFW enabled
  - [ ] Default policy: deny incoming, allow outgoing
  - [ ] Logging enabled
- [ ] **Port Management**
  - [ ] SSH: Port 22 (or custom port)
  - [ ] HTTP: Port 80
  - [ ] HTTPS: Port 443
  - [ ] Unnecessary ports closed
  - [ ] ICMP echo requests limited

### ⚙️ Service Management
- [ ] **Unnecessary Services Disabled**
  - [ ] Telnet
  - [ ] FTP
  - [ ] RPC
  - [ ] NIS
  - [ ] Bluetooth (if not needed)
  - [ ] CUPS (if no printer)
- [ ] **Essential Services Secured**
  - [ ] SSH: Key authentication only
  - [ ] SSH: Root login disabled
  - [ ] SSH: Protocol 2 only
  - [ ] SSH: Idle timeout set

### 📊 System Hardening
- [ ] **Kernel Parameters**
  - [ ] IP spoofing protection enabled
  - [ ] SYN flood protection enabled
  - [ ] ICMP redirects disabled
  - [ ] Source routing disabled
- [ ] **Logging & Monitoring**
  - [ ] Auditd installed and configured
  - [ ] Log rotation configured
  - [ ] Failed login attempts logged
  - [ ] Sudo commands logged

### 🔄 Update Management
- [ ] **Automatic Updates**
  - [ ] Unattended-upgrades installed
  - [ ] Security updates automated
  - [ ] Update notifications enabled
  - [ ] Regular update schedule

### 🔐 Additional Security
- [ ] **SELinux/AppArmor**
  - [ ] SELinux/AppArmor enabled
  - [ ] Running in enforcing mode
  - [ ] Policies configured for critical services
- [ ] **Network Security**
  - [ ] TCP Wrappers configured
  - [ ] Hosts.allow/hosts.deny configured
  - [ ] NTP synchronization enabled

---

## 🪟 Windows Security Checklist

### 🔐 Account Security
- [ ] **User Accounts**
  - [ ] Administrator account renamed
  - [ ] Guest account disabled
  - [ ] Built-in administrator account disabled
  - [ ] Minimum password length: 14 characters
  - [ ] Account lockout threshold: 5 attempts
  - [ ] Account lockout duration: 30 minutes
- [ ] **User Account Control (UAC)**
  - [ ] UAC enabled
  - [ ] UAC level: Default or higher
  - [ ] Admin approval mode enabled

### 🛡️ Windows Defender & Firewall
- [ ] **Windows Defender**
  - [ ] Real-time protection enabled
  - [ ] Cloud-delivered protection enabled
  - [ ] Automatic sample submission enabled
  - [ ] Periodic scanning enabled
- [ ] **Windows Firewall**
  - [ ] Firewall enabled for all profiles
  - [ ] Inbound connections blocked by default
  - [ ] Outbound connections allowed by default
  - [ ] Notification settings configured

### ⚙️ Service Management
- [ ] **Services Disabled**
  - [ ] Telnet Client/Server
  - [ ] Remote Registry
  - [ ] Fax Service
  - [ ] Bluetooth Support Service
  - [ ] Windows Remote Management (if not needed)
  - [ ] Print Spooler (if no printer)
- [ ] **Remote Access**
  - [ ] Remote Desktop disabled (if not needed)
  - [ ] RDP secured with Network Level Authentication
  - [ ] RDP port changed from 3389

### 📊 System Configuration
- [ ] **Network Settings**
  - [ ] SMBv1 disabled
  - [ ] LLMNR disabled
  - [ ] NetBIOS over TCP/IP disabled
  - [ ] Windows Script Host restricted
- [ ] **Browser Security**
  - [ ] SmartScreen enabled
  - [ ] Pop-up blocker enabled
  - [ ] Enhanced Protected Mode enabled

### 🔄 Update Management
- [ ] **Windows Update**
  - [ ] Automatic updates enabled
  - [ ] Critical updates installed automatically
  - [ ] Update notifications configured
  - [ ] Restart required notifications enabled

### 🔐 Encryption & Data Protection
- [ ] **BitLocker**
  - [ ] BitLocker enabled (if available)
  - [ ] TPM protection enabled
  - [ ] Recovery key backed up
- [ ] **Data Execution Prevention (DEP)**
  - [ ] DEP enabled for all programs
  - [ ] Hardware-enforced DEP enabled

### 📈 Auditing & Logging
- [ ] **Event Logs**
  - [ ] Security event log size: 128MB minimum
  - [ ] Audit account logon events enabled
  - [ ] Audit account management enabled
  - [ ] Audit object access enabled
  - [ ] Failed login attempts logged

---

## 🎯 Quick Hardening Commands (Linux)

### Basic Security Setup
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Enable firewall
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Secure SSH
sudo sed -i 's/#PermitRootLogin yes/PermitRootLogin no/g' /etc/ssh/sshd_config
sudo sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config
sudo systemctl restart sshd

# Disable unnecessary services
sudo systemctl disable telnet
sudo systemctl disable rpcbind
sudo systemctl disable bluetooth

# Set password policies
sudo apt install libpam-pwquality
sudo nano /etc/pam.d/common-password
# Add: minlen=12 difok=3 ucredit=-1 lcredit=-1 dcredit=-1 ocredit=-1
