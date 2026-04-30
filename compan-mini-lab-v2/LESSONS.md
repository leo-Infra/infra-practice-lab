# Lessons Learned - Company Mini Lab V2

## Networking

- A Linux machine with multiple interfaces does not route between them by default — IP forwarding must be explicitly enabled
- NAT (masquerade) allows internal machines to reach the internet by hiding their private IP behind the router's public IP
- A gateway must be configured on every machine, otherwise it cannot communicate outside its own subnet
- Network segmentation means two machines on different subnets cannot communicate without a router, even if they are on the same physical host
- VirtualBox internal networks act as virtual switches — no physical hardware required
- The routing table (`ip route`) is the first place to check when a machine cannot reach another network

## Linux

- Netplan YAML is indentation-sensitive — a single misplaced block causes the entire configuration to be rejected
- Netplan requires file permissions of 600 — too open and it refuses to apply
- `sysctl -p` applies kernel parameter changes immediately without rebooting
- iptables rules are lost on reboot unless persisted with `iptables-persistent`
- `systemctl enable` makes a service start at boot — `systemctl start` only starts it for the current session

## Security

- UFW with `default deny incoming` means every port must be explicitly opened — including DNS
- A firewall applied on the server controls access per source network, not just per port
- SSH root login and password authentication should be disabled in production — use key-based authentication only
- Port 22 open to all networks is a security risk — always restrict SSH to trusted subnets

## DNS

- Ubuntu uses `systemd-resolved` by default, which occupies port 53 with a stub listener
- Any external DNS server (dnsmasq, bind9) will conflict with systemd-resolved unless `DNSStubListener=no` is set
- Setting `nameservers` in netplan is not always enough — `systemd-resolved` must also be configured separately
- Always test DNS directly against the server IP (`nslookup hostname 192.168.10.10`) before assuming the issue is in the service itself
- `listen-address` and `bind-interfaces` in dnsmasq make its binding explicit and predictable

## Troubleshooting methodology

- Always debug step by step — never change multiple things at once
- The correct order when a machine cannot reach another: check state → check IP → check gateway → check routing → check firewall → check service
- A timeout means the packet is being dropped somewhere — a connection refused means it arrives but is rejected
- `ping` tests layer 3 (routing), `nslookup` tests layer 7 (application), `ss -tulnp` shows what is listening
- Checking a service on localhost first (`nslookup hostname 127.0.0.1`) confirms the service works before testing network access

## Virtualization

- Virtual machines behave like real machines on a real network
- Each network adapter on a VM defines which network it belongs to
- A VM with 3 adapters can act as a router between 3 networks
- RAM allocation matters — an under-resourced VM will become unresponsive under load

## Key takeaway

Understanding why each step is necessary matters more than following steps blindly.
A segmented network with a firewall is not just a technical exercise — it reflects how real enterprise infrastructure is designed and secured.
