# Lab 2: Linux Filesystem Navigation & Permissions

Goal: Explore Linux filesystem layout, create a shared project directory under `/srv`, and configure permissions, ownership, and setgid behavior to support secure collaboration between users.

## Architecture
- Hypervisor: VirtualBox (Adapter 1: NAT, Adapter 2: Host-Only)
- Windows 11 Host
- Ubuntu Server VM (Host-Only IP: 192.168.56.x)
- Existing Users:
  - alice (opsadmin)
  - bob (devteam)
  - carol (analytics)

## Steps I Performed
1. Reviewed filesystem layout and disk usage.  
   - Commands: `ls /`, `ls /home`, `ls /var`, `ls /srv`, `df -h`  
   - Screenshot: [fs-layout](./screenshots/fs-layout.png)

2. Created a project directory structure under `/srv`.  
   - Commands:  
     - `sudo mkdir -p /srv/projects/app1`  
     - `sudo mkdir -p /srv/projects/app2`  
     - `sudo ls -R /srv/projects`  
   - Screenshot: [srv-projects](./screenshots/srv-projects.png)

3. Inspected initial permissions and ownership.  
   - Command: `ls -ld /srv /srv/projects /srv/projects/app1 /srv/projects/app2`  
   - Screenshot: [srv-permissions-before](./screenshots/srv-permissions-before.png)

4. Configured group ownership and setgid for shared access.  
   - Commands:  
     - `sudo chgrp -R opsadmin /srv/projects`  
     - `sudo chmod 2775 /srv/projects /srv/projects/app1 /srv/projects/app2`  
     - `ls -ld /srv/projects /srv/projects/app1 /srv/projects/app2`  
   - Screenshot: [srv-permissions-after](./screenshots/srv-permissions-after.png)

5. Tested shared directory behavior as alice and bob.  
   - As alice:  
     - `su - alice`  
     - `cd /srv/projects/app1`  
     - `touch alice-notes.txt`  
     - `mkdir alice-logs`  
     - `ls -l`  
     - Screenshot: [alice-app1-contents](./screenshots/alice-app1-contents.png)

6. Examined and modified file permissions using `stat` and `chmod`.  
   - Commands:  
     - `stat alice-notes.txt`  
     - `ls -l alice-notes.txt`  
     - `chmod 660 alice-notes.txt`  
     - `ls -l alice-notes.txt`  
   - Screenshot: [stat-chmod-alice-notes](./screenshots/stat-chmod-alice-notes.png)

7. Checked default `umask` and its effect on new files.  
   - Commands:  
     - `umask`  
     - `touch umask-test.txt`  
     - `ls -l umask-test.txt`  
   - Screenshot: [umask-newfile](./screenshots/umask-newfile.png)

8. Audited `/srv/projects` using `find`.  
   - Commands:  
     - `sudo find /srv/projects -maxdepth 2 -type f -ls`  
     - `sudo find /srv/projects -maxdepth 2 -type d -ls`  
   - (Optional artifacts saved to `find-srv-projects.txt`)  
   - Screenshot: [find-srv-projects](./screenshots/find-srv-projects.png)

## Key Findings
- The `/srv` directory is a standard location for application or project data.
- Assigning group ownership with `chgrp` and using `chmod 2775` enables effective team collaboration through inherited group permissions.
- The setgid bit (`s`) ensures new files and directories automatically inherit the correct group.
- Default `umask` values directly influence the baseline permissions of new files.
- `stat`, `chmod`, and `find` are essential tools for auditing and managing permissions across Linux systems.

## Screenshots & Commands
- Filesystem Layout: [Screenshot](./screenshots/fs-layout.png)  
- Project Directory Tree: [Screenshot](./screenshots/srv-projects.png)  
- Permissions Before: [Screenshot](./screenshots/srv-permissions-before.png)  
- Permissions After: [Screenshot](./screenshots/srv-permissions-after.png)  
- alice in app1: [Screenshot](./screenshots/alice-app1-contents.png)  
- stat + chmod: [Screenshot](./screenshots/stat-chmod-alice-notes.png)  
- umask new file: [Screenshot](./screenshots/umask-newfile.png)  
- find audit: [Screenshot](./screenshots/find-srv-projects.png)
