---
title: "SledRE Documentation"
draft: false
---

# SledRE

[SledRE](https://github.com/sledre/sledre) is a scalable application for Windows malware analysis. It allows to run multiples jobs in parallels.
At the moment, two jobs are availables:
- [PESieve](https://github.com/hasherezade/pe-sieve): this job goal is to unpack a Windows PE malware using PESieve.
- [Detours](https://github.com/microsoft/Detours): this job goal is to hook and trace syscalls of Windows PE malware (more than a thousands common syscalls). Theses traces can be used to create artificial intelligence models. But they can also be directly imported to Ghidra to help reverse engineers.   

## Main features
* Windows 7 sandbox using qemu and Linux containers
* Automated installation using a script to build the VM with required binaries
* Scalability of the Windows workers dependaning on the host resources
* Windows syscall hooking to generate traces
* Malware unpacking using PESieve
* Tag creation based on hook traces
* Dataset generation
* Ghidra extension to import SledRE traces


## Architecture

![SledRE Architecture](/images/SledREArchi.png?height=600px)


## Contribution

Feel free to contribute to this project. Everything is available on [SledRE Organization](https://github.com/sledre).