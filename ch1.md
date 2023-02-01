# Chapter 1: Introducting Container Technology 29-11-2022 10:36:26
# Chapter 1 - Section 1 - Overview of container technology:
## What's a container?
* It's a set of one or more processes that are isolated from the rest of the system.

## What are the benefits of containers over traditional Servers?
1. Containers provide many of the same benefits as virtual machines, such as security, storage and network isolation.
2. Containers require far fewer hardware resources and are quick to start and terminate.
3. They also isolate the libraries and the runtime resources (such as CPU and storage) for an application to minimize the impact of any OS update to the host OS.
4. It helps with the efficiency, elasticity, and resusability of the hosted applications.
5. Helps with application portability.


## Traditional deployment:  
1. Application's dependencies are closely related to the runtime environment, so an OS may break when any updates or patches are applied to the base OS
2. There's a downtime for an application to have its dependencies upgraded.

## What's the OCI?
* OCI "Open Container Initiative" provides a set of industry standards that define a container runtime specification and a container image specification  
* The image specification defines the format for the bundle of files and metadata that form a container image.  
* When youbuild an application as a container image, which compiles with the OCI standard, you can use any OCI-complicant container engine to execute the application.  
* There are many container engines available to manage and execute individual containers, including Rocket, Drawbridge, LXC, Docker, and Podman.  
* Podman is available in Red Hat Enterprise Linux 7.6 and later, and is used in this course to start, manage, and terminate individual containers.  

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
