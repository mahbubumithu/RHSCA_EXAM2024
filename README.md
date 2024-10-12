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
**QUESTION : Create a backup file named /root/backup.tar.bz2 or /root/backup.tar.gz2. The backup file should contain the content
of /usr/local and should be zipped with bzip2 or gzip2 compression format**.

**ANSWER:**

Both bzip2 and gzip are popular compression tools in Unix/Linux environments.
1. gzip (GNU Zip)

gzip is a widely used compression tool that is based on the DEFLATE compression algorithm. Files compressed with gzip typically have the .gz extension.

2. bzip2

bzip2 is another compression tool. Files compressed with bzip2 have the .bz2 extension.

**Which to Use?**

- Use gzip if you want faster compression and decompression with decent file size reduction.

- Use bzip2 if you need maximum compression and are willing to wait a bit longer for the process to complete.

Both tools can also be combined with tar to compress multiple files into a single archive:

**With gzip:**

```linux
#tar -czvf archive.tar.gz directory/

```
---

**With bzip:**

```linux
#tar -cjvf archive.tar.bz2 directory/

```
