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




## What's podman unshare command?

## What's tap device?

## What's slirp?

## What are namespaces and how they work?

## How SELinux work?
