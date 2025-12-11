# Lab 1: Linux User Management, Sudo Configuration & SSH Hardening

Goal: Create and manage Linux users and groups, configure role-based sudo access, enforce password complexity, and harden SSH access on Ubuntu in a VirtualBox environment.

## Architecture
- Hypervisor: VirtualBox (Adapter 1: NAT, Adapter 2: Host-Only)
- Windows 11 Host (used for SSH testing attempts)
- Ubuntu Server VM (Host-Only IP: 192.168.56.x)
- Users Created: alice (opsadmin), bob (devteam), carol (analytics)

## Steps I Performed
1. Verified Ubuntu system information and network interfaces.  
   - Screenshot: [system-info](./screenshots/system-info.png)

2. Created role-based groups (opsadmin, devteam, analytics).  
   - Screenshot: [groups-created](./screenshots/groups-created.png)

3. Created users and assigned group memberships.  
   - Screenshot: [users-and-groups](./screenshots/users-and-groups.png)

4. Enabled password complexity using `libpam-pwquality`.  
   - Screenshot: [pwquality-config](./screenshots/pwquality-config.png)

5. Configured sudo privileges using visudo.  
   - Screenshot (sudoers file): [sudoers-config](./screenshots/sudoers-config.png)  
   - Screenshot (alice sudo test): [sudo-test-alice](./screenshots/sudo-test-alice.png)

6. Hardened SSH configuration by editing `sshd_config`.  
   - Screenshot: [sshd-config](./screenshots/sshd-config.png)

7. Attempted SSH from Windows to Ubuntu.  
   - SSH service active; connection blocked due to VirtualBox Host-Only network issue.

## Key Findings
- Role-based groups simplify user and permission management.  
- Sudo delegation using `%opsadmin ALL=(ALL:ALL) ALL` provides secure administrative access.  
- Password complexity enforcement strengthens credential security.  
- SSH hardening reduces attack surface by disabling remote root login.  
- SSH configuration was correct; network issue was due to VirtualBox and not Linux.

## Screenshots & Commands
- System Info: [Screenshot](./screenshots/system-info.png)  
- Groups Created: [Screenshot](./screenshots/groups-created.png)  
- Users & Groups: [Screenshot](./screenshots/users-and-groups.png)  
- Password Policy Config: [Screenshot](./screenshots/pwquality-config.png)  
- Sudoers File: [Screenshot](./screenshots/sudoers-config.png)  
- Sudo Test (alice): [Screenshot](./screenshots/sudo-test-alice.png)  
- SSH Hardening: [Screenshot](./screenshots/sshd-config.png)
