# **How to install Docker and Almalinux9 on Windows** 
---

## **Introduction**
The goal of this guide is to explain how to install Docker on Windows and how to install and run an Almalinux 9 container thanks to it.

[Docker](https://en.wikipedia.org/wiki/Docker_(software)) is an OS-virtualization based open-source software that allows to install and run applications in isolated environments called **containers**, which are faster and lighter with respect to a traditional Virtual Machine. We will use it to install and run an [Almalinux9](https://en.wikipedia.org/wiki/AlmaLinux) container.
## **Preliminaries: installing Windows Subsystem for Linux (WSL)**
In order to work, Docker requires a _Linux-compatible environment_. Thus, before installing Docker, we need to install **Windows Subsystem for Linux (WSL)** from the terminal:
1. Open the terminal.
2. Install WSL with the following command:
```
wsl --install
```
3. Set the default version of WSL to 2:
```
wsl --set-default-version 2
```

## **Installing Docker**


## **Running an Almalinux 9 container**
