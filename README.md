# Linux Server Health Check Script

A Bash script that gives a quick snapshot of a Linux server's health — useful for daily checks, on-call triage, and learning system monitoring fundamentals.

> Environment: RHEL 9.6 on VMware Workstation

---

## What It Checks

| Check | Command Used | Why It Matters |
|---|---|---|
| Hostname & OS | `hostname`, `uname -r` | Confirms which server you're on |
| System uptime | `uptime` | Shows load average and time since last reboot |
| Memory usage | `free -h` | Identifies memory pressure |
| Disk usage | `df -h` | Catches filesystems nearing capacity |
| Top CPU processes | `ps aux --sort=-%cpu` | Finds runaway processes |
| Top memory processes | `ps aux --sort=-%mem` | Catches memory hogs |

---

## How to Run

**1. Clone the repo**
```bash
git clone https://github.com/gouthamkalal12/linux-health-check-script.git
cd linux-health-check-script
```

**2. Make it executable**
```bash
chmod +x health-check.sh
```

**3. Run it**
```bash
./health-check.sh
```

---

## Sample Output

Tested on RHEL 9.6 running inside VMware Workstation:

```
========================================
   LINUX SERVER HEALTH CHECK REPORT
========================================
Date       : Mon 22 Jun 2026 10:42:13 IST
Hostname   : rhel9-lab.localdomain

--- UPTIME ---
 10:42:13 up 1 day,  4:23,  1 user,  load average: 0.02, 0.01, 0.00

--- MEMORY USAGE ---
              total        used        free      shared  buff/cache   available
Mem:           1.8G        721M        614M        9.2M        497M        1.1G
Swap:          2.0G          0B        2.0G

--- DISK USAGE ---
Filesystem                  Size  Used Avail Use% Mounted on
devtmpfs                    4.0M     0  4.0M   0% /dev
tmpfs                       896M     0  896M   0% /dev/shm
tmpfs                       359M  9.3M  349M   3% /run
/dev/mapper/rhel-root        17G  4.8G   13G  28% /
/dev/mapper/rhel-home       8.9G  134M  8.8G   2% /home
/dev/sda1                   960M  261M  700M  28% /boot
tmpfs                       179M  4.0K  179M   1% /run/user/1000

--- TOP 5 CPU PROCESSES ---
USER       PID  %CPU %MEM   COMMAND
root       892   1.2  2.1   /usr/bin/vmtoolsd
root         1   0.1  0.5   /usr/lib/systemd/systemd
root       674   0.1  1.2   /usr/sbin/NetworkManager
dbus       531   0.0  0.3   /usr/bin/dbus-daemon
root       412   0.0  0.2   /usr/lib/systemd/systemd-journald

--- TOP 5 MEMORY PROCESSES ---
USER       PID  %CPU %MEM   COMMAND
root       892   1.2  2.1   /usr/bin/vmtoolsd
root       674   0.1  1.2   /usr/sbin/NetworkManager
root         1   0.1  0.5   /usr/lib/systemd/systemd
dbus       531   0.0  0.3   /usr/bin/dbus-daemon
root       723   0.0  0.3   /usr/sbin/rsyslogd

========================================
     END OF HEALTH CHECK REPORT
========================================
```

---

## Skills Demonstrated

- Bash scripting (variables, functions, formatting)
- Linux system monitoring commands
- Process management (`ps`, `top`)
- Disk and memory analysis (`df`, `free`)
- Script permissions and execution
- RHEL 9.6 LVM disk layout understanding

---

## Planned Improvements

- [ ] Add alert thresholds (e.g. warn if disk > 80%)
- [ ] Email report output via `mail` command
- [ ] Add failed systemd services check (`systemctl --failed`)
- [ ] Schedule via cron for automated daily reports
- [ ] Add network interface status check (`ip addr`)
- [ ] Add Red Hat subscription status check

---

## Author

**Shiva Chandra Goutham Kalal**  
Linux Administrator Aspirant | Pune, India  
[GitHub](https://github.com/gouthamkalal12)

---

*Built as part of RHCSA preparation and Linux portfolio development.*  
*Environment: RHEL 9.6 | VMware Workstation | Bash*
