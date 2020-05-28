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

### Networking with standalone containers
This series of tutorials deals with networking for standalone Docker containers.
This topic includes two different tutorials

- Use the default **bridge** network demonstrates how to use the default bridge network that Docker sets up for you automatically. This    network is not the best choice for production systems.

- Use **user-defined bridge** networks shows how to create and use your own custom bridge networks, to connect containers running on the same Docker host. This is recommended for standalone containers running in production.

### Use the default bridge network
In this example, you start two different alpine containers on the same Docker host and do some tests to understand how they communicate with each other. You need to have Docker installed and running.

```
#To list available networks
docker network ls
```
Start two alpine containers running ash, which is Alpine’s default shell rather than bash. The -dit flags mean to start the container detached (in the background), interactive (with the ability to type into it), and with a TTY (so you can see the input and output). Since you are starting it detached, you won’t be connected to the container right away. Instead, the container’s ID will be printed. Because you have not specified any --network flags, the containers connect to the default bridge network.

```
docker run -dit --name alpine1 alpine ash

docker run -dit --name alpine2 alpine ash
```

Check that both containers are actually started:

```
docker ps
```
Inspect the bridge network to see what containers are connected to it.

```
docker network inspect bridge
```

[Output]

```json
[
    {
        "Name": "bridge",
        "Id": "7e036800a97c8150206d570d6b781c1f9e3e99392533f01dc411eff760a49cdc",
        "Created": "2020-05-28T14:20:12.071483312Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "3485a425ed17ede9bec0bdfb9b971508042afc2e6c78ba3751b821e3e3004a98": {
                "Name": "alpine2",
                "EndpointID": "497729c65ae1a929d6eee8ce024115e103b114973578b05fa9ed9cd945511c32",
				"MacAddress": "02:42:ac:11:00:03",
                "IPv4Address": "172.17.0.3/16",
                "IPv6Address": ""
            },
            "5788f74fdc59f95ced36d908245b923cd940ed5917ae4a464ea42c7a135be21c": {
                "Name": "alpine1",
                "EndpointID": "663581b9cd9cc26fcd3d091257d2e4ce4fbb54d3ae05732a48877492f64aa539",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```


