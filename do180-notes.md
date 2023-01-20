# My DO180 notes - 14-chapters
# * Introduction: 10-pages max
# 1. Introducing Container Technology: 3-sections:
- Overview of container technology: 3-pages
- Overview of Container Architecture: 3-pages
- Overview of Kubernetes and OpenShift: 2-pages
# 2. Creating Containerized Services: 2-sections:
- Provisioning Containerized Services: 6-pages
- Using Rootless Containers: 2-pages
# 3. Managing Containers: 3-sections:
- Managing the Lifecycle of Containers: 8-pages
- Attaching Persistent Storage to Containers: 4-pages
- Accessing Containers: 2-pages
# 4. Managing Container Images: 2-sections:
- Accessing Registeries: 6-pages
- Manipulating Container Images: 6-pages
# 5. Creating Custom Container Images: 2-sections:
- Designing Custom Container Images: 4-pages
- Building Custom Container Images with ContainerFiles: 6-pages
# 6. Deploying Containerized Applications On OpenShift: 5-sections
- Describing Kubernetes and OpenShift Architecture: 7-pages
- Creating Kubernetes Resources: 12-pages
- Creating Routes: 4-pages
- Creating Applications with Source-to-image: 10-pages
- Creating Applications with the OpenShift Web Console: 5-pages
# 7. Deploying Multi-Container Applications: 3-sections
- Considerations for Multi-Container Applications: 5-pages
- Deploying a Multi-Container Application on OpenShift: 2-pages
- Deploying a Multi-container Application on OpenShift Using a Template: 6-pages
# 8. Trouchleshooting Containerized Applications: 2-sections
- Troubleshooting S2I Builds and Deployments: 6-pages
- Troubleshooting Containerized Applications: 6-pages
# 9. Comprehensive Review: 3-pages
# 10. Implementing Microservices Architecture: 5-pages
# 11: Creating a GitHub Account: 1-page
# 12: Creating a Quay Account: 3-pages
# Creating a Red Hat Account: 1-page
# Useful Git Commands: 1-page

# Chapter 1: Introducting Container Technology 29-11-2022 10:36:26
# Chapter 1 - Section 1 - Overview of container technology:
## What's a container?
It's a set of one or more processes that are isolated from the rest of the system.

## What are the benefits of containers over traditional Servers?
1. Containers provide many of the same benefits as virtual machines, such as security, storage and network isolation.
2. Containers require far fewer hardware resources and are quick to start and terminate.
3. They also isolate the libraries and the runtime resources (such as CPU and storage) for an application to minimize the impact of any OS update to the host OS.
4. It helps with the efficiency, elasticity, and resusability of the hosted applications.
5. Helps with application portability.


Traditional deployment:  
1. Application's dependencies are closely related to the runtime environment, so an OS may break when any updates or patches are applied to the base OS
2. There's a downtime for an application to have its dependencies upgraded.

## What's the OCI?
OCI "Open Container Initiative" provides a set of industry standards that define a container runtime specification and a container image specification  
The image specification defines the format for the bundle of files and metadata that form a container image.  
When youbuild an application as a container image, which compiles with the OCI standard, you can use any OCI-complicant container engine to execute the application.  
There are many container engines available to manage and execute individual containers, including Rocket, Drawbridge, LXC, Docker, and Podman.  
Podman is available in Red Hat Enterprise Linux 7.6 and later, and is used in this course to start, manage, and terminate individual containers.  

## What are the major advs of using containers?
1. Low hardware footprint:
* Using namespaces and cgroups, CPU and memory overhead is minimized in comparison with VM hypervisor,
* Because VM requires a heavy layer of services to support the same low hardware footprint isolation provided by containers.
2. Envrionment isolation:
* Running containers and it libraries are contained in it, an update to any library in the host OS doesn't affect the version existing in the container.
3. Quick Deployment:
* No underlying OS needs to be installed to support the isolation,
* No services restart is required for it to work
4. Multiple environment deployment:
* Each application has its own environment and its dependencies.
5. Reusability:
* A container image is used to create multple instances of a service in different development cycle.

## What kind of application are not well suited for a containerized environment?
For example applications acessing low-level hardware information, such as memory, file systems, and devices might be unreliable due to container limitations.



