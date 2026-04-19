# VM company Mini Lab

## Overview

This lab simulates a small enterprise-like infrastructure using virtual machines.

The environment includes:
- 1 Linux server
- 2 Linux clients
- a private internal network
- remote administration through SSH
- basic service deployment
- basic security and troubleshooting

## Objectives

- build a virtual lab from scratch
- understand how machines communicate on a network
- configure static IP addresses
- use SSH for remote administration
- understand the difference between internal network and internet access
- practice troubleshooting

## Architecture

```
client-admin        client-user
     |                   |
     |                   |
     +------ lab-net ----+
              |
          srv-infra
```

## Machines

- `srv-infra` - main Linux server → 192.168.56.10
- `client-admin` - administration workstation → 192.168.56.20
- `client-user` - user workstation → 192.168.56.30

## Main topics covered

- virtualization
- Linux installation
- hostname configuration
- static IP configuration
- network connectivity checks
- SSH
- local name resolution
- web service deployment
- file sharing
- firewall basics
- troubleshooting methodology

## Expected outcome

At the end of the lab, the server should be reachable from both clients, provide at least one service, and be documented clearly with configuration choices and lessons learned.
