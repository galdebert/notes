# CHECK virtualization support

run `systeminfo`
```
Hyper-V Requirements:      VM Monitor Mode Extensions: Yes
                           Virtualization Enabled In Firmware: No
                           Second Level Address Translation: Yes
                           Data Execution Prevention Available: Yes
```

OR press win+S > "System Information"

```
Hyper-V - VM Monitor Mode Extensions	Yes
Hyper-V - Second Level Address Translation Extensions	Yes
Hyper-V - Virtualization Enabled in Firmware	No
Hyper-V - Data Execution Protection	Yes
```

# enable virtualization in the BIOS

restart
press SUPPR while rebooting

in the bios

> overclock (OC)
  > CPU features
    > SVM mode = enabled

save and reboot

Now press win+S > "System Information"

```
Hyper-V - VM Monitor Mode Extensions	Yes
Hyper-V - Second Level Address Translation Extensions	Yes
Hyper-V - Virtualization Enabled in Firmware	Yes
Hyper-V - Data Execution Protection	Yes
```


# install WSL


install WSL https://docs.microsoft.com/en-us/windows/wsl/install

in a command prompt opened as administrator
```
wsl --install
```

This command will
- enable the required optional components
- download the latest Linux kernel
- set WSL 2 as your default
- install a Linux distribution for you (Ubuntu by default)
  
```
C:\WINDOWS\system32>wsl --install
Installing: Virtual Machine Platform
Virtual Machine Platform has been installed.
Installing: Windows Subsystem for Linux
Windows Subsystem for Linux has been installed.
Downloading: WSL Kernel
Installing: WSL Kernel
WSL Kernel has been installed.
Downloading: Ubuntu
The requested operation is successful. Changes will not be effective until the system is rebooted.
```

restart

Ubuntu is being installed...

Enter new UNIX username
New password

# Best practices for setting up a WSL development environment

https://docs.microsoft.com/en-us/windows/wsl/setup/environment

Once you create a User Name and Password, the account will be your default user for the distribution and automatically sign-in on launch.

This account will be considered the Linux administrator, with the ability to run sudo (Super User Do) administrative commands.

## Update and upgrade packages

`sudo apt update && sudo apt upgrade`


# Set up Windows Terminal

Windows Terminal can run any application with a command line interface. Its main features include multiple tabs, panes, Unicode and UTF-8 character support, a GPU accelerated text rendering engine, and the ability to create your own themes and customize text, colors, backgrounds, and shortcuts.

We recommend using WSL with Windows Terminal, especially if you plan to work with multiple command lines.

https://docs.microsoft.com/en-us/windows/terminal/get-started

# File storage

when storing your WSL project files:
- Use the Linux file system root directory: `\\wsl$\Ubuntu\home\galdebert\Project`
- NOT the Windows file system root directory: `C:\Users\galdebert\Project` or `/mnt/c/Users/galdebert/Project`

- win+S `ubuntu` working dir= `~`
- win+S `wsl` working dir= `/mnt/c/WINDOWS/system32`
- win+S `Windows Terminal` and open new tab Ubuntu, working dir= `/mnt/c/Users/galde`

alternatively

- win+S `Windows Terminal`
- cd ~
- `explorer.exe .`
- opens `\\wsl$\Ubuntu\home\galdebert`


# Set up VS Code for editing and debugging

https://docs.microsoft.com/en-us/windows/wsl/setup/environment#set-up-vs-code-for-editing-and-debugging




# Set up remote development containers with Docker

https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers

WSL 2 now runs on a Linux kernel with full system call capacity, Docker can fully run in WSL 2. This means that Linux containers can run natively without emulation, resulting in better performance and interoperability between your Windows and Linux tools.

Download **Docker Desktop for Window**  and follow the installation instructions.
https://docs.docker.com/desktop/windows/wsl/




# performance accross file systems with bad with WSL 2






# Docker Desktop WSL 2 backend

https://docs.docker.com/desktop/windows/wsl/


