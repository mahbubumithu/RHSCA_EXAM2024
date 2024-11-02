# podman login registry.lab.example.com
Username:
Password:

The default configuration file for container registries:
/etc/containers/registryies.conf

RedHat recommends to create a registries.conf file for non-privileged user. which file location will be in $HOME/.config/containers

# dnf install container-tools

# dnf info container-tools

# podman search nginx

# skopeo inspect docker://registry.access.redhat.io/nginx

# podman pull nginx

# podman images

# podman build -t myweb -f /root/Containerfile

or

# podman build -t myweb .

# podman create --name myweb nginx  (create but not started)

# podman start myweb

# podman exec myweb ps -au

# podman exec python36 python3 --version

# podman cp /tmp/hello.sh python36:/tmp/hello.sh

# podman stop myweb

# podman rm myweb

# podman rmi nginx
