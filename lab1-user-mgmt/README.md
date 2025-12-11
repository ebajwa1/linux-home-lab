# Lab 1: Linux User Management, Sudo Configuration & SSH Hardening

Goal: Create and manage Linux users and groups, configure role-based sudo access, enable password complexity, and harden SSH access on Ubuntu in a controlled VirtualBox lab.

## Architecture

Hypervisor: VirtualBox (Adapter 1: NAT, Adapter 2: Host-Only)

Windows 11 Host (used for SSH testing attempts)

Ubuntu Server (Host-Only IP: 192.168.56.x)

## Steps I Performed

Verified Ubuntu system information and network adapters:

Commands used: lsb_release -a, hostnamectl, ip a

Screenshot: system-info.png

Created three role-based groups for RBAC modeling:

opsadmin, devteam, analytics

Verified with getent group

Screenshot: groups-created.png

Created users and assigned them to appropriate groups:

Users: alice, bob, carol

Used: adduser, usermod -aG <group> <user>

Verified with id <user>

Screenshot: users-and-groups.png

Enabled password complexity using PAM module:

Installed: libpam-pwquality

Updated /etc/security/pwquality.conf for stronger password rules

Screenshot: pwquality-config.png

Configured sudo privileges with visudo:

Added rule for operations administrators:

%opsadmin   ALL=(ALL:ALL) ALL


Tested sudo access as alice using sudo id

Screenshots: sudoers-config.png, sudo-test-alice.png

Hardened SSH configuration by editing /etc/ssh/sshd_config:

Updated settings:

PermitRootLogin no
PasswordAuthentication yes
PubkeyAuthentication yes


Restarted SSH and confirmed service status

Screenshot: sshd-config.png

Attempted SSH login from Windows → Ubuntu:

SSH daemon active and listening

VirtualBox Host-Only connectivity issue prevented successful remote SSH

Ubuntu-side hardening validated and correct

## Key Findings

RBAC via Linux groups (opsadmin, devteam, analytics) simplifies permission management and mirrors real enterprise structures.

Sudo delegation using %opsadmin ALL=(ALL:ALL) ALL provides secure, traceable admin access without enabling root login.

libpam-pwquality enforces strong password policies aligned with security best practices.

Disabling PermitRootLogin significantly reduces attack surface and prevents brute-force attacks on root.

SSH configuration and service validation succeeded; networking limitation was isolated to VirtualBox Host-Only adapter.

## Screenshots & Commands

System Info: ./screenshots/system-info.png

Groups Created: groups-created.png

User & Group Membership: users-and-groups.png

Password Policy Config: pwquality-config.png

Sudoers Configuration: sudoers-config.png

Sudo Test (alice): sudo-test-alice.png

SSH Hardening: sshd-config.png
