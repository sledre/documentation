---
title: "Installation"
date: 2021-09-12T12:45:53+02:00
draft: false
weight: 15
---

### Prerequisites
The first step is to download the latest [SledRE Release](https://github.com/sledre/sledre/releases)
`wget https://github.com/sledre/sledre/releases/download/vX.X.X/SledRE-X.X.X.zip`

Then you can unzip the release and setup a **virtualenv**:  
```properties
unzip SledRE-X.X.X.zip
cd SledRE-X.X.X
python3 -m pip install --user virtualenv
python3 -m venv venv
source venv/bin/activate
```

Now, it's time to install python dependencies needed by the installation script:  
`python3 -m pip install -r requirements.txt`

### Installation

This step is now fully automated. Just run the following command:  
`python3 setup.py -w <number of workers>`  
The number of workers represent the number of QEMU Windows 7 VMs (1 CPU, 1GB of memory) running in parallel.  
An higher number will make simultaneous analysis faster but will also increase the resources consumption.  

This script will take some time to finish since it is doing the following steps for you:
* Cleaning the directories ;
* Downloading, uncompressing and converting a Windows 7 VM from Microsoft repository ;
* Creating a QEMU container able to run the Windows VM ;
* Configuring the VM and installing needed files dependacies through SSH ;
* Rebooting the VM since it's  needed by some compoenents (.Net Framework for example) ;
* Making an external snapshot of the VM with the SledRE Agent runnning ;
* Creating a *.env* file.

### Running
You may now run the project using **docker-compose**:  
`docker-compose -p sledre -f docker-compose.yml up -d`  
The first run will take longer since it is downloading all the images.