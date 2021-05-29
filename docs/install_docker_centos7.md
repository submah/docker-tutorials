<img src="../images/c4logo.png">

### Install using the repository

Before you install Docker CE for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

#### SET UP THE REPOSITORY


1. Install required packages. yum-utils provides the yum-config-manager utility, and device-mapper-persistent-data and lvm2 are
   required by the devicemapper storage driver.

```sh 
   sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

2. Use the following command to set up the stable repository. You always need the stable repository, even if you want to install 
   builds from the edge or test repositories as well.

```
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```
#### Update your repository 

```
yum update -y

```
#### INSTALL DOCKER CE

Install the latest version of Docker CE, or go to the next step to install a specific version.

```
sudo yum install docker-ce -y
```
