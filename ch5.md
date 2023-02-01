
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
