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
