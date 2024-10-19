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
#nmcli con mod LAN ipv4.addresses 172.24.40.40/24 ipv4.gateway 172.24.40.1 ipv4.dns 172.24.40.1 ipv4.method manual connection.autoconnect yes
#nmcli con down LAN && nmcli con up LAN
nmcli device status
nmcli connection show -active
If the connection is unmanaged or not connecting, try this command.
sudo nmcli connection mod LAN connection.autoconnect yes
Activate Changes
nmcli connection reload
This only makes the NM aware of the changes.
You have to take the connection down and then up (nmcli con down NAME; nmcli con up NAME) or most changes can be applied directly with nmcli dev reapply NAME

Firewalld

Firewalld is a good interface to create and manage a simple firewall but the framework behind it is the Netfilter (nftables) firewall.

To see config files for services, check out. "/usr/lib/firewalld/"
General commands

firewall-cmd --list-all

firewall-cmd --get-services

firewall-cmd --add-service squid --permanent
Remember to use the permanent switch, otherwise the rule is written only to the runtime and is lost if you restart firewalld or the server!

firewall-cmd --reload

Add IP address to the trusted zone. firewall-cmd --zone=trusted --add-source=192.168.124.1 --permanent

List configuration for all zones. firewall-cmd --list-all-zones


or
#systemctl restart NetworkManager

#hostnamectl set-hostname station.domain40.example.com
#hostnamectl status
```

**QUESTION 2: Create a backup file named /root/backup.tar.bz2 or /root/backup.tar.gz2. The backup file should contain the content
of /usr/local and should be zipped with bzip2 or gzip2 compression format**.

Both bzip2 and gzip are popular compression tools in Unix/Linux environments.

1. gzip (GNU Zip)

gzip is a widely used compression tool that is based on the DEFLATE compression algorithm. Files compressed with gzip typically have the .gz extension.

2. bzip2

bzip2 is another compression tool. Files compressed with bzip2 have the .bz2 extension.

**Which to Use?**

- Use gzip if you want faster compression and decompression with decent file size reduction.

- Use bzip2 if you need maximum compression and are willing to wait a bit longer for the process to complete.

Both tools can also be combined with tar to compress multiple files into a single archive:

**ANSWER:**
**With gzip:**

```linux
#tar -czvf archive.tar.gz directory/

```

---

**With bzip:**

```linux
#tar -cjvf archive.tar.bz2 directory/

```

---

**QUESTION 3: Change the current tuning profile for serverb to default profile.**

**Tuned** is a powerful tool used on Linux systems (mainly Red Hat-based distributions like RHEL, CentOS, and Fedora) to optimize and manage system performance. It is a dynamic system tuning daemon that can adjust system settings based on specific workload profiles to achieve better performance, power savings, or a balance between the two.

**ANSWER:**

```linux
# dnf install tuned -y
# systemctl enable tuned
# systemctl start tuned
# tuned-adm recommend
virtual-guest
# tuned-adm profile virtual-guest
# tuned-adm active
# tuned-adm profile_info ( check summary information of the current active tuned profile )

```

---

**QUESTION 4: Configure local repository using following link**

- <http://content.example.com/rhel9.0/x86_64/BaseOS>
- <http://content.example.com/rhel9.0/x86_64/AppStream>

**ANSWER:**

```linux
# vi /etc/yum.repos.d/local.repo
[BaseOS]
name=RHEL v9 BaseOS
baseurl= http://content.example.com/rhel9.0/x86_64/BaseOS
enabled=1
gpgcheck=0
[AppStream]
name=RHEL v9 AppStram
baseurl= http://content.example.com/rhel9.0/x86_64/AppStream
enabled=1
gpgcheck=0

#yum repolist

```

---

**QUESTION 5: Create a user named alex, and the user id should be 1234, and the password should be redhat.**

**ANSWER:**
The **useradd** command in Linux is used to create new user accounts. The -u option specifies the user ID (UID) for the new user.

```linux
#useradd -u 1234 alex
#passwd alex
.
.
#tail -1 /etc/passwd
```

---

**QUESTION 6: Add 3 users: harry, natasha, tom.
The requirements: The Additional group of the two users: harry, Natasha is the admin group. The user: tom's login shell should be non-interactive.**

1. **useradd -g** (Primary Group):
   The -g option is used to specify the primary group of the user. Each user must belong to a primary group, and this group is used for file ownership by default.
2. **useradd -G** (Supplementary Groups):
   The -G option allows you to add the user to one or more supplementary groups. A user can belong to multiple groups
3. The **useradd -s** option is used to specify the login shell for the user. A shell is a command-line interface that a user interacts with when they log into a Linux system.
   **Common Shells:**
   /bin/bash: Bash shell (most common and default for many distributions)
   /bin/sh: Bourne shell (a basic shell)
   /bin/zsh: Z shell (advanced shell with more features)
   /sbin/nologin: This is used to prevent the user from logging in interactively. This is useful for system accounts or users who should not have direct shell access.
   **ANSWER:**

```linux
#groupadd admin
#useradd -G admin harry
#useradd -G admin natasha
#useradd -s /sbin/nologin tom
#passwd harry
.
.
```

---

**QUESTION 7: Find all the files owned by user natasha and redirect the output to /tmp/output.
Find all files that are larger than 5MiB in the /etc directory and copy them to /find/largedir and redirect the output to /find/largefiles.**

The **find** command in Linux is used to search for files and directories based on various criteria such as name, size, type, ownership, permissions, etc. It is a powerful tool for searching files in a hierarchical directory structure.
**Common Options:**

- By Name: Find files or directories by name using **-name**

```linux
find /path -name "filename"
```

- By Type: Find files by type (**-type**):
  - f: regular file
  - d: directory
  - l: symbolic link

```linux
find /path -type f   # for files
find /path -type d   # for directories
```

- By Size: Find files by size (**-size**):

  - **+** for greater than
  - **-** for less than

```linux
find /path -size +10M  # files larger than 10MB
find /path -size -1G   # files smaller than 1GB
```

- By Ownership: Find files by user or group ownership:

```linux
find /path -user username    # files owned by a specific user
find /path -group groupname  # files owned by a specific group
```

- By Permissions: Find files with specific permissions:

```linux
find /path -perm 755    # files with permission 755
```

- By Modification Time: Find files based on their last modification time (-mtime):

  - +n: More than n days old
  - -n: Less than n days old

```linux
find /path -mtime +7   # files modified more than 7 days ago
find /path -mtime -3   # files modified less than 3 days ago

```

**ANSWER:**

```linux
# find / -user natasha -type f > /tmp/output
# cat /tmp/output
# find /etc -size +5M -exec cp {} /find/largedir \;
#cd /find/largedir; ls
```
