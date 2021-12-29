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
unzip -d sledre SledRE-X.X.X.zip
cd sledre
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
If you wish to allow the Windows VMs internet access (and also LAN access if you don't setup any firewall rules), you can use the `--disable-network-isolation` option.  

This script will take some time to finish since it is doing the following steps for you:
* Cleaning the directories ;
* Downloading, uncompressing and converting a Windows 7 VM from Microsoft repository ;
* Creating a QEMU container able to run the Windows VM ;
* Configuring the VM and installing needed files dependencies through SSH ;
* Rebooting the VM since it's  needed by some components (.Net Framework for example) ;
* Making an external snapshot of the VM with the SledRE Agent running ;
* Creating a *.env* file.

### Running
You may now run the project using **docker-compose**:  
`docker-compose up -d`  
The first run will take longer since it is downloading all the images.


### Known issues
Sometimes if the installation doesn't work on the first time and you try to restart it, you can encounter the following error:
```
[2021-12-29 12:26:44,708] [+] http://localhost:None "POST /v1.41/containers/create?name=sledre_qemu_gen HTTP/1.1" 409 242
Traceback (most recent call last):
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/docker/api/client.py", line 268, in _raise_for_status
    response.raise_for_status()
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/requests/models.py", line 953, in raise_for_status
    raise HTTPError(http_error_msg, response=self)
requests.exceptions.HTTPError: 409 Client Error: Conflict for url: http+docker://localhost/v1.41/containers/create?name=sledre_qemu_gen

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "setup.py", line 519, in <module>
    main(args)
  File "setup.py", line 459, in main
    run_qemu_container(docker_client, snapshot_mode=False)
  File "setup.py", line 322, in run_qemu_container
    client.containers.run(
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/docker/models/containers.py", line 819, in run
    container = self.create(image=image, command=command,
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/docker/models/containers.py", line 878, in create
    resp = self.client.api.create_container(**create_kwargs)
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/docker/api/container.py", line 428, in create_container
    return self.create_container_from_config(config, name)
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/docker/api/container.py", line 439, in create_container_from_config
    return self._result(res, True)
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/docker/api/client.py", line 274, in _result
    self._raise_for_status(response)
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/docker/api/client.py", line 270, in _raise_for_status
    raise create_api_error_from_http_exception(e)
  File "/home/kn0wledge/Downloads/sledre/venv/lib64/python3.8/site-packages/docker/errors.py", line 31, in create_api_error_from_http_exception
    raise cls(e, response=response, explanation=explanation)
docker.errors.APIError: 409 Client Error for http+docker://localhost/v1.41/containers/create?name=sledre_qemu_gen: Conflict ("Conflict. The container name "/sledre_qemu_gen" is already in use by container "e4f713e2d903be17dbaf22a8012f6bea36c8c41ba15281c269a4b405de46e030". You have to remove (or rename) that container to be able to reuse that name.")
```

It means that the container used for the installation has not been stopped. You must stop it manualy (`docker stop sledre_qemu_gen`) before starting the installation again.
