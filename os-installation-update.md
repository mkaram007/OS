# About OpenShift Container Platform installation
* The OpenShift Container Platform installation program offers you flexibility.
* You can use the program to:
- Deploy a cluster on provisioned infrastructure and the cluster it maintains.
- Deploy a cluster on infrastructure that you prepare and maintain
* These two basic types of OpenShift Container Platform clusters are frequently called:
- Installer-provisioned infrastructure clusters.
- User-provisioned infrastructure clusters.

* Both cluster types have the following characteristics:
1. Highly available infrastructure with no single points of failure is available by default.
2. Administrators maintain control over what updates are applied and when.

* The Agent-based Installer is part of the OpenShift Container Platform Installer.
* The installer provides you with the flexibility of user-provisioned infrastructure (UPI) installation and the ease of use of the Assisted Installer (AI).



# About the installation program
* You can use the installation program to deploy both types of clusters.
* The installation program generates main assets such as:
- Ignition config files for the:
1. bootstrap,
2. master,
3. and worker machines.
* You can start an OpenShift Container Platform cluster with these three configurations and correctly configured infrastructure.


## How's the installation parallelized?
* The OpenShift Container Platform installation program uses a set of targets and dependencies to manage cluster installations.
* The installation program has a set of targets that it must achieve, and each target has a set of dependencies.
* Because each target is only concerned with its own dependencies, the installation program can act to achieve multiple targets in parallel with the ultimate target being a running cluster.

## How does the installation program make use of the existing components instead of creating them again?
* The installation program recognizes and uses existing components instead of running commands to create them again because the program meets dependencies.
* os/1.png



# About Red Hat Enterprise Linux CoreOS (RHCOS)
## What OS do the cluster machines use after installation?
* Post-installation, each cluster machine uses Red Hat Enterprise Linux CoreOS (RHCOS) as the operating system.
## What's RHCOS?
* RHCOS is the immutable container host version of Red Hat Enterprise Linux (RHEL)
* and features a RHEL kernel with SELinux enabled by default.
## What tools does RHCOS include?
* It includes the kubelet, which is the Kubernetes node agent,
* and the CRI-O container runtime, which is optimized for Kubernetes.


## Why RHCOS?
* Every control plane machine in an OpenShift Container Platform 4.12 cluster must use RHCOS, which includes:
- a critical first-boot provisioning tool called Ignition.
## What's Ignition tool?
* This tool enables the cluster to configure the machines.
## How updates are delivered to the machines?
* Operating system updates are delivered as an Atomic OSTree repository that is embedded in a container image that is deployed across the cluster by an Operator.
* Actual operating system changes are made in-place on each machine as an atomic operation by using rpm-ostree.
* Together, these technologies enable OpenShift Container Platform to manage the operating system like it manages any other application on the cluster, by in-place upgrades that keep the entire platform up-to-date.
* These in-place updates can reduce the burden (Load) on operations teams.
## What advs of having RHCOS on all machines in the cluster?
* If you use RHCOS as the operating system for all cluster machines, the cluster manages all aspects of its components and machines, including the operating system.
## What would change RHCOS machines in OCP?
* Because of this, only the installation program and the Machine Config Operator can change machines.
## What configures the state of cluster machines?
* The installation program uses:
1. Ignition config files to set the exact state of each machine,
2. Machine Config Operator completes more changes to the machines, such as the application of new certificates or keys, after installation.




# Installation process
* When you install an OpenShift Container Platform cluster, you download the installation program from the appropriate Infrastructure Provider page on the OpenShift Cluster Manager site.
* This site manages:
1. REST API for accounts
2. Registry tokens, which are the pull secrets that you use to obtain the required components
3. Cluster registration, which associates the cluster identity to your Red Hat account to facilitate the gathering of usage metrics

* In OpenShift Container Platform 4.12, the installation program is a `Go` binary file that performs a series of file transformations on a set of assets.
* The way you interact with the installation program differs depending on your installation type.

* For clusters with installer-provisioned infrastructure, you delegate the infrastructure bootstrapping and provisioning to the installation program instead of doing it yourself. The installation program creates all of the networking, machines, and operating systems that are required to support the cluster.
