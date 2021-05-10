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
## Getting Information about Docker Setup
```bash
docker -v  

docker version  

docker system info
```
## Docker list of commands
```bash
sudo docker
```
```bash
Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/root/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env
                           var and default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/root/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/root/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/root/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  builder     Manage builds
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  engine      Manage the docker engine
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes
Commands:

  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.
``

