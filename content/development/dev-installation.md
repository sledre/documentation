---
title: "Development Installation"
date: 2021-09-12T12:46:01+02:00
draft: false
weight: 10
---

### Prerequisites
The first step is to clone the repository using **git** in recursive mode:  
`git clone --recursive https://github.com/sledre/sledre.git`

Then you can setup a **virtualenv**:  
```properties
cd sledre
python3 -m pip install --user virtualenv
python3 -m venv venv
source venv/bin/activate
```

Now, it's time to install python dependencies needed by the installation script:  
`python3 -m pip install -r requirements.txt`

### Agent binaries
Now, you'll need the agent binaries. If you're looking for a specific version or directly modifying and testing the agent, you should compile everything yourself. 
However, if you're not planning to change the agent nor its interactions with the API, you should be fine with the binaries of the last published release.

#### Building the binaries

To do that, you'll need a Windows development environment.

##### Agent
To build the agent, run the following commands:
```properties
cd agent/
nuget restore .
msbuild /m /p:Configuration=Debug /p:Platform=x86 .
cd ..
```

##### Hooking module
To build the hooking binaries based on [Microsoft Detours](https://github.com/microsoft/Detours), run the following commands:
```properties
cd agent/plugins/hooking
nmake
cd ../../..
```

##### Unpacking module
To build the hooking binaries based on [PESieve](https://github.com/hasherezade/pe-sieve), run the following commands:
```properties
cd agent/plugins/unpacking/mal_unpack
mkdir build
cd build
cmake .. -A Win32 -T host=x86
cd ..
cmake --build ./build --config Release
cd ../../../..
```

##### Creating the *bin* directory
The installation script needs a `/bin/` directory at the root of the project containing the binaries that we just built and the static binaries.  
Static binaries such as `7zip` and `dotnetframework` are located in `sledre/agent/bin`.  

Just run the commands below:
```properties
mkdir bin/
cp agent/bin/* bin/
cp agent/SledREAgent/bin/x86/Release/SledREAgent.exe bin/
cp agent/SledREAgent/bin/x86/Release/Newtonsoft.Json.dll bin/
cp agent/plugins/hooking/bin.x86/withdll.exe bin/
cp agent/plugins/hooking/bin.x86/trcapi32.dll bin/
cp agent/plugins/unpacking/mal_unpack/build/Release/mal_unpack.exe bin/
```

#### Downloading the binaries

Just download the latest release and extract the `bin/` directory from the zip file.
{{% notice note %}}
You can also download specific binaries from GithHub actions artifacts.
{{% /notice %}}

### Installing the project in development mode

This last step is now fully automated. Just run the following command:  
`python3 setup.py --dev -w <number of workers>`  
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
`docker-compose -f docker-compose.dev.yml up -d`  
The first run will take longer since it's building all the images.  
The development docker-compose configuration will setup shared volume with the host which will allow hot reloading the frontend and the backend.