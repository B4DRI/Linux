# 💪 Linux Networking Study Case: Automated File Sync & Web Service Health Monitor

**Author**: Badri Mahazir  
**Environment**: WSL Linux (Client) ↔ Oracle VirtualBox Linux (Server)  
**Skills Covered**: `ifconfig`, `ping`, `ssh`, `scp`, `curl`, and shell scripting.

---

## 📘 Overview

This case study simulates a real-world scenario for a junior DevOps engineer. You will monitor a web server's health and automatically retrieve its log files at scheduled intervals for backup and analysis — all within your own controlled environment.

---

## 🤩 Scenario

> Your web server is running on a **VirtualBox Linux** guest machine. From your **WSL Linux** host machine, you are responsible for:
> 
> 1. Checking network connectivity.
> 2. Verifying server health using `curl`.
> 3. Retrieving log files using `scp`.
> 4. Automating the entire process using shell scripts and `cron`.

---

## 🔧 Prerequisites

- Ensure WSL and VirtualBox are on the same network (bridged or host-only).
- SSH is enabled and running on the VirtualBox guest.
- Your WSL machine has network access to the VM.

---

## 📂 Step-by-Step Guide

### 🔹 1. Check IP Address and Network Connectivity

**On WSL:**
```bash
ifconfig    # or `ip a`
ping <VM_IP>  # Replace with your VM's IP address
```

---

### 🔹 2. SSH into the VirtualBox Server

```bash
ssh youruser@<VM_IP>
```

Copy your SSH public key to avoid repeated password prompts:
```bash
ssh-copy-id youruser@<VM_IP>
```

---

### 🔹 3. Health Check Using `curl`

Create a health check script on WSL:

```bash
nano ~/healthcheck.sh
```

**Script Content:**
```bash
#!/bin/bash

URL="http://<VM_IP>"
STATUS=$(curl -s -o /dev/null -w "%{http_code}" $URL)

if [ "$STATUS" == "200" ]; then
    echo "$(date): Web server is UP" >> ~/server_health.log
else
    echo "$(date): Web server is DOWN or ERROR $STATUS" >> ~/server_health.log
fi
```

Make it executable:
```bash
chmod +x ~/healthcheck.sh
```

---

### 🔹 4. Simulate a Web Log File on VirtualBox

**On VM:**
```bash
echo "User accessed homepage at $(date)" >> ~/web.log
```

---

### 🔹 5. Secure File Transfer with `scp`

On WSL:
```bash
mkdir -p ~/vm_logs

nano ~/sync_logs.sh
```

**Script Content:**
```bash
#!/bin/bash

scp youruser@<VM_IP>:/home/youruser/web.log ~/vm_logs/web-$(date +%Y%m%d%H%M%S).log
```

Make it executable:
```bash
chmod +x ~/sync_logs.sh
```

---

### 🔹 6. Automate with `cron` (Optional)

Edit your crontab:
```bash
crontab -e
```

Add:
```bash
*/5 * * * * /home/badri/healthcheck.sh
*/10 * * * * /home/badri/sync_logs.sh
```

---

## ✅ Outcome

You now have:

- 💡 Health monitoring of your web server with logs.
- 🔐 Secure, timestamped backups of server logs.
- 🔁 Fully automated system via cron jobs.

---

## 📌 Notes

- Use `journalctl` or `systemctl status ssh` on the server if SSH isn't responding.
- Test scripts manually before scheduling them via `cron`.
