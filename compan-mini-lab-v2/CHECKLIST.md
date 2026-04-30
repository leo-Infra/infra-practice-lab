# Checklist - Company Mini Lab V2

## 1. Project preparation

- [x] Define the goal of the lab
- [x] Define the expected final architecture
- [x] Choose the operating systems for each VM
- [x] Define the hostname of each machine
- [x] Define the IP addressing plan for both subnets
- [x] Define the services to deploy on the server
- [x] Define the firewall rules per network

## 2. Virtual machine creation

- [x] Create the router virtual machine (Ubuntu Server)
- [x] Create the server virtual machine (Ubuntu Server)
- [x] Create the admin client virtual machine
- [x] Create the user client virtual machine
- [x] Allocate CPU, RAM, and disk space correctly
- [x] Configure 3 network adapters on the router (NAT, net-admin, net-user)
- [x] Attach correct network to each VM

## 3. Operating system installation

- [x] Install Ubuntu Server on router
- [x] Install Ubuntu Server on srv-infra
- [x] Install Linux Desktop on client-admin
- [x] Install Linux Desktop on client-user
- [x] Create local users on each machine
- [x] Update all systems after installation

## 4. Router configuration

- [x] Identify the 3 network interfaces (NAT, net-admin, net-user)
- [x] Configure static IPs via netplan (192.168.10.1 and 192.168.20.1)
- [x] Keep NAT interface in DHCP
- [x] Fix netplan file permissions (chmod 600)
- [x] Apply configuration with netplan apply
- [x] Enable IP forwarding (net.ipv4.ip_forward=1 in sysctl.conf)
- [x] Apply sysctl changes
- [x] Set up NAT with iptables masquerade
- [x] Persist iptables rules with iptables-persistent

## 5. Client and server network configuration

- [x] Configure static IP on srv-infra (192.168.10.10)
- [x] Set gateway to 192.168.10.1 on srv-infra
- [x] Configure static IP on client-admin (192.168.10.20)
- [x] Set gateway to 192.168.10.1 on client-admin
- [x] Configure static IP on client-user (192.168.20.20)
- [x] Set gateway to 192.168.20.1 on client-user

## 6. Routing validation

- [x] Ping router from client-admin
- [x] Ping router from client-user
- [x] Ping srv-infra from client-admin
- [x] Ping srv-infra from client-user (inter-network)
- [x] Ping client-user from client-admin (inter-network)

## 7. Services on srv-infra

- [x] Install and start OpenSSH server
- [x] Install and start Apache2
- [x] Create custom index.html
- [x] Install and configure Samba
- [x] Create shared folder /srv/partage
- [x] Test HTTP access from client-admin

## 8. Firewall configuration

- [x] Install UFW on srv-infra
- [x] Set default policy: deny incoming, allow outgoing
- [x] Allow SSH from net-admin only
- [x] Allow HTTP from anywhere
- [x] Allow Samba from net-admin only
- [x] Allow DNS (port 53) from net-admin
- [x] Allow DNS (port 53) from net-user
- [x] Enable UFW
- [x] Verify rules with ufw status

## 9. DNS configuration

- [x] Install dnsmasq on srv-infra
- [x] Disable systemd-resolved DNSStubListener to free port 53
- [x] Configure dnsmasq.conf with company.local domain
- [x] Add address entries for all machines
- [x] Set listen-address to 127.0.0.1 and 192.168.10.10
- [x] Restart and verify dnsmasq is running
- [x] Configure resolved.conf on each client (DNS=192.168.10.10)
- [x] Test DNS resolution from srv-infra
- [x] Test DNS resolution from client-admin
- [x] Test DNS resolution from client-user

## 10. Final validation

- [x] nslookup srv-infra.company.local from client-admin
- [x] nslookup srv-infra.company.local from client-user
- [x] curl http://srv-infra.company.local from client-admin
- [x] SSH to srv-infra from client-admin succeeds
- [x] SSH to srv-infra from client-user is blocked