# Chapter 1 - Section 2 - Overview of container Architecture
## What and when was the first attempt to apply containerization concept?
In 2001, VServer was the first attempt at running complete sets of processes inside a single server with a high degree of isolation,  
It was the source of the idea of isolated processes which because formalized with the following features:  
- Namespaces: 
* Only processes of a certain namespace can see the allocated resources like network interfaces, PID list, mount points, IPC resources, and the system's host name information    
- cgroups:
* Used to partition processes and their children and limit the allowed resources for them to consume    
- Seccomp:
* Limits how processes could use system calls.
* Defines a security profile for processes that lists the system calls, parameters and file descriptors they are allowed to use.    
- SELinux:
* Used to protect processes from each other and 
* To protect the host from its running processes.    

## What's containerization again?
Containers are processes in the linux kernel making use of its security features to create an isolated environment.  
This environment forbits isolated processes from misusing system or other container resources.    
A common use case of containers is having several replicas of the same service (For example a database server), each replica has isolated resources (filesystem, ports, memory),  
so there's no need for the service to handle resource sharing.  
Isolation guarantees that a malfunctioning or hardmful service does not impact other services or containers in the same host, nor in the underlying system.

## Linux container Architecture
In containerization, a container -which's a process in the perspective of linux kernel- runs an image instead of binary file,  
An image is a file-system bundle that contains all dependencies reuiqred to execute a process ( files in the fs, installed packages, available resources, running processes, and kernel modules).  
Executable files for running processes are like images for running containers (foundation)  
Running containers use an immutable view of the image, allowing multiple containers to reuse the same image simultaneously.  
As images are files, they can be managed by versioning systems, improving automation on container and image provisioning.  

