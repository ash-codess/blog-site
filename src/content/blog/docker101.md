---
author: Ash
pubDatetime: 2023-02-22T1:20:00Z
title: Docker 101
postSlug: docker 101
featured: true
draft: false
tags:
  - cloud
ogImage: ""
description: DOCKER 101
---

# DOCKER

I started learning docker this week and here are some of my notes. So first let's get some definitions straight before we proceed.

<details>
  <summary> What are containers?</summary>
 
<br />
A container is a lightweight, standalone executable package that contains everything needed to run an application. It is built from an image, which is a static snapshot of a containerized application and its dependencies. <br/>
Containers provide an isolated environment for an application to run, allowing it to be deployed and run consistently across different environments, such as development, testing, and production. Containers can be quickly and easily deployed, scaled, and managed, making them a popular choice for modern application development and deployment.

 </details>

<br>

<details>
<summary> Virtual machine Vs Containers</summary>
 
 <br/>
 Virtual machines (VMs) and containers are both technologies used to create isolated environments for applications to run in, but they differ in their approach and the resources they require.
 A virtual machine is a software emulation of a physical machine that runs on top of a host operating system. It creates a complete virtualized environment with its own operating system, hardware resources, and network interface. Each virtual machine is isolated from the host system and other virtual machines running on the same host. <br>
 Containers, on the other hand, are lightweight and share the same host operating system as the host machine. Containers are created from a base image, which includes the application and its dependencies, and run as isolated processes on the host. Each container has its own file system and network interface, but shares the same kernel and operating system as the host.<br>One of the main advantages of containers over virtual machines is their lightweight nature. Containers can be spun up and down quickly, and require less memory and disk space than a virtual machine. They also have less overhead, which means that more containers can be run on a single host than virtual machines.
</details>
<br>

<details>
<summary> Hypervisor Vs Docker</summary>
<br>
 A hypervisor, also known as a virtual machine monitor (VMM), is a software program that allows multiple virtual machines to run on a single physical machine. Each virtual machine runs its own operating system and applications, which are completely isolated from other virtual machines running on the same physical machine. The hypervisor provides a layer of abstraction between the virtual machines and the underlying physical hardware.<br>
 Docker, on the other hand, is a containerization platform that allows multiple containers to run on a single host machine. Each container shares the same host operating system, but has its own isolated file system, network interface, and process space. Docker uses operating system-level virtualization to create these isolated containers, which means that each container runs on the same kernel as the host operating system.<br>
 The main difference between a hypervisor and Docker is the level of isolation provided. Hypervisors provide hardware-level isolation between virtual machines, while Docker provides operating system-level isolation between containers. This means that while virtual machines can run completely different operating systems and applications, Docker containers can only run on the same operating system as the host machine. <br>
 Another difference between a hypervisor and Docker is the overhead required to run them. Hypervisors require a significant amount of resources to run, as each virtual machine needs its own operating system and associated software. Docker, on the other hand, has much less overhead, as each container shares the same host operating system and only needs to run the application and its dependencies.
 
 </details>

 <br>
 <details>
<summary>  Image and container</summary>
 An image is a static snapshot of a containerized application and its dependencies. It contains everything needed to run the application, including the application code, libraries, and system tools, as well as any configuration files or environment variables. Images are created from a Dockerfile, which defines the configuration for the image.
 
 Containers, on the other hand, are running instances of an image. When an image is run, it creates a container, which is an isolated environment for the application to run in.
<br>
 Images are created from Dockerfile and are used to create and manage containers.
 </details>

---

### Getting Docker on our system

I am on linux mint machine and here are the steps i followed to get docker on my system.

1. Checking off prerequisite:
   - 64-bit kernel and CPU support for virtualization.
   - KVM virtualization support
   - QEMU must be version 5.2 or newer.
   - Gnome, KDE, or MATE Desktop environment.
   - At least 4 GB of RAM.

For more info: [Guide](https://docs.docker.com/desktop/install/linux-install/#system-requirements)

Check ubuntu version:

- Ubuntu Kinetic 22.10
- Ubuntu Jammy 22.04 (LTS)
- Ubuntu Focal 20.04 (LTS)
- Ubuntu Bionic 18.04 (LTS)

```sh
  cat /etc/*release*
```

My system had jammy

<br>

2. Remove any preinstalled docker image present(if any)

```sh
  sudo apt-get remove docker docker-engine docker.io containerd runc
```

<br>

3. Installing using the convenience script

Note: The convenience script isn’t recommended for production environments, but it’s useful for creating a provisioning script tailored to your needs.

```sh
  curl -fsSL https://get.docker.com -o get-docker.sh
  sudo sh ./get-docker.sh
```

<br>

4. Check docker version to confirm installation

```sh
  sudo docker version
```

5. Extra step to check if everything is working fine

we will go to docker hub and run test an image

```sh
  sudo docker run docker/whalesay cowsay yay:D
```
   You should see something like this: <br>
   ![blog-docker](https://user-images.githubusercontent.com/123767474/220609847-8ef50152-9e92-4ef4-b47e-beda4ff8e7c5.png)

   
---

## Basic docker commands

| Commands                      | Usage                                | Example             |
| ----------------------------- | ------------------------------------ | ------------------- |
| docker run [image-name]       | To run image                         | docker run nginx    |
| docker ps                     | To list containers which are running | -                   |
| docker ps -a                  | To list all the containers           | -                   |
| docker stop [image-name/id]   | To stop an image                     | docker stop nginx   |
| docker rm [image-name/id]     | To remove container                  | docker rm nginx     |
| docker rmi [image-name/id]    | To remove an image                   | docker rmi nginx    |
| docker pull [image-name]      | To pull image from docker hub        | docker pull nginx   |
| docker run -d [image-name/id] | To run container in detached mode    | docker run -d nginx |

---
