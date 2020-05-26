<img src="images/c4logo.png">

## Docker Images
In this session we are goin to learn about:

* Introduction to Docker Images
* Building a Docker Image with a Dockerfile
* Sharing Data in Your Docker Host with Containers
* Sharing Data Between Containers
* Copying Data to and from Containers
* Creatoing Docker Hub Account.
* Building Images using DockerFile.
* Pull and Push Images From/To Docker Hub.

### Introduction to Docker Images and Layer

A Docker image is a file, which consist of multiple layers that is used to execute code in a Docker container. 
An image is essentially built from the instructions for a complete and executable version of an application, which relies on the host OS kernel. When the Docker user runs an image, it can create one or more containers.

A Docker image includes the elements needed to run an application as a container -- such as code, config files, environment variables, libraries and run time. If the image is deployed to a Docker environment it can then be executed as a Docker container. The docker run command will create a container from a given image.

<img src="images/docker_image_layer.jpg">

### Building a Docker Image with a Dockerfile
- Create a file loop.sh and append the below lines.

```bash
#!/bin/bash

loop(){
count=1
#a=3
a=$1
while [ "$count" -le $a ]; do

echo -e "Running endless loop: $count\n"
echo $cunt
sleep 1
((count++))
#clear
done
}


###
# Main body of script starts here
###
if [ "$1" = loop ];
then
shift
loop $1
else
echo -e "not a valid agrument\n"
echo -e "example: loop.sh loop"
fi
```
- Create a file i.e Dockerfile and append below code

```Dockerfile
FROM alpine
MAINTAINER Subrat Kumar
RUN apk update && apk add bash
COPY loop.sh .
ENTRYPOINT ["/bin/bash", "loop.sh"]
```

### Some docker image commands
- **docker image build:**       Builds an image from a Dockerfile.
- **docker image inspect:**     Displays information on one or more images.
- **docker image load:**        Loads an image from a tar archive or streams for receiving or reading input (STDIN).
- **docker image prune:**       Removes unused images.
- **docker image pull:**        Pulls an image or a repository from a registry.
- **docker image push:**        Pushes an image or a repository to a registry.
- **docker image rm:**          Removes one or more images.
- **docker image save:**        Saves one or more images to a tar archive (streamed to STDOUT by default).
- **docker image tag:**         Creates a tag TARGET_IMAGE that refers to SOURCE_IMAGE.


### Sharing Data in Your Docker Host with Containers

Once deployed, your containers are limited in how they can save and contain data. The limitation lies within the container filesystem. Docker containers make use of the Union File System (UFS), which works with a series of read-only layers that includes a final read-write layer on top. This system functions perfectly when a container doesn’t need to save data. But when you need to deploy a service that requires the ability to save data (such as an application that works with a database), what do you do?

- ### Welcome to Volumes

    A Docker volume is a directory (or collection of files) that lives on the host file system and is not a part of the container’s UFS.    It is within these volumes that containers are capable of saving data. With the docker volume command, you can easily manage volumes   to expand your containers well beyond their basic capability

- ### Creating the Host Data Volume
    The first step is to create a new directory to house the volume. To do this, open a terminal window and issue the command:
    ```
    mkdir ~/container-data
    ```
    **Note:You must ensure the newly-created directory is housed in a location the Docker user can access (with read-write privilege).**    

    Once you’ve created that directory, you’re ready to mount a volume inside. Let’s say you’re going to deploy 
    a container, based on the official Ubuntu image, that contains a directory called /data. 
    To deploy such a container that attaches the internal /data directory to a volume within the host directory 
    ~/container-data, you would issue the command:

    ```
    docker run -dit -P --name ubuntu-test -v ~/container-data:/data ubuntu
    ```
    The above command breaks down like this:

    - **docker run**___is the main command that says we’re going to run a command in a new container.
    - **-dit**___________is d for detached mode, and it ensures that bash or sh can be allocated to a pseudo terminal.
    - **-P**  ____________publishes the containers ports to the host.
    - **–name**________says what follows is the name of the new container.
    - **-v**_____________says what follows is to be the volume.
    - **ubuntu**_______is the image to be used for the container.


    <img src="images/creating-host-data-volume-jpg">



