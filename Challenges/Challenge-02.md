🚀 Linux Challenge 2: Server Hardening and Basic Automation

Module: Linux Mastery
Difficulty: Intermediate
Estimated Time: 90–120 minutes
Focus: Server setup, security hardening, service management, permissions, and Bash scripting

---

🎯 Objective

Set up a secure Linux server from scratch and automate basic maintenance tasks.

This challenge emphasizes real-world DevOps Linux skills:

- Hardening
- Proper permissions
- Service configuration
- Automation

---

✅ Prerequisites

- A fresh Ubuntu 22.04 or 24.04 VM (GCP, AWS, Azure, or VirtualBox/Multipass)
- SSH access to the VM (browser console or "gcloud" is fine)
- Basic comfort with terminal commands

---

🧩 Tasks

---

🔐 Part 1: Initial Server Setup & Hardening

1. Update and Upgrade System
```bash
sudo apt update && sudo apt upgrade -y
```
---

2. Create a New User with Sudo Privileges

```bash
sudo adduser devopsuser
sudo usermod -aG sudo devopsuser
```

---

3. Disable Root Login & Password Authentication

Edit SSH config:

```bash
sudo nano /etc/ssh/sshd_config
```

Update the following lines:

```bash
PermitRootLogin no
PasswordAuthentication no
```

Restart SSH:

```bash
sudo systemctl restart ssh

```
---

4. Setup SSH Key-Based Authentication

Generate SSH key (locally if not already):

```bash
ssh-keygen -t ed25519
```

Copy key to server:

```bash
ssh-copy-id devopsuser@YOUR-VM-IP
```

---

5. Configure UFW Firewall

```bash
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw --force enable
sudo ufw status
```
---

6. Install Essential DevOps Tools

```bash
sudo apt install curl vim htop fail2ban -y
```

---

🌐 Part 2: Web Service Setup

1. Install and Start NGINX

sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx

---

2. Create Custom Web Page

sudo nano /var/www/html/index.html

Add:

<!DOCTYPE html>
<html>
<head><title>Linux Challenge 2</title></head>
<body>
  <h1>Linux Challenge 2 Completed</h1>
  <p>Deployed by Mohammed Adil Rehan</p>
  <p>Server hardened and automated successfully!</p>
</body>
</html>

---

3. Set Permissions

sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

Reload NGINX:

sudo systemctl reload nginx

---

4. Verify Deployment

Open in browser:

http://YOUR-VM-IP

---

⚙️ Part 3: Automation with Bash Scripting

1. Create Maintenance Script

sudo nano /usr/local/bin/server-maintenance.sh

Add:

#!/bin/bash
# Server Maintenance Script

LOGFILE="/var/log/server-maintenance.log"
echo "=== Maintenance Run Started at $(date) ===" >> $LOGFILE

# Update packages
apt update && apt upgrade -y >> $LOGFILE 2>&1

# Disk usage check
DISK_USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')
if [ "$DISK_USAGE" -gt 80 ]; then
    echo "WARNING: Disk usage is ${DISK_USAGE}% - High!" >> $LOGFILE
else
    echo "Disk usage is ${DISK_USAGE}% - Normal" >> $LOGFILE
fi

# Memory usage check
MEM_USAGE=$(free | awk '/Mem/{printf("%.0f"), $3/$2*100}')
if [ "$MEM_USAGE" -gt 85 ]; then
    echo "WARNING: Memory usage is ${MEM_USAGE}% - High!" >> $LOGFILE
else
    echo "Memory usage is ${MEM_USAGE}% - Normal" >> $LOGFILE
fi

# Clean apt cache
apt autoremove -y && apt clean >> $LOGFILE 2>&1

echo "=== Maintenance Completed at $(date) ===" >> $LOGFILE
echo "" >> $LOGFILE

---

2. Make Script Executable

sudo chmod +x /usr/local/bin/server-maintenance.sh

---

3. Test Script

sudo /usr/local/bin/server-maintenance.sh
cat /var/log/server-maintenance.log

---

4. (Bonus) Schedule with Cron

sudo crontab -e

Add:

0 2 * * * /usr/local/bin/server-maintenance.sh

---

🎯 Success Criteria

- ✅ SSH works only via new user + key
- ✅ Root login and password authentication disabled
- ✅ NGINX serving custom page on port 80
- ✅ Firewall allows only SSH and HTTP
- ✅ Maintenance script runs and logs properly
- ✅ No critical errors in logs

---

📚 Learning Outcomes

- Server hardening best practices
- SSH security and least privilege
- File permissions and ownership
- Bash scripting for automation
- Service management using systemd
- Logging and monitoring basics
- Scheduling with cron

---

📦 Submission

Create folder:

challenges/linux-challenge-2/

Include:

- "README.md" — Summary, issues faced, solutions, screenshots
- Screenshots of:
  - SSH login with new user
  - Browser showing NGINX page
  - "ufw status"
  - "systemctl status nginx"
  - "/var/log/server-maintenance.log"
- "server-maintenance.sh" script

---

🚀 Final Step

git add .
git commit -m "Completed Linux Challenge 2"
git push

---

❓ Need Help?

Open an issue in the repository 🚀
