<img src="images/c4logo.png">

#### Let’s see what we are going to go learn in this article:

- Difference Between Docker Repository and Docker Registry More About Docker Hub
- Creating a Local Docker Registry
- Pushing images to a Local Docker Registry
- Use Cases for Local Docker Registry

### Difference Between Docker Repository and Docker Registry
    Docker registry is an enterprise grade service for storing Images.
    We can use one of the existing and well-established cloud registries like Docker Hub, Quay, Google Container Registry, Amazon Elastic Container Registry or any other. We can also make our own registry and host it locally. We’re going to learn how to do that later on in this post. 

    Docker Repository is a collection of Docker images with the same name and different tags. For example, the repository we’ve used several times so far, mcr.microsoft.com/dotnet/core/aspnet repository, has many different images in it.

- ### More About Docker Hub
    As we’ve mentioned, Docker Hub is just one of the registry providers. And a good one at that. We can find all sorts of images over there and push our own. We can create unlimited public repositories and one private repo free of charge. If you need more private repositories, you can choose one of the Docker Hub monthly plans.

    Besides providing a centralized resource for image discovery and distribution, Docker Hub’s functionality extends to:

    - Automated builds of images on source code changes and parallel builds
    - Webhooks on image creation and push
    - Groups and organizations management
    - GitHub and BitBucket integration

    To push the image from the local machine to Docker Hub we need to type docker login and enter the credentials of your account in the prompt. After that, you can easily push the image by typing docker push accountname/imagename:tag.


### Creating a Local Docker Registry
Docker Hub is super neat and very intuitive and offers a great deal of functionality for free.
But what if we need more privacy? Or our client wants to use its own server.

If that’s the case, we can make our own Docker Registry.

So how do we do that?

Well, we can set up the registry in two different ways:

- Directly with the Docker command
- Using Docker compose

    ### Directly with docker command
    Creating a local registry using docker is pretty straightforward and shouldn’t be such a big deal if you followed the docker series so far. The registry repository is located on the Docker Hub here. (heh, registry repository) Aren’t you glad now that we talked about the differences between these terms 🙂

    So if we want to set up the local registry we can type:

    ```
    docker run -d -p 50000:5000 --restart always --name my-registry registry:latest
    ```` 
