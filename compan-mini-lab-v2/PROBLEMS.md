# Problems Encountered - Company Mini Lab V2

## 1. Netplan — invalid YAML indentation

**Problem**
Running `sudo netplan apply` returned an error about an unknown key `nameservers`.
The `nameservers` block was placed at the root level of the YAML file instead of inside the interface block.

**Error message**
```
Error in network definition: unknown key 'nameservers'
```

**Cause**
YAML is indentation-sensitive. A block placed at the wrong level is treated as an unknown key.

**Fix**
Move `nameservers` inside the interface definition:
```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      addresses:
        - 192.168.10.20/24
      routes:
        - to: default
          via: 192.168.10.1
      nameservers:
        addresses: [192.168.10.10]
```

**Lesson learned**
In netplan YAML, every option must be nested under the correct parent. Always validate indentation carefully before applying.

---

## 2. Netplan — file permissions too open

**Problem**
Netplan showed a warning and refused to apply the configuration.

**Error message**
```
WARNING: Permissions for /etc/netplan/00-config.yaml are too open.
Netplan configuration should NOT be accessible by others.
```

**Fix**
```
sudo chmod 600 /etcnt/netplan/00-config.yaml
```

**Lesson learned**
Netplan requires strict file permissions (read/write for owner only) as a security measure. Always run `chmod 600` after creating or editing a netplan file.

---

## 3. dnsmasq — port 53 already in use

**Problem**
dnsmasq failed to start after installation.

**Error message**
```
failed to create listening socket for port 53: Address already in use
FAILED to start up
```

**Cause**
Ubuntu uses `systemd-resolved` by default, which runs a local DNS stub listener on port 53. This conflicted with dnsmasq trying to bind the same port.

**Fix**
Disable the stub listener in systemd-resolved:
```
sudo nano /etc/systemd/resolved.conf

[Resolve]
DNSStubListener=no
```
Then restart resolved and dnsmasq:
```
sudo systemctl restart systemd-resolved
sudo systemctl restart dnsmasq
```

**Lesson learned**
On modern Ubuntu systems, port 53 is occupied by systemd-resolved by default. Any DNS server installed alongside it (dnsmasq, bind9) will conflict unless the stub listener is explicitly disabled.

---

## 4. DNS resolution — clients using 127.0.0.53 instead of dnsmasq

**Problem**
After configuring dnsmasq and pointing clients to `192.168.10.10`, `nslookup` was still querying `127.0.0.53` (the local systemd-resolved stub).

**Error message**
```
;; Got SERVFAIL reply from 127.0.0.53
server can't find srv-infra.company.local: SERVFAIL
```

**Cause**
Even though `nameservers` was set in netplan, systemd-resolved was intercepting DNS queries before they reached the configured server. The `DNSStubListener` was not yet disabled on the clients.

**Fix**
On each client, configure systemd-resolved to use the internal DNS server:
```
sudo nano /etc/systemd/resolved.conf

[Resolve]
DNS=192.168.10.10
Domains=company.local
DNSStubListener=no
```
Then restart:
```
sudo systemctl restart systemd-resolved
```

**Lesson learned**
On Ubuntu, netplan nameserver settings alone are not always sufficient. systemd-resolved has its own configuration and must be updated separately to fully redirect DNS queries.

---

## 5. UFW blocking DNS port 53

**Problem**
DNS queries from `client-user` to `srv-infra` timed out even though dnsmasq was running and the routing was working.

**Error message**
```
;; communications error to 192.168.10.10#53: timed out
```

**Cause**
UFW was configured with `default deny incoming`. Port 53 was never explicitly opened, so all DNS requests from both subnets were silently dropped.

**Fix**
On srv-infra, open port 53 for both subnets:
```
sudo ufw allow from 192.168.10.0/24 to any port 53
sudo ufw allow from 192.168.20.0/24 to any port 53
sudo ufw reload
```

**Lesson learned**
When using `default deny incoming`, every service port must be explicitly opened — including DNS. This is easy to forget because DNS is often taken for granted as infrastructure, not as a service.

---

## 6. dnsmasq not listening on the correct address

**Problem**
DNS queries from `client-user` timed out even after opening port 53 in UFW.

**Cause**
dnsmasq was not explicitly configured with a `listen-address`, so its behavior depended on the system defaults. Adding `bind-interfaces` and `listen-address` made its binding explicit and reliable.

**Fix**
Add to `/etc/dnsmasq.conf`:
```
listen-address=127.0.0.1,192.168.10.10
bind-interfaces
```
Then restart:
```
sudo systemctl restart dnsmasq
```

**Lesson learned**
Always explicitly define which addresses a service listens on. Relying on defaults can lead to unpredictable behavior that is hard to debug.
