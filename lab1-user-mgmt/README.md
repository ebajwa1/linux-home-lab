Lab 1: Linux User Management, Sudo Configuration & SSH Hardening

Goal: Create users, groups, enforce password policies, configure sudo using best practices, and harden SSH access on Ubuntu to simulate junior Linux administrator responsibilities.

Architecture

Hypervisor: VirtualBox (Adapter 1: NAT, Adapter 2: Host-Only)

Ubuntu Server: Host-Only IP: 192.168.56.x

Windows 11 Host: Used for external connectivity testing

Users Created: alice (opsadmin), bob (devteam), carol (analytics)

Steps I Performed

Verified Ubuntu system info and networking:

Ran: lsb_release -a, hostnamectl, ip a

Confirmed correct hostname, OS version, NAT + Host-Only interfaces.

Created role-based groups:

opsadmin, devteam, analytics

Verified with: getent group opsadmin devteam analytics

Created users and assigned group memberships:

Added: alice, bob, carol

Assigned using: usermod -aG <group> <user>

Verified with: id alice, id bob, id carol

Enabled password complexity rules:

Installed: libpam-pwquality

Updated /etc/security/pwquality.conf for minimum length + mixed characters

Configured sudo privileges using visudo:

Backed up /etc/sudoers

Added:

%opsadmin   ALL=(ALL:ALL) ALL


Tested admin access: su - alice → sudo id

Hardened SSH configuration:

Edited /etc/ssh/sshd_config:

PermitRootLogin no
PasswordAuthentication yes
PubkeyAuthentication yes


Restarted SSH: sudo systemctl restart ssh

SSH login test attempt:

Ubuntu SSH service active and listening

Windows → Ubuntu SSH not reachable due to VirtualBox Host-Only network issue

Ubuntu-side SSH hardening was successfully validated

Key Findings

Role-based groups (opsadmin, devteam, analytics) simplify user permission management and reflect real enterprise RBAC structure.

Using %opsadmin ALL=(ALL:ALL) ALL provides secure, auditable admin access instead of enabling root login.

Password rules via libpam-pwquality enforce strong credential hygiene required on production Linux servers.

SSH hardening (PermitRootLogin no) significantly reduces remote attack surface and forces least-privilege logins.

SSH service was confirmed installed and running; networking prevented external connections, but configuration was correct.

Screenshots

System Info & Network — system-info.png

Groups Created — groups-created.png

User/Group Membership — users-and-groups.png

Password Policy Config — pwquality-config.png

Sudoers Configuration — sudoers-config.png

Sudo Test (alice) — sudo-test-alice.png

SSH Hardening — sshd-config.png
