<img src="images/c4logo.png">


## Install Docker Engine on Ubuntu
### OS requirements
Docker can be Installed on one of the 64-bit of these Ubuntu versions: 

* Ubuntu Eoan 19.10
* Ubuntu Bionic 18.04 (LTS)
* Ubuntu Xenial 16.04 (LTS)

### Installation methods
You can install Docker Engine in different ways, depending on your needs:

Most of the users use repositories approack to install Docker which is the recommended approach.

Some users download the deb package and install it manually. 

In testing and development environments, some users choose to use automated convenience scripts to install Docker.

### Install using the Docker repository approach
1. Update the apt packages and allow apt to use repository over HTTPS

```vim
apt-get update
apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

2. Addin Docker Official GPG key
```vim
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
apt-key fingerprint 0EBFCD88
```

3. Below command will allow you to create a stable repository for Docker
```vim
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

### INSTALL DOCKER ENGINE
1. Update you apt package index and install the latest version of Docker Engine and containerd
```vim
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io
```
2. To install a specific version of Docker Engine
```vim
apt-cache madison docker-ce
pt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```

### Install from a package
If you are not using repository approach, you can download the **.deb** file from the docker engine version that you want to download.

1. Go to [https://download.docker.com/linux/ubuntu/dists/](https://download.docker.com/linux/ubuntu/dists/), choose your Ubuntu version, then browse to pool/stable/, choose amd64, armhf, arm64, ppc64el, or s390x, and download the .deb file for the Docker Engine version you want to install.

2. Once you download the package you can execute the below command to install
```vim
dpkg -i /path/to/package.deb
```
### Install using the convenience script
```diff
- The scripts require root or sudo privileges to run. Therefore, you should carefully examine and audit the scripts before running them.
```
```vim
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
<command output not available>

usermod -aG docker your-user
```

### Access Docker as a non-root user
1. Create Docker group
```vim
sudo groupadd docker
```
2.  Add your user to the docker group.
```vim
sudo usermod -aG docker $USER
```
3. you can also run the below command to activate the changes to groups:
```vim
newgrp docker 
```

### Configure Docker to start on boot
Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and higher) use systemd to manage which services start when the system boots.
```bash
sudo systemctl enable docker
sudo chkconfig docker on
```
