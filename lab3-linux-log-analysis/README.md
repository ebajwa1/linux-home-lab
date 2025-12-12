# Lab 3: Linux SSH Log Analysis (Failed & Successful Login Monitoring)

Goal: Analyze SSH authentication logs on Ubuntu by generating failed and successful login attempts, then reviewing entries using `journalctl` and `/var/log/auth.log`.

## Architecture
- Hypervisor: VirtualBox (NAT mode used; Host-Only unavailable due to adapter issue)
- Ubuntu Server VM (localhost used for SSH testing)
- Users Tested: alice (valid user), wronguser (invalid user)

## Steps I Performed
1. Attempted SSH login using an invalid user (`wronguser`) to generate failed authentication logs.  
   - Screenshot: [failed-ssh-attempts](./screenshots/failed-ssh-attempts.png)

2. Logged in successfully as a valid user (`alice`) using SSH to localhost.  
   - Screenshot: [successful-ssh-login](./screenshots/successful-ssh-login.png)

3. Viewed failed SSH events using `journalctl` with filtering.  
   - Screenshot: [journalctl-failed](./screenshots/journalctl-failed.png)

4. Checked `/var/log/auth.log` to view both failed and successful entries.  
   - Screenshot (failed): [authlog-failed](./screenshots/authlog-failed.png)  
   - Screenshot (successful): [authlog-successful](./screenshots/authlog-successful.png)

5. Verified SSH logging configuration (`LogLevel VERBOSE`).  
   - Screenshot: [ssh-loglevel](./screenshots/ssh-loglevel.png)

## Key Findings
- Failed SSH attempts create log entries such as:  
  `Failed password for invalid user wronguser from 127.0.0.1`
- Successful SSH attempts create:  
  `Accepted password for alice from 127.0.0.1`
- Authentication logs help identify:
  - brute-force attempts  
  - password-spraying activity  
  - unauthorized access behavior  
  - normal user login patterns
- Using `journalctl` provides real-time, time-filtered insight into SSH activity.
- `/var/log/auth.log` stores persistent records for deeper analysis and SOC investigations.

## Screenshots & Commands
- Failed SSH Attempt: [Screenshot](./screenshots/failed-ssh-attempts.png)  
  Command: `ssh wronguser@localhost`

- Successful SSH Login: [Screenshot](./screenshots/successful-ssh-login.png)  
  Command: `ssh alice@localhost`

- Journalctl Failed Entries: [Screenshot](./screenshots/journalctl-failed.png)  
  Command:  
  `sudo journalctl -u ssh -S today | grep -i "failed"`

- Auth Log (Failed): [Screenshot](./screenshots/authlog-failed.png)  
  Command:  
  `sudo grep "Failed password" /var/log/auth.log`

- Auth Log (Successful): [Screenshot](./screenshots/authlog-successful.png)  
  Command:  
  `sudo grep "Accepted password" /var/log/auth.log`

- SSH Logging Config: [Screenshot](./screenshots/ssh-loglevel.png)
