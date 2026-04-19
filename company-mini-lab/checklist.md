# CHecklist - VM company mini lab

## 1. Project preparation
- [x] Define the goal of the lab
- [x] Define the expected final architecture
- [x] Choose the operating systems for each VM
- [x] Define the hostname of each machine
- [x] Define the IP addressing plan
- [x] Define the services to deploy on the server

## 2. Virtual machine creation
- [x] Create the server virtual machine
- [x] Create the admin client virtual machine
- [x] Create the user client virtual machine
- [x] Allocate CPU, RAM, and disk space correctly
- [x] Attach the installation ISO to each VM
- [x] Boot each VM successfully

## 3. Operating system installation
- [x] Install Ubuntu Server on the server VM
- [x] Install Linux Desktop on the admin client
- [x] Install Linux Desktop on the user client
- [x] Create local users
- [x] Update the systems after installation

## 4. Network setup
- [x] Create or configure the internal virtual network
- [x] Connect all VMs to the same lab network
- [x] Check that the network interfaces are detected
- [x] Identify the interface names on each machine

## 5. Hostname configuration
- [x] Set the hostname of the server
- [x] Set the hostname of the admin client
- [x] Set the hostname of the user client
- [x] Verify that each hostname is correctly applied

## 6. Static IP configuration
- [x] Configure a static IP on the server
- [x] Configure a static IP on the admin client
- [x] Configure a static IP on the user client
- [x] Verify the IP address on each machine
- [x] Verify that all machines are in the same subnet

## 7. Basic connectivity tests
- [x] Ping the server from the admin client
- [x] Ping the server from the user client
- [x] Ping both clients from the server
- [x] Verify that all machines can reach each other
- [x] Note any connectivity issue and troubleshoot it

## 8. SSH server setup
- [x] Install OpenSSH Server on the server VM
- [x] Start and enable the SSH service
- [x] Connect to the server from the admin client using SSH
- [x] Verify SSH access with the server IP
- [x] Document the SSH connection command

## 9. Name resolution
- [x] Add local name resolution using /etc/hosts
- [x] Add the server hostname on both clients
- [x] Test ping using the hostname instead of the IP
- [x] Test SSH using the hostname instead of the IP

## 10. Web service deployment
- [x] Install Apache or Nginx on the server
- [x] Verify that the web service is running
- [x] Create a simple test page
- [x] Access the web page from the admin client
- [x] Access the web page from the user client

## 11. Shared resource setup
- [x] Create a shared directory on the server
- [x] Choose a sharing method (NFS or Samba)
- [x] Configure the sharing service
- [x] Access the shared resource from the admin client
- [x] Access the shared resource from the user client

## 12. Basic firewall configuration
- [x] Install or enable the firewall on the server
- [x] Allow SSH traffic
- [x] Allow web service traffic
- [x] Allow sharing service traffic if needed
- [x] Deny unnecessary incoming traffic
- [x] Verify that required services still work

## 13. Validation
- [x] Verify SSH access again
- [x] Verify hostname resolution again
- [x] Verify web access again
- [x] Verify file sharing again
- [x] Verify firewall rules
- [x] Record the final working state

## 14. Troubleshooting practice
- [x] Simulate a wrong IP address
- [x] Simulate a wrong hostname resolution entry
- [x] Stop the SSH service and diagnose the issue
- [x] Block the web service with the firewall and diagnose it
- [x] Restore the correct configuration

## 15. Documentation
- [x] Write the lab objective
- [x] Document the architecture
- [x] Document the IP addressing plan
- [x] Document the services installed
- [x] Document the tests performed
- [x] Document the issues encountered
- [x] Document the lessons learned
