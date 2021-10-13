---
title: "Requirements"
date: 2021-09-12T12:39:51+02:00
draft: false
weight: 10
---

### Introduction
In order to work, **SledRE** requires the following components:
- python3
- pip3
- Docker
- docker-compose
- qemu-utils

### Python3 & pip3
Python3 and pip3 are needed to run the installation script.  
{{% notice info %}}
It is also recommend to use a virtualenv to avoid any conflict.
{{% /notice %}}

### Docker
**SledRE** project is packaged and deployed using Docker. 
You can follow this [link](https://docs.docker.com/get-docker/) to install Docker.  

{{% notice note %}}
We'll soon support podman. We believe that it is a strong alternative to Docker since it is able to easily run in rootless mode (improving protection for the sandbox).
{{% /notice %}}

### docker-compose
You can easily install docker-compose using pip:  
`sudo pip install docker-compose`

Or if you are not using virtualenv:  
`pip install docker-compose`


### KVM
KVM is used to drastically improve QEMU performances so the Windows 7 workers are running faster and smoother.  
So you'll need a recent CPU (with hardware virtualization such as Intel VT-x or AMD-V) and a kernel version higher than 2.6.20.

### QEMU binutils
The installation script has to convert an ova to a qcow2 format. In order to do that, the package `qemu-utils` is needed.  
On Debian systems, you can use the following command:  
`sudo apt update && sudo apt install qemu-utils`