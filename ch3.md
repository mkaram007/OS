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
