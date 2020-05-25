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

### Introduction to Docker Images
A Docker image is a file, which consist of multiple layers that is used to execute code in a Docker container. 
An image is essentially built from the instructions for a complete and executable version of an application, which relies on the host OS kernel. When the Docker user runs an image, it can create one or more containers.

A Docker image includes the elements needed to run an application as a container -- such as code, config files, environment variables, libraries and run time. If the image is deployed to a Docker environment it can then be executed as a Docker container. The docker run command will create a container from a given image.

### Building a Docker Image with a Dockerfile
- Create a file loop.sh and append the below lines

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

