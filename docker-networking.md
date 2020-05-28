<img src="images/c4logo.png">

### Docker Networking
When you Install the Docker by default docker create three Networks
- Bridge
- Host
- None

**Note: Bridge is the default network that a container can attach to.**

Examples:
```
docker run -itd ubuntu  #Auto assign Bridge network


docker run -itd --network=host ubuntu   #Creata a hostonly netwotrk and assign the IP address to container


docker run -itd --network=none ubunut   #No network will assign to container

```

- ### Bridge Network
Bridge network is a private network create by the Docker in the docker host, all created container(s) attach bydefault and they getan Internal IP Address in the range 172.17.0.0 series.
A container can reach to another with Internal IP address if required. To access the container outside world map the ports of theContainers to the Ports on the Docker host.
<img src="images/bridge-network.jpg">

- ### Host Network
For standalone containers, remove network isolation between the container and the Docker host, and use the host’s networkingdirectly. host is only available for swarm services on Docker 17.06 and higher. See [use the host network](https://docs.docker.comnetwork/host/).  
The --net=host option is used to make the programs inside the Docker container look like they are running on the host itself, fromthe perspective of the network. It allows the container greater network access than it can normally get.

Normally you have to forward ports from the host machine into a container, but when the containers share the host's network, any network activity happens directly on the host machine - just as it would if the program was running locally on the host instead of inside a container.

While this does mean you no longer have to expose ports and map them to container ports, it means you have to edit your Dockerfiles to adjust the ports each container listens on, to avoid conflicts as you can't have two containers operating on the same host port. However, the real reason for this option is for running apps that need network access that is difficult to forward through to a container at the port level. 

Generally speaking, --net=host is only needed when you are running programs with very specific, unusual network needs.

Example:
```
docker run --rm -d  --name my_httpd httpd
```
Try to access the http UI with port number 80.

```
docker run --rm -d --network host --name my_httpd httpd
```
Now, try to access the httpd service with port 80.





