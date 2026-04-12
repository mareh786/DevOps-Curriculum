# Linux Challenge 2: Server Hardening and Basic Automation

**Module**: Linux Mastery  
**Difficulty**: Intermediate  
**Estimated Time**: 90–120 minutes  

### Objective
Set up a secure Linux server from scratch and create basic automation for maintenance tasks. This challenge focuses purely on core Linux skills: user management, SSH hardening, firewall configuration, service setup, permissions, and Bash scripting.

### Prerequisites
- A fresh Ubuntu 22.04 or 24.04 VM (GCP, AWS, Azure free tier, or local)
- Initial SSH access to the VM (you may use browser-based SSH or `gcloud` initially)
- Basic terminal comfort (from `linux.md`)

### Tasks

#### Part 1: Server Hardening
1. Fully update and upgrade the system.
2. Create a new non-root user and grant it sudo privileges.
3. Disable direct root login and password-based SSH authentication.
4. Set up SSH key-based authentication for the new user from your local machine.
5. Configure UFW firewall to allow only SSH (port 22) and HTTP (port 80), and enable it.
6. Install essential tools: `curl`, `vim`, `htop`, and `fail2ban`.

#### Part 2: Web Service Setup
7. Install NGINX and configure it to start automatically on boot.
8. Create a custom `index.html` page in the default web directory that displays a message including your name and "Linux Challenge 2 Completed".
9. Set correct ownership and permissions for the web files (use the appropriate user/group for NGINX).
10. Verify that the website is accessible from your browser using the VM's public IP.

#### Part 3: Automation with Bash Scripting
11. Create a Bash script named `server-maintenance.sh` that performs the following:
    - Updates the package list and upgrades installed packages (non-interactively)
    - Checks disk usage and logs a warning if any partition exceeds 80%
    - Checks memory usage and logs a warning if it exceeds 85%
    - Cleans the apt cache
    - Logs all actions with timestamps to `/var/log/server-maintenance.log`

12. Make the script executable and place it in a suitable system location.
13. Test the script manually.
14. (Bonus) Set up a cron job to run the maintenance script automatically every day at 2:00 AM.

### Success Criteria
- You can SSH into the server **only** using the new user with key authentication (root login and password auth must be disabled).
- NGINX is running and serving your custom page correctly on port 80.
- The firewall allows only SSH and HTTP traffic.
- The maintenance script executes successfully and generates a proper log file with timestamps.
- No critical errors appear in service logs.

### Learning Outcomes
- Server hardening best practices (least privilege, secure SSH)
- Proper file permissions and ownership for services
- Writing practical Bash automation scripts
- Service management using systemd
- Basic system monitoring and logging
- Scheduling tasks with cron

### Submission Instructions
In your repository fork, create a folder:
`challenges/linux-challenge-2/`

Inside it, include:
- A `README.md` file containing:
  - Brief summary of the steps you followed
  - Any problems you encountered and how you solved them
- Screenshots showing:
  - Successful SSH login using the new user + key
  - Your custom NGINX page in the browser
  - Firewall status (`ufw status`)
  - NGINX service status
  - Content of the maintenance log file

Commit and push your work. You may open a PR if you want feedback.

**Tip**: Refer to `topics/linux.md` for commands related to users, permissions, services, firewall, and scripting.

Questions or need hints? Open an issue in the main repository.

Good luck! This challenge builds essential Linux skills used daily in DevOps environments.
