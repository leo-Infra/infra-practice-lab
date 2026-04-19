# Useful Commands

## Network

Check interfaces:
ip a

Check routes:
ip route

Test connectivity:
ping 192.168.56.10

## Netplan
Edit config:
sudo nano /etc/netplan/00-installer-config.yaml

Apply config:
sudo netplan apply

Fix permissions:
sudo chmod 600 /etc/netplan/00-installer-config.yaml

## SSH
Check status:
sudo systemctl status ssh

Connect:
ssh leo@192.168.56.10

## System
Update:
sudo apt update

Upgrade:
sudo apt upgrade
