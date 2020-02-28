
<img src="images/c4logo.png">




In this module we are going to learn about

  * Introduction to Docker
  * Docker Architecture
  * Anatomy of a Container: Namespaces, Cgroups and Union filesystems(OverlayFS)
  * Understanding Virtualization
  * Virtualization vs Container

## Introduction to Docker
Docker is an open platform for developing, shipping & running distributed applications, whether on laptops, data center VMs or cloud. Docker provides the ability to package and run an application in a loosely isolated environment called a container. The Docker Platform consists of multiple product/tools, including the Docker Engine, Images, Containers, and Hub, among others.

The Docker platform is the only container platform to build, secure and manage the widest array of applications from development to production both on premises and in the cloud.


## Docker Architecture

<img src="images/dockerarchitecture.PNG">


## Anatomy of a Container

<img src="images/container-anatomy.PNG">

#### Namespaces
Docker makes use of kernel namespaces to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container. These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.

Docker Engine uses the following namespaces on Linux:

  * **PID** namespace for process isolation.
  * **NET** namespace for managing network interfaces.
  * **IPC** namespace for managing access to IPC resources.
  * **MNT** namespace for managing filesystem mount points.
  * **UTS** namespace for isolating kernel and version identifiers

#### Cgroups
Docker also makes use of kernel control groups for resource allocation and isolation. A cgroup limits an application to a specific set of resources. Control groups allow Docker Engine to share available hardware resources to containers and optionally enforce limits and constraints.

Docker Engine uses the following cgroups:
 * **Memory cgroup** for managing accounting, limits and notifications.
 * **HugeTBL cgroup** for accounting usage of huge pages by process group.
 * **CPU group** for managing user / system CPU time and usage.
 * **CPUSet cgroup** for binding a group to specific CPU. Useful for real time applications and NUMA systems with localized memory per CPU.
 * **BlkIO cgroup** for measuring & limiting amount of blckIO by group.
 * **net_cls and net_prio cgroup** for tagging the traffic control.
 * **Devices cgroup** for reading / writing access devices.
 * **Freezer cgroup** for freezing a group. Useful for cluster batch scheduling, process migration and debugging without affecting prtrace.  


#### Union filesystems(OverlayFS)



