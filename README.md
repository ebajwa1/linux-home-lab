# Linux Security & Administration Home Lab (Ubuntu + Windows 11)

Hands-on portfolio project built to develop and showcase **Linux system administration and security monitoring skills**.  
This lab series demonstrates practical experience with **user and group management, filesystem permissions, SSH hardening, and authentication log analysis** in a VirtualBox environment.  
Each lab includes step-by-step actions, commands, screenshots, and documented security findings.

---

## 🖥️ Architecture
- **Host OS:** Windows 11  
- **Hypervisor:** VirtualBox  
- **Virtual Machines:**  
  - Ubuntu Server (user management, permissions, SSH, logging)  
- **Networking:**  
  - NAT (internet access)  
  - Host-Only (used where available; SSH testing when functional)

---

## 🔬 Labs

### **Lab 1: Linux User Management, Sudo Configuration & SSH Hardening**
**Goal:** Create and manage Linux users and groups, configure role-based sudo access, enforce password complexity, and harden SSH access on Ubuntu.

- Created users and role-based groups (`opsadmin`, `devteam`, `analytics`)
- Assigned group memberships and validated access
- Enforced password complexity using `libpam-pwquality`
- Configured sudo access securely with `visudo`
- Hardened SSH by disabling root login and reviewing SSH settings
- Tested SSH access from Windows host (network limitation documented)

📂 Folder: `/lab1-linux-user-management`

---

### **Lab 2: Linux Filesystem Navigation & Permissions**
**Goal:** Explore Linux filesystem layout and configure shared project directories with secure permissions and collaborative access.

- Reviewed Linux filesystem hierarchy and disk usage
- Created shared project directories under `/srv/projects`
- Configured group ownership and permissions using `chgrp` and `chmod`
- Implemented setgid to enforce inherited group permissions
- Tested file creation behavior across users
- Audited permissions using `stat`, `umask`, and `find`

📂 Folder: `/lab2-linux-filesystem-permissions`

---

### **Lab 3: Linux SSH Log Analysis (Failed & Successful Login Monitoring)**
**Goal:** Analyze SSH authentication logs by generating failed and successful login attempts and reviewing system logs.

- Generated failed SSH logins using invalid users
- Performed successful SSH login as a valid user
- Analyzed authentication events using `journalctl`
- Reviewed persistent logs in `/var/log/auth.log`
- Verified SSH logging verbosity (`LogLevel VERBOSE`)
- Identified log patterns associated with brute-force and unauthorized access attempts

📂 Folder: `/lab3-linux-ssh-log-analysis`

---

## 📂 How to Use This Repository
Each lab folder contains:
- Clear lab objectives and architecture
- Step-by-step procedures
- Terminal commands and configuration changes
- Screenshots with descriptive filenames
- Key findings and security observations

---

## 🎯 Skills Demonstrated
- Linux user and group administration
- Role-based access control with sudo
- Password policy enforcement
- Filesystem permissions and setgid behavior
- SSH hardening and authentication analysis
- Linux log analysis for security monitoring
- Clear technical documentation

---

## 📌 Notes
This lab environment reflects real-world conditions, including documented networking limitations, emphasizing troubleshooting, validation, and accurate security analysis over idealized configurations.
