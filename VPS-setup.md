Here's how to secure your fresh VPS server:

## Set up SSH keys and disable password authentication

**1. Generate SSH key pair (on your local machine):**
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
# Or use RSA if ed25519 isn't supported:
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**2. Copy public key to server:**
```bash
ssh-copy-id username@your_server_ip
# Or manually:
cat ~/.ssh/id_ed25519.pub | ssh username@your_server_ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

**3. Test SSH key login:**
```bash
ssh username@your_server_ip
```

**4. Configure SSH daemon (edit `/etc/ssh/sshd_config`):**
```bash
sudo nano /etc/ssh/sshd_config
```

Make these changes:
```
# Disable root login
PermitRootLogin no

# Disable password authentication
PasswordAuthentication no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys

# Other security settings
Protocol 2
Port 2222  # Change default port
PermitEmptyPasswords no
ChallengeResponseAuthentication no
UsePAM no
X11Forwarding no
PrintMotd no
ClientAliveInterval 120
ClientAliveCountMax 2
MaxAuthTries 3
LoginGraceTime 60
```

**5. Restart SSH service:**
```bash
sudo systemctl restart sshd
# Test connection on new port: ssh -p 2222 username@your_server_ip
```

## Additional security hardening

**Create a non-root user (if you haven't already):**
```bash
sudo adduser newusername
sudo usermod -aG sudo newusername
```

**Set up firewall:**
```bash
# UFW (Ubuntu/Debian)
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2222/tcp  # Your SSH port
sudo ufw allow 80/tcp    # HTTP
sudo ufw allow 443/tcp   # HTTPS
sudo ufw enable

# Or iptables
sudo iptables -A INPUT -p tcp --dport 2222 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
sudo iptables -A INPUT -j DROP
```

**Install fail2ban:**
```bash
sudo apt update && sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

**Keep system updated:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades
```

**Disable unused services:**
```bash
sudo systemctl list-unit-files --type=service --state=enabled
sudo systemctl disable [unused-service]
```

**Set up log monitoring:**
```bash
# Install logwatch
sudo apt install logwatch
# Configure to email daily reports
```
