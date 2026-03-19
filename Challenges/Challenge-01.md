# Challenge 1: Deploy a Simple Web Application to a Virtual Machine

**Module**: Foundations & Culture (Early hands-on to apply Linux basics)  
**Difficulty**: Beginner  
**Estimated time**: 60–90 minutes  
**Goal**: Manually deploy and serve a basic web app on a Linux VM, verifying access from your browser. This builds core skills: VM setup, SSH, package management, file transfer, and basic web serving — before we automate with CI/CD, Docker, etc.

### Prerequisites
- A Linux VM (Ubuntu 22.04 LTS or 24.04 recommended):
  - Local: VirtualBox, VMware, Multipass, or UTM (free)
  - Cloud: AWS EC2 (free tier t3.micro), Google Cloud e2-micro, Azure B1ls, DigitalOcean $4 droplet, etc.
- SSH access to the VM (key-based preferred over password)
- Basic terminal comfort (from module 01 Linux mastery)
- Your local machine has `ssh`, `scp` (or rsync), and a browser

### Challenge Tasks

1. **Launch and Secure Your VM**
   - Create/start your Ubuntu VM.
   - Update packages: `sudo apt update && sudo apt upgrade -y`
   - Install OpenSSH if not present: `sudo apt install openssh-server -y`
   - (Optional but recommended) Set up key-based SSH:
     - Generate key pair locally if needed: `ssh-keygen -t ed25519`
     - Copy public key: `ssh-copy-id user@vm-ip` or manual `\~/.ssh/authorized_keys`
   - Firewall: Allow SSH (port 22) and HTTP (port 80):
     ```bash
     sudo ufw allow OpenSSH
     sudo ufw allow 80/tcp
     sudo ufw enable
     ```

2. **Install and Configure a Web Server (NGINX)**
   - Install NGINX:
     ```bash
     sudo apt install nginx -y
     sudo systemctl enable nginx
     sudo systemctl start nginx
     ```
   - Verify it's running: `sudo systemctl status nginx`
   - Test default page: From your local browser, visit `http://your-vm-public-ip` (or `http://localhost` if local VM with port forwarding). You should see the NGINX welcome page.

3. **Deploy Your Simple Web Application**
   Option A – **Static HTML (easiest – recommended for absolute beginners)**  
   - Create a simple `index.html` on your **local machine**:
     ```html
     <!DOCTYPE html>
     <html>
     <head>
       <title>Hello from DevOps!</title>
       <style>body { font-family: Arial; text-align: center; padding: 50px; background: #f0f4f8; }</style>
     </head>
     <body>
       <h1>Hello, DevOps World!</h1>
       <p>Deployed by Mohammed Adil Rehan on <strong>[Your Name]'s VM</strong></p>
       <p>Current date/time: <span id="time"></span></p>
       <script>document.getElementById('time').innerText = new Date().toLocaleString();</script>
     </body>
     </html>
     ```
   - Copy it to VM:
     ```bash
     scp index.html user@vm-ip:/home/user/
     ```
   - On VM: Move to NGINX default site and set permissions:
     ```bash
     sudo mv /home/user/index.html /var/www/html/
     sudo chown www-data:www-data /var/www/html/index.html
     sudo chmod 644 /var/www/html/index.html
     ```
   - Reload NGINX: `sudo systemctl reload nginx`

   Option B – **Bonus: Basic Node.js App (if comfortable with JS/Node)**
   - On VM: Install Node.js (use nodesource for latest LTS):
     ```bash
     curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
     sudo apt install -y nodejs
     ```
   - Create app folder: `mkdir \~/my-todo-app && cd \~/my-todo-app`
   - Create `server.js`:
     ```js
     const http = require('http');
     const hostname = '0.0.0.0';
     const port = 3000;
     const server = http.createServer((req, res) => {
       res.statusCode = 200;
       res.setHeader('Content-Type', 'text/html');
       res.end('<h1>Hello from Node.js on VM!</h1><p>Deployed via manual DevOps steps.</p>');
     });
     server.listen(port, hostname, () => {
       console.log(`Server running at http://\( {hostname}: \){port}/`);
     });
     ```
   - Start it: `node server.js &`
   - Configure NGINX as reverse proxy (edit `/etc/nginx/sites-available/default`):
     ```
     server {
         listen 80;
         server_name _;
         location / {
             proxy_pass http://localhost:3000;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
         }
     }
     ```
   - Test & reload: `sudo nginx -t && sudo systemctl reload nginx`

4. **Verify & Document**
   - Access from browser: `http://your-vm-ip` (should show your custom page)
   - Take screenshot of:
     - Browser showing your app
     - `curl http://localhost` output on VM
     - `systemctl status nginx` (or Node process)
   - Bonus: Add a custom domain or dynamic content if time allows.

### Success Criteria
- App is live and accessible externally (or locally forwarded)
- No errors in NGINX logs (`sudo journalctl -u nginx` or `/var/log/nginx/error.log`)
- You can explain each step: why SSH, why update packages, why NGINX, file permissions, etc.

### Learning Outcomes
- Hands-on Linux VM management
- Package installation & service control
- File transfer (SCP)
- Basic web serving & troubleshooting
- Understanding manual deployment pain points (→ motivation for automation later)

### Submit Your Work
- Create a folder in your fork/clone: `challenges/challenge1-myname/`
- Add: README.md with steps you took, screenshots, any issues & fixes
- Push & open PR to main repo (or share link in issues/discussions)

Questions? Stuck? Open an issue in the repo — happy debugging!

**Next challenge preview**: Automate this deployment with a simple Bash script.
