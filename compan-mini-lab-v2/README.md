# Company Mini Lab V2

## Overview

This lab simulates a more realistic enterprise network infrastructure using virtual machines.
It extends the V1 lab by introducing network segmentation, routing, a firewall, internal services, and DNS resolution.

The environment includes:

- 1 Linux router (Ubuntu Server)
- 1 Linux server with multiple services
- 2 Linux clients on separate network segments
- 2 isolated internal networks
- Inter-network routing through a Linux router
- Firewall rules based on network source
- Internal DNS with dnsmasq

## Objectives

- design a segmented network architecture
- build a Linux-based router with NAT
- configure static IPs and gateways across multiple subnets
- deploy and restrict services using UFW
- set up internal DNS resolution with dnsmasq
- understand the difference between routing, NAT, and firewalling
- practice real enterprise-style troubleshooting

## Architecture

```
               INTERNET (NAT)
                     |
                  [ router ]
                  /        \
         net-admin          net-user
         /      \              |
  srv-infra  client-admin   client-user
```

## Machines

| Machine | Role | Network | IP |
|---|---|---|---|
| router | Linux router + NAT | net-admin + net-user + NAT | 192.168.10.1 / 192.168.20.1 |
| srv-infra | Server (SSH, Apache, Samba, DNS) | net-admin | 192.168.10.10 |
| client-admin | Admin workstation | net-admin | 192.168.10.20 |
| client-user | User workstation | net-user | 192.168.20.20 |

## Networks

| Network | Subnet | Gateway |
|---|---|---|
| net-admin | 192.168.10.0/24 | 192.168.10.1 |
| net-user | 192.168.20.0/24 | 192.168.20.1 |

## Services deployed on srv-infra

| Service | Port | Access |
|---|---|---|
| SSH | 22 | net-admin only |
| Apache (HTTP) | 80 | all networks |
| Samba | 445 | net-admin only |
| dnsmasq (DNS) | 53 | all networks |

## Firewall rules (UFW on srv-infra)

| Source | Destination | Port | Rule |
|---|---|---|---|
| 192.168.10.0/24 | srv-infra | 22 | ALLOW |
| 192.168.20.0/24 | srv-infra | 22 | DENY (default) |
| any | srv-infra | 80 | ALLOW |
| 192.168.10.0/24 | srv-infra | 445 | ALLOW |
| 192.168.20.0/24 | srv-infra | 445 | DENY (default) |
| 192.168.10.0/24 | srv-infra | 53 | ALLOW |
| 192.168.20.0/24 | srv-infra | 53 | ALLOW |

## DNS domain

Internal domain: `company.local`

| Hostname | Resolves to |
|---|---|
| router.company.local | 192.168.10.1 |
| srv-infra.company.local | 192.168.10.10 |
| client-admin.company.local | 192.168.10.20 |
| client-user.company.local | 192.168.20.20 |

## Main topics covered

- network segmentation
- Linux router configuration
- IP forwarding and NAT (iptables masquerade)
- static IP and gateway configuration with netplan
- UFW firewall with per-network rules
- Apache web server deployment
- Samba file sharing
- dnsmasq internal DNS server
- systemd-resolved conflicts and resolution
- inter-network troubleshooting methodology
