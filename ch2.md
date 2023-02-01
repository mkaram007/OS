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
