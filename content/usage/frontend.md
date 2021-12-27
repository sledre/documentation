---
title: "SledRE"
date: 2021-09-12T12:41:41+02:00
draft: false
weight: 5
---

### Usage
#### Adding a sample
**SledRE** frontend allows malware submission through the **Add a Malware** page.  

![Add a Malware page](/images/frontend/add-malware1.png?classes=border,shadow&height=400px)

There, you can submit a single sample or a folder containing multiples samples.  
The format can be either *Windows PE* or *DLL*. In the case of a DLL, the entrypoint must be provided following the **rundll32.exe** format (because that's the binary being called).  

![Malware submission](/images/frontend/add-malware2.png?classes=border,shadow&height=400px)

A specific label can also be specified and associated to the sample.

Then, clicking on the **Upload** button will submit the samples into **SledRE**. At this point, it is possile to request jobs associated to the submitted samples.

![Malware submission jobs](/images/frontend/add-malware3.png?classes=border,shadow&height=400px)

At the moment, two jobs are availables:
- [PESieve](https://github.com/hasherezade/pe-sieve): this job goal is to unpack a Windows PE malware using PESieve.
- [Detours](https://github.com/microsoft/Detours): this job goal is to hook and trace syscalls of Windows PE malware (more than a thousands common syscalls). Theses traces can be used to create artificial intelligence models. But they can also be directly imported to Ghidra to help reverse engineers.  

You can also specify the analysis time which is 30 seconds by default.  

![Malware analysis submission](/images/frontend/start-analysis.png?classes=border,shadow&height=400px)

#### Malware entries

Samples submitted to **SledRE** are accessible on the **Malware** page. 
It is possible to filter samples by name, status, hash...

![Malware entries](/images/frontend/malware-entry.png?classes=border,shadow&height=60)

The button **Show Details** is used to access samples information and jobs details. The results can be downloaded from there.

![Malware details](/images/frontend/malware-details.png?classes=border,shadow&height=300px)

#### Workers status

The page **Workers** is used to display information regarding the QEMU workers. 

![Workers information](/images/frontend/worker-status.png?classes=border,shadow&height=300px)

#### Datasets

It is possible to generate datasets which is a zip file containing the results of all jobs that have been run.  
The dataset is organized in a tree which subdirectories are defined by the samples sha256 hashs with a depth of 5 bytes.

![Dataset Generation](/images/frontend/dataset-gen.png?classes=border,shadow&height=200)

![Dataset Format](/images/frontend/dataset-format.png?classes=border,shadow&height=700)

#### Rules management

The page **Rules** is used to manage Detours job rules. These rules allow to tag a sample with *Crypto* if it is using cryptographic functions.  
**SledRE** comes with default rules but allow you to edit them or add yours.