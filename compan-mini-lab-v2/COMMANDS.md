# Useful Commands - Company Mini Lab V2

## Network

Check all interfaces and IPs
```
ip a
```

Check routing table
```
ip route
```

Test connectivity
```
ping 192.168.10.10
```

Check who is listening on a port
```
sudo ss -tulnp | grep :53
```

Scan all hosts on a subnet
```
nmap -sn 192.168.10.0/24
```

Scan open ports on a machine
```
nmap -sV 192.168.10.10
```

Capture live traffic on an interface
```
sudo tcpdump -i enp0s8 -n
```

## Netplan

Edit network configuration
```
sudo nano /etc/netplan/00-config.yaml
```

Apply configuration
```
sudo netplan apply
```

Fix file permissions (required before applying)
```
sudo chmod 600 /etc/netplan/00-config.yaml
```

## Routing and NAT (on router)

Enable IP forwarding permanently
```
sudo nano /etc/sysctl.conf
# Set: net.ipv4.ip_forward=1

sudo sysctl -p
```

Verify forwarding is active
```
cat /proc/sys/net/ipv4/ip_forward
```

Set up NAT masquerade
```
sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
sudo iptables -A FORWARD -i enp0s8 -o enp0s3 -j ACCEPT
sudo iptables -A FORWARD -i enp0s9 -o enp0s3 -j ACCEPT
sudo iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
```

Persist iptables rules across reboots
```
sudo apt install iptables-persistent -y
sudo netfilter-persistent save
```

## UFW Firewall

Check status and rules
```
sudo ufw status verbose
sudo ufw status numbered
```

Allow SSH from a specific subnet
```
sudo ufw allow from 192.168.10.0/24 to any port 22
```

Allow HTTP from anywhere
```
sudo ufw allow 80/tcp
```

Allow DNS from a subnet
```
sudo ufw allow from 192.168.10.0/24 to any port 53
```

Delete a rule by number
```
sudo ufw delete 3
```

Enable / disable UFW
```
sudo ufw enable
sudo ufw disable
```

## SSH

Check SSH service status
```
sudo systemctl status ssh
```

Connect to a machine
```
ssh vboxuser@192.168.10.10
ssh vboxuser@srv-infra.company.local
```

Generate SSH key pair
```
ssh-keygen -t ed25519 -C "admin@company-lab"
```

Copy public key to server
```
ssh-copy-id vboxuser@192.168.10.10
```

## Apache

Check Apache status
```
sudo systemctl status apache2
```

Test web server locally
```
curl http://localhost
curl http://192.168.10.10
curl http://srv-infra.company.local
```

Edit default web page
```
sudo nano /var/www/html/index.html
```

## Samba

Check Samba status
```
sudo systemctl status smbd
```

Edit Samba configuration
```
sudo nano /etc/samba/smb.conf
```

Restart Samba after config change
```
sudo systemctl restart smbd
```

## DNS (dnsmasq)

Check dnsmasq status
```
sudo systemctl status dnsmasq
```

Edit dnsmasq configuration
```
sudo nano /etc/dnsmasq.conf
```

Restart dnsmasq
```
sudo systemctl restart dnsmasq
```

Test DNS resolution against a specific server
```
nslookup srv-infra.company.local 192.168.10.10
nslookup srv-infra.company.local 127.0.0.1
```

Check which DNS server is currently used
```
resolvectl status
```

Edit systemd-resolved configuration
```
sudo nano /etc/systemd/resolved.conf
```

Restart systemd-resolved
```
sudo systemctl restart systemd-resolved
```

## System

Update package list
```
sudo apt update
```

Upgrade installed packages
```
sudo apt upgrade
```

Check active connections and listening ports
```
sudo netstat -tulnp
```

Check running services
```
sudo systemctl list-units --type=service --state=running
```

View authentication logs (SSH login attempts)
```
sudo tail -f /var/log/auth.log
```

View current logged-in users
```
who
last | head -20
```
