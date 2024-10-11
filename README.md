# **RHCSA(Ex200)EXAM QUESTIONS and ANSWER**
---
**QUESTION 1: Configure your Host Name, IP Address, Gateway and DNS**.
```linux
Host name: station.domain40.example.com
IP Address:172.24.40.40/24
Gateway172.24.40.1
DNS:172.24.40.1
```

**ANSWER:**
```linux
#mcli con show
#nmcli con mod LAN ipv4.addresses 172.24.40.40/24 ipv4.gateway 172.24.40.1 ipv4.dns 172.24.40.1
#nmcli con mod LAN ipv4.method manual
#nmcli con up LAN
or 
#systemctl restart NetworkManager

#hostnamectl set-hostname station.domain40.example.com
#hostnamectl status
```
