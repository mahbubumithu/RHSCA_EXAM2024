# podman login registry.lab.example.com
Username:
Password:

The default configuration file for container registries:
/etc/containers/registryies.conf

RedHat recommends to create a registries.conf file for non-privileged user. which file location will be in $HOME/.config/containers

### dnf install container-tools

### dnf info container-tools

### podman search nginx

### skopeo inspect docker://registry.access.redhat.io/nginx

### podman pull nginx

### podman images

### podman build -t myweb -f /root/Containerfile

or

### podman build -t myweb .

### podman create --name myweb nginx  (create but not started)

### podman start myweb

### podman exec myweb ps -au

### podman exec python36 python3 --version

### podman cp /tmp/hello.sh python36:/tmp/hello.sh

### podman stop myweb

### podman rm myweb

### podman rmi nginx

# Container Questions

## Questions 01: Create a container image named monitor from a Containerfile from below link 
http://fromwebserver/Containerfile . All this task done using student user.
## Answer: 
[student@hosta ~]$ podman login <exam registry url >
username: yourusername
password: your registry login pass

[student@hosta ~]$ mkdir demo
[student@hosta ~]$ cd demo 
[student@hosta demo]$ wget http://fromwebserver/Containerfile
[student@hosta demo]$ 
[student@hosta demo]$ cat Containerfile

FROM registry.redhat.io/rhel8/nginx-114:latest
RUN echo " Hello RHCSA Candidate !!!." >> index.html
USER 0
CMD nginx -g "daemon off;"

[student@hosta demo]$ podman build -t monitor . 
[student@hosta demo]$ podman images 
REPOSITORY TAG IMAGE ID CREATED SIZE
localhost/monitor latest aa30769bf294 30 seconds ago 489 MB
 
## Questions 02: Create rootless container and do volume mapping which they asked you in the question and run container 
as a service from normal user account, the service must be enable so it could start automatically after reboot.
▪ Create a container named as ‘ascii2pdf’ using the previously created container image from previous question 
monitor
▪ Map the ‘/opt/files’ to container ‘/opt/incoming’
▪ Map the ‘/opt/processed’ to container ‘/opt/outgoing’
▪ Create systemd service as container-ascii2pdf.service
▪ Make service active after all server reboots
## Answer: 

#mkdir /opt/files /opt/processed 
#chown student:student /opt/files /opt/processed 
#ssh studednt@localhost 

$podman run -d –name ascii2pdf -v /opt/files:/opt/incoming:Z -v /opt/processed:/opt/outgoing:Z localhost:monitor:latest

$ mkdir ~/.config/systemd/user 
$cd ~/.config/systemd/user 
$podman generate systemd –name ascii2pdf –new –files 
$podman stop ascii2pdf 
$podman rm ascii2pdf 
$systemctl –user daemon-reload 
$loginctl enable-linger
$systemctl –user enable container-ascii2pdf.service –now 
$ podman ps

========================================================================================
