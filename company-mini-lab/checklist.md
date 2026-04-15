# CHecklist - VM company mini lab

## 1. Project preparation
- [ ] Define the goal of the lab
- [ ] Define the expected final architecture
- [ ] Choose the operating systems for each VM
- [ ] Define the hostname of each machine
- [ ] Define the IP addressing plan
- [ ] Define the services to deploy on the server

## 2. Virtual machine creation
- [ ] Create the server virtual machine
- [ ] Create the admin client virtual machine
- [ ] Create the user client virtual machine
- [ ] Allocate CPU, RAM, and disk space correctly
- [ ] Attach the installation ISO to each VM
- [ ] Boot each VM successfully

## 3. Operating system installation
- [ ] Install Ubuntu Server on the server VM
- [ ] Install Linux Desktop on the admin client
- [ ] Install Linux Desktop on the user client
- [ ] Create local users
- [ ] Update the systems after installation

## 4. Network setup
- [ ] Create or configure the internal virtual network
- [ ] Connect all VMs to the same lab network
- [ ] Check that the network interfaces are detected
- [ ] Identify the interface names on each machine

## 5. Hostname configuration
- [ ] Set the hostname of the server
- [ ] Set the hostname of the admin client
- [ ] Set the hostname of the user client
- [ ] Verify that each hostname is correctly applied

## 6. Static IP configuration
- [ ] Configure a static IP on the server
- [ ] Configure a static IP on the admin client
- [ ] Configure a static IP on the user client
- [ ] Verify the IP address on each machine
- [ ] Verify that all machines are in the same subnet

## 7. Basic connectivity tests
- [ ] Ping the server from the admin client
- [ ] Ping the server from the user client
- [ ] Ping both clients from the server
- [ ] Verify that all machines can reach each other
- [ ] Note any connectivity issue and troubleshoot it

## 8. SSH server setup
- [ ] Install OpenSSH Server on the server VM
- [ ] Start and enable the SSH service
- [ ] Connect to the server from the admin client using SSH
- [ ] Verify SSH access with the server IP
- [ ] Document the SSH connection command

## 9. Name resolution
- [ ] Add local name resolution using /etc/hosts
- [ ] Add the server hostname on both clients
- [ ] Test ping using the hostname instead of the IP
- [ ] Test SSH using the hostname instead of the IP

## 10. Web service deployment
- [ ] Install Apache or Nginx on the server
- [ ] Verify that the web service is running
- [ ] Create a simple test page
- [ ] Access the web page from the admin client
- [ ] Access the web page from the user client

## 11. Shared resource setup
- [ ] Create a shared directory on the server
- [ ] Choose a sharing method (NFS or Samba)
- [ ] Configure the sharing service
- [ ] Access the shared resource from the admin client
- [ ] Access the shared resource from the user client

## 12. Basic firewall configuration
- [ ] Install or enable the firewall on the server
- [ ] Allow SSH traffic
- [ ] Allow web service traffic
- [ ] Allow sharing service traffic if needed
- [ ] Deny unnecessary incoming traffic
- [ ] Verify that required services still work

## 13. Validation
- [ ] Verify SSH access again
- [ ] Verify hostname resolution again
- [ ] Verify web access again
- [ ] Verify file sharing again
- [ ] Verify firewall rules
- [ ] Record the final working state

## 14. Troubleshooting practice
- [ ] Simulate a wrong IP address
- [ ] Simulate a wrong hostname resolution entry
- [ ] Stop the SSH service and diagnose the issue
- [ ] Block the web service with the firewall and diagnose it
- [ ] Restore the correct configuration

## 15. Documentation
- [ ] Write the lab objective
- [ ] Document the architecture
- [ ] Document the IP addressing plan
- [ ] Document the services installed
- [ ] Document the tests performed
- [ ] Document the issues encountered
- [ ] Document the lessons learned
