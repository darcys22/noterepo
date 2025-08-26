
## 0) Decide your network details

Pick values that match your home/office LAN. Example values (change them to yours):

* **Interface name:** `eno1` (you’ll confirm below)
* **Static IP:** `192.168.1.50/24`
* **Gateway (router):** `192.168.1.1`
* **DNS:** `1.1.1.1 8.8.8.8`

> Tip: Choose an IP **outside** your router’s DHCP pool, or create a DHCP reservation on the router to avoid conflicts.

---

## 1) Create the `ubuntu` user (with sudo)

On the machine (local keyboard/monitor once), open Terminal:

```bash
# Check if user already exists
getent passwd ubuntu || echo "user 'ubuntu' does not exist"

# If it does NOT exist, create it:
sudo adduser ubuntu
sudo usermod -aG sudo ubuntu

# If it DOES exist, ensure it has a password & sudo:
# (only run if necessary)
sudo passwd ubuntu
sudo usermod -aG sudo ubuntu
```

(Optional but recommended) Add your SSH public key to that user:

```bash
sudo -u ubuntu mkdir -m 700 ~ubuntu/.ssh
sudo -u ubuntu nano ~ubuntu/.ssh/authorized_keys  # paste your public key
sudo -u ubuntu chmod 600 ~ubuntu/.ssh/authorized_keys
```

---

## 2) Install & enable the SSH server

```bash
sudo apt update
sudo apt install -y openssh-server
sudo systemctl enable --now ssh
sudo systemctl status ssh --no-pager
```

Allow SSH through the firewall:

```bash
sudo ufw allow OpenSSH
sudo ufw enable     # press 'y' when prompted
sudo ufw status
```

> If you added your key above and want to harden later, you can disable password logins after you’ve confirmed key-based SSH works (see §5).

---

## 3) Set a static IP for the wired interface (Desktop-friendly method: NetworkManager)

Ubuntu Desktop uses **NetworkManager**. We’ll use `nmcli`.

1. Find your **wired interface** and current **connection name**:

```bash
nmcli device status     # look for TYPE=ethernet; note the DEVICE (e.g., eno1)
nmcli connection show   # note the Active connection name (e.g., "Wired connection 1")
```

2. **Modify the existing wired connection** (replace values as appropriate):

```bash
# Variables (EDIT THESE to your actual values)
IFACE="eno1"
CONNAME="Wired connection 1"
IPV4ADDR="192.168.1.50/24"
GATEWAY="192.168.1.1"
DNS="1.1.1.1 8.8.8.8"

# Apply static config
sudo nmcli connection modify "$CONNAME" \
  ipv4.addresses "$IPV4ADDR" \
  ipv4.gateway "$GATEWAY" \
  ipv4.dns "$DNS" \
  ipv4.method manual \
  ipv6.method ignore \
  connection.autoconnect yes

# Bring it up
sudo nmcli connection up "$CONNAME"
```

If there isn’t an existing connection profile, you can **create a new one**:

```bash
sudo nmcli connection add type ethernet ifname "$IFACE" con-name "static-$IFACE" \
  ipv4.addresses "$IPV4ADDR" ipv4.gateway "$GATEWAY" ipv4.dns "$DNS" \
  ipv4.method manual ipv6.method ignore autoconnect yes

sudo nmcli connection up "static-$IFACE"
```

3. **Verify**:

```bash
ip -4 addr show dev "$IFACE"
ip route
ping -c 3 8.8.8.8
ping -c 3 google.com
```

> **Alternative (Netplan):** If you prefer a YAML file, create `/etc/netplan/01-wired-static.yaml`:
>
> ```yaml
> network:
>   version: 2
>   renderer: NetworkManager
>   ethernets:
>     eno1:
>       dhcp4: no
>       addresses: [192.168.1.50/24]
>       routes:
>         - to: default
>           via: 192.168.1.1
>       nameservers:
>         addresses: [1.1.1.1, 8.8.8.8]
> ```
>
> Then:
>
> ```bash
> sudo netplan generate
> sudo netplan apply   # or: sudo netplan try (auto-reverts if it fails)
> ```

---

## 4) Make it “headless-safe”

Prevent sleep so it stays reachable:

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

(Optionally) set a nice hostname & mDNS so you can use `hostname.local`:

```bash
sudo hostnamectl set-hostname my-ubuntu
echo "127.0.1.1   my-ubuntu" | sudo tee -a /etc/hosts
sudo apt install -y avahi-daemon   # often already present on Desktop
```

---

## 5) (Optional) SSH hardening once keys work

After you’ve confirmed `ssh ubuntu@<STATIC_IP>` works **with your key**, you can disable password logins:

```bash
# Create a custom SSHD config drop-in
sudo editor /etc/ssh/sshd_config.d/90-hardening.conf
```

Add these lines:

```
PasswordAuthentication no
ChallengeResponseAuthentication no
PermitRootLogin no
PubkeyAuthentication yes
UsePAM yes
```

Then reload:

```bash
sudo systemctl reload ssh
```

---

## 6) Test from your other machine

From your laptop/desktop on the same network:

```bash
# If you added your key manually:
ssh ubuntu@192.168.1.50

# Or copy your key in one command (if password auth still enabled):
ssh-copy-id ubuntu@192.168.1.50
ssh ubuntu@192.168.1.50
```

If you set mDNS:

```bash
ssh ubuntu@my-ubuntu.local
```

---

## 7) Troubleshooting quick checks

* Interface/connection status: `nmcli device status`, `nmcli connection show`
* IP & route: `ip -4 a`, `ip r`
* SSH running: `systemctl status ssh`
* Port listening: `ss -tlnp | grep ':22'`
* Firewall: `sudo ufw status`
* Logs: `journalctl -u ssh -b --no-pager`

---

If you share your chosen IP, gateway, and what `nmcli device status` shows, I can tailor the exact commands (with your interface and connection names) so you can paste them as-is.



## WIFI
This is the structure of the netplan file on ubuntu 24.04 to get static ip on wifi
save to `/etc/netplan/50-cloud-init.yaml`
```
network:
    version: 2
    ethernets: {}
    wifis:
        wlp6s0:
            access-points:
                SSIDThatIAmUsing: //e.g. PrettyFlyForAWIFI
                    password: password
            dhcp4: false
            addresses:
                - 192.168.1.100/24
            routes:
              - to: default
                via: 192.168.1.1
            nameservers:
                addresses:
                    - 8.8.8.8
                    - 8.8.4.4
```