## Where should be the container images?
They need to be locally available for the runtime to execute them, but they are stored in a repo manager like: 
* Red hat container catalog [https://registry.redhat.io/], 
* Red hat Quay [https://quay.io/], 
* hub.docker.com, 
* cloud.google.com/container-registry, 
* aws.amazon.com/ect/

## What's PodMan?
It's an open source tool for managing containers, container images, and interacting with image registries with the following features:
1. Uses image format specified by OCI [www.opencontainers.org]
2. Stores the images in local file-system, doing so avoids unnecessary client/server architecture or having daemons running on local machine.
3. Podman follows docker
4. Compatible with k8s


# Chaptar 1 - Section 3 - Overview of Kubernetes and OpenShift
## What are the limitations of containers?
The work of manually starting growing number of containers rises exponentially, requirements needed in that case are:  
1. Easy communication between large number of services.
2. Resource limits on applications regardless of the number of containers running them.
3. Responses to application usage spikes to increase or decrease running containers.
4. Reaction to service deterioration (Becoming worse)
5. Gradual roll-out (Introduce) of new release to a set of users.  
That's why enterprises require container orchestration technology.


## What's K8s?
It's an orchestration service that simplifies the deployment, management, and scaling of containerized applications.  

## What's the pod?
It's the smallest unit manageable in K8s,  
It consists of one or more containers with their storage resources and IP address that represent a single application.  
K8s also uses pods to orchestrate the containers inside it and to limit its resources as a single unit.

## What are K8s features?
1. Service discovery (DNS) and load balancing
2. Horizontal scaling manually/automatically, CLI/WebUI, what's the difference between horizontal and vertical scaling?
* Horizontal scaling: adding additional nodes
* Vertical scaling: adding more power to your current machines
3. Self-healing: Using user-defined health checks to monitor pods to restart and reschedule them in case of failure.
4. Automated rollout: Making sure upgrade is done smoothely without a down time that may result from failure.
5. Secrets and configuration management
6. Operators: Packaged kubernetes applications  

## What's RHOCP (OpenShift)?
Red Hat OpenShift Container Platform is a set of modular components and services built on top of a k8s container infrastructure.  
It adds the capabilities to provide a production PaaS platform such as:  
* Remote management
* Multitenancy
* Increased security
* Monitoring
* Auditing
* Application life-cycle management
* Self-service interfaces for developers

## What's the underlying operating system of OpenShift hosts?
Beginning with Red Hat OpenShift v4, hosts in an OpenShift cluster all use Red Hat Enterprise Linux CoreOS as the underlying os.

## What are OpenShift features added to K8S?
1. Integrated developer workflow:
- Built-in container registry
- CI/CD pipelines
- S2I "Source to Image": A tool to build artifacts from source repositories to container images
2. Routes: Exposing services to the outside world
3. Metrics and logging: Including a built-in and Self-analyzing metrics service and aggregated logging
4. Unified UI: Manage different capabilities from a unified UI.


# Chapter 2: Creating Containerized Services
# Chapter 2 - Section 1: Provisioning Containerized Services
## How to find available images from remote or local registries in podman?
`podman search rhel`

## How to pass the entry point to podman while running a new container?
`podman run ubi8/ubi:8.3 echo 'Hello world!'`

## How to get the port mapping of the containers?
`podman port -l`

## How to test the availability of the httpd server in terminal?
`curl http://0.0.0.0:44389`

## Note
Most Podman subcommands accept the -l flag (l for latest) as a replacement for the container id. This flag applies the command to the latest used container in any Podman command.

## How to set a container name while creating it in podman?
`--name`

## How to inject environment variables into a podman container?
`-e`

## How to run a container and print its environment variables?
`podman run -e GREET=Hello -e NAME=RedHat ubi8/ubi:8.3 printenv GREET NAME`

## What is Red Hat Container Catalog?
- It's a repository that Red Hat maintains its finely-tuned container images,   
- It has a layer of protection and reliability against known vulnerabilities that could potentially be caused by untested images.  
- the standard podman command is compatible with it  
- It gives access to the errata documentation for an image.

## What's the health index grade?
It indicates how current an image is,  
And whether it contains the latest security updates.  
It could be A

## How to access the Red Hat Container Catalog?
`catalog.redhat.com`

## How to verify the podman containers available?
`podman ps --format "{{.ID}} {{.Image}} {{.Names}}"`

# Chapter 2 - Section 2: Using Rootless Containers
## What are rootless containers?
They are a new concept of containers that do not require root privileges to run.  
It has a lot of advantages like:  
- Run a code with root privileges, without having to run as the host's root user.
- An attacker the compromises the container engine won't gain root privileges on the host.
- Allows multiple unprivileged users to run containers on the same machine.
- Allows isolation inside nested containers
## What are nested containers?
A nested container is a new Container object that still retains access to the parent container that created it so that it can efficiently share registrations, policies, and cached build plans. You can, however, register services into the nested container that override the parent container.

## What are the disadvantages of rootless container?
* Dropped capabilities: You cannot use overlay networks to distribute containers between multiple Docker hosts.
* Binding to ports less than 1024: You cannot map containers to privileged host ports (those below 1024), which means you may need a proxy in front of your system.
* Volume mounting other content: there are limits to which storage drivers you may use for managing the images and containers on your system.

## What're user namespaces and how containers use them?
User namespaces is a Linux feature that allows to map users in the container to different users in the host. Furthermore, the capabilities granted to a pod in a user namespace are valid only in the namespace and void outside of it.  
Containers use linux namespaces to isolate themselves from the host on which they run.  
In particular, the user namespace is used to make containers rootless, this namespace maps user and group IDs so that a process inside the namespace might appear to be running under a different ID.  
Rootless containers use the user namespace to make application code appear to be running as root, however from the host's perspective, permissions are limited to those of a regular user.  
If an attacker manages to escape the user namespace onto the host, then it will have only the capabilities of a regular, unprivileged user.

## How does networking work in containers?
To allow proper networking inside a container, a Virtual Ethernet device is created, this poses a problem for rootless containers because only a real root user has the privileges to create this and similar devices.  
On a rootless container, networking is usually managed by Slirp.  
It works by forking into the container's user and network namespaces and creating a tap device that becomes the default route, then it passes the device's file descriptor to the parent, who runs in the default network namespace and can now communicate with both the container and the Internet.

## What's Slirp???
It's a technique to translate Ethernet packets to unprivileged TCP/IP socket syscalls. Widely used by virtual machine implementations such as QEMU and Rootless Container implementations.  
`https://mcastelino.medium.com/slirp4netns-how-does-it-work-5c0bd31200ce`

## What's a tap device???
It's a virtual interface created by the Child process of the slirp clone to limit the data communication between the container and the host


## How does storage work in containers?
Container engines use a special driver called Overlay2 (or Overlay) to create a layered file system that is efficient in both capacity and performance.  
This cannot be done with rootless containers, becaulse most linux distributions do not allow mounting overlay file systems in user namespaces.  
So the solution is to create a new storage driver, the FUSE-OverlayFS is a user-space implementation of Overlay, which is more efficient than the VFS storage driver user before and can run inside user namespaces.

# Chapter 3: Managing Containers
# Chapter 3 - Section 1: Managing the Lifecycle of Containers:
## Draw a figure that shows a summary of the commonly used podman subcommands that manage the container and container image lifecycle.
xdg-open Pictures/Screenshot_20221202_091706.png 
## Draw a figure that shows a summary of podman commands to query information from containers and images.
xdg-open Pictures/Screenshot_20221202_093419.png

## How to create a named podman container?
`podman run -d -p 8080:8080 --name karam-web registry.redhat.io/rhel8/httpd-24`

## What's the container entry point?
It's the command to run to start the containerized process.  

## How could we override the entrypoint?
By entring the required command after the name of the image  
`podman run registry.redhat.io/rhel8/httpd-24 ls /tmp`  
This wouldn't start the httpd service

## How to start an interactive bash shell in a container while creating it?
`podman run -it registry.redhat.io/rhel8/httpd-24 /bin/bash`  
The -it enables terminal redirection for interactive text-based programs  
The -t option allocates a pseudo-tty (a terminal) and attaches it to the standard input of the container.  
The -i option keeps the container's standard input open, even if it was detached, so the main process can continue waiting for input.  

## How to run a command in a container (Starting an additional process)?
`podman exec ContainerID/ContainerName cat /etc/hostname`

## What're the use cases for running commands in container?
* Executing an interactive shell in an already running container.
* Running processes that update or display the container's files.
* Starting new background processes inside the container.

## How to run a command in a container without mentioning its id or name?
`podman exec -l cat /etc/hostname`  
This runs the command on the last remembered container created

## Note
Podman does not discard stopped containers immediately. Podman preserves their local file systems and other states for facilitating postmortem analysis.

## How to stop/kill a container?
* using `podman stop` is easier than finding the container start process on the host OS and killing it.
* using `podman kill` sends Unix signals to the main process in the container, if no signal is specified, it sends the `SIGKILL` signal, terminating the main process and the container.  
`podman kill karam-web`  
`podman kill -s SIGKILL karam-web`  
podman accepts either the signal name or number ===> SIGHUP or 1

## How to restart a container?
`podman restart karam-web`, it creates a new container with the same container ID, reusing the stopped container state and file system.

## What's the option for applying podman command on all containerS?
`-a`

## How to review the logs of a podman container?
`podman logs containerName`

## How to copy files to a container?
`podman cp FileName ContainerName:PathRequired`  
`podman cp db.sql mysql:/`

## How to add the db file to the mysql database?
`podman exec mysql /bin/bash -c 'mysql -uuser1 -pmypa55 items < /db.sql'

## How to list contents of a table in a database?
`podman exec mysql /bin/bash -c  'mysql -uuser1 -pmypa55 -e "select * from items.Projects;"'`


# Chapter 3 - Section 2: Attaching Persistent Storage to Containers
## Note:
Previously in this course, container images were characterized as immutable and layered, meaning that they are never changed, but rather composed of layers that add or override the contents of layers below.  
A running container gets a new layer over its base container image, and this layer is the container storage.

## How to configure a host directory to avoid information leakege between the host system and the applications running inside containers?
```
mkdir /home/student/dbfiles
podman unshare chown -R 27:27 /home/student/dbfiles
sudo semanage fcontext -a -t container_file_t \
'/home/student/dbfiles(/.*)?'
sudo restorecon -Rv /home/student/dbfiles
```

## How to mount a host directory into a container?
`podman run -v /home/student/dbfiles:/var/lib/mysql rhmap47/mysql`  
In this command, if the /var/lib/mysql already exists inside the mysql container image,  
the /home/student/dbfiles mount overlays, but does not remove, the content from the container image.  
If the mount is removed, the original content is accessible again.

## How to verify the SELinux context type of a directory?
`ls -ldZ DirectoryName`

## What's the `podman unshare` command?
The podman unshare command provides a session to execute commands within the same user namespace as the process running inside the container.
podman unshare lets you run a command in the same user namespace as your containers. podman unshare runs a command in Podman's modified user namespace. It's intended to be run with rootless podman (where you run podman as a non-root user).

# Chapter 3 - Lesson 3: Accessing Containers
## How to make a container externally accessible?
By adding `-p [<IP address>:][<host port>:]<container port>` to the `podman run` command  
`-p 8080:8080` means any request to port 8080 on the host is forwarded to port 8080 within the container.  
`-p 127.0.0.1:8081:8080` limits external access to the container to requests from localhost to host port 8081  
If a port is not specified for the host port, Podman assigns a random available host port for the container:
`podman run -d --name apache3 -p 127.0.0.1::8080 registry.redhat.io/rhel8/httpd-24`  
To see the port assigned by Podman, use the podman port <container name> command:  
`podman port apache3`  
`curl -s 127.0.0.1:35134 | egrep '</?title>'`  
If only a container port is specified with the -p option, then a random available host port is assigned to the container. Requests to this assigned host port from any IP address are forwarded to the container port.
`podman run -d --name apache4 -p 8080 registry.redhat.io/rhel8/httpd-24`  
`podman port apache4`


## How to access the database in a container with port forwarding `13306:3306`?
## How to load databases into a server?
`mysql -uuser1 -h 127.0.0.1 -pmypa55 -P13306 items < /home/student/DO180/labs/manage-networking/db.sql`



# Chapter 4: Managing Container Images
# Chapter 4 - Section 1: Accessing Registeries
## How to configure registries for the podman command?
`/etc/containers/registries.conf`
For secured registries:  
```
[registries.search]
registries = ["registry.access.redhat.com", "quay.io"]
```   
They by default use the port number 5000 if not specified
But for insecured:  
```
[registries.insecure]
registries = ['localhost:5000']
```


## How to access images registries?
1. Using commands
2. Using APIs

## How using commands?
`podman search [OPTIONS] <term>`  
Options are limit, filter, tls-verify, list-tags

## How using Resitry HTTP API?
To list all repositories available in a registry, use the /v2/_catalog endpoint. The n parameter is used to limit the number of repositories to return:
```
curl -Ls https://myserver/v2/_catalog?n=3
{"repositories":["centos/httpd","do180/custom-httpd","hello-openshift"]}
```
If Python is available, use it to format the JSON response:
```
curl -Ls https://myserver/v2/_catalog?n=3 \
| python -m json.tool
```
The /v2/<name>/tags/list endpoint provides the list of tags available for a single image:
```
curl -Ls \
https://quay.io/v2/redhattraining/httpd-parent/tags/list \
| python -m json.tool
```
## Note
Quay.io offers a dedicated API to interact with repositories beyond what is specified in Docker Repository API. See https://docs.quay.io/api/ for details.

## Note
The registry HTTP API requires authentication credentials. First, use the Red Hat Single Sign On (SSO) service to obtain an access token:  
`curl -u username:password -Ls "https://sso.redhat.com/auth/realms/rhcc/protocol/redhat-docker-v2/auth? service=docker-registry"`  

Then, include this token in a Bearer authorization header in subsequent requests:  
`curl -H "Authorization: Bearer eyJh...mgL4" -Ls https://registry.redhat.io/v2/rhel8/mysql-80/tags/list | python -mjson.tool`  


## Note
Red Hat recommends always including the regitry name to prevent accidental use of unexpected images.

## Where does podman store container images?
In `/var/lib/containers/storage/overlay-images`

# Chapter 4 - Section 2: Manipulating Container Images
## How could we transfer a new container image to another host?
1. Save the container image to a .tar file  
2. Publish (push) the container image to an image registry
3. podman commit
4. Containerfiles
## How to save a container image to a .tar file?
Generating a tar archive contains image metadata and preserves the original image layers  
`podman save [-o FileName] ImageName[:Tag]`  
`podman save -o mysql.tar registry.redhat.io/rhel8/mysql-80`  
Podman sends the generated image to the standard output as binary data. To avoid that, use the -o option.  
## How to use the .tar files generated by the save command?
`podman load [-i FileName]
## Note
To save disk space, compress the file generated by the save subcommand with Gzip using the --compress parameter. The load subcommand uses the gunzip command before importing the file to the local storage.

## How to save the layers of a container to create a new container image?
`podman commit` command provides this feature  
`podman commit [OPTIONS] CONTAINER [REPOSITORY[:PORT]/]IMAGE_NAME[:TAG]`  
## Warning
Even though the podman commit command is the most straightforward approach to creating new images, it is not recommended because of the image size (commit keeps logs and process ID files in the captured layers), and the lack of change traceability. A Containerfile provides a robust mechanism to customize and implement changes to a container using a human-readable set of commands, without the set of files that are generated by the operating system.

## How to identify which files were changed, created, or deleted since the container was started?
Using the `diff` command, it requires container name or ID  
```
podman diff mysql-basic
C /run
C /run/mysqld
A /run/mysqld/mysqld.pid
A /run/mysqld/mysqld.sock
A /run/mysqld/mysqld.sock.lock
A /run/secrets
```
The diff subcommand tags any added file with an A, any changed ones with a C, and any deleted file with a D.

## Important Note
The diff command only reports added, changed, or deleted files to the container file system.  Files that are mounted to a running container are not considered part of the container file system.  To retrieve the list of mounted files and directories for a running container, use the podman inspect command:  
`podman inspect -f "{{range .Mounts}}{{println .Destination}}{{end}}" CONTAINER_NAME/ID`  
Any file in this list, or file under a directory in this list, is not shown in the output of the podman diff command.  

## How To commit the changes to another image?
`podman commit mysql-basic mysql-custom`  
This command creates a new image nmed mysql-custom.

## Note
Because multiple tags can point to the same image, to remove an image referred to by multiple tags, first remove each tag individually.

## Another Note
multiple tags are provided to minimize the need to remember the latest release of a particular version of a project. Thus, if there is a project version release, for example, 2.1.10, another tag named 2.1 can be created pointing to the same image from the 2.1.10 release. This simplifies pulling images from the registry.

## How to push an image to its repository?
`podman push [OPTIONS] IMAGE [DESTINATION]`  
`podman push quay.io/bitnami/nginx`


# Chapter 5: Creating Custom Container Images
# Chapter 5 - Section 1: Designing Custom Container Images
## What're the problems of using the technique of commiting changes to create custom images?
It doesn't follow best software practicies, like maintainability, automation of building and repeatability.

## What're the advs of using Containerfiles as an alternative to committing changes?
1. Easy to share
2. Easy to Version control
3. Easy to Reuse
4. Easy Extent: to get a child image from another one called parent, the child image incorporates everything in the parent image and all change and additions made to create it.

## What're the scenarios creating a child image could be used in?
1. Add new runtime libraries, such as database connectors/
2. Include organization-wide customization such as SSH certificates and authentication providers.
3. Add internal libraries to be shared as a single image layer by multiple container images for different applications.
4. Trim the container image by removing unused material (Such as man pages, or documentation found in /usr/share/doc)
5. Lock either the parent image or some included software package to a specific release to lower risk related to future software updates.

## What are the available sources of container images?
1. Parent images
2. Containerfiles from Docker Hub or Red Hat Software Collections Library (RHSCL).

## How to use RHSCL?
* It's redhat solution for developers who require the latest development tools that usually do not fit the standard RHEL release schedule.

## What is a Backport? 
Backporting is when a software patch or update is taken from a recent software version and applied to an older version of the same software. A backport is most commonly used to address security flaws in legacy software or older versions of the software that are still supported by the developer.

## Notes
In RHEL, security and performace fixes are backported from later upstream releases, but new features that would break backwards compatibility are not backported.  
RHSCL allows software developers to use the latest version without impacting RHEL, because RHSCL packages do not replace or conflict with default RHEL packages.  
Default RHEL packages and RHSCL packages are installed side by side.  
All RHEL subscribers have access to the RHSCL. To enable a particular software collection for a specific user or application environment (for example, MySQL 5.7, which is named rh-mysql57), enable the RHSCL software Yum repositories and follow a few simple steps.

## How to get Containerfiles from RHSCL?
From the rhscl-dockerfiles package available from the RHSCL repository.  
Community users can get Containerfiles for CentOS-based equivalent container images from GitHub's repository at `https://github.com/sclorg?q=-container`.

## Good Note
Many RHSCL container images include suuport for S2I, best known as an OpenShift Container Platform feature.  
Having support for S2I doesn't affect the use of these container images with docker.

## What's the makefile written in?
It's written in C

## To build a Python image from scratch?
clone the s2i repository, edit it if some change is required, and run the `make build` command

## What's RHCC?
It's one source of container images  
It's Red Hat Container Catalog, it's the red hat repository of reliable, tested, certified and curated collection of container images built on version of RHEL and related systems.  
`https://catalog.redhat.com/software/containers/explore`

## Another advanced source of images
`Quay.io/search`

## Another source is Docker Hub
Docker Hub includes images by anyone, which should be tested individually to make sure about its security and quality  
`https://hub.docker.com/_/mysql`  
This's the official image of mysql on Docker Hub.  
In the documentation, under the supported tags and respective Dockerfile links section, each of the tags points to the docker-library GitHub project,  
Which hosts Containerfiles for images built by the Docker community automatic build syste.  
The direct URL for the Docker Hub MySQL 8.0 Containerfile tree is:  
`https://github.com/docker-library/mysql/blob/master/8.0`  


## How to use the OpenShift Source-to-Image tool?
It's an alternative to using Containerfiles to create new container images that can be used either as a feature from OpenShift or as standalone s2i utility.  
It allows developers to work using their usual tools, instead of learning Containerfile syntax and using os commands such as yum.  
It usually creates slimmer images with fewer layers.  

## What's the process of S2I to build a custom container image for an application?
1. Starting a container from a base container image called the builder image,  
This image includes a programming language runtime and essential developement tools, such as compilers and package managers.  
2. Fetch the application source code, usually from a Git server, and send it to the container.
3. Build the application binary files inside the container.
4. Save the container, after some clean up, as a new container image, which includes the programming language runtime and the application binaries.

## Tell me more about the builder image
It's a regular container image following a standard directory structure and providing scripts that are called during the S2I process.  
Most of these builder images can also be used as base images for Containerfiles, outside the S2I process.

## How to use the S2I utility?
It could be used outside of OpenShift, in a Docker-only environment.  
It can be installed on a RHEL system from RPM package, and on other platforms, including Windows and Mac OS, from the installers available in the S2I project on GitHub.

# Chapter 5 - Section 2: Building Custom Container Images with Containerfiles
## How to build a container image from Containerfile?
1. Create a working directory
2. Write the Containerfile
3. Build the image with Podman

## What's that working directory?
It's a directory containing all files needed to build the image.

## How to write a Containerfile?
It's a file named either Containerfile or Dockerfile  
Its statements are of the form `INSTRUCTION arguments`  
Instructions are not case-sensitive, but the convention is to make instructions all uppercase to improve visibility.

## Note:
Each Containerfile instruction runs in an independent container using an intermediate image built from every previous command.  
This means each instruction is independent from other instructions in the Containerfile.

## What's the `EXPOSE` Instruction in the Containerfile?
It indicates that the container listens on the specified network port at runtime, it only defines metadata, it doesn't make ports accessible from the host.  
The `-p` option in the `podman run` command exposes container ports from the host.

## What's the difference between `ADD` and `COPY` instructions?
They both copy files from working directory, but `ADD` command copies files or folders from a local or remote source, which the COPY is limited to just local files, can't use URLs.
Also ADD command has the functionality to unpack recognized compression format files (Identity, gzip, bzip2 or xz)

## What shell does the `RUN` command uses?
`/bin/sh`

## What's the `USER` Instruction?
It specifies the username or the UID to use when running the container image for the `RUN`, `CMD`, `ENTRYPOINT` Instructions.  
It's a good proctice to define a different user other than root for security reasons.

## What's the difference between `ENTRYPOINT` and `CMD` instructions?
`ENTRYPOINT` specifies the default command to execute when the image runs in a container.  
If omitted, the default ENTRYPOINT is `/bin/sh -c`  
`CMD` provides the default arguments for the ENTRYPOINT instruction.  
If the default `ENTRYPOINT` applies `/bin/sh -c`, then `CMD` forms an executable command and parameters that run at container start
```
ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-D", "FOREGROUND"]
```

## What are the two formats of CMD and ENTRYPOINT?
1. Exec form: Using a JSON array
```
ENTRYPOINT ["command", "param1", "param2"]
CMD ["param1", "param2"]
```
2. Shell form
```
ENTRYPOINT command param1 param2
CMD param1 param2
```

## Note
The Containerfile should contain at most one ENTRYPOINT and one CMD instruction. If more than one of each is present, then only the last instruction takes effect.


## Important Note
Podman can override the CMD instruction when starting a container. If present, all parameters for the podman run command after the image name form the CMD instruction.

## Important
Both the ADD and COPY instructions copy normal files, with root as the owner. The ADD instruction retrieves the contents of the URL and the file is copied with root as the owner. The ADD instruction extracts the tar archive and preserve the owner and permissions.
You can use the --chown=<user>:<group> option with the COPY or ADD command to set the desired owner or use a RUN instruction after the copy to set the owner and permissions.

## Note
Red Hat recommends minimizing the number of layers. You can achieve the same objective by creating a single layer image using the && conjunction in the RUN instruction.  
Use the \ escape code to insert line breaks and improve readability. You can also indent lines to align the commands  

## What are the commands create new image layer?
RUN, COPY, and ADD instructions create new image layers

## What instructions accept multiple parameters in the Containerfile?
`LABEL` and `ENV`

## How to build images with Podman?
`podman build -t NAME:TAG DIR`

## Check this [link](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) for Best practices for writing Dockerfiles

# Chapter 6: Deploying Containerized Applications on OpenShift
# Chapter 6 - Section 1: Describing Kubernetes and OpenShift Architecture
## Why is it named kubernetes or k8s?
The name Kubernetes originates from Greek, meaning helmsman or pilot.  K8s as an abbreviation results from counting the eight letters between the "K" and the "s". 
## What's one advantage of k8s?
It uses several nodes to ensure the resiliency and scalability of its managed applications.  
K8s forms a cluster of node servers that run containers and are centrally managed by a set of control plane servers.  
A server can act as both a control plane node and a compute node, but those roles are usually separated for increased stability.

## What's a Resource in k8s?
It's any kind of component definition managed by K8s.  
Resources contain:  
The configuration of the managed component (for example, the role assigned to a node),  
And the current state of the component (for example, if the node is available).


## What's the Controller in K8s?
It's a k8s process that watches resources, and mkaes changes attempting to move the current state towards te desired state.

## What's a label?
It's a key-value pair that can be assigned to any k8s resource.  
Selectors use labels to filter eligible resources for scheduling and other operations.

## What're operators?
Operators are k8s plug-in components that can react to cluster events and control the state of resources.  

## What's RHOCP?
It's a set of modular components and services built on top of Red Hat CoreOS and K8s.  
RHOCP adds PaaS capabilities such as:  
* Remote management,
* Increased security,
* Monitoring and autiting,
* Application lifecycle management, 
* And self-service interfaces for developers.  
An OpenShift cluster is a k8s cluster that can be managed the same way, but using the management tools provided by OpenShift such as:  
* Command-line interface
* Web console  
This allows for more productive workflows and makes common tasks much easier.

## What's an Infra Node in OpenShift?
It's a node server containing infrastructure services like:
* Monitoring,
* Logging,
* External routing

## A console
A web UI provided by the RHOCP cluster that allows developers and administrators to interact with cluster resources.

## A project
OpenShift extension of Kubernetes' namespaces.  
Allows the definition of user access control (UAC) to resources.

## Draw the OpenShift Container Platform stack:
`xdg-open ~/Pictures/Screenshot_20221204_080902.png`  
* Container optimized OS: the base OS is Red Hat CoreOS, Which's a linux distribution focused on providing an immutable operating system for container execution.
* Container runtime: CRI-O is an implementation of the k8s container runtume interface (CRI) to enable using OCI compatible runtimes,  
CRI-O can use any container runtime that satisfies CRI:  
`runc` ==> Used by the docker service  
`libpod` ==> used by podman  
`rkt` ==> from CoreOS
* Kubernetes (Container orchestration and management): manages a cluster of hosts, physical or virtual, that run containers.  
It uses resources that describe multicontainer applcations composed of multiple resources, and how they interconnect



























































































































































## What's podman unshare command?

## What's tap device?

## What's slirp?

## What are namespaces and how they work?

## How SELinux work?
