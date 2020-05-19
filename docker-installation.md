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
Update you apt package index and install the latest version of Docker Engine and containerd
```vim
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io
```