## develop-with-docker-and-wsl-2

https://docs.docker.com/desktop/windows/wsl/#develop-with-docker-and-wsl-2

The following section describes how to start developing your applications using Docker and WSL 2. We **recommend that you have your code in your default Linux distribution** for the best development experience using Docker and WSL 2. After you have enabled WSL 2 on Docker Desktop, you can **start working with your code inside the Linux distro and ideally with your IDE still in Windows**. This workflow can be pretty straightforward if you are using **VSCode**.

Open VSCode and install the **Remote - WSL extension**. This extension allows you to work with a remote server in the Linux distro and your IDE client still on Windows.

open your terminal and type:
```
wsl
code .
```
or
```
win+S ubuntu
code .
```
This opens a **new VSCode connected remotely to your default Linux distro** which you can check in the bottom corner of the screen.





# The Getting Started project

is a simple GitHub repository which contains everything you need to build an image and run it as a container.

## get git using the docker container `alpine/git`

and run git to clone a repository

```
docker run --name repo alpine/git clone https://github.com/docker/getting-started.git
```

does 2 things
1. pull the docker image `alpine/git:latest` in the container `repo`
2. run the git command `git clone https://github.com/docker/getting-started.git`
(`repo` is a terrible name for the container that gives us git)

## BUILD a docker image

A **Docker image** is a **private file system just for your container**. It provides all the files and code your container needs.

```
cd getting-started
docker build -t docker101tutorial .
```

## RUN a container with a given image.
Start a container based on the image you built in the previous step. Running a container launches your application with private resources, securely isolated from the rest of your machine.

```
docker run -d -p 80:80 --name docker-tutorial docker101tutorial
```

You'll notice a few flags being used. Here's some more info on them:

* `-d` - run the container in detached mode (in the background)
* `-p 80:80` - map port 80 of the host to port 80 in the container
* `docker-tutorial` - the container name
* `docker101tutorial` - the image name

if signed in on docker, one can save and share your image on Docker Hub to enable other users to easily download and run the image on any destination machine.

```
docker tag docker101tutorial {username}/docker101tutorial
docker push {username}/docker101tutorial
```


after the tutorial we end up having

2 containers
- alpine/git
- docker-tutorial

2 images
- alpine/git         tag=latest
- docker101tutorial  tag=latest

# The Docker Dashboard

gives you a quick view of the containers running on your machine. It
- gives you quick access to **container logs**
- lets you get a **shell inside the container**
- and lets you easily manage container lifecycle (stop, remove, etc.)


# What is a container ?

A container is simply **another process on your machine that has been isolated from all other processes on the host machine**. That isolation leverages **kernel namespaces** and **cgroups**, features that have been in Linux for a long time. Docker has worked to make these capabilities approachable and easy to use.

# What is a container image ?

When running a container, it uses an **isolated filesystem**. This custom filesystem is provided by a container image. Since the image contains the container's filesystem, it contains
- all files needed to run an application:
  - all dependencies
  - configuration, scripts, binaries, etc...
- configuration for the container
  - environment variables
  - default command to run
  - other metadata


# What's in a container

the `app` folder contains the code of our node.js application


## Building the App's Container Image

In order to build the application, we need to use a `Dockerfile`.
A `Dockerfile` is simply a text-based script of instructions that is used to create a container imag


Dockerfile
```
FROM node:12-alpine
RUN apk add --no-cache python g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```

`docker build -t getting-started`

the `-t` flag tags our image. Think of this simply as a human-readable name for the final image. Since we named the image getting-started, we can refer to that image when we run a container.

This command used the Dockerfile to build a new container image. You might have noticed that a lot of "layers" were downloaded. This is because we instructed the builder that we wanted to start from the `node:12-alpine` image. But, since we didn't have that on our machine, that image needed to be downloaded.

After the image was downloaded, we copied in our application and used yarn to install our application's dependencies. The `CMD` directive specifies the default command to run when starting a container from this image.

## Starting an App Container

...

